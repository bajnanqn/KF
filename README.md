<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BEBI & LEDI Tailor Manager</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBlue: '#0f172a',
                        cardBlue: '#1e293b',
                        darkGreen: '#065f46',
                        darkRed: '#991b1b',
                        accentBlue: '#3b82f6'
                    }
                }
            }
        }
    </script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-darkBlue text-gray-100 font-sans min-h-screen pb-12 font-bold">

    <!-- Top Navigation / Header -->
    <header class="bg-cardBlue border-b border-slate-700 p-4 sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-4">
            <h1 class="text-xl tracking-wide flex items-center gap-2">
                ✂️ <span class="text-pink-400">BEBI</span> & <span class="text-purple-400">LEDI</span>
            </h1>
            <nav class="flex flex-wrap gap-2">
                <button onclick="switchTab('dashboard')" class="tab-btn px-3 py-2 bg-accentBlue text-white rounded-lg text-sm transition">📊 Dashboard</button>
                <button onclick="switchTab('customers')" class="tab-btn px-3 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm transition">👥 Customers</button>
                <button onclick="switchTab('completed')" class="tab-btn px-3 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm transition">✅ Completed</button>
                <button onclick="switchTab('employees')" class="tab-btn px-3 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm transition">👔 Employees</button>
                <button onclick="switchTab('store')" class="tab-btn px-3 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm transition">🛍️ Store</button>
                <button onclick="switchTab('analytics')" class="tab-btn px-3 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm transition">📈 Analytics</button>
            </nav>
        </div>
    </header>

    <main class="max-w-7xl mx-auto p-4 mt-4">

        <!-- ================= 1. DASHBOARD TAB ================= -->
        <div id="tab-dashboard" class="space-y-6 tab-content">
            
            <!-- Top Revenue & Profit -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg relative overflow-hidden">
                    <div class="absolute right-4 top-4 text-emerald-500/20 text-6xl">💵</div>
                    <h3 class="text-slate-400 text-sm uppercase tracking-wider">💰 TOTAL REVENUE</h3>
                    <p id="dash-total-revenue" class="text-4xl text-emerald-400 mt-2">₹0</p>
                    <div class="mt-4 flex gap-4 text-xs text-slate-300">
                        <span>💖 BEBI: <strong id="dash-bebi-rev" class="text-white">₹0</strong></span>
                        <span>💜 LEDI: <strong id="dash-ledi-rev" class="text-white">₹0</strong></span>
                    </div>
                </div>

                <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg relative overflow-hidden">
                    <div class="absolute right-4 top-4 text-blue-500/20 text-6xl">📈</div>
                    <h3 class="text-slate-400 text-sm uppercase tracking-wider">🚀 TOTAL PROFIT</h3>
                    <p id="dash-total-profit" class="text-4xl text-blue-400 mt-2">₹0</p>
                    <div class="mt-4 flex gap-4 text-xs text-slate-300">
                        <span>💖 BEBI: <strong id="dash-bebi-prof" class="text-white">₹0</strong></span>
                        <span>💜 LEDI: <strong id="dash-ledi-prof" class="text-white">₹0</strong></span>
                    </div>
                </div>
            </div>

            <!-- Quick Stats Row -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                <div class="bg-cardBlue border border-slate-700 p-4 rounded-xl">
                    <h4 class="text-xs text-slate-400 uppercase">📦 WORK ORDERS</h4>
                    <div class="mt-3 flex justify-between items-center">
                        <div>
                            <span class="text-2xl text-emerald-400" id="stat-active-count">0</span>
                            <p class="text-xs text-slate-400">⚡ Active</p>
                        </div>
                        <div class="border-l border-slate-700 pl-4">
                            <span class="text-2xl text-blue-400" id="stat-completed-count">0</span>
                            <p class="text-xs text-slate-400">🏁 Finished</p>
                        </div>
                    </div>
                </div>

                <div class="bg-cardBlue border border-slate-700 p-4 rounded-xl flex flex-col justify-between">
                    <h4 class="text-xs text-slate-400 uppercase">👥 TOTAL EMPLOYEES</h4>
                    <div class="my-2">
                        <span class="text-3xl text-purple-400" id="stat-employee-count">0</span>
                    </div>
                    <span class="text-xs text-slate-400">👔 Active Staff</span>
                </div>

                <div class="bg-darkRed/20 border border-darkRed p-4 rounded-xl flex flex-col justify-between">
                    <h4 class="text-xs text-red-300 uppercase">👛 ANU FUND BOX</h4>
                    <div class="my-2">
                        <span class="text-3xl text-red-400" id="dash-anu-total">₹0</span>
                    </div>
                    <span class="text-xs text-red-200">💸 Expense Balance</span>
                </div>

                <div class="bg-cardBlue border border-slate-700 p-4 rounded-xl flex flex-col justify-between cursor-pointer hover:border-accentBlue transition" onclick="switchTab('customers')">
                    <h4 class="text-xs text-amber-400 uppercase">⏰ NEXT DELIVERY</h4>
                    <div class="my-1">
                        <p id="dash-next-name" class="text-lg text-white truncate">-</p>
                        <p id="dash-next-date" class="text-xs text-amber-300">-</p>
                    </div>
                    <span class="text-[10px] text-slate-400">👆 Click to view</span>
                </div>
            </div>
        </div>

        <!-- ================= 2. CUSTOMER TAB ================= -->
        <div id="tab-customers" class="space-y-6 tab-content hidden">
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg">
                <h2 class="text-lg mb-4 text-accentBlue">➕ ADD NEW CUSTOMER</h2>
                
                <div class="mb-4">
                    <label class="block text-sm text-slate-300 mb-2">🏷️ SELECT CATEGORY</label>
                    <div class="flex gap-4">
                        <button type="button" onclick="setCustomerCategory('BEBI')" id="cat-bebi-btn" class="flex-1 py-2 px-4 rounded-lg border border-pink-500 bg-pink-900/40 text-pink-300 transition">💖 BEBI</button>
                        <button type="button" onclick="setCustomerCategory('LEDI')" id="cat-ledi-btn" class="flex-1 py-2 px-4 rounded-lg border border-slate-600 bg-slate-800 text-slate-300 transition">💜 LEDI</button>
                    </div>
                </div>

                <form id="customer-form" onsubmit="saveCustomer(event)" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <input type="hidden" id="cust-category" value="BEBI">
                    
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">👤 CUSTOMER NAME</label>
                        <input type="text" id="cust-name" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">💬 WHATSAPP NUMBER</label>
                        <input type="text" id="cust-whatsapp" required placeholder="919876543210" class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">📅 DELIVERY DATE</label>
                        <input type="date" id="cust-date" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">✂️ STITCHING CHARGE</label>
                        <input type="number" id="cust-stitch-charge" oninput="calculateCustomerFinancials()" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">💵 ADVANCE AMOUNT</label>
                        <input type="number" id="cust-advance" oninput="calculateCustomerFinancials()" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                        <p id="cust-advance-balance-text" class="text-[11px] text-red-400 mt-1">👛 Balance: ₹0</p>
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">👔 ASSIGNED EMPLOYEE</label>
                        <select id="cust-employee" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                            <option value="">Select Employee</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">💸 TOTAL EXPENSE</label>
                        <input type="number" id="cust-expense" oninput="calculateCustomerFinancials()" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    </div>

                    <div>
                        <label class="block text-xs text-slate-300 mb-1">📈 TOTAL PROFIT</label>
                        <input type="number" id="cust-profit" readonly class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm text-emerald-400 focus:outline-none">
                    </div>

                    <div class="md:col-span-2 flex justify-end gap-2 mt-4">
                        <button type="submit" class="bg-accentBlue hover:bg-blue-600 text-white px-6 py-2.5 rounded-lg text-sm transition">💾 SAVE CUSTOMER</button>
                    </div>
                </form>
            </div>

            <!-- Active Table -->
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg mt-6">
                <h3 class="text-md mb-4 text-slate-200">⚡ ACTIVE ORDERS</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm text-slate-300">
                        <thead class="bg-slate-800 text-xs uppercase text-slate-400">
                            <tr>
                                <th class="p-3">🏷️</th>
                                <th class="p-3">👤 Name</th>
                                <th class="p-3">💬 WhatsApp</th>
                                <th class="p-3">📅 Date</th>
                                <th class="p-3">👔 Staff</th>
                                <th class="p-3">📈 Profit</th>
                                <th class="p-3 text-center">⚙️ Action</th>
                            </tr>
                        </thead>
                        <tbody id="active-customers-tbody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- ================= 3. COMPLETED TAB ================= -->
        <div id="tab-completed" class="space-y-6 tab-content hidden">
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg">
                <h2 class="text-lg mb-4 text-emerald-400">🏁 COMPLETED ORDERS LIST</h2>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm text-slate-300">
                        <thead class="bg-slate-800 text-xs uppercase text-slate-400">
                            <tr>
                                <th class="p-3">🏷️</th>
                                <th class="p-3">👤 Name</th>
                                <th class="p-3">💬 WhatsApp</th>
                                <th class="p-3">📅 Date</th>
                                <th class="p-3">👔 Staff</th>
                                <th class="p-3">✂️ Charge</th>
                                <th class="p-3 text-center">💬 Chat</th>
                            </tr>
                        </thead>
                        <tbody id="completed-customers-tbody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- ================= 4. EMPLOYEES TAB ================= -->
        <div id="tab-employees" class="space-y-6 tab-content hidden">
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg">
                <h2 class="text-lg mb-4 text-purple-400">👔 EMPLOYEE MANAGER</h2>
                <form onsubmit="saveEmployee(event)" class="flex gap-4 mb-6">
                    <input type="text" id="emp-name" placeholder="Enter Employee Name" required class="flex-1 bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:border-accentBlue focus:outline-none">
                    <button type="submit" class="bg-purple-600 hover:bg-purple-700 text-white px-6 py-2.5 rounded-lg text-sm transition">➕ ADD</button>
                </form>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4" id="employee-cards-container"></div>
            </div>
        </div>

        <!-- ================= 5. STORE TAB ================= -->
        <div id="tab-store" class="space-y-6 tab-content hidden">
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg">
                <h2 class="text-lg mb-4 text-amber-400">🛍️ STORE ITEMS (Max 5MB)</h2>
                <form onsubmit="saveStoreItem(event)" class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">🏷️ ITEM NAME</label>
                        <input type="text" id="store-item-name" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">💵 PRICE</label>
                        <input type="number" id="store-item-price" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2.5 text-sm focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">📷 IMAGE</label>
                        <input type="file" id="store-item-image" accept="image/*" required class="w-full bg-darkBlue border border-slate-700 rounded-lg p-2 text-xs text-slate-400">
                    </div>
                    <div class="md:col-span-3 flex justify-end">
                        <button type="submit" class="bg-amber-600 hover:bg-amber-700 text-white px-6 py-2.5 rounded-lg text-sm transition">💾 SAVE ITEM</button>
                    </div>
                </form>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4" id="store-items-grid"></div>
            </div>
        </div>

        <!-- ================= 6. ANALYTICS TAB ================= -->
        <div id="tab-analytics" class="space-y-6 tab-content hidden">
            <div class="bg-cardBlue border border-slate-700 p-6 rounded-2xl shadow-lg">
                <h2 class="text-lg mb-4 text-accentBlue">📊 DATA ANALYZERS</h2>
                <div class="flex flex-wrap gap-4 mb-6">
                    <div>
                        <input type="date" id="filter-analytics-date" onchange="renderAnalytics()" class="bg-darkBlue border border-slate-700 rounded-lg p-2 text-sm text-white">
                    </div>
                    <div class="flex items-end">
                        <button onclick="resetAnalyticsFilter()" class="bg-slate-700 hover:bg-slate-600 text-white px-4 py-2 rounded-lg text-sm">🔄 Reset Filter</button>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                    <div class="bg-darkBlue p-4 rounded-xl border border-slate-700">
                        <p class="text-xs text-slate-400">📦 Total Orders</p>
                        <h3 id="ana-total-orders" class="text-2xl text-white mt-1">0</h3>
                    </div>
                    <div class="bg-darkBlue p-4 rounded-xl border border-slate-700">
                        <p class="text-xs text-slate-400">💵 Revenue</p>
                        <h3 id="ana-total-rev" class="text-2xl text-emerald-400 mt-1">₹0</h3>
                    </div>
                    <div class="bg-darkBlue p-4 rounded-xl border border-slate-700">
                        <p class="text-xs text-slate-400">📈 Profit</p>
                        <h3 id="ana-total-prof" class="text-2xl text-blue-400 mt-1">₹0</h3>
                    </div>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm text-slate-300">
                        <thead class="bg-slate-800 text-xs uppercase text-slate-400">
                            <tr>
                                <th class="p-3">📅 Date</th>
                                <th class="p-3">👤 Name</th>
                                <th class="p-3">🏷️ Category</th>
                                <th class="p-3">💵 Revenue</th>
                                <th class="p-3">📈 Profit</th>
                                <th class="p-3">⚡ Status</th>
                            </tr>
                        </thead>
                        <tbody id="analytics-tbody"></tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <script>
        let db = {
            customers: JSON.parse(localStorage.getItem('tailor_customers')) || [],
            completed: JSON.parse(localStorage.getItem('tailor_completed')) || [],
            employees: JSON.parse(localStorage.getItem('tailor_employees')) || ['Anu', 'Rahul', 'Fatima'],
            store: JSON.parse(localStorage.getItem('tailor_store')) || []
        };

        function saveData() {
            localStorage.setItem('tailor_customers', JSON.stringify(db.customers));
            localStorage.setItem('tailor_completed', JSON.stringify(db.completed));
            localStorage.setItem('tailor_employees', JSON.stringify(db.employees));
            localStorage.setItem('tailor_store', JSON.stringify(db.store));
            updateDashboard();
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById('tab-' + tabId).classList.remove('hidden');

            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-accentBlue');
                btn.classList.add('bg-slate-700');
            });
            event.currentTarget.classList.remove('bg-slate-700');
            event.currentTarget.classList.add('bg-accentBlue');

            if(tabId === 'customers') populateEmployeeDropdown();
            if(tabId === 'employees') renderEmployees();
            if(tabId === 'store') renderStore();
            if(tabId === 'analytics') renderAnalytics();
        }

        function setCustomerCategory(cat) {
            document.getElementById('cust-category').value = cat;
            if(cat === 'BEBI') {
                document.getElementById('cat-bebi-btn').className = "flex-1 py-2 px-4 rounded-lg border border-pink-500 bg-pink-900/40 text-pink-300 transition";
                document.getElementById('cat-ledi-btn').className = "flex-1 py-2 px-4 rounded-lg border border-slate-600 bg-slate-800 text-slate-300 transition";
            } else {
                document.getElementById('cat-ledi-btn').className = "flex-1 py-2 px-4 rounded-lg border border-purple-500 bg-purple-900/40 text-purple-300 transition";
                document.getElementById('cat-bebi-btn').className = "flex-1 py-2 px-4 rounded-lg border border-slate-600 bg-slate-800 text-slate-300 transition";
            }
        }

        function calculateCustomerFinancials() {
            let expense = parseFloat(document.getElementById('cust-expense').value) || 0;
            let advance = parseFloat(document.getElementById('cust-advance').value) || 0;
            let stitchCharge = parseFloat(document.getElementById('cust-stitch-charge').value) || 0;

            let balanceAdvance = advance - expense;
            document.getElementById('cust-advance-balance-text').innerText = `👛 Balance: ₹${balanceAdvance}`;

            let calculatedProfit = 0;
            if (expense > 300) {
                calculatedProfit = stitchCharge - (expense - 300);
            } else {
                calculatedProfit = stitchCharge;
            }
            if(calculatedProfit < 0) calculatedProfit = 0;
            document.getElementById('cust-profit').value = calculatedProfit;
        }

        function populateEmployeeDropdown() {
            let select = document.getElementById('cust-employee');
            select.innerHTML = '<option value="">Select Employee</option>';
            db.employees.forEach(emp => {
                select.innerHTML += `<option value="${emp}">${emp}</option>`;
            });
        }

        function saveCustomer(e) {
            e.preventDefault();
            let newCust = {
                id: Date.now(),
                category: document.getElementById('cust-category').value,
                name: document.getElementById('cust-name').value,
                whatsapp: document.getElementById('cust-whatsapp').value,
                date: document.getElementById('cust-date').value,
                stitchCharge: parseFloat(document.getElementById('cust-stitch-charge').value) || 0,
                advance: parseFloat(document.getElementById('cust-advance').value) || 0,
                employee: document.getElementById('cust-employee').value,
                expense: parseFloat(document.getElementById('cust-expense').value) || 0,
                profit: parseFloat(document.getElementById('cust-profit').value) || 0
            };

            db.customers.push(newCust);
            saveData();
            document.getElementById('customer-form').reset();
            renderActiveCustomers();
            alert('✅ Saved Successfully!');
            switchTab('dashboard');
        }

        function renderActiveCustomers() {
            let tbody = document.getElementById('active-customers-tbody');
            tbody.innerHTML = '';
            
            if(db.customers.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-500">❌ No Active Orders</td></tr>`;
                return;
            }

            db.customers.forEach(cust => {
                let waLink = `https://wa.me/${cust.whatsapp.replace(/\D/g,'')}`;
                tbody.innerHTML += `
                    <tr class="border-b border-slate-800 hover:bg-slate-800/50">
                        <td class="p-3"><span class="px-2 py-1 rounded text-xs ${cust.category==='BEBI'?'bg-pink-900 text-pink-300':'bg-purple-900 text-purple-300'}">${cust.category}</span></td>
                        <td class="p-3 text-white">${cust.name}</td>
                        <td class="p-3"><a href="${waLink}" target="_blank" class="text-emerald-400">💬 Chat</a></td>
                        <td class="p-3">${cust.date}</td>
                        <td class="p-3">${cust.employee || '-'}</td>
                        <td class="p-3 text-emerald-400">₹${cust.profit}</td>
                        <td class="p-3 text-center flex justify-center gap-2">
                            <button onclick="completeCustomer(${cust.id})" class="bg-emerald-600 hover:bg-emerald-700 text-white px-2 py-1 rounded text-xs">✅ Complete</button>
                            <button onclick="deleteCustomer(${cust.id})" class="bg-red-600 hover:bg-red-700 text-white px-2 py-1 rounded text-xs">🗑️</button>
                        </td>
                    </tr>
                `;
            });
        }

        function completeCustomer(id) {
            let index = db.customers.findIndex(c => c.id === id);
            if(index !== -1) {
                let cust = db.customers.splice(index, 1)[0];
                cust.completedDate = new Date().toISOString().split('T')[0];
                db.completed.push(cust);
                saveData();
                renderActiveCustomers();
                renderCompletedCustomers();
                updateDashboard();
                alert('✅ Order Completed!');
            }
        }

        function deleteCustomer(id) {
            if(confirm('Are you sure you want to delete?')) {
                db.customers = db.customers.filter(c => c.id !== id);
                saveData();
                renderActiveCustomers();
            }
        }

        function renderCompletedCustomers() {
            let tbody = document.getElementById('completed-customers-tbody');
            tbody.innerHTML = '';

            if(db.completed.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-500">❌ No Completed Orders</td></tr>`;
                return;
            }

            db.completed.forEach(cust => {
                let waLink = `https://wa.me/${cust.whatsapp.replace(/\D/g,'')}`;
                tbody.innerHTML += `
                    <tr class="border-b border-slate-800 hover:bg-slate-800/50">
                        <td class="p-3"><span class="px-2 py-1 rounded text-xs ${cust.category==='BEBI'?'bg-pink-900 text-pink-300':'bg-purple-900 text-purple-300'}">${cust.category}</span></td>
                        <td class="p-3 text-white">${cust.name}</td>
                        <td class="p-3"><a href="${waLink}" target="_blank" class="text-emerald-400">💬 Chat</a></td>
                        <td class="p-3">${cust.date}</td>
                        <td class="p-3 text-purple-300">${cust.employee || '-'}</td>
                        <td class="p-3 text-emerald-400">₹${cust.stitchCharge}</td>
                        <td class="p-3 text-center">
                            <a href="${waLink}" target="_blank" class="bg-emerald-600 text-white px-2 py-1 rounded text-xs">💬 Open</a>
                        </td>
                    </tr>
                `;
            });
        }

        function saveEmployee(e) {
            e.preventDefault();
            let name = document.getElementById('emp-name').value.trim();
            if(name && !db.employees.includes(name)) {
                db.employees.push(name);
                saveData();
                document.getElementById('emp-name').value = '';
                renderEmployees();
                alert('✅ Employee Added!');
            }
        }

        function renderEmployees() {
            let container = document.getElementById('employee-cards-container');
            container.innerHTML = '';

            db.employees.forEach(emp => {
                let empCompletedOrders = db.completed.filter(c => c.employee === emp);
                let totalEarned = empCompletedOrders.reduce((sum, c) => sum + c.stitchCharge, 0);
                let totalCompletedCount = empCompletedOrders.length;

                container.innerHTML += `
                    <div class="bg-darkBlue border border-slate-700 p-4 rounded-xl flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-center mb-2">
                                <h4 class="text-purple-300 text-base">👤 ${emp}</h4>
                                <button onclick="deleteEmployee('${emp}')" class="text-red-400 text-xs">🗑️</button>
                            </div>
                            <p class="text-xs text-slate-400">📦 Orders: <strong class="text-white">${totalCompletedCount}</strong></p>
                        </div>
                        <div class="mt-4 pt-3 border-t border-slate-800 flex justify-between items-center">
                            <span class="text-xs text-slate-400">💵 Total Paid:</span>
                            <span class="text-xl text-emerald-400">₹${totalEarned}</span>
                        </div>
                    </div>
                `;
            });
        }

        function deleteEmployee(empName) {
            if(confirm('Are you sure?')) {
                db.employees = db.employees.filter(e => e !== empName);
                saveData();
                renderEmployees();
            }
        }

        function saveStoreItem(e) {
            e.preventDefault();
            let name = document.getElementById('store-item-name').value;
            let price = document.getElementById('store-item-price').value;
            let fileInput = document.getElementById('store-item-image');

            if(fileInput.files.length > 0) {
                let file = fileInput.files[0];
                if(file.size > 5 * 1024 * 1024) {
                    alert('⚠️ Image size exceeds 5MB!');
                    return;
                }

                let reader = new FileReader();
                reader.onload = function(uploadEvent) {
                    db.store.push({ id: Date.now(), name, price, image: uploadEvent.target.result });
                    saveData();
                    renderStore();
                    document.getElementById('store-item-name').value = '';
                    document.getElementById('store-item-price').value = '';
                    fileInput.value = '';
                    alert('✅ Store Item Saved!');
                };
                reader.readAsDataURL(file);
            }
        }

        function renderStore() {
            let grid = document.getElementById('store-items-grid');
            grid.innerHTML = '';

            if(db.store.length === 0) {
                grid.innerHTML = `<p class="text-slate-500 col-span-full">❌ No Store Items Available</p>`;
                return;
            }

            db.store.forEach(item => {
                grid.innerHTML += `
                    <div class="bg-darkBlue border border-slate-700 rounded-xl overflow-hidden shadow">
                        <img src="${item.image}" alt="${item.name}" class="w-full h-36 object-cover">
                        <div class="p-3">
                            <h4 class="text-white text-sm">${item.name}</h4>
                            <p class="text-emerald-400 text-xs mt-1">₹${item.price}</p>
                            <button onclick="deleteStoreItem(${item.id})" class="mt-3 w-full bg-red-900/40 border border-red-700 text-red-300 py-1 rounded text-xs">🗑️ Delete</button>
                        </div>
                    </div>
                `;
            });
        }

        function deleteStoreItem(id) {
            if(confirm('Delete this item?')) {
                db.store = db.store.filter(i => i.id !== id);
                saveData();
                renderStore();
            }
        }

        function renderAnalytics() {
            let filterDate = document.getElementById('filter-analytics-date').value;
            let tbody = document.getElementById('analytics-tbody');
            tbody.innerHTML = '';

            let allOrders = [...db.customers, ...db.completed];
            if(filterDate) {
                allOrders = allOrders.filter(o => o.date === filterDate || o.completedDate === filterDate);
            }

            document.getElementById('ana-total-orders').innerText = allOrders.length;
            document.getElementById('ana-total-rev').innerText = `₹${allOrders.reduce((s, o) => s + (o.stitchCharge || 0), 0)}`;
            document.getElementById('ana-total-prof').innerText = `₹${allOrders.reduce((s, o) => s + (o.profit || 0), 0)}`;

            if(allOrders.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="p-4 text-center text-slate-500">❌ No Data Available</td></tr>`;
                return;
            }

            allOrders.forEach(o => {
                let statusBadge = db.completed.some(c => c.id === o.id) ? '✅ Completed' : '⚡ Active';
                tbody.innerHTML += `
                    <tr class="border-b border-slate-800">
                        <td class="p-3">${o.date}</td>
                        <td class="p-3 text-white">${o.name}</td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded text-xs ${o.category==='BEBI'?'bg-pink-900 text-pink-300':'bg-purple-900 text-purple-300'}">${o.category}</span></td>
                        <td class="p-3 text-emerald-400">₹${o.stitchCharge}</td>
                        <td class="p-3 text-blue-400">₹${o.profit}</td>
                        <td class="p-3">${statusBadge}</td>
                    </tr>
                `;
            });
        }

        function resetAnalyticsFilter() {
            document.getElementById('filter-analytics-date').value = '';
            renderAnalytics();
        }

        function updateDashboard() {
            let allOrders = [...db.customers, ...db.completed];
            let totalRevenue = allOrders.reduce((sum, o) => sum + (o.stitchCharge || 0), 0);
            let bebiRev = allOrders.filter(o => o.category === 'BEBI').reduce((sum, o) => sum + (o.stitchCharge || 0), 0);
            let lediRev = allOrders.filter(o => o.category === 'LEDI').reduce((sum, o) => sum + (o.stitchCharge || 0), 0);

            let totalProfit = allOrders.reduce((sum, o) => sum + (o.profit || 0), 0);
            let bebiProf = allOrders.filter(o => o.category === 'BEBI').reduce((sum, o) => sum + (o.profit || 0), 0);
            let lediProf = allOrders.filter(o => o.category === 'LEDI').reduce((sum, o) => sum + (o.profit || 0), 0);

            document.getElementById('dash-total-revenue').innerText = `₹${totalRevenue}`;
            document.getElementById('dash-bebi-rev').innerText = `₹${bebiRev}`;
            document.getElementById('dash-ledi-rev').innerText = `₹${lediRev}`;

            document.getElementById('dash-total-profit').innerText = `₹${totalProfit}`;
            document.getElementById('dash-bebi-prof').innerText = `₹${bebiProf}`;
            document.getElementById('dash-ledi-prof').innerText = `₹${lediProf}`;

            document.getElementById('stat-active-count').innerText = db.customers.length;
            document.getElementById('stat-completed-count').innerText = db.completed.length;
            document.getElementById('stat-employee-count').innerText = db.employees.length;

            let anuTotal = 0;
            allOrders.forEach(o => {
                let exp = o.expense || 0;
                anuTotal += (exp <= 300) ? exp : 300;
            });
            document.getElementById('dash-anu-total').innerText = `₹${anuTotal}`;

            if(db.customers.length > 0) {
                let sortedActive = [...db.customers].sort((a,b) => new Date(a.date) - new Date(b.date));
                let nextCust = sortedActive[0];
                document.getElementById('dash-next-name').innerText = `${nextCust.name} (${nextCust.category})`;
                document.getElementById('dash-next-date').innerText = `📅 ${nextCust.date}`;
            } else {
                document.getElementById('dash-next-name').innerText = '-';
                document.getElementById('dash-next-date').innerText = '-';
            }

            renderActiveCustomers();
            renderCompletedCustomers();
        }

        window.onload = function() {
            updateDashboard();
        };
    </script>
</body>
</html>
