<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إدارة المبيعات والمصروفات</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .tabs {
            display: flex;
            background: #f5f5f5;
            border-bottom: 2px solid #ddd;
            flex-wrap: wrap;
        }

        .tab-btn {
            padding: 15px 30px;
            border: none;
            background: #f5f5f5;
            cursor: pointer;
            font-size: 1em;
            font-weight: bold;
            color: #666;
            transition: all 0.3s;
            border-bottom: 3px solid transparent;
        }

        .tab-btn:hover {
            background: #e0e0e0;
        }

        .tab-btn.active {
            background: white;
            color: #667eea;
            border-bottom-color: #667eea;
        }

        .content {
            padding: 30px;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.3s;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
            font-family: inherit;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 5px rgba(102, 126, 234, 0.3);
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .form-row.full {
            grid-template-columns: 1fr;
        }

        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        button:active {
            transform: translateY(0);
        }

        .btn-secondary {
            background: #6c757d;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .btn-danger {
            background: #dc3545;
        }

        .btn-danger:hover {
            background: #c82333;
        }

        .table-responsive {
            overflow-x: auto;
            margin-top: 20px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }

        th {
            background: #667eea;
            color: white;
            padding: 15px;
            text-align: right;
            font-weight: bold;
        }

        td {
            padding: 12px 15px;
            border-bottom: 1px solid #ddd;
        }

        tr:hover {
            background: #f9f9f9;
        }

        .success-message {
            background: #d4edda;
            color: #155724;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #c3e6cb;
            display: none;
        }

        .success-message.show {
            display: block;
        }

        .error-message {
            background: #f8d7da;
            color: #721c24;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #f5c6cb;
            display: none;
        }

        .error-message.show {
            display: block;
        }

        .alert-warning {
            background: #fff3cd;
            color: #856404;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #ffeaa7;
        }

        .alert-danger {
            background: #f8d7da;
            color: #721c24;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border: 1px solid #f5c6cb;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-card h3 {
            font-size: 0.9em;
            margin-bottom: 10px;
            opacity: 0.9;
        }

        .stat-card .value {
            font-size: 2em;
            font-weight: bold;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal.show {
            display: flex;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            font-size: 1.5em;
            margin-bottom: 20px;
            border-bottom: 2px solid #ddd;
            padding-bottom: 15px;
        }

        .modal-footer {
            margin-top: 20px;
            display: flex;
            gap: 10px;
            justify-content: flex-start;
        }

        .action-buttons {
            display: flex;
            gap: 5px;
            justify-content: center;
            flex-wrap: wrap;
        }

        .action-buttons button {
            padding: 8px 12px;
            font-size: 0.9em;
        }

        .btn-sm {
            padding: 8px 12px;
            font-size: 0.85em;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            z-index: 2000;
            max-width: 400px;
            animation: slideIn 0.3s;
        }

        @keyframes slideIn {
            from {
                transform: translateX(400px);
            }
            to {
                transform: translateX(0);
            }
        }

        .notification.warning {
            border-right: 5px solid #ff9800;
        }

        .notification.success {
            border-right: 5px solid #4caf50;
        }

        .notification.error {
            border-right: 5px solid #f44336;
        }

        .notification-title {
            font-weight: bold;
            margin-bottom: 5px;
        }

        .close-btn {
            float: left;
            cursor: pointer;
            font-size: 1.5em;
            color: #999;
        }

        @media (max-width: 768px) {
            .form-row {
                grid-template-columns: 1fr;
            }

            .tabs {
                flex-direction: column;
            }

            .tab-btn {
                width: 100%;
                text-align: right;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }

            table {
                font-size: 0.9em;
            }

            th, td {
                padding: 8px 10px;
            }
        }

        .payment-method-badge {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 3px;
            font-size: 0.85em;
            font-weight: bold;
        }

        .payment-card {
            background: #e3f2fd;
            color: #1976d2;
        }

        .payment-cash {
            background: #f3e5f5;
            color: #7b1fa2;
        }

        .payment-account {
            background: #e8f5e9;
            color: #388e3c;
        }

        .low-stock {
            color: #f44336;
            font-weight: bold;
        }

        .print-btn {
            background: #4caf50;
        }

        .print-btn:hover {
            background: #45a049;
        }

        @media print {
            body {
                background: white;
                padding: 0;
            }
            .tabs, .action-buttons, .btn-secondary, .print-btn, .btn-danger {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏪 نظام إدارة المبيعات والمصروفات</h1>
            <p>إدارة منتجاتك والمبيعات والمصروفات بسهولة</p>
        </div>

        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('products')">📦 المنتجات</button>
            <button class="tab-btn" onclick="switchTab('sales')">💳 المبيعات</button>
            <button class="tab-btn" onclick="switchTab('expenses')">💰 المصروفات</button>
            <button class="tab-btn" onclick="switchTab('reports')">📊 التقارير</button>
            <button class="tab-btn" onclick="switchTab('notifications')">🔔 الإشعارات</button>
        </div>

        <div class="content">
            <!-- Products Tab -->
            <div id="products" class="tab-content active">
                <h2>إدارة المنتجات</h2>
                <div class="success-message" id="productSuccess"></div>
                <div class="error-message" id="productError"></div>

                <div class="form-row">
                    <div class="form-group">
                        <label>اسم المنتج</label>
                        <input type="text" id="productName" placeholder="أدخل اسم المنتج">
                    </div>
                    <div class="form-group">
                        <label>السعر</label>
                        <input type="number" id="productPrice" placeholder="أدخل السعر" min="0" step="0.01">
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>الكمية</label>
                        <input type="number" id="productQuantity" placeholder="أدخل الكمية" min="0">
                    </div>
                    <div class="form-group">
                        <label>حد التنبيه (إشعار عند الوصول)</label>
                        <input type="number" id="productAlert" placeholder="أدخل الحد الأدنى" min="0">
                    </div>
                </div>

                <div class="form-group">
                    <label>الوصف</label>
                    <textarea id="productDescription" placeholder="أدخل وصف المنتج" rows="3"></textarea>
                </div>

                <button onclick="addProduct()">➕ إضافة منتج</button>

                <div class="table-responsive">
                    <table id="productsTable">
                        <thead>
                            <tr>
                                <th>الرقم</th>
                                <th>اسم المنتج</th>
                                <th>السعر</th>
                                <th>الكمية</th>
                                <th>حد التنبيه</th>
                                <th>الحالة</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- Sales Tab -->
            <div id="sales" class="tab-content">
                <h2>تسجيل المبيعات</h2>
                <div class="success-message" id="saleSuccess"></div>
                <div class="error-message" id="saleError"></div>

                <div class="form-row">
                    <div class="form-group">
                        <label>تاريخ البيع</label>
                        <input type="date" id="saleDate">
                    </div>
                    <div class="form-group">
                        <label>المنتج</label>
                        <select id="saleProduct"></select>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>الكمية</label>
                        <input type="number" id="saleQuantity" placeholder="أدخل الكمية المباعة" min="1">
                    </div>
                    <div class="form-group">
                        <label>السعر النهائي</label>
                        <input type="number" id="salePrice" placeholder="السعر النهائي" min="0" step="0.01">
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>طريقة الدفع</label>
                        <select id="paymentMethod">
                            <option value="card">💳 بطاقة</option>
                            <option value="cash">💵 نقدا</option>
                            <option value="account">📖 على الحساب</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>اسم العميل</label>
                        <input type="text" id="customerName" placeholder="اسم العميل (اختياري)">
                    </div>
                </div>

                <div class="form-group">
                    <label>ملاحظات</label>
                    <textarea id="saleNotes" placeholder="ملاحظات إضافية" rows="2"></textarea>
                </div>

                <button onclick="addSale()">✅ تسجيل البيع</button>

                <div class="table-responsive">
                    <table id="salesTable">
                        <thead>
                            <tr>
                                <th>التاريخ</th>
                                <th>المنتج</th>
                                <th>الكمية</th>
                                <th>السعر</th>
                                <th>طريقة الدفع</th>
                                <th>العميل</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- Expenses Tab -->
            <div id="expenses" class="tab-content">
                <h2>إدارة المصروفات</h2>
                <div class="success-message" id="expenseSuccess"></div>
                <div class="error-message" id="expenseError"></div>

                <div class="form-row">
                    <div class="form-group">
                        <label>تاريخ المصروف</label>
                        <input type="date" id="expenseDate">
                    </div>
                    <div class="form-group">
                        <label>فئة المصروف</label>
                        <select id="expenseCategory">
                            <option value="rent">🏠 إيجار</option>
                            <option value="utilities">💡 فواتير</option>
                            <option value="salary">👥 رواتب</option>
                            <option value="supplies">📋 مستلزمات</option>
                            <option value="advertising">📢 إعلانات</option>
                            <option value="transport">🚗 مواصلات</option>
                            <option value="maintenance">🔧 صيانة</option>
                            <option value="other">📌 أخرى</option>
                        </select>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>المبلغ</label>
                        <input type="number" id="expenseAmount" placeholder="أدخل المبلغ" min="0" step="0.01">
                    </div>
                    <div class="form-group">
                        <label>طريقة الدفع</label>
                        <select id="expensePaymentMethod">
                            <option value="card">💳 بطاقة</option>
                            <option value="cash">💵 نقدا</option>
                            <option value="account">📖 على الحساب</option>
                        </select>
                    </div>
                </div>

                <div class="form-group">
                    <label>الوصف</label>
                    <textarea id="expenseDescription" placeholder="وصف المصروف" rows="3"></textarea>
                </div>

                <button onclick="addExpense()">➕ إضافة مصروف</button>

                <div class="table-responsive">
                    <table id="expensesTable">
                        <thead>
                            <tr>
                                <th>التاريخ</th>
                                <th>الفئة</th>
                                <th>المبلغ</th>
                                <th>طريقة الدفع</th>
                                <th>الوصف</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- Reports Tab -->
            <div id="reports" class="tab-content">
                <h2>التقارير العامة</h2>

                <div class="stats-grid">
                    <div class="stat-card">
                        <h3>إجمالي المبيعات</h3>
                        <div class="value" id="totalSales">0</div>
                        <p id="totalSalesCount">0 بيعة</p>
                    </div>
                    <div class="stat-card">
                        <h3>إجمالي المصروفات</h3>
                        <div class="value" id="totalExpenses">0</div>
                        <p id="expenseCount">0 مصروف</p>
                    </div>
                    <div class="stat-card">
                        <h3>الربح الصافي</h3>
                        <div class="value" id="netProfit">0</div>
                        <p id="profitMargin">معدل الربح</p>
                    </div>
                    <div class="stat-card">
                        <h3>عدد المنتجات</h3>
                        <div class="value" id="productsCount">0</div>
                        <p id="lowStockCount">منخفضة المخزون</p>
                    </div>
                </div>

                <h3 style="margin-top: 30px; margin-bottom: 20px;">التفاصيل حسب طريقة الدفع</h3>

                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>طريقة الدفع</th>
                                <th>إجمالي المبيعات</th>
                                <th>عدد المبيعات</th>
                                <th>النسبة المئوية</th>
                            </tr>
                        </thead>
                        <tbody id="paymentMethodStats"></tbody>
                    </table>
                </div>

                <h3 style="margin-top: 30px; margin-bottom: 20px;">المنتجات الأكثر مبيعاً</h3>

                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>المنتج</th>
                                <th>إجمالي المبيعات</th>
                                <th>الكمية المباعة</th>
                                <th>المتبقي</th>
                            </tr>
                        </thead>
                        <tbody id="topProductsStats"></tbody>
                    </table>
                </div>

                <h3 style="margin-top: 30px; margin-bottom: 20px;">المصروفات حسب الفئة</h3>

                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>الفئة</th>
                                <th>إجمالي المبلغ</th>
                                <th>عدد المصروفات</th>
                                <th>النسبة المئوية</th>
                            </tr>
                        </thead>
                        <tbody id="expenseCategoryStats"></tbody>
                    </table>
                </div>

                <button onclick="printReport()" class="print-btn" style="margin-top: 30px;">🖨️ طباعة التقرير</button>
            </div>

            <!-- Notifications Tab -->
            <div id="notifications" class="tab-content">
                <h2>الإشعارات والتنبيهات</h2>

                <div id="notificationsContainer" style="margin-top: 20px;">
                    <!-- Notifications will be added here -->
                </div>
            </div>
        </div>
    </div>

    <!-- Edit Product Modal -->
    <div class="modal" id="editProductModal">
        <div class="modal-content">
            <div class="modal-header">تعديل المنتج</div>
            <div class="form-group">
                <label>اسم المنتج</label>
                <input type="text" id="editProductName">
            </div>
            <div class="form-group">
                <label>السعر</label>
                <input type="number" id="editProductPrice" min="0" step="0.01">
            </div>
            <div class="form-group">
                <label>الكمية</label>
                <input type="number" id="editProductQuantity" min="0">
            </div>
            <div class="form-group">
                <label>حد التنبيه</label>
                <input type="number" id="editProductAlert" min="0">
            </div>
            <div class="form-group">
                <label>الوصف</label>
                <textarea id="editProductDescription" rows="3"></textarea>
            </div>
            <div class="modal-footer">
                <button onclick="saveEditedProduct()">💾 حفظ التعديلات</button>
                <button onclick="closeModal('editProductModal')" class="btn-secondary">إغلاق</button>
            </div>
        </div>
    </div>

    <script>
        // Data storage
        let products = JSON.parse(localStorage.getItem('products')) || [];
        let sales = JSON.parse(localStorage.getItem('sales')) || [];
        let expenses = JSON.parse(localStorage.getItem('expenses')) || [];
        let editingProductId = null;

        // Set today's date as default
        document.getElementById('saleDate').valueAsDate = new Date();
        document.getElementById('expenseDate').valueAsDate = new Date();

        // Initialize
        loadProducts();
        loadSales();
        loadExpenses();
        generateReports();
        checkStockAlerts();

        // Tab switching
        function switchTab(tabName) {
            const tabs = document.querySelectorAll('.tab-content');
            const btns = document.querySelectorAll('.tab-btn');
            
            tabs.forEach(tab => tab.classList.remove('active'));
            btns.forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(tabName).classList.add('active');
            event.target.classList.add('active');

            if (tabName === 'reports') {
                generateReports();
            } else if (tabName === 'notifications') {
                loadNotifications();
            }
        }

        // PRODUCTS FUNCTIONS
        function addProduct() {
            const name = document.getElementById('productName').value.trim();
            const price = parseFloat(document.getElementById('productPrice').value);
            const quantity = parseInt(document.getElementById('productQuantity').value);
            const alertLevel = parseInt(document.getElementById('productAlert').value) || 10;
            const description = document.getElementById('productDescription').value.trim();

            if (!name || !price || isNaN(quantity)) {
                showMessage('productError', 'يرجى ملء جميع الحقول المطلوبة');
                return;
            }

            const product = {
                id: Date.now(),
                name,
                price,
                quantity,
                alertLevel,
                description,
                dateAdded: new Date().toISOString()
            };

            products.push(product);
            saveProducts();
            loadProducts();
            clearProductForm();
            showMessage('productSuccess', '✅ تم إضافة المنتج بنجاح');
            checkStockAlerts();
        }

        function loadProducts() {
            const tbody = document.querySelector('#productsTable tbody');
            tbody.innerHTML = '';
            
            updateProductSelect();

            products.forEach((product, index) => {
                const status = product.quantity <= product.alertLevel ? 
                    `<span class="low-stock">⚠️ منخفض (${product.quantity})</span>` : 
                    `✅ متاح (${product.quantity})`;
                
                const row = `
                    <tr>
                        <td>${index + 1}</td>
                        <td><strong>${product.name}</strong></td>
                        <td>${product.price.toFixed(2)}</td>
                        <td>${product.quantity}</td>
                        <td>${product.alertLevel}</td>
                        <td>${status}</td>
                        <td class="action-buttons">
                            <button onclick="editProduct(${product.id})" class="btn-sm">✏️ تعديل</button>
                            <button onclick="deleteProduct(${product.id})" class="btn-sm btn-danger">🗑️ حذف</button>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        function editProduct(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            editingProductId = productId;
            document.getElementById('editProductName').value = product.name;
            document.getElementById('editProductPrice').value = product.price;
            document.getElementById('editProductQuantity').value = product.quantity;
            document.getElementById('editProductAlert').value = product.alertLevel;
            document.getElementById('editProductDescription').value = product.description;

            openModal('editProductModal');
        }

        function saveEditedProduct() {
            if (editingProductId === null) return;

            const product = products.find(p => p.id === editingProductId);
            if (!product) return;

            product.name = document.getElementById('editProductName').value.trim();
            product.price = parseFloat(document.getElementById('editProductPrice').value);
            product.quantity = parseInt(document.getElementById('editProductQuantity').value);
            product.alertLevel = parseInt(document.getElementById('editProductAlert').value);
            product.description = document.getElementById('editProductDescription').value.trim();

            saveProducts();
            loadProducts();
            closeModal('editProductModal');
            showMessage('productSuccess', '✅ تم تعديل المنتج بنجاح');
            checkStockAlerts();
        }

        function deleteProduct(productId) {
            if (confirm('هل أنت متأكد من حذف هذا المنتج؟')) {
                products = products.filter(p => p.id !== productId);
                saveProducts();
                loadProducts();
                showMessage('productSuccess', '✅ تم حذف المنتج بنجاح');
            }
        }

        function clearProductForm() {
            document.getElementById('productName').value = '';
            document.getElementById('productPrice').value = '';
            document.getElementById('productQuantity').value = '';
            document.getElementById('productAlert').value = '';
            document.getElementById('productDescription').value = '';
        }

        function updateProductSelect() {
            const select = document.getElementById('saleProduct');
            select.innerHTML = '<option value="">-- اختر منتجاً --</option>';
            products.forEach(product => {
                const option = document.createElement('option');
                option.value = product.id;
                option.textContent = `${product.name} (السعر: ${product.price.toFixed(2)})`;
                select.appendChild(option);
            });

            // Update price when product is selected
            select.onchange = function() {
                const productId = parseInt(this.value);
                const product = products.find(p => p.id === productId);
                if (product) {
                    document.getElementById('salePrice').value = (product.price * parseInt(document.getElementById('saleQuantity').value || 1)).toFixed(2);
                }
            };
        }

        // SALES FUNCTIONS
        function addSale() {
            const date = document.getElementById('saleDate').value;
            const productId = parseInt(document.getElementById('saleProduct').value);
            const quantity = parseInt(document.getElementById('saleQuantity').value);
            const price = parseFloat(document.getElementById('salePrice').value);
            const paymentMethod = document.getElementById('paymentMethod').value;
            const customerName = document.getElementById('customerName').value.trim();
            const notes = document.getElementById('saleNotes').value.trim();

            if (!date || !productId || !quantity || !price) {
                showMessage('saleError', 'يرجى ملء جميع الحقول المطلوبة');
                return;
            }

            const product = products.find(p => p.id === productId);
            if (!product) {
                showMessage('saleError', 'المنتج غير موجود');
                return;
            }

            if (product.quantity < quantity) {
                showMessage('saleError', `الكمية المتاحة: ${product.quantity} فقط`);
                return;
            }

            const sale = {
                id: Date.now(),
                date,
                productId,
                productName: product.name,
                quantity,
                price,
                paymentMethod,
                customerName: customerName || 'غير محدد',
                notes,
                dateAdded: new Date().toISOString()
            };

            sales.push(sale);
            product.quantity -= quantity;

            saveSales();
            saveProducts();
            loadSales();
            loadProducts();
            clearSaleForm();
            showMessage('saleSuccess', '✅ تم تسجيل البيع بنجاح');
            checkStockAlerts();
            generateReports();
        }

        function loadSales() {
            const tbody = document.querySelector('#salesTable tbody');
            tbody.innerHTML = '';

            sales.forEach((sale, index) => {
                const paymentBadge = getPaymentBadge(sale.paymentMethod);
                const row = `
                    <tr>
                        <td>${sale.date}</td>
                        <td>${sale.productName}</td>
                        <td>${sale.quantity}</td>
                        <td>${sale.price.toFixed(2)}</td>
                        <td>${paymentBadge}</td>
                        <td>${sale.customerName}</td>
                        <td class="action-buttons">
                            <button onclick="deleteSale(${sale.id})" class="btn-sm btn-danger">🗑️ حذف</button>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        function deleteSale(saleId) {
            if (confirm('هل أنت متأكد من حذف هذه البيعة؟')) {
                const sale = sales.find(s => s.id === saleId);
                if (sale) {
                    const product = products.find(p => p.id === sale.productId);
                    if (product) {
                        product.quantity += sale.quantity;
                    }
                }
                sales = sales.filter(s => s.id !== saleId);
                saveSales();
                saveProducts();
                loadSales();
                loadProducts();
                showMessage('saleSuccess', '✅ تم حذف البيعة بنجاح');
                generateReports();
            }
        }

        function clearSaleForm() {
            document.getElementById('saleDate').valueAsDate = new Date();
            document.getElementById('saleProduct').value = '';
            document.getElementById('saleQuantity').value = '';
            document.getElementById('salePrice').value = '';
            document.getElementById('paymentMethod').value = 'card';
            document.getElementById('customerName').value = '';
            document.getElementById('saleNotes').value = '';
        }

        // EXPENSES FUNCTIONS
        function addExpense() {
            const date = document.getElementById('expenseDate').value;
            const category = document.getElementById('expenseCategory').value;
            const amount = parseFloat(document.getElementById('expenseAmount').value);
            const paymentMethod = document.getElementById('expensePaymentMethod').value;
            const description = document.getElementById('expenseDescription').value.trim();

            if (!date || !category || !amount) {
                showMessage('expenseError', 'يرجى ملء جميع الحقول المطلوبة');
                return;
            }

            const expense = {
                id: Date.now(),
                date,
                category,
                amount,
                paymentMethod,
                description,
                dateAdded: new Date().toISOString()
            };

            expenses.push(expense);
            saveExpenses();
            loadExpenses();
            clearExpenseForm();
            showMessage('expenseSuccess', '✅ تم إضافة المصروف بنجاح');
            generateReports();
        }

        function loadExpenses() {
            const tbody = document.querySelector('#expensesTable tbody');
            tbody.innerHTML = '';

            expenses.forEach((expense, index) => {
                const categoryLabel = getCategoryLabel(expense.category);
                const paymentBadge = getPaymentBadge(expense.paymentMethod);
                const row = `
                    <tr>
                        <td>${expense.date}</td>
                        <td>${categoryLabel}</td>
                        <td>${expense.amount.toFixed(2)}</td>
                        <td>${paymentBadge}</td>
                        <td>${expense.description}</td>
                        <td class="action-buttons">
                            <button onclick="deleteExpense(${expense.id})" class="btn-sm btn-danger">🗑️ حذف</button>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        function deleteExpense(expenseId) {
            if (confirm('هل أنت متأكد من حذف هذا المصروف؟')) {
                expenses = expenses.filter(e => e.id !== expenseId);
                saveExpenses();
                loadExpenses();
                showMessage('expenseSuccess', '✅ تم حذف المصروف بنجاح');
                generateReports();
            }
        }

        function clearExpenseForm() {
            document.getElementById('expenseDate').valueAsDate = new Date();
            document.getElementById('expenseCategory').value = 'other';
            document.getElementById('expenseAmount').value = '';
            document.getElementById('expensePaymentMethod').value = 'cash';
            document.getElementById('expenseDescription').value = '';
        }

        // REPORTS FUNCTIONS
        function generateReports() {
            const totalSalesAmount = sales.reduce((sum, sale) => sum + sale.price, 0);
            const totalExpensesAmount = expenses.reduce((sum, expense) => sum + expense.amount, 0);
            const netProfit = totalSalesAmount - totalExpensesAmount;
            const profitMargin = totalSalesAmount > 0 ? ((netProfit / totalSalesAmount) * 100).toFixed(1) : 0;

            // Update stats cards
            document.getElementById('totalSales').textContent = totalSalesAmount.toFixed(2);
            document.getElementById('totalSalesCount').textContent = `${sales.length} بيعة`;
            document.getElementById('totalExpenses').textContent = totalExpensesAmount.toFixed(2);
            document.getElementById('expenseCount').textContent = `${expenses.length} مصروف`;
            document.getElementById('netProfit').textContent = netProfit.toFixed(2);
            document.getElementById('profitMargin').textContent = `${profitMargin}%`;
            document.getElementById('productsCount').textContent = products.length;

            const lowStockProducts = products.filter(p => p.quantity <= p.alertLevel).length;
            document.getElementById('lowStockCount').textContent = `${lowStockProducts} منخفضة`;

            // Payment method stats
            const paymentStats = {};
            sales.forEach(sale => {
                if (!paymentStats[sale.paymentMethod]) {
                    paymentStats[sale.paymentMethod] = { total: 0, count: 0 };
                }
                paymentStats[sale.paymentMethod].total += sale.price;
                paymentStats[sale.paymentMethod].count++;
            });

            const paymentStatsTable = document.getElementById('paymentMethodStats');
            paymentStatsTable.innerHTML = '';
            const totalSales2 = Object.values(paymentStats).reduce((sum, stat) => sum + stat.total, 0);
            Object.entries(paymentStats).forEach(([method, stats]) => {
                const percentage = totalSales2 > 0 ? ((stats.total / totalSales2) * 100).toFixed(1) : 0;
                const methodLabel = getPaymentLabel(method);
                const row = `
                    <tr>
                        <td>${methodLabel}</td>
                        <td>${stats.total.toFixed(2)}</td>
                        <td>${stats.count}</td>
                        <td>${percentage}%</td>
                    </tr>
                `;
                paymentStatsTable.innerHTML += row;
            });

            // Top products
            const productStats = {};
            sales.forEach(sale => {
                if (!productStats[sale.productId]) {
                    productStats[sale.productId] = {
                        name: sale.productName,
                        total: 0,
                        quantity: 0
                    };
                }
                productStats[sale.productId].total += sale.price;
                productStats[sale.productId].quantity += sale.quantity;
            });

            const topProductsTable = document.getElementById('topProductsStats');
            topProductsTable.innerHTML = '';
            Object.entries(productStats)
                .sort((a, b) => b[1].total - a[1].total)
                .forEach(([productId, stats]) => {
                    const product = products.find(p => p.id === parseInt(productId));
                    const remaining = product ? product.quantity : 0;
                    const row = `
                        <tr>
                            <td>${stats.name}</td>
                            <td>${stats.total.toFixed(2)}</td>
                            <td>${stats.quantity}</td>
                            <td>${remaining}</td>
                        </tr>
                    `;
                    topProductsTable.innerHTML += row;
                });

            // Expense category stats
            const categoryStats = {};
            expenses.forEach(expense => {
                if (!categoryStats[expense.category]) {
                    categoryStats[expense.category] = { total: 0, count: 0 };
                }
                categoryStats[expense.category].total += expense.amount;
                categoryStats[expense.category].count++;
            });

            const expenseCategoryTable = document.getElementById('expenseCategoryStats');
            expenseCategoryTable.innerHTML = '';
            const totalExpenses2 = Object.values(categoryStats).reduce((sum, stat) => sum + stat.total, 0);
            Object.entries(categoryStats).forEach(([category, stats]) => {
                const percentage = totalExpenses2 > 0 ? ((stats.total / totalExpenses2) * 100).toFixed(1) : 0;
                const categoryLabel = getCategoryLabel(category);
                const row = `
                    <tr>
                        <td>${categoryLabel}</td>
                        <td>${stats.total.toFixed(2)}</td>
                        <td>${stats.count}</td>
                        <td>${percentage}%</td>
                    </tr>
                `;
                expenseCategoryTable.innerHTML += row;
            });
        }

        // STOCK ALERTS
        function checkStockAlerts() {
            const alerts = [];
            products.forEach(product => {
                if (product.quantity <= product.alertLevel) {
                    alerts.push({
                        type: product.quantity === 0 ? 'critical' : 'warning',
                        productId: product.id,
                        productName: product.name,
                        quantity: product.quantity,
                        alertLevel: product.alertLevel,
                        timestamp: new Date().toISOString()
                    });
                }
            });

            if (alerts.length > 0) {
                saveAlerts(alerts);
                alerts.forEach(alert => {
                    if (alert.type === 'critical') {
                        showNotification('danger', '⚠️ تنبيه حرج', `المنتج "${alert.productName}" نفذ تماماً!`);
                    } else {
                        showNotification('warning', '⚠️ تنبيه مخزون', `المنتج "${alert.productName}" انخفض إلى ${alert.quantity} (الحد: ${alert.alertLevel})`);
                    }
                });
            }
        }

        function loadNotifications() {
            const container = document.getElementById('notificationsContainer');
            const alerts = JSON.parse(localStorage.getItem('alerts')) || [];

            if (alerts.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: #999;">لا توجد تنبيهات حالياً</p>';
                return;
            }

            container.innerHTML = '';
            alerts.forEach((alert, index) => {
                const alertDiv = document.createElement('div');
                const alertClass = alert.type === 'critical' ? 'alert-danger' : 'alert-warning';
                const icon = alert.type === 'critical' ? '🔴' : '🟡';
                
                alertDiv.className = alertClass;
                alertDiv.innerHTML = `
                    <strong>${icon} ${alert.productName}</strong><br>
                    الكمية الحالية: ${alert.quantity} | الحد الأدنى: ${alert.alertLevel}<br>
                    <small>${new Date(alert.timestamp).toLocaleString('ar-SA')}</small>
                `;
                container.appendChild(alertDiv);
            });
        }

        // UTILITIES
        function getPaymentBadge(method) {
            const badges = {
                'card': '<span class="payment-method-badge payment-card">💳 بطاقة</span>',
                'cash': '<span class="payment-method-badge payment-cash">💵 نقدا</span>',
                'account': '<span class="payment-method-badge payment-account">📖 على الحساب</span>'
            };
            return badges[method] || method;
        }

        function getPaymentLabel(method) {
            const labels = {
                'card': '💳 بطاقة',
                'cash': '💵 نقدا',
                'account': '📖 على الحساب'
            };
            return labels[method] || method;
        }

        function getCategoryLabel(category) {
            const labels = {
                'rent': '🏠 إيجار',
                'utilities': '💡 فواتير',
                'salary': '👥 رواتب',
                'supplies': '📋 مستلزمات',
                'advertising': '📢 إعلانات',
                'transport': '🚗 مواصلات',
                'maintenance': '🔧 صيانة',
                'other': '📌 أخرى'
            };
            return labels[category] || category;
        }

        function showMessage(elementId, message) {
            const element = document.getElementById(elementId);
            element.textContent = message;
            element.classList.add('show');
            setTimeout(() => {
                element.classList.remove('show');
            }, 3000);
        }

        function showNotification(type, title, message) {
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.innerHTML = `
                <span class="close-btn" onclick="this.parentElement.remove()">×</span>
                <div class="notification-title">${title}</div>
                <div>${message}</div>
            `;
            document.body.appendChild(notification);
            setTimeout(() => {
                if (notification.parentElement) {
                    notification.remove();
                }
            }, 5000);
        }

        function openModal(modalId) {
            document.getElementById(modalId).classList.add('show');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('show');
        }

        function printReport() {
            window.print();
        }

        // LOCAL STORAGE
        function saveProducts() {
            localStorage.setItem('products', JSON.stringify(products));
        }

        function saveSales() {
            localStorage.setItem('sales', JSON.stringify(sales));
        }

        function saveExpenses() {
            localStorage.setItem('expenses', JSON.stringify(expenses));
        }

        function saveAlerts(alerts) {
            localStorage.setItem('alerts', JSON.stringify(alerts));
        }

        // Close modal on outside click
        window.onclick = function(event) {
            const modals = document.querySelectorAll('.modal.show');
            modals.forEach(modal => {
                if (event.target === modal) {
                    modal.classList.remove('show');
                }
            });
        }
    </script>
</body>
</html>
