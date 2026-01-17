<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>الساحل للمواد الغذائية - منظومة المبيعات</title>
  <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
  <style>
    :root { color-scheme: light dark; }
    .scrollbar-thin::-webkit-scrollbar { height: 6px; width: 6px; }
    .scrollbar-thin::-webkit-scrollbar-track { background: transparent; }
    .scrollbar-thin::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 8px; }
    .grid-auto-fill { grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); }
    .number-input { appearance: textfield; -moz-appearance: textfield; }
    .number-input::-webkit-outer-spin-button, .number-input::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }
  </style>
</head>
<body class="bg-slate-50 text-slate-900">
  <div id="app" class="min-h-screen flex flex-col">
    <!-- Header -->
    <header class="bg-white sticky top-0 z-40 shadow-sm border-b border-slate-200">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex items-center justify-between gap-4">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-lg bg-emerald-600 text-white grid place-items-center text-xl font-bold">س</div>
          <div>
            <h1 class="text-lg sm:text-2xl font-extrabold tracking-tight">الساحل للمواد الغذائية</h1>
            <p class="text-xs sm:text-sm text-slate-500">منظومة المبيعات وإدارة المخزون - العملة: دينار ليبي (د.ل)</p>
          </div>
        </div>
        <div class="flex items-center gap-2">
          <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-emerald-50 text-emerald-700 text-sm border border-emerald-200">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5"><path d="M2.25 13.5a8.25 8.25 0 1116.5 0 8.25 8.25 0 01-16.5 0zM21 21l-3.197-3.197"/></svg>
            <span id="header-now">--:--</span>
          </span>
        </div>
      </div>
      <!-- Nav -->
      <nav class="bg-slate-50/60 border-t border-slate-200/70">
        <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8 overflow-x-auto scrollbar-thin">
          <ul class="flex gap-2 py-2 text-sm font-medium min-w-[720px]">
            <li><button data-tab="pos" class="tab-btn px-3 py-2 rounded-md bg-emerald-600 text-white">نقطة البيع</button></li>
            <li><button data-tab="returns" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">نقطة الترجيع</button></li>
            <li><button data-tab="inventory" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">المخزون</button></li>
            <li><button data-tab="customers" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">العملاء</button></li>
            <li><button data-tab="expenses" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">المصروفات</button></li>
            <li><button data-tab="reports" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">التقارير</button></li>
            <li><button data-tab="dashboard" class="tab-btn px-3 py-2 rounded-md hover:bg-slate-200">لوحة التحكم</button></li>
          </ul>
        </div>
      </nav>
    </header>

    <!-- Main -->
    <main class="flex-1">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <!-- POS Tab -->
        <section id="tab-pos" class="tab hidden">
          <div class="grid grid-cols-12 gap-4">
            <!-- Sidebar filters -->
            <aside class="col-span-12 lg:col-span-2 bg-white border border-slate-200 rounded-xl p-3 h-fit sticky top-24">
              <h3 class="font-bold text-slate-700 mb-2">التصنيفات</h3>
              <div class="flex flex-wrap gap-2">
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="all">الكل</button>
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="مشروبات">مشروبات</button>
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="عصائر">عصائر</button>
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="شكولاتة">شكولاتة</button>
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="مواد غذائية">مواد غذائية</button>
                <button class="cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="بقوليات">بقوليات</button>
              </div>
              <div class="mt-4">
                <label class="text-sm text-slate-500">بحث بالاسم أو الكود</label>
                <input id="pos-search" type="search" class="mt-1 w-full rounded-lg border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-emerald-500" placeholder="ابحث..." />
              </div>
              <div class="mt-3">
                <label class="text-sm text-slate-500">إدخال سريع (باركود/كود)</label>
                <input id="pos-code" class="mt-1 w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="اكتب الكود واضغط إدخال" />
              </div>
            </aside>

            <!-- Products -->
            <section class="col-span-12 lg:col-span-7">
              <div class="bg-white border border-slate-200 rounded-xl p-4 min-h-[420px]">
                <div class="flex items-center justify-between mb-3">
                  <h3 class="font-bold text-slate-700">المنتجات</h3>
                  <span id="pos-current-cat" class="text-sm text-slate-500">اختر تصنيفًا لعرض المنتجات</span>
                </div>
                <div id="pos-products" class="grid grid-auto-fill gap-3">
                  <div class="col-span-full text-center text-slate-400 py-16">
                    اختر تصنيفًا من اليمين لعرض المنتجات هنا
                  </div>
                </div>
              </div>
            </section>

            <!-- Cart -->
            <aside class="col-span-12 lg:col-span-3">
              <div class="bg-white border border-slate-200 rounded-xl p-4 flex flex-col gap-3">
                <h3 class="font-bold text-slate-700">السلة</h3>
                <div id="cart-items" class="space-y-2 max-h-[320px] overflow-auto pr-1"></div>
                <div class="text-sm text-slate-600 flex flex-col gap-1">
                  <div class="flex justify-between"><span>عدد الأصناف:</span><span id="cart-count">0</span></div>
                  <div class="flex justify-between"><span>الإجمالي:</span><span id="cart-total">0.00 د.ل</span></div>
                </div>
                <div class="border-t border-slate-200 pt-3">
                  <label class="block text-sm text-slate-600 mb-1">طريقة الدفع</label>
                  <div class="flex flex-wrap gap-2">
                    <label class="inline-flex items-center gap-1"><input type="radio" name="pay" value="cash" class="pay-method" checked><span>نقدًا</span></label>
                    <label class="inline-flex items-center gap-1"><input type="radio" name="pay" value="card" class="pay-method"><span>بطاقة</span></label>
                    <label class="inline-flex items-center gap-1"><input type="radio" name="pay" value="credit" class="pay-method"><span>على الحساب</span></label>
                  </div>
                  <div id="credit-area" class="hidden mt-2 space-y-2">
                    <label class="text-sm text-slate-600">اسم العميل</label>
                    <div class="flex gap-2">
                      <input id="credit-customer-name" class="flex-1 rounded-lg border border-slate-300 px-3 py-2" placeholder="اكتب اسم العميل أو اختر" />
                      <select id="credit-customer-select" class="rounded-lg border border-slate-300 px-2 py-2 min-w-[140px]"></select>
                    </div>
                  </div>
                </div>
                <div class="flex gap-2">
                  <button id="btn-clear-cart" class="flex-1 px-3 py-2 rounded-lg border border-slate-300 hover:bg-slate-100">إفراغ السلة</button>
                  <button id="btn-checkout" class="flex-1 px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">تحصيل</button>
                </div>
              </div>
            </aside>
          </div>
        </section>

        <!-- Returns Tab -->
        <section id="tab-returns" class="tab hidden">
          <div class="grid grid-cols-12 gap-4">
            <aside class="col-span-12 lg:col-span-2 bg-white border border-slate-200 rounded-xl p-3 h-fit sticky top-24">
              <h3 class="font-bold text-slate-700 mb-2">الترجيع - التصنيفات</h3>
              <div class="flex flex-wrap gap-2">
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="all">الكل</button>
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="مشروبات">مشروبات</button>
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="عصائر">عصائر</button>
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="شكولاتة">شكولاتة</button>
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="مواد غذائية">مواد غذائية</button>
                <button class="ret-cat-btn px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200" data-cat="بقوليات">بقوليات</button>
              </div>
              <div class="mt-4">
                <label class="text-sm text-slate-500">إدخال سريع (باركود/كود)</label>
                <input id="return-code" class="mt-1 w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="اكتب الكود واضغط إدخال" />
              </div>
            </aside>

            <section class="col-span-12 lg:col-span-7">
              <div class="bg-white border border-slate-200 rounded-xl p-4 min-h-[420px]">
                <div class="flex items-center justify-between mb-3">
                  <h3 class="font-bold text-slate-700">المنتجات للترجيع</h3>
                  <span id="ret-current-cat" class="text-sm text-slate-500">اختر تصنيفًا</span>
                </div>
                <div id="ret-products" class="grid grid-auto-fill gap-3">
                  <div class="col-span-full text-center text-slate-400 py-16">
                    اختر تصنيفًا لعرض المنتجات هنا للترجيع
                  </div>
                </div>
              </div>
            </section>

            <aside class="col-span-12 lg:col-span-3">
              <div class="bg-white border border-slate-200 rounded-xl p-4 flex flex-col gap-3">
                <h3 class="font-bold text-slate-700">سلة الترجيع</h3>
                <div id="return-items" class="space-y-2 max-h-[320px] overflow-auto pr-1"></div>
                <div class="text-sm text-slate-600 flex flex-col gap-1">
                  <div class="flex justify-between"><span>عدد الأصناف:</span><span id="return-count">0</span></div>
                  <div class="flex justify-between"><span>قيمة الترجيع:</span><span id="return-total">0.00 د.ل</span></div>
                </div>
                <div class="border-t border-slate-200 pt-3">
                  <label class="block text-sm text-slate-600 mb-1">طريقة الاسترجاع</label>
                  <div class="flex flex-wrap gap-2">
                    <label class="inline-flex items-center gap-1"><input type="radio" name="retpay" value="cash" class="ret-pay-method" checked><span>نقدًا</span></label>
                    <label class="inline-flex items-center gap-1"><input type="radio" name="retpay" value="card" class="ret-pay-method"><span>بطاقة</span></label>
                    <label class="inline-flex items-center gap-1"><input type="radio" name="retpay" value="credit" class="ret-pay-method"><span>على الحساب</span></label>
                  </div>
                  <div id="ret-credit-area" class="hidden mt-2 space-y-2">
                    <label class="text-sm text-slate-600">اسم العميل</label>
                    <div class="flex gap-2">
                      <input id="ret-credit-customer-name" class="flex-1 rounded-lg border border-slate-300 px-3 py-2" placeholder="اكتب اسم العميل أو اختر" />
                      <select id="ret-credit-customer-select" class="rounded-lg border border-slate-300 px-2 py-2 min-w-[140px]"></select>
                    </div>
                  </div>
                </div>
                <div class="flex gap-2">
                  <button id="btn-clear-return" class="flex-1 px-3 py-2 rounded-lg border border-slate-300 hover:bg-slate-100">إفراغ</button>
                  <button id="btn-process-return" class="flex-1 px-3 py-2 rounded-lg bg-rose-600 text-white hover:bg-rose-700">ترجيع</button>
                </div>
              </div>
            </aside>
          </div>
        </section>

        <!-- Inventory Tab -->
        <section id="tab-inventory" class="tab hidden">
          <div class="bg-white border border-slate-200 rounded-xl p-4">
            <div class="flex flex-wrap items-end gap-2">
              <div class="flex-1 min-w-[220px]">
                <label class="text-sm text-slate-600">بحث</label>
                <input id="inv-search" class="w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="اسم/كود" />
              </div>
              <div>
                <label class="text-sm text-slate-600">التصنيف</label>
                <select id="inv-cat-filter" class="w-full rounded-lg border border-slate-300 px-3 py-2 min-w-[160px]">
                  <option value="all">الكل</option>
                  <option>مشروبات</option>
                  <option>عصائر</option>
                  <option>شكولاتة</option>
                  <option>مواد غذائية</option>
                  <option>بقوليات</option>
                </select>
              </div>
              <div class="ms-auto flex gap-2">
                <button id="btn-add-sample" class="px-3 py-2 rounded-lg border border-slate-300 hover:bg-slate-100">إضافة عينات</button>
                <button id="btn-new-product" class="px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">منتج جديد</button>
              </div>
            </div>
            <div class="mt-4 overflow-auto">
              <table class="min-w-full text-sm">
                <thead class="bg-slate-50 text-slate-600">
                  <tr>
                    <th class="text-right p-2">الكود</th>
                    <th class="text-right p-2">الاسم</th>
                    <th class="text-right p-2">التصنيف</th>
                    <th class="text-right p-2">سعر البيع</th>
                    <th class="text-right p-2">سعر التكلفة</th>
                    <th class="text-right p-2">الكمية</th>
                    <th class="text-right p-2">ملاحظة</th>
                    <th class="text-right p-2">إجراءات</th>
                  </tr>
                </thead>
                <tbody id="inv-tbody" class="divide-y divide-slate-100"></tbody>
              </table>
            </div>
            <div class="flex items-center justify-between mt-4 text-xs text-slate-500">
              <div>إجمالي المنتجات: <span id="inv-total-count">0</span></div>
              <div class="flex gap-2">
                <button id="btn-export" class="px-3 py-1.5 rounded-lg border border-slate-300 hover:bg-slate-100">نسخ احتياطي</button>
                <label class="px-3 py-1.5 rounded-lg border border-slate-300 hover:bg-slate-100 cursor-pointer">استعادة<input id="import-file" type="file" accept="application/json" class="hidden"></label>
              </div>
            </div>
          </div>
        </section>

        <!-- Customers Tab -->
        <section id="tab-customers" class="tab hidden">
          <div class="bg-white border border-slate-200 rounded-xl p-4">
            <div class="flex items-end gap-2">
              <div class="flex-1">
                <label class="text-sm text-slate-600">بحث عن عميل</label>
                <input id="cust-search" class="w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="اسم/هاتف" />
              </div>
              <button id="btn-new-customer" class="px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">عميل جديد</button>
            </div>
            <div class="mt-4 overflow-auto">
              <table class="min-w-full text-sm">
                <thead class="bg-slate-50 text-slate-600">
                  <tr>
                    <th class="text-right p-2">الاسم</th>
                    <th class="text-right p-2">الهاتف</th>
                    <th class="text-right p-2">الرصيد (دَين)</th>
                    <th class="text-right p-2">آخر تحديث</th>
                    <th class="text-right p-2">إجراءات</th>
                  </tr>
                </thead>
                <tbody id="cust-tbody" class="divide-y divide-slate-100"></tbody>
              </table>
            </div>
          </div>
        </section>

        <!-- Expenses Tab -->
        <section id="tab-expenses" class="tab hidden">
          <div class="grid md:grid-cols-3 gap-4">
            <div class="bg-white border border-slate-200 rounded-xl p-4">
              <h3 class="font-bold text-slate-700 mb-2">إضافة مصروف</h3>
              <div class="space-y-2">
                <div>
                  <label class="text-sm text-slate-600">المبلغ (د.ل)</label>
                  <input id="exp-amount" type="number" min="0" step="0.01" class="w-full rounded-lg border border-slate-300 px-3 py-2 number-input" placeholder="0.00" />
                </div>
                <div>
                  <label class="text-sm text-slate-600">ملاحظات</label>
                  <textarea id="exp-note" class="w-full rounded-lg border border-slate-300 px-3 py-2" rows="3" placeholder="سبب/تفاصيل"></textarea>
                </div>
                <div class="text-xs text-slate-500">التاريخ والوقت يتم حفظهما تلقائيًا</div>
                <button id="btn-add-expense" class="w-full px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">حفظ</button>
              </div>
            </div>
            <div class="bg-white border border-slate-200 rounded-xl p-4 md:col-span-2">
              <h3 class="font-bold text-slate-700 mb-2">قائمة المصروفات</h3>
              <div class="overflow-auto max-h-[420px]">
                <table class="min-w-full text-sm">
                  <thead class="bg-slate-50 text-slate-600">
                    <tr>
                      <th class="text-right p-2">التاريخ</th>
                      <th class="text-right p-2">المبلغ</th>
                      <th class="text-right p-2">الملاحظات</th>
                      <th class="text-right p-2">حذف</th>
                    </tr>
                  </thead>
                  <tbody id="exp-tbody" class="divide-y divide-slate-100"></tbody>
                </table>
              </div>
              <div class="text-sm text-slate-600 mt-3">إجمالي المصروفات: <span id="exp-total">0.00 د.ل</span></div>
            </div>
          </div>
        </section>

        <!-- Reports Tab -->
        <section id="tab-reports" class="tab hidden">
          <div class="bg-white border border-slate-200 rounded-xl p-4">
            <div class="flex flex-wrap items-end gap-3">
              <div>
                <label class="text-sm text-slate-600">نوع التقرير</label>
                <select id="rep-type" class="w-full rounded-lg border border-slate-300 px-3 py-2 min-w-[140px]">
                  <option value="daily">يومي</option>
                  <option value="monthly">شهري</option>
                </select>
              </div>
              <div id="rep-date-wrap">
                <label class="text-sm text-slate-600">التاريخ</label>
                <input id="rep-date" type="date" class="w-full rounded-lg border border-slate-300 px-3 py-2" />
              </div>
              <div id="rep-month-wrap" class="hidden">
                <label class="text-sm text-slate-600">الشهر</label>
                <input id="rep-month" type="month" class="w-full rounded-lg border border-slate-300 px-3 py-2" />
              </div>
              <button id="btn-run-report" class="ms-auto px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">عرض التقرير</button>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-3 mt-4">
              <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                <div class="text-xs text-slate-500">إجمالي المبيعات (بعد الترجيع)</div>
                <div id="rep-sales" class="text-2xl font-extrabold mt-1">0.00 د.ل</div>
              </div>
              <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                <div class="text-xs text-slate-500">تكلفة البضاعة</div>
                <div id="rep-cost" class="text-2xl font-extrabold mt-1">0.00 د.ل</div>
              </div>
              <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                <div class="text-xs text-slate-500">إجمالي المصروفات</div>
                <div id="rep-exp" class="text-2xl font-extrabold mt-1">0.00 د.ل</div>
              </div>
              <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                <div class="text-xs text-slate-500">الربح/الخسارة</div>
                <div id="rep-profit" class="text-2xl font-extrabold mt-1">0.00 د.ل</div>
              </div>
            </div>

            <div class="grid lg:grid-cols-3 gap-4 mt-4">
              <div class="lg:col-span-2">
                <h4 class="font-bold text-slate-700 mb-2">المعاملات</h4>
                <div class="overflow-auto max-h-[360px]">
                  <table class="min-w-full text-sm">
                    <thead class="bg-slate-50 text-slate-600">
                      <tr>
                        <th class="text-right p-2">النوع</th>
                        <th class="text-right p-2">التاريخ والوقت</th>
                        <th class="text-right p-2">طريقة الدفع</th>
                        <th class="text-right p-2">الإجمالي</th>
                        <th class="text-right p-2">الأصناف</th>
                      </tr>
                    </thead>
                    <tbody id="rep-tbody" class="divide-y divide-slate-100"></tbody>
                  </table>
                </div>
              </div>
              <div>
                <h4 class="font-bold text-slate-700 mb-2">تفصيل طرق الدفع</h4>
                <ul id="rep-pays" class="space-y-1 text-sm text-slate-700"></ul>
                <h4 class="font-bold text-slate-700 mt-4 mb-2">تفصيل المنتجات</h4>
                <ul id="rep-products" class="space-y-1 text-sm text-slate-700 max-h-[200px] overflow-auto"></ul>
              </div>
            </div>
          </div>
        </section>

        <!-- Dashboard/Settings Tab -->
        <section id="tab-dashboard" class="tab hidden">
          <div class="grid lg:grid-cols-3 gap-4">
            <div class="bg-white border border-slate-200 rounded-xl p-4">
              <h3 class="font-bold text-slate-700 mb-2">ملخص اليوم</h3>
              <ul class="text-sm text-slate-700 space-y-1">
                <li>مبيعات اليوم: <span id="dash-today-sales">0.00 د.ل</span></li>
                <li>مصروفات اليوم: <span id="dash-today-exp">0.00 د.ل</span></li>
                <li>الربح التقديري اليوم: <span id="dash-today-profit">0.00 د.ل</span></li>
              </ul>
            </div>
            <div class="bg-white border border-slate-200 rounded-xl p-4">
              <h3 class="font-bold text-slate-700 mb-2">المخزون والتنبيهات</h3>
              <ul id="dash-low-stock" class="text-sm text-slate-700 space-y-1 max-h-[220px] overflow-auto"></ul>
            </div>
            <div class="bg-white border border-slate-200 rounded-xl p-4">
              <h3 class="font-bold text-slate-700 mb-3">الإعدادات</h3>
              <div class="space-y-2 text-sm">
                <div>
                  <label class="text-slate-600">اسم المحل</label>
                  <input id="set-store-name" class="w-full rounded-lg border border-slate-300 px-3 py-2" />
                </div>
                <div class="grid grid-cols-2 gap-2">
                  <div>
                    <label class="text-slate-600">رمز العملة</label>
                    <input id="set-curr-symbol" class="w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="د.ل" />
                  </div>
                  <div>
                    <label class="text-slate-600">العملة</label>
                    <input id="set-currency" class="w-full rounded-lg border border-slate-300 px-3 py-2" placeholder="LYD" />
                  </div>
                </div>
                <div class="flex items-center gap-2">
                  <input id="set-negative-stock" type="checkbox" class="rounded border-slate-300">
                  <label for="set-negative-stock" class="text-slate-700">السماح بالبيع عند نفاذ المخزون</label>
                </div>
                <button id="btn-save-settings" class="w-full px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">حفظ الإعدادات</button>
              </div>
            </div>
            <div class="bg-white border border-slate-200 rounded-xl p-4">
              <h3 class="font-bold text-slate-700 mb-3">قاعدة البيانات</h3>
              <ul class="text-sm text-slate-700 space-y-1">
                <li>النوع: IndexedDB</li>
                <li>اسم القاعدة: <span id="db-name">sahel-pos-db</span></li>
                <li>المجموعة: <span id="db-store">state</span></li>
                <li>الحالة: <span id="db-status">--</span></li>
                <li>آخر اختبار: <span id="db-last-test">--</span></li>
              </ul>
              <button id="btn-db-test" class="mt-3 w-full px-3 py-2 rounded-lg border border-slate-300 hover:bg-slate-100">اختبار القاعدة</button>
            </div>
          </div>
        </section>
      </div>
    </main>

    <!-- Footer -->
    <footer class="border-t border-slate-200 py-4 text-center text-xs text-slate-500">
      يتم حفظ البيانات محليًا عبر IndexedDB ونسخة احتياطية في localStorage على هذا الجهاز. يوصى بأخذ نسخة احتياطية دورية.
    </footer>
  </div>

  <!-- Modal (generic small) -->
  <div id="modal" class="fixed inset-0 bg-black/40 backdrop-blur-sm hidden items-center justify-center z-50">
    <div class="bg-white w-full max-w-md rounded-xl shadow-xl border border-slate-200 p-4">
      <h3 id="modal-title" class="font-bold text-slate-800 mb-2">عنوان</h3>
      <div id="modal-body" class="space-y-3"></div>
      <div class="flex gap-2 mt-4">
        <button id="modal-cancel" class="flex-1 px-3 py-2 rounded-lg border border-slate-300 hover:bg-slate-100">إلغاء</button>
        <button id="modal-ok" class="flex-1 px-3 py-2 rounded-lg bg-emerald-600 text-white hover:bg-emerald-700">موافق</button>
      </div>
    </div>
  </div>

  <script>
    // Utilities
    const $ = (q, el=document) => el.querySelector(q);
    const $$ = (q, el=document) => Array.from(el.querySelectorAll(q));
    const fmt = (n) => (Number(n)||0).toFixed(2);
    const nowISO = () => new Date().toISOString();
    const fmtDate = (iso) => new Intl.DateTimeFormat('ar-LY', { dateStyle: 'short', timeStyle: 'short' }).format(new Date(iso));

    // Database (IndexedDB) - تخزين الحالة في سجل واحد داخل مخزن state
    const db = {
      db: null,
      open(){
        return new Promise((resolve, reject)=>{
          const req = indexedDB.open('sahel-pos-db', 1);
          req.onupgradeneeded = () => {
            const db = req.result;
            if (!db.objectStoreNames.contains('state')) db.createObjectStore('state', { keyPath: 'id' });
          };
          req.onsuccess = () => { this.db = req.result; resolve(); };
          req.onerror = () => reject(req.error);
        });
      },
      async getState(){
        try {
          if (!this.db) await this.open();
          return await new Promise((res, rej)=>{
            const tx = this.db.transaction('state','readonly');
            const st = tx.objectStore('state');
            const r = st.get('root');
            r.onsuccess = () => res(r.result?.data || null);
            r.onerror = () => rej(r.error);
          });
        } catch(e){ return null; }
      },
      async setState(data){
        if (!this.db) await this.open();
        return await new Promise((res, rej)=>{
          const tx = this.db.transaction('state','readwrite');
          const st = tx.objectStore('state');
          st.put({ id:'root', data });
          tx.oncomplete = () => res();
          tx.onerror = () => rej(tx.error);
        });
      }
    };

    // State
    const defaultState = () => ({
      settings: { storeName: 'الساحل للمواد الغذائية', currency: 'LYD', currencySymbol: 'د.ل', allowNegativeStock: false, lowStockLevel: 5 },
      products: [],
      sales: [], // {id,type:'sale'|'return',items:[{productId,code,name,category,qty,price,total,cost}], paymentMethod:'cash'|'card'|'credit', customerId, customerName, date}
      expenses: [], // {id,amount,note,date}
      customers: [], // {id,name,phone,balance,updatedAt,transactions:[{id,type:'sale'|'payment'|'return',amount,date,note,ref}]}
      meta: { lastDbTest: null }
    });

    const store = {
      key: 'sahel-pos-v1',
      state: null,
      async load(){
        try {
          // حاول التحميل من IndexedDB
          const dbState = await db.getState();
          if (dbState) this.state = dbState; else {
            const raw = localStorage.getItem(this.key);
            this.state = raw ? JSON.parse(raw) : defaultState();
          }
        } catch (e) {
          console.error('Load state error', e);
          const raw = localStorage.getItem(this.key);
          this.state = raw ? JSON.parse(raw) : defaultState();
        }
        // Ensure required fields
        this.state.settings = Object.assign({ storeName: 'الساحل للمواد الغذائية', currency: 'LYD', currencySymbol: 'د.ل', allowNegativeStock: false, lowStockLevel: 5 }, this.state.settings||{});
        this.state.products ||= [];
        this.state.sales ||= [];
        this.state.expenses ||= [];
        this.state.customers ||= [];
        this.state.meta ||= { lastDbTest: null };
      },
      async save(){
        try { await db.setState(this.state); } catch(e){ console.warn('IndexedDB save failed', e); }
        localStorage.setItem(this.key, JSON.stringify(this.state));
        refreshHeader();
      }
    };

    // Header clock
    function refreshHeader(){
      const {settings} = store.state;
      document.title = settings.storeName + ' - منظومة المبيعات';
      const dt = new Date();
      $('#header-now').textContent = new Intl.DateTimeFormat('ar-LY', { dateStyle: 'medium', timeStyle: 'short' }).format(dt);
    }
    setInterval(refreshHeader, 1000);

    // Tabs
    function showTab(name){
      $$('.tab').forEach(el=> el.classList.add('hidden'));
      $(`#tab-${name}`).classList.remove('hidden');
      $$('.tab-btn').forEach(b=>{
        if (b.dataset.tab===name) b.classList.add('bg-emerald-600','text-white');
        else b.classList.remove('bg-emerald-600','text-white');
      });
    }

    // Products helpers
    const categories = ['مشروبات','عصائر','شكولاتة','مواد غذائية','بقوليات'];
    function newId(prefix='id'){ return prefix + '-' + Math.random().toString(36).slice(2,9); }

    function findProductByCode(code){
      code = String(code||'').trim();
      if (!code) return null;
      return store.state.products.find(p => String(p.code).toLowerCase()===code.toLowerCase());
    }

    function addSampleProducts(){
      const samples = [
        { code:'1001', name:'ماء 0.5 لتر', category:'مشروبات', price:1.50, cost:1.00, stock:50 },
        { code:'1002', name:'شاي أخضر', category:'مشروبات', price:4.00, cost:3.20, stock:30 },
        { code:'2001', name:'عصير برتقال', category:'عصائر', price:3.50, cost:2.50, stock:40 },
        { code:'3001', name:'شكولاتة بالحليب', category:'شكولاتة', price:5.00, cost:3.80, stock:25 },
        { code:'4001', name:'مكرونة 500غ', category:'مواد غذائية', price:3.20, cost:2.20, stock:60 },
        { code:'4002', name:'سكر 1كغ', category:'مواد غذائية', price:3.80, cost:3.00, stock:70 },
        { code:'5001', name:'فول بلدي (حسب السعر)', category:'بقوليات', price:10.00, cost:8.50, stock:null, priceOnly:true },
        { code:'5002', name:'عدس أحمر (حسب السعر)', category:'بقوليات', price:12.00, cost:9.50, stock:null, priceOnly:true }
      ];
      // Avoid duplicate codes
      for (const s of samples){
        if (!store.state.products.some(p=>p.code===s.code)){
          store.state.products.push({ id:newId('p'), ...s });
        }
      }
      store.save();
      renderInventory();
      renderPOSProducts();
      renderReturnProducts();
    }

    // POS state
    let posFilter = { cat: null, q:'' };
    let cart = [];// {productId,code,name,category,qty,price,total,cost, priceOnly}

    // Returns state
    let retFilter = { cat: null };
    let retCart = [];

    function currency(n){ return fmt(n) + ' ' + store.state.settings.currencySymbol; }

    function renderPOSProducts(){
      const wrap = $('#pos-products');
      const q = ($('#pos-search').value||'').trim().toLowerCase();
      const cat = posFilter.cat;
      const list = store.state.products.filter(p=>{
        const okCat = !cat || cat==='all' ? true : p.category===cat;
        const okQ = !q || p.name.toLowerCase().includes(q) || String(p.code).includes(q);
        return okCat && okQ;
      });
      wrap.innerHTML = '';
      if (!cat){
        wrap.innerHTML = '<div class="col-span-full text-center text-slate-400 py-16">اختر تصنيفًا من اليمين لعرض المنتجات هنا</div>';
        return;
      }
      if (list.length===0){
        wrap.innerHTML = '<div class="col-span-full text-center text-slate-400 py-16">لا توجد منتجات مطابقة</div>';
        return;
      }
      for (const p of list){
        const stockTxt = p.priceOnly ? 'يُباع بالسعر' : (p.stock ?? 0)+' متاح';
        const disabled = (!store.state.settings.allowNegativeStock && !p.priceOnly && (p.stock||0)<=0);
        const card = document.createElement('button');
        card.className = 'text-right rounded-lg border border-slate-200 hover:border-emerald-400 hover:shadow-sm p-3 bg-white disabled:opacity-50 disabled:cursor-not-allowed';
        card.disabled = disabled;
        card.innerHTML = `
          <div class="font-bold text-slate-800 line-clamp-1">${p.name}</div>
          <div class="text-xs text-slate-500">${p.category} • كود: ${p.code}</div>
          <div class="mt-2 flex items-center justify-between">
            <div class="text-emerald-700 font-bold">${currency(p.price)}</div>
            <div class="text-xs text-slate-500">${stockTxt}</div>
          </div>`;
        card.addEventListener('click', ()=> addToCart(p));
        wrap.appendChild(card);
      }
    }

    function renderReturnProducts(){
      const wrap = $('#ret-products');
      const cat = retFilter.cat;
      const list = store.state.products.filter(p=> !cat || cat==='all' ? true : p.category===cat);
      wrap.innerHTML = '';
      if (!cat){
        wrap.innerHTML = '<div class="col-span-full text-center text-slate-400 py-16">اختر تصنيفًا من اليمين لعرض المنتجات هنا للترجيع</div>';
        return;
      }
      if (list.length===0){
        wrap.innerHTML = '<div class="col-span-full text-center text-slate-400 py-16">لا توجد منتجات</div>';
        return;
      }
      for (const p of list){
        const card = document.createElement('button');
        card.className = 'text-right rounded-lg border border-slate-200 hover:border-rose-400 hover:shadow-sm p-3 bg-white';
        card.innerHTML = `
          <div class="font-bold text-slate-800 line-clamp-1">${p.name}</div>
          <div class="text-xs text-slate-500">${p.category} • كود: ${p.code}</div>
          <div class="mt-2 flex items-center justify-between">
            <div class="text-rose-700 font-bold">${currency(p.price)}</div>
            <div class="text-xs text-slate-500">${p.priceOnly ? 'يُباع بالسعر' : 'متوفر'}</div>
          </div>`;
        card.addEventListener('click', ()=> addToReturn(p));
        wrap.appendChild(card);
      }
    }

    function addToCart(p){
      if (p.priceOnly){
        // ask for price
        promptModal('إدخال قيمة البند (بقوليات)', `أدخل قيمة البيع لهذا البند: ${p.name}`, { fields:[{id:'price',label:'المبلغ (د.ل)',type:'number',step:'0.01',min:'0',value:fmt(p.price)}] })
          .then(data=>{
            if (!data) return; const price = Number(data.price||0);
            if (!(price>0)) return;
            cart.push({ productId:p.id, code:p.code, name:p.name, category:p.category, qty:1, price:price, total:price, cost:Number(p.cost||0), priceOnly:true });
            renderCart();
          });
      } else {
        // increase quantity or add
        const existing = cart.find(i=>i.productId===p.id && !i.priceOnly);
        const canAdd = store.state.settings.allowNegativeStock || (Number(p.stock||0) > (existing? existing.qty : 0));
        if (!canAdd){ alert('لا يمكن إضافة المزيد، المخزون غير كافٍ'); return; }
        if (existing){ existing.qty += 1; existing.total = existing.qty * existing.price; }
        else cart.push({ productId:p.id, code:p.code, name:p.name, category:p.category, qty:1, price:Number(p.price||0), total:Number(p.price||0), cost:Number(p.cost||0), priceOnly:false });
        renderCart();
      }
    }

    function addToReturn(p){
      if (p.priceOnly){
        promptModal('ترجيع (بقوليات)', `أدخل قيمة الترجيع لهذا البند: ${p.name}`, { fields:[{id:'price',label:'المبلغ (د.ل)',type:'number',step:'0.01',min:'0',value:fmt(p.price)}] })
          .then(data=>{ if (!data) return; const price = Number(data.price||0); if (!(price>0)) return; retCart.push({ productId:p.id, code:p.code, name:p.name, category:p.category, qty:1, price:price, total:price, cost:Number(p.cost||0), priceOnly:true }); renderRetCart(); });
      } else {
        const existing = retCart.find(i=>i.productId===p.id && !i.priceOnly);
        if (existing){ existing.qty += 1; existing.total = existing.qty * existing.price; }
        else retCart.push({ productId:p.id, code:p.code, name:p.name, category:p.category, qty:1, price:Number(p.price||0), total:Number(p.price||0), cost:Number(p.cost||0), priceOnly:false });
        renderRetCart();
      }
    }

    function renderCart(){
      const wrap = $('#cart-items');
      wrap.innerHTML = '';
      let total = 0; let count = 0;
      for (const item of cart){
        total += Number(item.total||0); count += 1;
        const row = document.createElement('div');
        row.className = 'border border-slate-200 rounded-lg p-2 text-sm';
        row.innerHTML = `
          <div class="flex justify-between items-center gap-2">
            <div>
              <div class="font-bold text-slate-800">${item.name}</div>
              <div class="text-xs text-slate-500">كود: ${item.code} • ${item.priceOnly ? 'بند بالسعر' : 'كمية'}</div>
            </div>
            <button class="text-rose-600 hover:text-rose-700" title="حذف">✕</button>
          </div>
          <div class="mt-2 grid grid-cols-3 gap-2 items-center">
            <div>
              ${item.priceOnly ? '<div class="text-xs text-slate-500 mb-1">المبلغ (د.ل)</div>' : '<div class="text-xs text-slate-500 mb-1">الكمية</div>'}
              ${item.priceOnly ? `<input class="i-price w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="0" step="0.01" value="${fmt(item.price)}">` : `<input class="i-qty w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="1" step="1" value="${item.qty}">`}
            </div>
            <div>
              <div class="text-xs text-slate-500 mb-1">سعر الوحدة</div>
              <input class="i-unit w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="0" step="0.01" value="${fmt(item.priceOnly ? (item.total||item.price) : item.price)}" ${item.priceOnly ? 'disabled' : ''}>
            </div>
            <div>
              <div class="text-xs text-slate-500 mb-1">الإجمالي</div>
              <div class="font-bold">${currency(item.total)}</div>
            </div>
          </div>`;
        const btnDel = row.querySelector('button');
        btnDel.addEventListener('click', ()=>{ cart = cart.filter(x=>x!==item); renderCart(); });
        if (item.priceOnly){
          row.querySelector('.i-price').addEventListener('input', (e)=>{ item.price = Number(e.target.value||0); item.total = item.price; renderCartTotals(); row.querySelectorAll('.font-bold')[1]?.textContent; });
        } else {
          row.querySelector('.i-qty').addEventListener('input', (e)=>{
            let q = Math.max(1, Math.floor(Number(e.target.value||1)));
            // stock validation
            const prod = store.state.products.find(p=>p.id===item.productId);
            if (prod && !store.state.settings.allowNegativeStock && q > (Number(prod.stock||0))){
              alert('الكمية تتجاوز المخزون المتاح');
              q = Number(prod.stock||0) || 1;
            }
            item.qty = q; item.total = q * item.price; renderCartTotals();
          });
          row.querySelector('.i-unit').addEventListener('input', (e)=>{ item.price = Number(e.target.value||0); item.total = item.qty * item.price; renderCartTotals(); });
        }
        wrap.appendChild(row);
      }
      $('#cart-count').textContent = count;
      $('#cart-total').textContent = currency(total);
    }

    function renderCartTotals(){
      let total = cart.reduce((a,c)=> a + Number(c.total||0), 0);
      $('#cart-total').textContent = currency(total);
    }

    function renderRetCart(){
      const wrap = $('#return-items');
      wrap.innerHTML = '';
      let total = 0; let count = 0;
      for (const item of retCart){
        total += Number(item.total||0); count += 1;
        const row = document.createElement('div');
        row.className = 'border border-slate-200 rounded-lg p-2 text-sm';
        row.innerHTML = `
          <div class="flex justify-between items-center gap-2">
            <div>
              <div class="font-bold text-slate-800">${item.name}</div>
              <div class="text-xs text-slate-500">كود: ${item.code} • ${item.priceOnly ? 'بند بالسعر' : 'كمية'}</div>
            </div>
            <button class="text-rose-600 hover:text-rose-700" title="حذف">✕</button>
          </div>
          <div class="mt-2 grid grid-cols-3 gap-2 items-center">
            <div>
              ${item.priceOnly ? '<div class="text-xs text-slate-500 mb-1">المبلغ (د.ل)</div>' : '<div class="text-xs text-slate-500 mb-1">الكمية</div>'}
              ${item.priceOnly ? `<input class="i-price w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="0" step="0.01" value="${fmt(item.price)}">` : `<input class="i-qty w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="1" step="1" value="${item.qty}">`}
            </div>
            <div>
              <div class="text-xs text-slate-500 mb-1">سعر الوحدة</div>
              <input class="i-unit w-full rounded-lg border border-slate-300 px-2 py-1 number-input" type="number" min="0" step="0.01" value="${fmt(item.priceOnly ? (item.total||item.price) : item.price)}" ${item.priceOnly ? 'disabled' : ''}>
            </div>
            <div>
              <div class="text-xs text-slate-500 mb-1">الإجمالي</div>
              <div class="font-bold">${currency(item.total)}</div>
            </div>
          </div>`;
        row.querySelector('button').addEventListener('click', ()=>{ retCart = retCart.filter(x=>x!==item); renderRetCart(); });
        if (item.priceOnly){ row.querySelector('.i-price').addEventListener('input', (e)=>{ item.price = Number(e.target.value||0); item.total = item.price; renderRetTotals(); }); }
        else {
          row.querySelector('.i-qty').addEventListener('input', (e)=>{ let q = Math.max(1, Math.floor(Number(e.target.value||1))); item.qty = q; item.total = q * item.price; renderRetTotals(); });
          row.querySelector('.i-unit').addEventListener('input', (e)=>{ item.price = Number(e.target.value||0); item.total = item.qty * item.price; renderRetTotals(); });
        }
        wrap.appendChild(row);
      }
      $('#return-count').textContent = count;
      $('#return-total').textContent = currency(total);
    }

    function renderRetTotals(){
      const total = retCart.reduce((a,c)=> a + Number(c.total||0), 0);
      $('#return-total').textContent = currency(total);
    }

    // Inventory rendering
    function renderInventory(){
      const q = ($('#inv-search').value||'').trim().toLowerCase();
      const fcat = $('#inv-cat-filter').value;
      const body = $('#inv-tbody');
      body.innerHTML = '';
      let rows = 0;
      for (const p of store.state.products){
        const okQ = !q || p.name.toLowerCase().includes(q) || String(p.code).includes(q);
        const okCat = fcat==='all' || p.category===fcat;
        if (!okQ || !okCat) continue;
        rows++;
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td class="p-2">${p.code}</td>
          <td class="p-2">${p.name}</td>
          <td class="p-2">${p.category}</td>
          <td class="p-2">${currency(p.price)}</td>
          <td class="p-2">${currency(p.cost||0)}</td>
          <td class="p-2">${p.priceOnly ? '-' : (p.stock ?? 0)}</td>
          <td class="p-2 text-slate-500 text-xs">${p.priceOnly ? 'يباع بالسعر فقط (بدون كمية)' : ''}</td>
          <td class="p-2">
            <div class="flex flex-wrap gap-2">
              <button class="px-2 py-1 rounded border border-slate-300 hover:bg-slate-100 edit">تعديل</button>
              <button class="px-2 py-1 rounded border border-rose-300 text-rose-600 hover:bg-rose-50 del">حذف</button>
              ${!p.priceOnly ? '<button class="px-2 py-1 rounded border border-slate-300 hover:bg-slate-100 stock">تعديل الكمية</button>' : ''}
            </div>
          </td>`;
        tr.querySelector('.edit').addEventListener('click', ()=> openProductModal(p));
        tr.querySelector('.del').addEventListener('click', ()=> deleteProduct(p.id));
        if (!p.priceOnly) tr.querySelector('.stock').addEventListener('click', ()=> adjustStock(p));
        body.appendChild(tr);
      }
      $('#inv-total-count').textContent = rows;
    }

    function deleteProduct(id){
      if (!confirm('تأكيد حذف المنتج؟')) return;
      store.state.products = store.state.products.filter(p=>p.id!==id);
      store.save();
      renderInventory();
      renderPOSProducts();
      renderReturnProducts();
    }

    function adjustStock(p){
      promptModal('تعديل الكمية', `أدخل الكمية الجديدة للمنتج: ${p.name}`, { fields:[{id:'stock',label:'الكمية',type:'number',step:'1',min:'0',value: String(p.stock ?? 0)}] })
        .then(data=>{ if (!data) return; p.stock = Math.max(0, Math.floor(Number(data.stock||0))); store.save(); renderInventory(); renderPOSProducts(); });
    }

    // Product modal
    function openProductModal(p=null){
      const isEdit = !!p;
      const fields = [
        {id:'code',label:'الكود',type:'text',value:p?.code||''},
        {id:'name',label:'الاسم',type:'text',value:p?.name||''},
        {id:'category',label:'التصنيف',type:'select',options:['مشروبات','عصائر','شكولاتة','مواد غذائية','بقوليات'],value:p?.category||'مشروبات'},
        {id:'price',label:'سعر البيع (د.ل)',type:'number',step:'0.01',min:'0',value:fmt(p?.price||0)},
        {id:'cost',label:'سعر التكلفة (د.ل)',type:'number',step:'0.01',min:'0',value:fmt(p?.cost||0)},
        {id:'stock',label:'الكمية',type:'number',step:'1',min:'0',value: p?.priceOnly ? '' : String(p?.stock ?? 0)},
        {id:'priceOnly',label:'يباع بالسعر فقط (بدون كمية) - للبقوليات',type:'checkbox',checked: !!p?.priceOnly}
      ];
      promptModal(isEdit ? 'تعديل منتج' : 'إضافة منتج', 'يرجى إدخال بيانات المنتج', {fields}).then(data=>{
        if (!data) return;
        const code = (data.code||'').trim();
        const name = (data.name||'').trim();
        const category = data.category;
        const price = Number(data.price||0);
        const cost = Number(data.cost||0);
        const priceOnly = !!data.priceOnly;
        const stock = priceOnly ? null : Math.max(0, Math.floor(Number(data.stock||0)));
        if (!code || !name){ alert('الكود والاسم إجباريان'); return; }
        // unique code check
        if (store.state.products.some(x=>x.code===code && x!==p)){ alert('الكود مستخدم لمنتج آخر'); return; }
        if (isEdit){ Object.assign(p, {code,name,category,price,cost,priceOnly,stock}); }
        else { store.state.products.push({ id:newId('p'), code,name,category,price,cost,priceOnly,stock }); }
        store.save();
        renderInventory(); renderPOSProducts(); renderReturnProducts();
      });
    }

    // Modal Helper
    function promptModal(title, message, opts={}){
      return new Promise(resolve=>{
        $('#modal-title').textContent = title||'';
        const body = $('#modal-body');
        body.innerHTML = '';
        if (message){ const p = document.createElement('p'); p.className='text-sm text-slate-600'; p.textContent = message; body.appendChild(p); }
        const form = document.createElement('div'); form.className='mt-2 space-y-2';
        const fields = opts.fields||[];
        for (const f of fields){
          const wrap = document.createElement('div');
          const label = document.createElement('label'); label.className='text-sm text-slate-600'; label.textContent = f.label||''; wrap.appendChild(label);
          if (f.type==='select'){
            const sel = document.createElement('select'); sel.className='w-full rounded-lg border border-slate-300 px-3 py-2';
            (f.options||[]).forEach(o=>{ const op = document.createElement('option'); op.value=o; op.textContent=o; if (String(o)===String(f.value)) op.selected = true; sel.appendChild(op); });
            sel.id = f.id; wrap.appendChild(sel);
          } else if (f.type==='checkbox'){
            const chkWrap = document.createElement('div'); chkWrap.className='flex items-center gap-2 mt-1';
            const inp = document.createElement('input'); inp.type='checkbox'; inp.id=f.id; inp.className='rounded border-slate-300'; inp.checked=!!f.checked;
            chkWrap.appendChild(inp);
            const lbl = document.createElement('label'); lbl.textContent = f.label; lbl.htmlFor=f.id; lbl.className='text-sm text-slate-700'; chkWrap.appendChild(lbl);
            wrap.innerHTML=''; wrap.appendChild(chkWrap);
          } else {
            const inp = document.createElement('input'); inp.className='w-full rounded-lg border border-slate-300 px-3 py-2'; inp.id=f.id; inp.type=f.type||'text';
            if (f.step) inp.step=f.step; if (f.min) inp.min=f.min; if (f.max) inp.max=f.max; if (f.placeholder) inp.placeholder=f.placeholder;
            if (f.value!==undefined) inp.value=f.value;
            wrap.appendChild(inp);
          }
          form.appendChild(wrap);
        }
        body.appendChild(form);
        $('#modal').classList.remove('hidden');
        const cancel = ()=>{ $('#modal').classList.add('hidden'); resolve(null); };
        $('#modal-cancel').onclick = cancel;
        $('#modal-ok').onclick = ()=>{
          const result = {};
          for (const f of fields){
            const el = document.getElementById(f.id);
            if (!el) continue;
            if ((f.type||'')==='checkbox') result[f.id] = el.checked; else result[f.id] = el.value;
          }
          $('#modal').classList.add('hidden');
          resolve(result);
        };
      });
    }

    // Checkout
    function checkout(){
      if (cart.length===0){ alert('السلة فارغة'); return; }
      let payment = ($('.pay-method:checked')||{}).value || 'cash';
      let custId = null, custName=null;
      if (payment==='credit'){
        custName = ($('#credit-customer-name').value||'').trim();
        const selId = $('#credit-customer-select').value;
        if (selId) custId = selId; else if (!custName) { alert('يرجى إدخال/اختيار العميل'); return; }
      }
      // stock validation for non-priceOnly
      for (const item of cart){
        if (!item.priceOnly){
          const p = store.state.products.find(x=>x.id===item.productId);
          const st = Number(p?.stock||0);
          if (!store.state.settings.allowNegativeStock && item.qty>st){
            alert('بعض الكميات تتجاوز المخزون'); return;
          }
        }
      }
      const date = nowISO();
      const total = cart.reduce((a,c)=> a + Number(c.total||0), 0);
      const costTotal = cart.reduce((a,c)=> a + (Number(c.cost||0) * (c.priceOnly? 0 : Number(c.qty||0))), 0);
      const sale = { id:newId('s'), type:'sale', items: JSON.parse(JSON.stringify(cart)), paymentMethod: payment, customerId:custId||null, customerName:custName||null, date, totals: { total, cost: costTotal, profit: total - costTotal } };
      store.state.sales.push(sale);
      // adjust stock
      for (const item of cart){
        if (!item.priceOnly){
          const p = store.state.products.find(x=>x.id===item.productId);
          if (p) p.stock = Number(p.stock||0) - Number(item.qty||0);
        }
      }
      // handle credit
      if (payment==='credit'){
        let customer = null;
        if (custId) customer = store.state.customers.find(c=>c.id===custId);
        if (!customer){ customer = { id:newId('c'), name: custName, phone:'', balance:0, updatedAt:date, transactions:[] }; store.state.customers.push(customer); }
        customer.balance += total; customer.updatedAt = date;
        customer.transactions.push({ id:newId('ct'), type:'sale', amount: total, date, note:'بيع على الحساب', ref: sale.id });
      }
      store.save();
      cart = []; renderCart(); renderInventory(); updateDash();
      alert('تمت عملية البيع بنجاح');
    }

    // Process return
    function processReturn(){
      if (retCart.length===0){ alert('سلة الترجيع فارغة'); return; }
      let payment = ($('.ret-pay-method:checked')||{}).value || 'cash';
      let custId = null, custName=null;
      if (payment==='credit'){
        custName = ($('#ret-credit-customer-name').value||'').trim();
        const selId = $('#ret-credit-customer-select').value;
        if (selId) custId = selId; else if (!custName) { alert('يرجى إدخال/اختيار العميل'); return; }
      }
      const date = nowISO();
      const total = retCart.reduce((a,c)=> a + Number(c.total||0), 0);
      const costTotal = retCart.reduce((a,c)=> a + (Number(c.cost||0) * (c.priceOnly? 0 : Number(c.qty||0))), 0);
      const sale = { id:newId('s'), type:'return', items: JSON.parse(JSON.stringify(retCart)), paymentMethod: payment, customerId:custId||null, customerName:custName||null, date, totals: { total: -total, cost: -costTotal, profit: -(total - costTotal) } };
      store.state.sales.push(sale);
      // adjust stock back
      for (const item of retCart){
        if (!item.priceOnly){ const p = store.state.products.find(x=>x.id===item.productId); if (p) p.stock = Number(p.stock||0) + Number(item.qty||0); }
      }
      // handle credit: reduce customer's balance
      if (payment==='credit'){
        let customer = null;
        if (custId) customer = store.state.customers.find(c=>c.id===custId);
        if (!customer){ customer = { id:newId('c'), name: custName, phone:'', balance:0, updatedAt:date, transactions:[] }; store.state.customers.push(customer); }
        customer.balance -= total; customer.updatedAt = date;
        customer.transactions.push({ id:newId('ct'), type:'return', amount: -total, date, note:'ترجيع على الحساب', ref: sale.id });
      }
      store.save();
      retCart = []; renderRetCart(); renderInventory(); updateDash();
      alert('تمت عملية الترجيع بنجاح');
    }

    // Customers
    function renderCustomers(){
      const q = ($('#cust-search').value||'').trim().toLowerCase();
      const body = $('#cust-tbody'); body.innerHTML = '';
      for (const c of store.state.customers){
        if (q && !(c.name.toLowerCase().includes(q) || (c.phone||'').includes(q))) continue;
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td class="p-2 font-bold">${c.name}</td>
          <td class="p-2">${c.phone||'-'}</td>
          <td class="p-2 ${c.balance>0 ? 'text-amber-700' : 'text-emerald-700'}">${currency(c.balance)}</td>
          <td class="p-2 text-slate-500 text-xs">${fmtDate(c.updatedAt)}</td>
          <td class="p-2">
            <div class="flex flex-wrap gap-2">
              <button class="px-2 py-1 rounded border border-slate-300 hover:bg-slate-100 pay">دفع الدين</button>
              <button class="px-2 py-1 rounded border border-slate-300 hover:bg-slate-100 view">تفاصيل</button>
              <button class="px-2 py-1 rounded border border-rose-300 text-rose-600 hover:bg-rose-50 del">حذف</button>
            </div>
          </td>`;
        tr.querySelector('.pay').addEventListener('click', ()=> payDebt(c));
        tr.querySelector('.view').addEventListener('click', ()=> viewCustomer(c));
        tr.querySelector('.del').addEventListener('click', ()=> deleteCustomer(c.id));
        body.appendChild(tr);
      }
    }

    function deleteCustomer(id){
      if (!confirm('حذف العميل سيحذف معاملاته الداخلية من السجل (لن يحذف المبيعات). تأكيد؟')) return;
      store.state.customers = store.state.customers.filter(c=>c.id!==id);
      store.save(); renderCustomers();
    }

    function payDebt(c){
      promptModal('دفع الدين', `إدخال دفعة للعميل: ${c.name}`, {fields:[{id:'amount',label:'المبلغ (د.ل)',type:'number',min:'0',step:'0.01',value:fmt(Math.max(0,c.balance))},{id:'note',label:'ملاحظة',type:'text',value:'دفع دين'}]}).then(data=>{
        if (!data) return; const amount = Number(data.amount||0); if (!(amount>0)) return;
        const date = nowISO();
        c.balance = Math.max(0, Number(c.balance||0) - amount);
        c.transactions.push({ id:newId('ct'), type:'payment', amount: -amount, date, note: data.note||'دفع دين' });
        c.updatedAt = date; store.save(); renderCustomers();
      });
    }

    function viewCustomer(c){
      const body = document.createElement('div');
      body.innerHTML = `<div class="text-sm text-slate-700">الرصيد الحالي: <strong>${currency(c.balance)}</strong></div>`;
      const list = document.createElement('div'); list.className='mt-2 max-h-[260px] overflow-auto';
      for (const t of (c.transactions||[]).slice().reverse()){
        const div = document.createElement('div');
        const typeTxt = t.type==='sale' ? 'بيع على الحساب' : (t.type==='return' ? 'ترجيع' : 'دفع');
        div.className='text-sm border-b border-slate-100 py-1';
        div.textContent = `${typeTxt} • ${fmtDate(t.date)} • ${currency(t.amount)}`;
        list.appendChild(div);
      }
      body.appendChild(list);
      // open modal
      $('#modal-title').textContent = 'تفاصيل العميل - ' + c.name;
      $('#modal-body').innerHTML = '';
      $('#modal-body').appendChild(body);
      $('#modal').classList.remove('hidden');
      $('#modal-ok').textContent = 'إغلاق';
      $('#modal-cancel').classList.add('hidden');
      const close = ()=>{ $('#modal').classList.add('hidden'); $('#modal-ok').textContent='موافق'; $('#modal-cancel').classList.remove('hidden'); };
      $('#modal-ok').onclick = close;
      $('#modal-cancel').onclick = close;
    }

    // Expenses
    function renderExpenses(){
      const body = $('#exp-tbody'); body.innerHTML='';
      let total = 0;
      for (const e of store.state.expenses.slice().reverse()){
        total += Number(e.amount||0);
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td class="p-2">${fmtDate(e.date)}</td>
          <td class="p-2">${currency(e.amount)}</td>
          <td class="p-2">${e.note||''}</td>
          <td class="p-2"><button class="px-2 py-1 rounded border border-rose-300 text-rose-600 hover:bg-rose-50 del">حذف</button></td>`;
        tr.querySelector('.del').addEventListener('click', ()=>{ if(!confirm('تأكيد حذف المصروف؟')) return; store.state.expenses = store.state.expenses.filter(x=>x.id!==e.id); store.save(); renderExpenses(); updateDash(); });
        body.appendChild(tr);
      }
      $('#exp-total').textContent = currency(total);
    }

    // Reports
    function runReport(){
      const type = $('#rep-type').value;
      const dateStr = $('#rep-date').value;
      const monthStr = $('#rep-month').value;
      let inRange;
      if (type==='daily'){
        const d = new Date(dateStr||new Date());
        inRange = (iso)=>{ const dt = new Date(iso); return dt.getFullYear()===d.getFullYear() && dt.getMonth()===d.getMonth() && dt.getDate()===d.getDate(); };
      } else {
        const d = new Date(monthStr ? monthStr+'-01' : new Date());
        inRange = (iso)=>{ const dt = new Date(iso); return dt.getFullYear()===d.getFullYear() && dt.getMonth()===d.getMonth(); };
      }
      const sales = store.state.sales.filter(s=> inRange(s.date));
      const expenses = store.state.expenses.filter(e=> inRange(e.date));
      // Totals
      const totalSales = sales.reduce((a,s)=> a + Number(s.totals.total||0), 0);
      const totalCost = sales.reduce((a,s)=> a + Number(s.totals.cost||0), 0);
      const expTotal = expenses.reduce((a,e)=> a + Number(e.amount||0), 0);
      const profit = (totalSales - totalCost) - expTotal;
      $('#rep-sales').textContent = currency(totalSales);
      $('#rep-cost').textContent = currency(totalCost);
      $('#rep-exp').textContent = currency(expTotal);
      $('#rep-profit').textContent = currency(profit);
      // transactions table
      const tbody = $('#rep-tbody'); tbody.innerHTML='';
      for (const s of sales.slice().reverse()){
        const tr = document.createElement('tr');
        const typeTxt = s.type==='sale' ? 'بيع' : 'ترجيع';
        const itemsTxt = s.items.map(i=> `${i.name}${i.priceOnly?'':` × ${i.qty}`}`).join('، ');
        const payTxt = s.paymentMethod==='cash' ? 'نقدًا' : s.paymentMethod==='card' ? 'بطاقة' : 'على الحساب';
        tr.innerHTML = `
          <td class="p-2">${typeTxt}</td>
          <td class="p-2">${fmtDate(s.date)}</td>
          <td class="p-2">${payTxt}</td>
          <td class="p-2">${currency(s.totals.total)}</td>
          <td class="p-2 text-slate-600">${itemsTxt}</td>`;
        tbody.appendChild(tr);
      }
      // payment breakdown
      const pays = { cash:0, card:0, credit:0 };
      for (const s of sales){ pays[s.paymentMethod] += Number(s.totals.total||0); }
      const paysWrap = $('#rep-pays'); paysWrap.innerHTML='';
      for (const k of ['cash','card','credit']){
        const li = document.createElement('li');
        const label = k==='cash' ? 'نقدًا' : k==='card' ? 'بطاقة' : 'على الحساب';
        li.textContent = `${label}: ${currency(pays[k])}`;
        paysWrap.appendChild(li);
      }
      // products breakdown
      const prods = new Map();
      for (const s of sales){
        for (const i of s.items){
          const key = i.name + (i.priceOnly? ' (سعر)' : '');
          if (!prods.has(key)) prods.set(key, { qty:0, total:0 });
          prods.get(key).qty += i.priceOnly ? 0 : (s.type==='sale'? i.qty : -i.qty);
          prods.get(key).total += s.type==='sale' ? Number(i.total||0) : -Number(i.total||0);
        }
      }
      const prodWrap = $('#rep-products'); prodWrap.innerHTML='';
      for (const [name,agg] of prods){
        const li = document.createElement('li');
        const qtyTxt = agg.qty ? ` • كمية: ${agg.qty}` : '';
        li.textContent = `${name}: ${currency(agg.total)}${qtyTxt}`;
        prodWrap.appendChild(li);
      }
    }

    // Dashboard
    function updateDash(){
      // today
      const today = new Date();
      const sameDay = (iso)=>{ const d=new Date(iso); return d.getFullYear()===today.getFullYear() && d.getMonth()===today.getMonth() && d.getDate()===today.getDate(); };
      const sales = store.state.sales.filter(s=> sameDay(s.date));
      const expenses = store.state.expenses.filter(e=> sameDay(e.date));
      const totalSales = sales.reduce((a,s)=> a + Number(s.totals.total||0), 0);
      const cost = sales.reduce((a,s)=> a + Number(s.totals.cost||0), 0);
      const exp = expenses.reduce((a,e)=> a + Number(e.amount||0), 0);
      const profit = (totalSales - cost) - exp;
      $('#dash-today-sales').textContent = currency(totalSales);
      $('#dash-today-exp').textContent = currency(exp);
      $('#dash-today-profit').textContent = currency(profit);
      // low stock
      const lvl = store.state.settings.lowStockLevel||5;
      const low = store.state.products.filter(p=> !p.priceOnly && Number(p.stock||0) <= lvl);
      const ul = $('#dash-low-stock'); ul.innerHTML='';
      if (low.length===0) ul.innerHTML = '<li class="text-slate-400">لا توجد تنبيهات</li>';
      for (const p of low){ const li = document.createElement('li'); li.textContent = `${p.name} • ${p.stock ?? 0}`; ul.appendChild(li); }
      // DB panel
      renderDbPanel();
    }

    // Export/Import
    function exportBackup(){
      const data = JSON.stringify(store.state, null, 2);
      const blob = new Blob([data], {type:'application/json'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href=url; a.download='sahel-backup.json'; a.click(); URL.revokeObjectURL(url);
    }

    function importBackup(file){
      const reader = new FileReader();
      reader.onload = ()=>{
        try {
          const data = JSON.parse(reader.result);
          if (!data || typeof data !== 'object') throw new Error('ملف غير صالح');
          store.state = Object.assign(defaultState(), data);
          store.save();
          initUI();
          alert('تم الاستيراد بنجاح');
        } catch(e){ alert('فشل الاستيراد: '+e.message); }
      };
      reader.readAsText(file);
    }

    // DB panel helpers
    function renderDbPanel(){
      // status
      $('#db-status').textContent = db.db ? 'متصل' : 'غير متصل';
      $('#db-last-test').textContent = store.state.meta?.lastDbTest ? fmtDate(store.state.meta.lastDbTest) : '--';
    }

    async function testDatabase(){
      try {
        // Save a small tick into meta and persist
        store.state.meta = store.state.meta || {};
        store.state.meta.lastDbTest = nowISO();
        await store.save();
        renderDbPanel();
        alert('تم اختبار القاعدة وحفظ التغيير بنجاح');
      } catch(e){
        alert('فشل الاختبار: '+ (e?.message||e));
      }
    }

    // Event bindings and init
    function initUI(){
      // Tabs
      $$('.tab-btn').forEach(b=> b.addEventListener('click', ()=> showTab(b.dataset.tab)));
      showTab('pos');

      // POS
      $$('.cat-btn').forEach(btn=> btn.addEventListener('click', ()=>{ posFilter.cat = btn.dataset.cat; $('#pos-current-cat').textContent = posFilter.cat==='all' ? 'عرض الكل' : ('التصنيف: '+posFilter.cat); renderPOSProducts(); }));
      $('#pos-search').addEventListener('input', renderPOSProducts);
      $('#pos-code').addEventListener('keydown', (e)=>{ if(e.key==='Enter'){ const p = findProductByCode(e.target.value); if(p){ addToCart(p); e.target.value=''; } else alert('لم يتم العثور على منتج بهذا الكود'); }});
      $('#btn-clear-cart').addEventListener('click', ()=>{ cart=[]; renderCart(); });
      $('#btn-checkout').addEventListener('click', checkout);
      $$('.pay-method').forEach(r=> r.addEventListener('change', ()=>{ const credit = ($('.pay-method:checked')||{}).value==='credit'; $('#credit-area').classList.toggle('hidden', !credit); refreshCreditSelect('#credit-customer-select'); }));

      // Returns
      $$('.ret-cat-btn').forEach(btn=> btn.addEventListener('click', ()=>{ retFilter.cat = btn.dataset.cat; $('#ret-current-cat').textContent = retFilter.cat==='all' ? 'عرض الكل' : ('التصنيف: '+retFilter.cat); renderReturnProducts(); }));
      $('#return-code').addEventListener('keydown', (e)=>{ if(e.key==='Enter'){ const p = findProductByCode(e.target.value); if(p){ addToReturn(p); e.target.value=''; } else alert('لم يتم العثور على منتج بهذا الكود'); }});
      $('#btn-clear-return').addEventListener('click', ()=>{ retCart=[]; renderRetCart(); });
      $('#btn-process-return').addEventListener('click', processReturn);
      $$('.ret-pay-method').forEach(r=> r.addEventListener('change', ()=>{ const credit = ($('.ret-pay-method:checked')||{}).value==='credit'; $('#ret-credit-area').classList.toggle('hidden', !credit); refreshCreditSelect('#ret-credit-customer-select'); }));

      // Inventory
      $('#btn-add-sample').addEventListener('click', addSampleProducts);
      $('#btn-new-product').addEventListener('click', ()=> openProductModal());
      $('#inv-search').addEventListener('input', renderInventory);
      $('#inv-cat-filter').addEventListener('change', renderInventory);
      $('#btn-export').addEventListener('click', exportBackup);
      $('#import-file').addEventListener('change', (e)=>{ if (e.target.files[0]) importBackup(e.target.files[0]); e.target.value=''; });

      // Customers
      $('#btn-new-customer').addEventListener('click', ()=>{
        promptModal('عميل جديد', 'أدخل بيانات العميل', {fields:[{id:'name',label:'الاسم',type:'text'},{id:'phone',label:'الهاتف',type:'text'}]}).then(data=>{
          if (!data) return; const name=(data.name||'').trim(); if (!name) return alert('الاسم مطلوب');
          const c={ id:newId('c'), name, phone:(data.phone||'').trim(), balance:0, updatedAt: nowISO(), transactions:[] };
          store.state.customers.push(c); store.save(); renderCustomers();
        });
      });
      $('#cust-search').addEventListener('input', renderCustomers);

      // Expenses
      $('#btn-add-expense').addEventListener('click', ()=>{
        const amount = Number($('#exp-amount').value||0); const note = $('#exp-note').value||'';
        if (!(amount>0)) return alert('أدخل مبلغًا صحيحًا');
        store.state.expenses.push({ id:newId('e'), amount, note, date: nowISO() });
        store.save(); $('#exp-amount').value=''; $('#exp-note').value=''; renderExpenses(); updateDash();
      });

      // Reports
      $('#rep-type').addEventListener('change', ()=>{
        const t = $('#rep-type').value;
        $('#rep-date-wrap').classList.toggle('hidden', t!=='daily');
        $('#rep-month-wrap').classList.toggle('hidden', t!=='monthly');
      });
      $('#btn-run-report').addEventListener('click', runReport);

      // Settings
      $('#btn-save-settings').addEventListener('click', ()=>{
        const s = store.state.settings;
        s.storeName = $('#set-store-name').value || s.storeName;
        s.currencySymbol = $('#set-curr-symbol').value || s.currencySymbol;
        s.currency = $('#set-currency').value || s.currency;
        s.allowNegativeStock = $('#set-negative-stock').checked;
        store.save(); refreshSettings(); refreshHeader(); renderPOSProducts(); updateDash();
        alert('تم حفظ الإعدادات');
      });

      // DB panel button
      $('#btn-db-test').addEventListener('click', testDatabase);
      renderDbPanel();

      refreshSettings();
      renderInventory();
      renderCustomers();
      renderExpenses();
      renderPOSProducts();
      renderReturnProducts();
      renderCart(); renderRetCart();
      updateDash();
      refreshCreditSelect('#credit-customer-select');
      refreshCreditSelect('#ret-credit-customer-select');

      // Default report date/month
      const today = new Date();
      $('#rep-date').valueAsDate = today;
      $('#rep-month').value = today.toISOString().slice(0,7);
      runReport();
    }

    function refreshCreditSelect(sel){
      const s = $(sel); if (!s) return;
      s.innerHTML = '<option value="">-- اختر عميل --</option>';
      for (const c of store.state.customers){ const op=document.createElement('option'); op.value=c.id; op.textContent=c.name + (c.balance? ` (${currency(c.balance)})`:''); s.appendChild(op); }
    }

    function refreshSettings(){
      const s = store.state.settings;
      $('#set-store-name').value = s.storeName;
      $('#set-curr-symbol').value = s.currencySymbol;
      $('#set-currency').value = s.currency;
      $('#set-negative-stock').checked = !!s.allowNegativeStock;
    }

    // Init
    (async function(){
      await store.load();
      refreshHeader();
      initUI();
    })();
  </script>
</body>
</html>
