SaaS Application (ဥပမာ - Stripe, Vercel, GitHub) တွေမှာ ခလုတ် (Button) တွေ နေရာချထားခြင်းဟာ User Experience (UX) အတွက် အသက်တမျှ အရေးကြီးပါတယ်။ အထူးသဖြင့် "Delete" လိုမျိုး အန္တရာယ်ရှိတဲ့ (Destructive) Action တွေကို နေရာချတဲ့အခါ **Spatial Distancing (နေရာခွဲခြားထားခြင်း)** နဲ့ **Visual Hierarchy (အမြင်ပိုင်းဆိုင်ရာ ဦးစားပေးမှု)** ကို တိတိကျကျ လိုက်နာရပါမယ်။

Professional UI/UX Designer တစ်ယောက်အနေနဲ့ Page (၅) မျိုးအတွက် အကောင်းဆုံး Button Placement စံနှုန်းများကို အောက်ပါအတိုင်း သုတေသနပြု ရှင်းလင်းတင်ပြအပ်ပါတယ်-

---

### ၁။ Index Page (Data Table)

Index page ဆိုတာ User တွေ အချက်အလက်တွေကို အမြန်ဖတ် (Scan) ဖို့ သုံးတဲ့နေရာပါ။

* **Eye (View), Edit, Delete နေရာ:** Table Row ရဲ့ **ညာဘက် အစွန်ဆုံး (Far Right)** မှာ ထားရပါမယ်။
* **ဒီဇိုင်းပုံစံ (Style):** * Solid Button (အရောင်အပြည့်) တွေကို **လုံးဝ (လုံးဝ) မသုံးရပါဘူး**။ အမြင်ရှုပ်ထွေးစေပြီး (Cognitive load) မျက်စိနောက်စေလို့ပါ။
* Icon သီးသန့် (Ghost buttons) ဒါမှမဟုတ် `...` (Dropdown / Action Menu) ပုံစံမျိုးပဲ သုံးရပါမယ်။
* Hover လုပ်မှသာ Delete Icon က အနီရောင်ပြောင်းသွားတာမျိုး လုပ်ပေးရပါမယ်။



---

### ၂။ Quick View Modal

Modal ဆိုတာ အချက်အလက်တွေကို အမြန်ကြည့်ဖို့နဲ့ လိုအပ်ရင် Action အနည်းငယ်လုပ်ဖို့ပါ။

* **Close, Edit, Full Details နေရာ:** Modal ရဲ့ **ညာဘက်အောက်ခြေ (Bottom-Right)** မှာ ထားပါ။ (User တွေက ညာသန်များပြီး Next/Save လိုမျိုး အရှေ့ဆက်သွားမယ့် Action တွေကို ညာဘက်မှာ ရှာလေ့ရှိလို့ပါ)။
* **Delete နေရာ:** Modal ရဲ့ **ဘယ်ဘက်အောက်ခြေ (Bottom-Left)** မှာ ထားပါ။
* **ဒီဇိုင်းပုံစံ (Style):**
* **[ Bottom-Left ]** Delete -> `variant="ghost"` (နောက်ခံအရောင်မပါ၊ စာသားအနီ)
* **[ Bottom-Right ]** Close -> `variant="outline"` (အဖြူရောင်နောက်ခံ၊ ဘောင်ပါ)
* **[ Bottom-Right ]** Edit / Details -> `variant="solid"` (Primary အရောင်)


* **UX အားသာချက်:** Delete နဲ့ တခြား Safe actions တွေကို ဘယ်နဲ့ညာ ခွဲထုတ်ထားတဲ့အတွက် Mouse မှားနှိပ်မိခြင်း (Accidental click) ကို ၉၉% ကာကွယ်ပေးပါတယ်။

---

### ၃။ Show Page (Full Details Page)

Show page ဟာ အချက်အလက်အပြည့်အစုံကို သေချာဖတ်ရှုဖို့ (Read-only) ဖြစ်ပါတယ်။

* **Back နေရာ:** Header ရဲ့ **ဘယ်ဘက်ထိပ် (Top-Left)** မှာထားပါ။ (Web Standard အရ Back ဆိုတာ အနောက်ကိုပြန်ဆုတ်တာဖြစ်လို့ ဘယ်ဘက်မှာ အမြဲရှိရပါမယ်)။
* **Edit, Delete, Download နေရာ:** Header ရဲ့ **ညာဘက်ထိပ် (Top-Right)** မှာ ထားရပါမယ်။
* **ဒီဇိုင်းပုံစံ (Style):**
* ညာဘက်ထိပ်မှာ အရေးကြီးဆုံးကနေ အရေးအကြီးဆုံးကို အစဉ်လိုက်စီရပါမယ်။
* `[ Delete (Ghost Red) ]` + `[ Download PDF (Outline) ]` + `[ Edit (Solid Primary) ]`


