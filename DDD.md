Laravel Project တစ်ခုကို ရေရှည်တည်တံ့စေဖို့ (Long-term Stable)၊ ကြီးထွားရလွယ်ကူစေဖို့ (Scalable) နဲ့ DRY (Don't Repeat Yourself) Principle တွေနဲ့အညီ **Modularization** နဲ့ **Centralized Types** ကို ပေါင်းစပ်ရေးသားမယ်ဆိုရင် **Domain-Driven Design (DDD)** သို့မဟုတ် **Modular Architecture** ကို အသုံးပြုဖို့ အကြံပြုချင်ပါတယ်။

Frontend (React/Vue/TypeScript) နဲ့ Backend (Laravel) ကြားမှာ Type တွေ နှစ်ခါပြန်မရေးရအောင် (Centralized Types) ဘယ်လိုလုပ်ရမလဲ ဆိုတာကိုပါ ထည့်သွင်းရှင်းပြပေးပါမယ်။

---

### ၁။ Folder Structure ကို Modular (သို့) Domain အလိုက် ခွဲခြားခြင်း

Laravel ရဲ့ ပုံမှန် `app/Controllers`, `app/Models` ဆိုပြီး နည်းပညာအလိုက် စုထားတဲ့ ပုံစံ (MVC) ဟာ Project ကြီးလာရင် ရှာရခက်ပြီး ပြုပြင်ရခက်ပါတယ်။ ဒါကြောင့် စီးပွားရေးလုပ်ငန်းစဉ် (Business Logic) အလိုက် **Modules (သို့) Domains** ခွဲထုတ်ရပါမယ်။ `nWidart/laravel-modules` package ကို သုံးနိုင်သလို၊ ကိုယ်တိုင် Folder Structure ချပြီး သုံးလို့လည်း ရပါတယ်။

**အကြံပြုလိုသော Domain-Driven Directory Structure:**

```text
app/
├── Domains/                // 🌟 Modules များအားလုံး ဤနေရာတွင်ထားမည်
│   ├── Dispatch/
│   │   ├── Actions/        // Business Logic များ (e.g., CreateTripAction.php)
│   │   ├── DTOs/           // Data Transfer Objects (e.g., TripData.php)
│   │   ├── Models/         // Trip.php, RouteDefinition.php
│   │   ├── Requests/       // StoreTripRequest.php
│   │   └── Controllers/    // TripController.php
│   ├── Finance/
│   │   ├── Actions/
│   │   ├── Models/
│   │   └── Controllers/
│   └── Fleet/

```

**အားသာချက်:** Dispatch နဲ့ ပတ်သက်တာပြင်ချင်ရင် `app/Domains/Dispatch` ထဲမှာပဲ အကုန်ရှိနေမှာမို့ အခြား Module တွေကို သွားထိခိုက်မှာ မဟုတ်တော့ပါဘူး။

---

### ၂။ Centralized Types (DRY Principle ကို ဖြေရှင်းခြင်း)

Laravel Project တွေမှာ အဖြစ်များဆုံး DRY Violation က Backend (PHP) မှာ Model/Validation ရေးပြီး၊ Frontend (TypeScript) မှာ `interface Trip { id: number, ... }` ဆိုပြီး **နှစ်ခါပြန်ရေးနေရခြင်း** ပါပဲ။ Backend က Column ပြင်လိုက်ရင် Frontend က လိုက်မပြင်မိဘဲ Error တက်တတ်ပါတယ်။

**ဖြေရှင်းနည်း:** `spatie/laravel-typescript-transformer` Package ကို အသုံးပြုပါ။

ဒီ Package က PHP Class (Models, DTOs) တွေကို ဖတ်ပြီး Frontend အတွက် TypeScript Types (`.d.ts`) တွေကို **Auto Generate** လုပ်ပေးပါတယ်။

**လုပ်ဆောင်ပုံ အဆင့်ဆင့်:**

1. Package ကို Install လုပ်ပါ: `composer require spatie/laravel-typescript-transformer`
2. သင်၏ Data Transfer Object (DTO) သို့မဟုတ် Model တွင် Annotation တပ်ပါ:

```php
// app/Domains/Dispatch/DTOs/TripData.php
namespace App\Domains\Dispatch\DTOs;

use Spatie\TypeScriptTransformer\Attributes\TypeScript;

#[TypeScript] // 🌟 ဤ Annotation လေးတပ်လိုက်ရုံပါပဲ
class TripData
{
    public function __construct(
        public readonly int $id,
        public readonly string $trip_number,
        public readonly int $vehicle_id,
        public readonly string $status,
        public readonly ?string $notes = null,
    ) {}
}

```

3. Command `php artisan typescript:transform` ကို Run လိုက်ပါက၊ `resources/js/types/generated.d.ts` ဆိုပြီး အလိုအလျောက် ထွက်လာပါမည်-

```typescript
// resources/js/types/generated.d.ts (Auto-generated file)
declare namespace App.Domains.Dispatch.DTOs {
    export interface TripData {
        id: number;
        trip_number: string;
        vehicle_id: number;
        status: string;
        notes: string | null;
    }
}

```

**အားသာချက်:** Backend မှာ Type ပြင်လိုက်တာနဲ့ Frontend Type ပါ အလိုအလျောက် ပြောင်းသွားမှာဖြစ်လို့ Types တွေကို Centralized ဖြစ်သွားစေပြီး DRY Principle ကို ၁၀၀% လိုက်နာနိုင်သွားပါပြီ။

---

### ၃။ Thin Controllers & Action Classes (Scalable ဖြစ်စေရန်)

Project ကြီးလာတဲ့အခါ Controller တွေထဲမှာ Code တွေ စာကြောင်းရာချီ ရှည်လာတတ်ပါတယ်။ Controller ရဲ့ တာဝန်ဟာ HTTP Request ကိုလက်ခံပြီး Response ပြန်ပေးဖို့ပဲ ဖြစ်သင့်ပါတယ်။ **Business Logic တွေကို Action Classes တွေဆီ ခွဲထုတ်ရပါမယ်။**

```php
// ❌ မလုပ်သင့်သော Fat Controller ပုံစံ
public function store(Request $request) {
    // Validation တွေရေးမယ်...
    // ပုံတွေ upload လုပ်မယ်...
    // Database ထဲ save မယ်...
    // Email ပို့မယ်... (Controller ကြီး ရှုပ်ပွသွားမည်)
}

```

```php
// ✅ လုပ်သင့်သော Thin Controller & Action ပုံစံ
namespace App\Domains\Dispatch\Controllers;

use App\Domains\Dispatch\Actions\CreateTripAction;
use App\Domains\Dispatch\Requests\StoreTripRequest;

class TripController extends Controller
{
    // Action Class ကို Dependency Injection ဖြင့် ခေါ်ယူခြင်း
    public function store(StoreTripRequest $request, CreateTripAction $createTrip)
    {
        // 1. Data ကို DTO ပြောင်းခြင်း
        $tripData = TripData::fromRequest($request);

        // 2. Action ထံသို့ လွှဲပြောင်းပေးခြင်း
        $trip = $createTrip->execute($tripData);

        return redirect()->route('trips.index')->with('success', 'Trip created!');
    }
}

```

**Action Class ဥပမာ (`CreateTripAction.php`):**

```php
namespace App\Domains\Dispatch\Actions;

use App\Domains\Dispatch\DTOs\TripData;
use App\Domains\Dispatch\Models\Trip;

class CreateTripAction
{
    public function execute(TripData $data): Trip
    {
        // ဒီနေရာမှာ သီးသန့် Business Logic တွေ ရေးပါမည်။
        // ဥပမာ - Notification ပို့ခြင်း၊ Activity Log မှတ်ခြင်း စသဖြင့်
        return Trip::create($data->toArray());
    }
}

```

---

### ၄။ Frontend (React/Inertia) Structure

Frontend ဘက်မှာလည်း Backend ရဲ့ Domain တွေအတိုင်း Structure ချထားရင် ရှာရဖွေရ အလွန်လွယ်ကူပါတယ်။

```text
resources/js/
├── Components/                    # 🧩 နေရာတိုင်းသုံးမည့် Shared UI (e.g., Button, Modal, Table)
├── Layouts/                       # 🖼️ Layouts (e.g., AppLayout, Sidebar)
├── types/                         # 📝 Centralized Types
│   ├── models.d.ts                # Database Models နှင့် တိုက်ရိုက်သက်ဆိုင်သော Types
│   └── index.d.ts                 # အထွေထွေ Types များ
│
└── Pages/                         # 📄 Inertia Pages များ
    ├── Dispatch/                  # Dispatch Module အတွက်
    │   ├── Components/            # Dispatch တွင်သာသုံးမည့် သီးသန့် UI များ (e.g., TripStatusBadge)
    │   ├── Trips/                 # ခရီးစဉ် Pages
    │   │   ├── Index.tsx
    │   │   ├── Create.tsx
    │   │   └── Show.tsx
    │   └── Customers/
    │
    ├── Finance/                   # Finance Module အတွက်
    └── Fleet/

```

### အနှစ်ချုပ် (Summary of the Architecture)

1. **Modules / Domains:** နည်းပညာအလိုက် (Controllers, Models) မစုဘဲ၊ လုပ်ငန်းစဉ်အလိုက် (Dispatch, Finance) Folder များ ခွဲထုတ်ပါ။
2. **Centralized Types:** `spatie/laravel-typescript-transformer` ကို သုံးပြီး PHP ကနေ TypeScript interfaces တွေကို Auto-generate လုပ်ပါ။ Frontend နဲ့ Backend ကြားမှာ Type တွေ အမြဲကိုက်ညီ (Sync) ဖြစ်နေပါစေ။
3. **Strict Boundaries:** Controller တွေကို ပါးပါးလျလျ (Thin) ထားပြီး၊ အလုပ်အားလုံးကို `Actions` Class တွေကသာ တာဝန်ယူပါစေ။
4. **DTOs (Data Transfer Objects):** Array တွေ အသုံးပြုခြင်းကို ရှောင်ကြဉ်ပြီး DTO တွေနဲ့သာ Data များကို အပြန်အလှန် ပေးပို့ပါ။

ဒီ Architecture ဟာ ပထမပိုင်း Setup လုပ်ရတာ အနည်းငယ် အချိန်ပေးရပေမယ့်၊ Project သက်တမ်း ၃ နှစ်၊ ၅ နှစ် ကြာလာတဲ့အခါ (သို့) Developer အသစ်တွေ အဖွဲ့ထဲ ရောက်လာတဲ့အခါ Code တွေ ရှုပ်ပွမသွားဘဲ (Maintainable) တည်ငြိမ်စွာ ဆက်လက်ကြီးထွား (Scale) နိုင်မှာ အသေအချာပဲ ဖြစ်ပါတယ်။
