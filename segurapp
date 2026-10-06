<!DOCTYPE html>
<html lang="es" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Control Financiero Personal (COP)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- FontAwesome para Iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }

        @keyframes pulse-red {
            0%, 100% {
                box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7);
                border-color: rgba(239, 68, 68, 1);
            }
            50% {
                box-shadow: 0 0 0 8px rgba(239, 68, 68, 0);
                border-color: rgba(220, 38, 38, 1);
            }
        }

        @keyframes blink-warning {
            0% { opacity: 1; }
            50% { opacity: 0.6; }
            100% { opacity: 1; }
        }

        .overdue-alert {
            animation: pulse-red 2s infinite, blink-warning 1.5s infinite ease-in-out;
            border: 2px solid #ef4444 !important;
            background-color: rgba(254, 242, 242, 0.7) !important;
        }

        .dark .overdue-alert {
            background-color: rgba(127, 29, 29, 0.3) !important;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-900 dark:text-slate-100 transition-colors duration-300 min-h-screen flex flex-col">

    <header class="bg-white dark:bg-slate-800 shadow-sm border-b border-slate-200 dark:border-slate-700 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="bg-emerald-600 text-white p-2.5 rounded-xl shadow-md">
                    <i class="fa-solid fa-wallet text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold tracking-tight">FinanzasApp</h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Control Financiero Personal (COP)</p>
                </div>
            </div>
            <div class="flex items-center gap-3">
                <!-- Botón de Modo Oscuro / Claro -->
                <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 dark:hover:bg-slate-600 transition text-slate-600 dark:text-slate-300 shadow-sm" title="Cambiar Tema">
                    <i id="theme-icon" class="fa-solid fa-moon"></i>
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 py-6 w-full flex-grow space-y-8">

        <!-- 1. DASHBOARD / RESUMEN GENERAL -->
        <section>
            <h2 class="text-lg font-semibold mb-4 flex items-center gap-2">
                <i class="fa-solid fa-chart-pie text-emerald-600"></i> Resumen General
            </h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                <!-- Balance Total -->
                <div class="bg-white dark:bg-slate-800 p-5 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                    <div class="flex justify-between items-center text-slate-500 dark:text-slate-400 mb-2">
                        <span class="text-sm font-medium">Balance Actual</span>
                        <i class="fa-solid fa-scale-balanced text-emerald-500 text-lg"></i>
                    </div>
                    <span id="card-balance" class="text-2xl font-bold tracking-tight">$0</span>
                </div>
                <!-- Total Ingresos -->
                <div class="bg-white dark:bg-slate-800 p-5 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                    <div class="flex justify-between items-center text-slate-500 dark:text-slate-400 mb-2">
                        <span class="text-sm font-medium">Total Ingresos</span>
                        <i class="fa-solid fa-arrow-trend-up text-blue-500 text-lg"></i>
                    </div>
                    <span id="card-income" class="text-2xl font-bold tracking-tight text-blue-600 dark:text-blue-400">$0</span>
                </div>
                <!-- Total Gastos -->
                <div class="bg-white dark:bg-slate-800 p-5 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                    <div class="flex justify-between items-center text-slate-500 dark:text-slate-400 mb-2">
                        <span class="text-sm font-medium">Total Gastos</span>
                        <i class="fa-solid fa-arrow-trend-down text-rose-500 text-lg"></i>
                    </div>
                    <span id="card-expense" class="text-2xl font-bold tracking-tight text-rose-600 dark:text-rose-400">$0</span>
                </div>
                <!-- Ahorro / Presupuesto Restante -->
                <div class="bg-white dark:bg-slate-800 p-5 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                    <div class="flex justify-between items-center text-slate-500 dark:text-slate-400 mb-2">
                        <span class="text-sm font-medium">Ahorros / Restante</span>
                        <i class="fa-solid fa-piggy-bank text-amber-500 text-lg"></i>
                    </div>
                    <span id="card-savings" class="text-2xl font-bold tracking-tight text-amber-600 dark:text-amber-400">$0</span>
                </div>
            </div>
        </section>

        <section class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700">
            <h3 class="text-md font-semibold mb-4 flex items-center gap-2">
                <i class="fa-solid fa-chart-bar text-indigo-500"></i> Distribución de Gastos por Categoría
            </h3>
            <div id="category-progress-container" class="space-y-3">
                <p class="text-sm text-slate-500 dark:text-slate-400 italic">No hay gastos registrados aún para mostrar estadísticas.</p>
            </div>
        </section>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
            
            <!-- 2. SECCIÓN DE INGRESOS -->
            <section class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                <div>
                    <h2 class="text-lg font-semibold mb-4 flex items-center gap-2 text-blue-600 dark:text-blue-400">
                        <i class="fa-solid fa-circle-plus"></i> Gestión de Ingresos
                    </h2>
                    <!-- Formulario de Ingresos -->
                    <form id="income-form" class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-6">
                        <input type="text" id="income-desc" placeholder="Descripción (ej. Salario, Venta)" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <input type="number" id="income-amount" placeholder="Monto ($ COP)" min="1" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <input type="date" id="income-date" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <input type="text" id="income-category" placeholder="Categoría (ej. Principal, Extra)" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button type="submit" class="sm:col-span-2 bg-blue-600 hover:bg-blue-700 text-white font-medium py-2.5 rounded-xl transition shadow-md shadow-blue-500/20 text-sm">
                            <i class="fa-solid fa-plus mr-1"></i> Registrar Ingreso
                        </button>
                    </form>
                </div>
                <!-- Lista de Ingresos -->
                <div>
                    <h3 class="text-sm font-semibold text-slate-500 dark:text-slate-400 mb-3">Historial de Ingresos</h3>
                    <div class="overflow-x-auto max-h-60 overflow-y-auto pr-1">
                        <table class="w-full text-left border-collapse text-sm">
                            <thead class="bg-slate-100 dark:bg-slate-700/50 sticky top-0 text-xs text-slate-500 uppercase">
                                <tr>
                                    <th class="p-2.5 rounded-l-lg">Descripción</th>
                                    <th class="p-2.5">Monto</th>
                                    <th class="p-2.5">Fecha</th>
                                    <th class="p-2.5 rounded-r-lg text-right">Acción</th>
                                </tr>
                            </thead>
                            <tbody id="income-table-body" class="divide-y divide-slate-100 dark:divide-slate-700">
                                <!-- Dinámico -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 3. SECCIÓN DE GASTOS -->
            <section class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                <div>
                    <h2 class="text-lg font-semibold mb-4 flex items-center gap-2 text-rose-600 dark:text-rose-400">
                        <i class="fa-solid fa-circle-minus"></i> Gestión de Gastos
                    </h2>
                    <!-- Formulario de Gastos -->
                    <form id="expense-form" class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-6">
                        <input type="text" id="expense-desc" placeholder="Descripción del Gasto" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-rose-500">
                        <input type="number" id="expense-amount" placeholder="Monto ($ COP)" min="1" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-rose-500">
                        
                        <!-- Categorías Obligatorias -->
                        <select id="expense-category" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-rose-500">
                            <option value="" disabled selected>Selecciona una categoría</option>
                            <option value="Servicios básicos">Servicios básicos</option>
                            <option value="Comida">Comida</option>
                            <option value="Comida de perros">Comida de perros</option>
                            <option value="Créditos">Créditos</option>
                            <option value="Arriendo">Arriendo</option>
                            <option value="Mantenimiento de moto">Mantenimiento de moto</option>
                            <option value="Suscripciones">Suscripciones</option>
                            <option value="Otros">Otros</option>
                        </select>

                        <input type="date" id="expense-date" required
                            class="bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-rose-500">
                        
                        <!-- Selector de Estado Inicial -->
                        <select id="expense-status" required
                            class="sm:col-span-2 bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-rose-500">
                            <option value="Pagado">Pagado</option>
                            <option value="Pendiente">Pendiente (Recordar en Google Calendar)</option>
                        </select>

                        <button type="submit" class="sm:col-span-2 bg-rose-600 hover:bg-rose-700 text-white font-medium py-2.5 rounded-xl transition shadow-md shadow-rose-500/20 text-sm">
                            <i class="fa-solid fa-plus mr-1"></i> Registrar Gasto
                        </button>
                    </form>
                </div>
                <!-- Lista de Gastos con Cambio de Estado Rápido -->
                <div>
                    <div class="flex justify-between items-center mb-3">
                        <h3 class="text-sm font-semibold text-slate-500 dark:text-slate-400">Historial de Gastos y Pagos</h3>
                        <span class="text-[11px] text-slate-400">💡 Haz clic en el botón de estado para cambiarlo al instante</span>
                    </div>
                    <div class="overflow-x-auto max-h-60 overflow-y-auto pr-1">
                        <table class="w-full text-left border-collapse text-sm">
                            <thead class="bg-slate-100 dark:bg-slate-700/50 sticky top-0 text-xs text-slate-500 uppercase">
                                <tr>
                                    <th class="p-2.5 rounded-l-lg">Detalle</th>
                                    <th class="p-2.5">Monto / Cat.</th>
                                    <th class="p-2.5">Estado / Calendario</th>
                                    <th class="p-2.5 rounded-r-lg text-right">Acción</th>
                                </tr>
                            </thead>
                            <tbody id="expense-table-body" class="divide-y divide-slate-100 dark:divide-slate-700">
                                <!-- Dinámico -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

        </div>

        <!-- 4. SECCIÓN DE AHORRO PROGRAMADO -->
        <section class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700">
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-6">
                <div>
                    <h2 class="text-lg font-semibold flex items-center gap-2 text-amber-600 dark:text-amber-400">
                        <i class="fa-solid fa-vault"></i> Módulo de Ahorro Programado (Metas Flexibles)
                    </h2>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Crea casillas de ahorro personalizado para cumplir tus propósitos financieros.</p>
                </div>
                <button onclick="openGoalModal()" class="bg-amber-600 hover:bg-amber-700 text-white font-medium px-4 py-2 rounded-xl text-sm transition shadow-md shadow-amber-500/20">
                    <i class="fa-solid fa-plus mr-1"></i> Nueva Meta de Ahorro
                </button>
            </div>

            <div id="savings-goals-container" class="space-y-6">
                <p class="text-sm text-slate-500 dark:text-slate-400 italic">No tienes metas de ahorro configuradas. ¡Crea una para comenzar a tachar tus casillas!</p>
            </div>
        </section>

    </main>

    <div id="goal-modal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl p-6 max-w-md w-full shadow-2xl border border-slate-200 dark:border-slate-700">
            <h3 class="text-lg font-bold mb-4 flex items-center gap-2 text-amber-600">
                <i class="fa-solid fa-bullseye"></i> Configurar Meta de Ahorro
            </h3>
            <form id="goal-form" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase text-slate-500 mb-1">¿Para qué es tu ahorro? (Propósito)</label>
                    <input type="text" id="goal-title" placeholder="ej. Fondo de Emergencia, Viaje, Moto" required
                        class="w-full bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase text-slate-500 mb-1">Monto inicial o personalizado por casilla</label>
                    <input type="text" id="goal-amounts-array" placeholder="2000, 5000, 10000, 20000, 40000" value="2000, 5000, 10000, 15000, 20000, 25000, 30000, 35000, 40000" required
                        class="w-full bg-slate-50 dark:bg-slate-900 border border-slate-300 dark:border-slate-700 px-4 py-2.5 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-amber-500">
                </div>
                <div class="flex justify-end gap-3 pt-2">
                    <button type="button" onclick="closeGoalModal()" class="px-4 py-2 rounded-xl text-sm bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-300 hover:bg-slate-300 transition">Cancelar</button>
                    <button type="submit" class="px-4 py-2 rounded-xl text-sm bg-amber-600 hover:bg-amber-700 text-white font-medium transition shadow-md">Crear Plantilla</button>
                </div>
            </form>
        </div>
    </div>

    <footer class="bg-white dark:bg-slate-800 border-t border-slate-200 dark:border-slate-700 py-4 mt-auto text-center text-xs text-slate-500 dark:text-slate-400">
        Control Financiero Personal Adaptado a Pesos Colombianos (COP) &bull; Datos guardados de forma local (LocalStorage).
    </footer>

    <!-- SCRIPT DE FUNCIONALIDAD -->
    <script>
        let finances = JSON.parse(localStorage.getItem('finances_data')) || {
            incomes: [],
            expenses: [],
            savingsGoals: []
        };

        function saveData() {
            localStorage.setItem('finances_data', JSON.stringify(finances));
            renderAll();
        }

        // --- MODO OSCURO / CLARO ---
        function toggleDarkMode() {
            const html = document.documentElement;
            const icon = document.getElementById('theme-icon');
            if (html.classList.contains('dark')) {
                html.classList.remove('dark');
                html.classList.add('light');
                localStorage.setItem('theme', 'light');
                icon.className = 'fa-solid fa-moon';
            } else {
                html.classList.remove('light');
                html.classList.add('dark');
                localStorage.setItem('theme', 'dark');
                icon.className = 'fa-solid fa-sun';
            }
        }

        if (localStorage.getItem('theme') === 'dark') {
            document.documentElement.classList.add('dark');
            document.getElementById('theme-icon').className = 'fa-solid fa-sun';
        }

        // --- FORMATO DE MONEDA (COP) ---
        function formatCOP(amount) {
            return new Intl.NumberFormat('es-CO', {
                style: 'currency',
                currency: 'COP',
                minimumFractionDigits: 0
            }).format(amount);
        }

        // --- GESTIÓN DE INGRESOS ---
        document.getElementById('income-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const newIncome = {
                id: Date.now(),
                desc: document.getElementById('income-desc').value,
                amount: parseFloat(document.getElementById('income-amount').value),
                date: document.getElementById('income-date').value,
                category: document.getElementById('income-category').value
            };
            finances.incomes.push(newIncome);
            document.getElementById('income-form').reset();
            saveData();
        });

        function deleteIncome(id) {
            finances.incomes = finances.incomes.filter(item => item.id !== id);
            saveData();
        }

        // --- GESTIÓN DE GASTOS Y ESTADOS ---
        document.getElementById('expense-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const newExpense = {
                id: Date.now(),
                desc: document.getElementById('expense-desc').value,
                amount: parseFloat(document.getElementById('expense-amount').value),
                category: document.getElementById('expense-category').value,
                date: document.getElementById('expense-date').value,
                status: document.getElementById('expense-status').value
            };
            finances.expenses.push(newExpense);
            document.getElementById('expense-form').reset();
            saveData();
        });

        function deleteExpense(id) {
            finances.expenses = finances.expenses.filter(item => item.id !== id);
            saveData();
        }

        function toggleExpenseStatus(id) {
            const expense = finances.expenses.find(exp => exp.id === id);
            if(expense) {
                expense.status = expense.status === 'Pagado' ? 'Pendiente' : 'Pagado';
                saveData();
            }
        }

        // Comprobar si un gasto está vencido (Fecha programada < Fecha actual y sigue Pendiente)
        function isExpenseOverdue(expenseDate, status) {
            if(status !== 'Pendiente' || !expenseDate) return false;
            
            // Obtener fecha actual en formato YYYY-MM-DD sin desfase de zona horaria local
            const today = new Date();
            const year = today.getFullYear();
            const month = String(today.getMonth() + 1).padStart(2, '0');
            const day = String(today.getDate()).padStart(2, '0');
            const todayStr = `${year}-${month}-${day}`;

            return expenseDate < todayStr;
        }

        // Generar enlace directo a Google Calendar
        function getGoogleCalendarUrl(expense) {
            const title = encodeURIComponent(`Pago pendiente: ${expense.desc} - Categoría: ${expense.category}`);
            const details = encodeURIComponent(`Monto a pagar: ${formatCOP(expense.amount)}. Gestionado desde Control Financiero Personal.`);
            let dateStr = expense.date ? expense.date.replace(/-/g, '') : new Date().toISOString().slice(0, 10).replace(/-/g, '');
            const dates = `${dateStr}/${dateStr}`;
            const email = 'segurappsite@gmail.com';

            return `https://calendar.google.com/calendar/render?action=TEMPLATE&text=${title}&details=${details}&dates=${dates}&add=${email}`;
        }

        // --- MÓDULO DE AHORRO PROGRAMADO ---
        function openGoalModal() {
            document.getElementById('goal-modal').classList.remove('hidden');
        }

        function closeGoalModal() {
            document.getElementById('goal-modal').classList.add('hidden');
        }

        document.getElementById('goal-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const title = document.getElementById('goal-title').value;
            const rawAmounts = document.getElementById('goal-amounts-array').value;
            const amountsArray = rawAmounts.split(',').map(val => parseFloat(val.trim())).filter(val => !isNaN(val) && val > 0);

            if(amountsArray.length === 0) {
                return;
            }

            const newGoal = {
                id: Date.now(),
                title: title,
                boxes: amountsArray.map(amt => ({ amount: amt, checked: false }))
            };

            finances.savingsGoals.push(newGoal);
            document.getElementById('goal-form').reset();
            closeGoalModal();
            saveData();
        });

        function toggleSavingsBox(goalId, boxIndex) {
            const goal = finances.savingsGoals.find(g => g.id === goalId);
            if(goal) {
                goal.boxes[boxIndex].checked = !goal.boxes[boxIndex].checked;
                saveData();
            }
        }

        function deleteGoal(goalId) {
            finances.savingsGoals = finances.savingsGoals.filter(g => g.id !== goalId);
            saveData();
        }

        function renderAll() {
            const totalIncome = finances.incomes.reduce((acc, curr) => acc + curr.amount, 0);
            const totalExpense = finances.expenses.reduce((acc, curr) => acc + curr.amount, 0);
            
            let totalSavedInGoals = 0;
            finances.savingsGoals.forEach(goal => {
                goal.boxes.forEach(box => {
                    if(box.checked) totalSavedInGoals += box.amount;
                });
            });

            const currentBalance = totalIncome - totalExpense;

            document.getElementById('card-balance').innerText = formatCOP(currentBalance);
            document.getElementById('card-income').innerText = formatCOP(totalIncome);
            document.getElementById('card-expense').innerText = formatCOP(totalExpense);
            document.getElementById('card-savings').innerText = formatCOP(totalSavedInGoals);

            // Renderizar Ingresos
            const incomeTable = document.getElementById('income-table-body');
            incomeTable.innerHTML = '';
            if(finances.incomes.length === 0) {
                incomeTable.innerHTML = `<tr><td colspan="4" class="p-3 text-center text-slate-400 italic">No hay ingresos registrados.</td></tr>`;
            } else {
                finances.incomes.forEach(inc => {
                    incomeTable.innerHTML += `
                        <tr class="hover:bg-slate-50 dark:hover:bg-slate-700/30 transition">
                            <td class="p-2.5 font-medium">${inc.desc}<br><span class="text-xs text-slate-400">${inc.category}</span></td>
                            <td class="p-2.5 text-blue-600 dark:text-blue-400 font-semibold">${formatCOP(inc.amount)}</td>
                            <td class="p-2.5 text-slate-500 text-xs">${inc.date}</td>
                            <td class="p-2.5 text-right">
                                <button onclick="deleteIncome(${inc.id})" class="text-slate-400 hover:text-rose-500 transition p-1"><i class="fa-solid fa-trash-can"></i></button>
                            </td>
                        </tr>`;
                });
            }

            // Renderizar Gastos con verificación de vencimiento y animación en rojo
            const expenseTable = document.getElementById('expense-table-body');
            expenseTable.innerHTML = '';
            if(finances.expenses.length === 0) {
                expenseTable.innerHTML = `<tr><td colspan="4" class="p-3 text-center text-slate-400 italic">No hay gastos registrados.</td></tr>`;
            } else {
                finances.expenses.forEach(exp => {
                    const isOverdue = isExpenseOverdue(exp.date, exp.status);
                    
                    // Definir clases de la fila según si está vencido
                    const rowClass = isOverdue 
                        ? 'overdue-alert rounded-xl transition my-1' 
                        : 'hover:bg-slate-50 dark:hover:bg-slate-700/30 transition';

                    let statusBadge = '';
                    if(exp.status === 'Pagado') {
                        statusBadge = `
                            <button onclick="toggleExpenseStatus(${exp.id})" title="Clic para marcar como Pendiente" class="inline-flex items-center gap-1.5 px-3 py-1 text-xs bg-emerald-100 text-emerald-700 dark:bg-emerald-900/50 dark:text-emerald-300 rounded-full font-medium hover:bg-emerald-200 transition shadow-sm cursor-pointer">
                                <i class="fa-solid fa-circle-check"></i> Pagado (Cambiar)
                            </button>`;
                    } else if(isOverdue) {
                        statusBadge = `
                            <div class="flex flex-col gap-1.5 items-start">
                                <button onclick="toggleExpenseStatus(${exp.id})" title="Clic para marcar como Pagado" class="inline-flex items-center gap-1.5 px-3 py-1 text-xs bg-rose-600 text-white rounded-full font-bold hover:bg-rose-700 transition shadow-md animate-bounce cursor-pointer">
                                    <i class="fa-solid fa-triangle-exclamation"></i> ¡VENCIDO! (Marcar Pagado)
                                </button>
                                <a href="${getGoogleCalendarUrl(exp)}" target="_blank" class="inline-flex items-center gap-1 text-[11px] text-rose-700 dark:text-rose-300 hover:underline px-2 py-0.5 rounded-md font-medium">
                                    <i class="fa-regular fa-calendar-days"></i> Agregar a Google Calendar
                                </a>
                            </div>`;
                    } else {
                        statusBadge = `
                            <div class="flex flex-col gap-1.5 items-start">
                                <button onclick="toggleExpenseStatus(${exp.id})" title="Clic para marcar como Pagado" class="inline-flex items-center gap-1.5 px-3 py-1 text-xs bg-amber-100 text-amber-700 dark:bg-amber-900/40 dark:text-amber-300 rounded-full font-medium hover:bg-amber-200 transition shadow-sm cursor-pointer">
                                    <i class="fa-solid fa-clock"></i> Pendiente (Marcar Pagado)
                                </button>
                                <a href="${getGoogleCalendarUrl(exp)}" target="_blank" class="inline-flex items-center gap-1 text-[11px] bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-300 hover:underline px-2 py-1 rounded-md font-medium border border-blue-200 dark:border-blue-800">
                                    <i class="fa-regular fa-calendar-days"></i> 📅 Google Calendar
                                </a>
                            </div>`;
                    }

                    expenseTable.innerHTML += `
                        <tr class="${rowClass} align-top">
                            <td class="p-3 font-medium">
                                ${exp.desc}
                                ${isOverdue ? '<span class="block text-[11px] font-bold text-rose-600 dark:text-rose-400"><i class="fa-solid fa-bell"></i> Fecha límite superada</span>' : ''}
                                <br><span class="text-xs text-slate-400">Fecha: ${exp.date}</span>
                            </td>
                            <td class="p-3">
                                <span class="text-rose-600 dark:text-rose-400 font-semibold">${formatCOP(exp.amount)}</span><br>
                                <span class="text-[11px] text-slate-500 bg-slate-100 dark:bg-slate-700 px-1.5 py-0.5 rounded">${exp.category}</span>
                            </td>
                            <td class="p-3">${statusBadge}</td>
                            <td class="p-3 text-right">
                                <button onclick="deleteExpense(${exp.id})" class="text-slate-400 hover:text-rose-500 transition p-1"><i class="fa-solid fa-trash-can"></i></button>
                            </td>
                        </tr>`;
                });
            }

            // Renderizar Gráfico de Categorías
            const categoryContainer = document.getElementById('category-progress-container');
            categoryContainer.innerHTML = '';
            if(finances.expenses.length === 0) {
                categoryContainer.innerHTML = `<p class="text-sm text-slate-500 dark:text-slate-400 italic">No hay gastos registrados aún para mostrar estadísticas.</p>`;
            } else {
                const categoryTotals = {};
                finances.expenses.forEach(exp => {
                    categoryTotals[exp.category] = (categoryTotals[exp.category] || 0) + exp.amount;
                });

                for(const [cat, amt] of Object.entries(categoryTotals)) {
                    const percentage = totalExpense > 0 ? ((amt / totalExpense) * 100).toFixed(1) : 0;
                    categoryContainer.innerHTML += `
                        <div>
                            <div class="flex justify-between text-xs font-medium mb-1">
                                <span class="text-slate-700 dark:text-slate-300">${cat}</span>
                                <span class="text-slate-500">${formatCOP(amt)} (${percentage}%)</span>
                            </div>
                            <div class="w-full bg-slate-100 dark:bg-slate-700 h-2.5 rounded-full overflow-hidden">
                                <div class="bg-rose-500 h-2.5 rounded-full transition-all duration-500" style="width: ${percentage}%"></div>
                            </div>
                        </div>`;
                }
            }

            // Renderizar Metas de Ahorro
            const goalsContainer = document.getElementById('savings-goals-container');
            goalsContainer.innerHTML = '';
            if(finances.savingsGoals.length === 0) {
                goalsContainer.innerHTML = `<p class="text-sm text-slate-500 dark:text-slate-400 italic">No tienes metas de ahorro configuradas. ¡Crea una para comenzar a tachar tus casillas!</p>`;
            } else {
                finances.savingsGoals.forEach(goal => {
                    let goalSaved = goal.boxes.filter(b => b.checked).reduce((acc, b) => acc + b.amount, 0);
                    let goalTotalPossible = goal.boxes.reduce((acc, b) => acc + b.amount, 0);
                    let goalProgress = goalTotalPossible > 0 ? ((goalSaved / goalTotalPossible) * 100).toFixed(0) : 0;

                    let boxesHtml = '';
                    goal.boxes.forEach((box, index) => {
                        let boxClass = box.checked 
                            ? 'bg-emerald-500 text-white border-emerald-600 shadow-sm scale-95 font-semibold' 
                            : 'bg-slate-50 dark:bg-slate-900 border-slate-300 dark:border-slate-700 text-slate-700 dark:text-slate-300 hover:border-amber-500';
                        boxesHtml += `
                            <button onclick="toggleSavingsBox(${goal.id}, ${index})" class="p-2.5 rounded-xl border text-xs font-medium transition-all flex flex-col items-center justify-center gap-1 ${boxClass}">
                                <span class="text-[10px] opacity-75">Casilla ${index + 1}</span>
                                <span>${formatCOP(box.amount)}</span>
                                <i class="fa-solid ${box.checked ? 'fa-circle-check text-white' : 'fa-circle text-slate-300 dark:text-slate-700'} text-xs"></i>
                            </button>`;
                    });

                    goalsContainer.innerHTML += `
                        <div class="bg-slate-50 dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-700 space-y-4">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
                                <div>
                                    <h4 class="font-bold text-base text-slate-800 dark:text-slate-100 flex items-center gap-2">
                                        <i class="fa-solid fa-flag text-amber-500"></i> ${goal.title}
                                    </h4>
                                    <p class="text-xs text-slate-500">Ahorrado: <span class="font-semibold text-emerald-600 dark:text-emerald-400">${formatCOP(goalSaved)}</span> de ${formatCOP(goalTotalPossible)} (${goalProgress}%)</p>
                                </div>
                                <button onclick="deleteGoal(${goal.id})" class="text-xs text-rose-500 hover:text-rose-700 font-medium transition flex items-center gap-1">
                                    <i class="fa-solid fa-trash-can"></i> Eliminar Meta
                                </button>
                            </div>
                            <div class="w-full bg-slate-200 dark:bg-slate-700 h-2 rounded-full overflow-hidden">
                                <div class="bg-emerald-500 h-2 rounded-full transition-all duration-500" style="width: ${goalProgress}%"></div>
                            </div>
                            <div class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-6 lg:grid-cols-8 gap-2 pt-2">
                                ${boxesHtml}
                            </div>
                        </div>`;
                });
            }
        }

        renderAll();
    </script>
</body>
</html>