* **UX အားသာချက်:** User တွေက စာဖတ်တဲ့အခါ အပေါ်ကနေ အောက်ကို ဖတ်ပါတယ်။ Page အောက်ခြေထိ ရောက်အောင်ဆင်းစရာမလိုဘဲ လိုချင်တဲ့ Action ကို ချက်ချင်းလုပ်နိုင်ဖို့ Header ညာဘက်မှာ ထားခြင်းဖြစ်ပါတယ်။

---

### ၄။ Edit Page (Form)

အချက်အလက်တွေ ပြင်ဆင်မယ့်နေရာ (Data Entry) ဖြစ်ပါတယ်။

* **Back / Cancel နေရာ:** * Back ကို Header **ဘယ်ဘက်ထိပ် (Top-Left)** မှာ ထားပါ။
* Form Cancel ကိုတော့ Form ရဲ့ အောက်ဆုံး **ညာဘက် (Bottom-Right)**၊ Save ခလုတ်ရဲ့ ဘေးမှာ ထားပါ။


* **Save နေရာ:** Form ရဲ့ အောက်ဆုံး **ညာဘက် (Bottom-Right)** မှာ ထားပါ။
* **Delete နေရာ:** Form ရဲ့ အောက်ဆုံး **ဘယ်ဘက် (Bottom-Left)** မှာ ထားပါ။
* **ဒီဇိုင်းပုံစံ (Style) (Sticky Footer သုံးပါ):**
* Edit လုပ်နေရင်း အချက်အလက်တွေ မှားနေမှန်းသိလို့ ဖျက်ချင်တယ်ဆိုရင် ပြန်ထွက်စရာမလိုဘဲ ဖျက်နိုင်အောင် Delete ကို ဘယ်ဘက်အောက်ခြေမှာ `variant="ghost"` နဲ့ ထည့်ပေးထားရပါမယ်။
* Cancel ကို `variant="outline"`, Save ကို `variant="solid"` (Primary Color) သုံးပါ။



---

### ၅။ Create Page (Form)

အသစ်ထည့်သွင်းမယ့်နေရာ ဖြစ်ပါတယ်။

* **Back / Cancel / Save နေရာ:** Edit page နဲ့ အတူတူပါပဲ။ Back က **Top-Left**၊ Cancel နဲ့ Save က **Bottom-Right** ပါ။
* **Delete နေရာ:** အသစ်ဖန်တီးတာဖြစ်တဲ့အတွက် Delete Button **လုံးဝ မပါရပါဘူး**။
* **UX အားသာချက်:** User ကို Data ထည့်သွင်းခြင်းဆိုတဲ့ Action တစ်ခုတည်းကိုသာ အာရုံစိုက်စေပါတယ်။

---

### 🌟 အနှစ်ချုပ် (The Golden Rules of SaaS UI)

1. **Top-to-Bottom Flow:** Form (Create/Edit) တွေဆိုရင် User က အပေါ်ကနေ အောက်ကို ဆင်းဖတ်ပြီး ဖြည့်ရတာမို့ Action Buttons (Save/Cancel/Delete) တွေကို **အောက်ခြေ (Bottom Footer)** မှာ ထားရပါမယ်။
2. **Immediate Access:** Read-only (Show page) တွေဆိုရင် ဖတ်ဖို့သက်သက်မို့ Action Buttons (Edit/Delete/Download) တွေကို **အပေါ်ဘက် ညာထောင့် (Top-Right Header)** မှာ ပြထားရပါမယ်။
3. **The Danger Zone:** Delete လိုမျိုး အန္တရာယ်ရှိတဲ့ ခလုတ်ကို Save/Edit ခလုတ်တွေနဲ့ ကပ်လျက် လုံးဝမထားရပါဘူး။ ဘယ်ညာ (သို့) ပုံစံခွဲပြီး (Solid vs Ghost) အမြဲ သီးသန့်ခွဲထားရပါမယ်။ ပြီးလျှင် Confirmation Modal အမြဲခံထားပေးရပါမယ်။

ဒါတွေက ကမ္ဘာ့အဆင့်မီ System တွေမှာ အသုံးပြုနေတဲ့ Standard UI/UX Guideline တွေပဲ ဖြစ်ပါတယ်။
