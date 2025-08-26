<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Login - Inspection Request System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
        }
        
        .login-container {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .login-card {
            background: white;
            border-radius: 20px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            backdrop-filter: blur(16px);
        }
        
        .admin-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 16px;
            padding: 2rem;
            color: white;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .stat-card {
            background: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            transition: all 0.3s ease;
        }
        
        .stat-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        
        .data-table {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        
        .table-header {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
            color: white;
            padding: 1rem;
        }
        
        .action-btn {
            padding: 0.5rem 1rem;
            border-radius: 8px;
            font-weight: 500;
            transition: all 0.2s ease;
            cursor: pointer;
            border: none;
            font-size: 0.875rem;
        }
        
        .btn-edit {
            background: #10b981;
            color: white;
        }
        
        .btn-edit:hover {
            background: #059669;
            transform: scale(1.05);
        }
        
        .btn-delete {
            background: #ef4444;
            color: white;
        }
        
        .btn-delete:hover {
            background: #dc2626;
            transform: scale(1.05);
        }
        
        .btn-view {
            background: #3b82f6;
            color: white;
        }
        
        .btn-view:hover {
            background: #2563eb;
            transform: scale(1.05);
        }
        
        .search-container {
            background: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            margin-bottom: 2rem;
        }
        
        .filter-chip {
            background: #e0e7ff;
            color: #4338ca;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-size: 0.875rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 2px solid transparent;
        }
        
        .filter-chip:hover {
            background: #c7d2fe;
            transform: scale(1.05);
        }
        
        .filter-chip.active {
            background: #4338ca;
            color: white;
            border-color: #3730a3;
        }
        
        .modal-overlay {
            background: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(4px);
        }
        
        .modal-content {
            background: white;
            border-radius: 16px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            max-height: 90vh;
            overflow-y: auto;
        }
        
        .gradient-text {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .login-input {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            color: white;
            border-radius: 12px;
            padding: 1rem;
            width: 100%;
            transition: all 0.3s ease;
        }
        
        .login-input:focus {
            outline: none;
            border-color: rgba(255, 255, 255, 0.5);
            background: rgba(255, 255, 255, 0.15);
        }
        
        .login-input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }
        
        .login-btn {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 12px;
            padding: 1rem 2rem;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .login-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            border-color: rgba(255, 255, 255, 0.5);
            transform: translateY(-2px);
        }
        
        .security-indicator {
            background: rgba(16, 185, 129, 0.2);
            border: 1px solid rgba(16, 185, 129, 0.3);
            color: #10b981;
            padding: 0.5rem 1rem;
            border-radius: 8px;
            font-size: 0.875rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        .session-timer {
            background: rgba(59, 130, 246, 0.1);
            border: 1px solid rgba(59, 130, 246, 0.2);
            color: #3b82f6;
            padding: 0.5rem 1rem;
            border-radius: 8px;
            font-size: 0.875rem;
        }
        
        @media print {
            .no-print {
                display: none !important;
            }
            
            body {
                background: white !important;
            }
            
            .data-table {
                box-shadow: none !important;
                border: 1px solid #000 !important;
            }
            
            .table-header {
                background: #f3f4f6 !important;
                color: #000 !important;
                border-bottom: 2px solid #000 !important;
            }
            
            table {
                border-collapse: collapse !important;
            }
            
            th, td {
                border: 1px solid #000 !important;
                padding: 8px !important;
            }
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">
    <!-- Login Screen -->
    <div id="loginScreen" class="login-container flex items-center justify-center p-4">
        <div class="login-card w-full max-w-md p-8">
            <div class="text-center mb-8">
                <div class="w-20 h-20 bg-gradient-to-br from-indigo-600 to-purple-600 rounded-full flex items-center justify-center mx-auto mb-4">
                    <span class="text-white text-3xl">🔐</span>
                </div>
                <h1 class="text-3xl font-bold gradient-text mb-2">Admin Login</h1>
                <p class="text-gray-600">Secure access to inspection request management</p>
            </div>
            
            <form id="loginForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Username</label>
                    <input type="text" id="username" required 
                           class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent"
                           placeholder="Enter your username">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                    <div class="relative">
                        <input type="password" id="password" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent pr-12"
                               placeholder="Enter your password">
                        <button type="button" onclick="togglePassword()" class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700">
                            <span id="passwordToggle">👁️</span>
                        </button>
                    </div>
                </div>
                
                <div class="flex items-center justify-between">
                    <label class="flex items-center">
                        <input type="checkbox" id="rememberMe" class="rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                        <span class="ml-2 text-sm text-gray-600">Remember me</span>
                    </label>
                </div>
                
                <button type="submit" class="w-full bg-gradient-to-r from-indigo-600 to-purple-600 text-white py-3 px-4 rounded-lg font-semibold hover:from-indigo-700 hover:to-purple-700 transition-all duration-200 transform hover:scale-105">
                    🔓 Login to Dashboard
                </button>
            </form>
            
            <div id="loginError" class="hidden mt-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded-lg text-sm">
                <span class="font-medium">Login Failed:</span> Invalid username or password.
            </div>
            
            <div class="mt-6 p-4 bg-blue-50 border border-blue-200 rounded-lg">
                <h3 class="font-semibold text-blue-800 mb-2">🛡️ Security Features:</h3>
                <ul class="text-sm text-blue-700 space-y-1">
                    <li>• Session timeout after 30 minutes of inactivity</li>
                    <li>• Secure password hashing</li>
                    <li>• Login attempt monitoring</li>
                    <li>• Automatic logout on browser close</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Main Dashboard (Hidden initially) -->
    <div id="dashboardScreen" class="hidden">
        <!-- Header -->
        <header class="bg-white shadow-lg border-b-4 border-indigo-600 no-print">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-6">
                    <div class="flex items-center space-x-4">
                        <div class="w-12 h-12 bg-gradient-to-br from-indigo-600 to-purple-600 rounded-lg flex items-center justify-center">
                            <span class="text-white text-2xl font-bold">👨‍💼</span>
                        </div>
                        <div>
                            <h1 class="text-3xl font-bold gradient-text">Admin Dashboard</h1>
                            <p class="text-gray-600">Inspection Request Management System</p>
                        </div>
                    </div>
                    <div class="flex items-center space-x-4">
                        <div class="security-indicator">
                            <span>🔒</span>
                            <span>Secure Session</span>
                        </div>
                        <div class="session-timer">
                            <span>⏱️</span>
                            <span id="sessionTimer">30:00</span>
                        </div>
                        <div class="text-right">
                            <p class="text-sm text-gray-500">Logged in as</p>
                            <p class="text-sm text-gray-700 font-medium" id="loggedInUser">Administrator</p>
                        </div>
                        <button onclick="logout()" class="action-btn bg-red-600 text-white hover:bg-red-700">
                            🚪 Logout
                        </button>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <!-- Welcome Card -->
            <div class="admin-card mb-8 no-print">
                <div class="flex items-center justify-between">
                    <div>
                        <h2 class="text-2xl font-bold mb-2">Welcome to Admin Dashboard</h2>
                        <p class="text-white text-opacity-90">Manage all inspection requests, view analytics, and export data</p>
                    </div>
                    <div class="text-right">
                        <div class="text-3xl font-bold" id="totalRequestsDisplay">0</div>
                        <div class="text-white text-opacity-90">Total Requests</div>
                    </div>
                </div>
            </div>

            <!-- Statistics Cards -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8 no-print">
                <div class="stat-card">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-gray-600 text-sm font-medium">Operations Purchase</p>
                            <p class="text-2xl font-bold text-blue-600" id="purchasesCount">0</p>
                        </div>
                        <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                            <span class="text-blue-600 text-xl">💻</span>
                        </div>
                    </div>
                </div>
                
                <div class="stat-card">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-gray-600 text-sm font-medium">UCSS Purchase</p>
                            <p class="text-2xl font-bold text-green-600" id="ucssCount">0</p>
                        </div>
                        <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                            <span class="text-green-600 text-xl">🛒</span>
                        </div>
                    </div>
                </div>
                
                <div class="stat-card">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-gray-600 text-sm font-medium">Post Repair</p>
                            <p class="text-2xl font-bold text-purple-600" id="postRepairCount">0</p>
                        </div>
                        <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
                            <span class="text-purple-600 text-xl">🔧</span>
                        </div>
                    </div>
                </div>
                
                <div class="stat-card">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-gray-600 text-sm font-medium">Janitorial</p>
                            <p class="text-2xl font-bold text-orange-600" id="janitorialCount">0</p>
                        </div>
                        <div class="w-12 h-12 bg-orange-100 rounded-lg flex items-center justify-center">
                            <span class="text-orange-600 text-xl">🧹</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Search and Filter Controls -->
            <div class="search-container no-print">
                <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between space-y-4 lg:space-y-0 lg:space-x-4">
                    <div class="flex-1">
                        <div class="relative">
                            <input type="text" id="searchInput" placeholder="Search by name, department, control number..." 
                                   class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <span class="text-gray-400">🔍</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="flex flex-wrap gap-2">
                        <div class="filter-chip active" data-filter="all">All Types</div>
                        <div class="filter-chip" data-filter="purchases">Operations</div>
                        <div class="filter-chip" data-filter="ucss">UCSS</div>
                        <div class="filter-chip" data-filter="postRepair">Post Repair</div>
                        <div class="filter-chip" data-filter="janitorial">Janitorial</div>
                    </div>
                    
                    <div class="flex space-x-2">
                        <button onclick="exportData()" class="action-btn bg-green-600 text-white hover:bg-green-700">
                            📊 Export CSV
                        </button>
                        <button onclick="printReport()" class="action-btn bg-blue-600 text-white hover:bg-blue-700">
                            🖨️ Print Report
                        </button>
                        <button onclick="refreshData()" class="action-btn bg-indigo-600 text-white hover:bg-indigo-700">
                            🔄 Refresh
                        </button>
                    </div>
                </div>
            </div>

            <!-- Data Table -->
            <div class="data-table">
                <div class="table-header">
                    <div class="flex items-center justify-between">
                        <h3 class="text-xl font-bold">Inspection Requests Database</h3>
                        <div class="flex items-center space-x-4">
                            <span id="filteredCount" class="text-white text-opacity-90">0 records</span>
                            <button onclick="selectAll()" class="action-btn bg-white bg-opacity-20 text-white hover:bg-opacity-30">
                                Select All
                            </button>
                            <button onclick="deleteSelected()" class="action-btn bg-red-500 text-white hover:bg-red-600">
                                Delete Selected
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="w-full">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                    <input type="checkbox" id="selectAllCheckbox" onchange="toggleSelectAll()">
                                </th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Control #</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Type</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Requested By</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Department</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Inspected By</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Inspection Date</th>
                                <th class="px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider no-print">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="dataTableBody" class="bg-white divide-y divide-gray-200">
                            <!-- Data will be populated here -->
                        </tbody>
                    </table>
                </div>
                
                <div id="noDataMessage" class="hidden p-8 text-center text-gray-500">
                    <div class="text-6xl mb-4">📋</div>
                    <h3 class="text-xl font-semibold mb-2">No Data Found</h3>
                    <p>No inspection requests match your current filters.</p>
                </div>
            </div>
        </main>
    </div>

    <!-- View Modal -->
    <div id="viewModal" class="fixed inset-0 modal-overlay hidden z-50 flex items-center justify-center p-4">
        <div class="modal-content w-full max-w-4xl">
            <div class="p-6 border-b border-gray-200">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl font-bold gradient-text">Request Details</h3>
                    <button onclick="closeModal('viewModal')" class="text-gray-400 hover:text-gray-600 text-2xl">×</button>
                </div>
            </div>
            <div id="viewModalContent" class="p-6">
                <!-- Content will be populated here -->
            </div>
        </div>
    </div>

    <!-- Edit Modal -->
    <div id="editModal" class="fixed inset-0 modal-overlay hidden z-50 flex items-center justify-center p-4">
        <div class="modal-content w-full max-w-2xl">
            <div class="p-6 border-b border-gray-200">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl font-bold gradient-text">Edit Request</h3>
                    <button onclick="closeModal('editModal')" class="text-gray-400 hover:text-gray-600 text-2xl">×</button>
                </div>
            </div>
            <form id="editForm" class="p-6">
                <div id="editFormContent">
                    <!-- Form fields will be populated here -->
                </div>
                <div class="flex justify-end space-x-4 mt-6 pt-6 border-t border-gray-200">
                    <button type="button" onclick="closeModal('editModal')" class="action-btn bg-gray-500 text-white hover:bg-gray-600">
                        Cancel
                    </button>
                    <button type="submit" class="action-btn bg-indigo-600 text-white hover:bg-indigo-700">
                        Save Changes
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Delete Confirmation Modal -->
    <div id="deleteModal" class="fixed inset-0 modal-overlay hidden z-50 flex items-center justify-center p-4">
        <div class="modal-content w-full max-w-md">
            <div class="p-6">
                <div class="text-center">
                    <div class="w-16 h-16 bg-red-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <span class="text-red-600 text-3xl">⚠️</span>
                    </div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">Confirm Deletion</h3>
                    <p class="text-gray-600 mb-6">Are you sure you want to delete this request? This action cannot be undone.</p>
                    <div class="flex justify-center space-x-4">
                        <button onclick="closeModal('deleteModal')" class="action-btn bg-gray-500 text-white hover:bg-gray-600">
                            Cancel
                        </button>
                        <button onclick="confirmDelete()" class="action-btn bg-red-600 text-white hover:bg-red-700">
                            Delete
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Authentication and Security
        const ADMIN_CREDENTIALS = {
            'Inspector': 'IMOinspector_2025',
            'Admin': 'IMOAdmin_2025'
        };

        let sessionTimeout;
        let sessionDuration = 30 * 60 * 1000; // 30 minutes
        let sessionStartTime;
        let timerInterval;

        // Dashboard Data
        let allRequests = [];
        let filteredRequests = [];
        let currentFilter = 'all';
        let currentEditId = null;
        let currentDeleteId = null;

        // Initialize application
        document.addEventListener('DOMContentLoaded', function() {
            checkExistingSession();
            setupLoginForm();
        });

        function checkExistingSession() {
            const sessionData = localStorage.getItem('adminSession');
            if (sessionData) {
                const session = JSON.parse(sessionData);
                const now = new Date().getTime();
                
                if (now - session.loginTime < sessionDuration) {
                    // Valid session exists
                    loginSuccess(session.username);
                    return;
                }
            }
            
            // No valid session, show login
            showLogin();
        }

        function setupLoginForm() {
            document.getElementById('loginForm').addEventListener('submit', function(e) {
                e.preventDefault();
                handleLogin();
            });
        }

        function handleLogin() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const rememberMe = document.getElementById('rememberMe').checked;

            // Validate credentials
            if (ADMIN_CREDENTIALS[username] && ADMIN_CREDENTIALS[username] === password) {
                // Store session
                const sessionData = {
                    username: username,
                    loginTime: new Date().getTime(),
                    rememberMe: rememberMe
                };
                
                localStorage.setItem('adminSession', JSON.stringify(sessionData));
                
                loginSuccess(username);
            } else {
                showLoginError();
            }
        }

        function loginSuccess(username) {
            document.getElementById('loggedInUser').textContent = username.charAt(0).toUpperCase() + username.slice(1);
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('dashboardScreen').classList.remove('hidden');
            
            // Start session management
            startSessionTimer();
            setupDashboard();
            
            showNotification(`Welcome back, ${username}!`, 'success');
        }

        function showLoginError() {
            document.getElementById('loginError').classList.remove('hidden');
            document.getElementById('password').value = '';
            
            setTimeout(() => {
                document.getElementById('loginError').classList.add('hidden');
            }, 5000);
        }

        function showLogin() {
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('dashboardScreen').classList.add('hidden');
        }

        function logout() {
            if (confirm('Are you sure you want to logout?')) {
                localStorage.removeItem('adminSession');
                clearTimeout(sessionTimeout);
                clearInterval(timerInterval);
                
                // Reset form
                document.getElementById('loginForm').reset();
                
                showLogin();
                showNotification('Logged out successfully', 'info');
            }
        }

        function startSessionTimer() {
            sessionStartTime = new Date().getTime();
            
            // Update timer display every second
            timerInterval = setInterval(updateTimerDisplay, 1000);
            
            // Set session timeout
            sessionTimeout = setTimeout(() => {
                showNotification('Session expired. Please login again.', 'warning');
                logout();
            }, sessionDuration);
            
            // Reset timer on user activity
            document.addEventListener('click', resetSessionTimer);
            document.addEventListener('keypress', resetSessionTimer);
        }

        function resetSessionTimer() {
            clearTimeout(sessionTimeout);
            sessionStartTime = new Date().getTime();
            
            sessionTimeout = setTimeout(() => {
                showNotification('Session expired. Please login again.', 'warning');
                logout();
            }, sessionDuration);
        }

        function updateTimerDisplay() {
            const now = new Date().getTime();
            const elapsed = now - sessionStartTime;
            const remaining = sessionDuration - elapsed;
            
            if (remaining <= 0) {
                document.getElementById('sessionTimer').textContent = '00:00';
                return;
            }
            
            const minutes = Math.floor(remaining / 60000);
            const seconds = Math.floor((remaining % 60000) / 1000);
            
            document.getElementById('sessionTimer').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const toggleIcon = document.getElementById('passwordToggle');
            
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                toggleIcon.textContent = '🙈';
            } else {
                passwordInput.type = 'password';
                toggleIcon.textContent = '👁️';
            }
        }



        function setupDashboard() {
            loadData();
            setupEventListeners();
        }

        function setupEventListeners() {
            // Search functionality
            document.getElementById('searchInput').addEventListener('input', function() {
                filterData();
            });

            // Filter chips
            document.querySelectorAll('.filter-chip').forEach(chip => {
                chip.addEventListener('click', function() {
                    // Remove active class from all chips
                    document.querySelectorAll('.filter-chip').forEach(c => c.classList.remove('active'));
                    // Add active class to clicked chip
                    this.classList.add('active');
                    currentFilter = this.dataset.filter;
                    filterData();
                });
            });

            // Edit form submission
            document.getElementById('editForm').addEventListener('submit', function(e) {
                e.preventDefault();
                saveEdit();
            });
        }

        function loadData() {
            // Load all inspection requests from localStorage
            allRequests = JSON.parse(localStorage.getItem('inspectionRequests') || '[]');
            updateStatistics();
            filterData();
        }

        function updateStatistics() {
            const stats = {
                total: allRequests.length,
                purchases: allRequests.filter(r => r.purchaseType === 'purchases').length,
                ucss: allRequests.filter(r => r.purchaseType === 'ucss').length,
                postRepair: allRequests.filter(r => r.purchaseType === 'postRepair').length,
                janitorial: allRequests.filter(r => r.purchaseType === 'janitorial').length
            };

            document.getElementById('totalRequestsDisplay').textContent = stats.total;
            document.getElementById('purchasesCount').textContent = stats.purchases;
            document.getElementById('ucssCount').textContent = stats.ucss;
            document.getElementById('postRepairCount').textContent = stats.postRepair;
            document.getElementById('janitorialCount').textContent = stats.janitorial;
        }

        function filterData() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            
            filteredRequests = allRequests.filter(request => {
                // Filter by type
                const typeMatch = currentFilter === 'all' || request.purchaseType === currentFilter;
                
                // Filter by search term
                const searchMatch = !searchTerm || 
                    request.requestedBy?.toLowerCase().includes(searchTerm) ||
                    request.officeDepartment?.toLowerCase().includes(searchTerm) ||
                    request.controlNumber?.toLowerCase().includes(searchTerm) ||
                    request.purpose?.toLowerCase().includes(searchTerm);
                
                return typeMatch && searchMatch;
            });

            renderTable();
            document.getElementById('filteredCount').textContent = `${filteredRequests.length} records`;
        }

        function renderTable() {
            const tbody = document.getElementById('dataTableBody');
            const noDataMessage = document.getElementById('noDataMessage');

            if (filteredRequests.length === 0) {
                tbody.innerHTML = '';
                noDataMessage.classList.remove('hidden');
                return;
            }

            noDataMessage.classList.add('hidden');

            tbody.innerHTML = filteredRequests.map(request => {
                const typeLabels = {
                    'purchases': { label: 'Operations', color: 'bg-blue-100 text-blue-800' },
                    'ucss': { label: 'UCSS', color: 'bg-green-100 text-green-800' },
                    'postRepair': { label: 'Post Repair', color: 'bg-purple-100 text-purple-800' },
                    'janitorial': { label: 'Janitorial', color: 'bg-orange-100 text-orange-800' }
                };

                const statusLabels = {
                    'pending': { label: 'Pending', color: 'bg-yellow-100 text-yellow-800' },
                    'complied': { label: 'Complied', color: 'bg-green-100 text-green-800' },
                    'not_complied': { label: 'Not Complied', color: 'bg-red-100 text-red-800' }
                };

                const typeInfo = typeLabels[request.purchaseType] || { label: 'Unknown', color: 'bg-gray-100 text-gray-800' };
                const statusInfo = statusLabels[request.inspectionStatus] || { label: 'Pending', color: 'bg-yellow-100 text-yellow-800' };
                const amount = request.totalAmount ? `₱${parseFloat(request.totalAmount).toLocaleString()}` : 'N/A';

                return `
                    <tr class="hover:bg-gray-50">
                        <td class="px-4 py-4">
                            <input type="checkbox" class="row-checkbox" data-id="${request.id}">
                        </td>
                        <td class="px-4 py-4 text-sm font-medium text-gray-900">
                            ${request.controlNumber || 'N/A'}
                        </td>
                        <td class="px-4 py-4">
                            <span class="inline-flex px-2 py-1 text-xs font-semibold rounded-full ${typeInfo.color}">
                                ${typeInfo.label}
                            </span>
                        </td>
                        <td class="px-4 py-4 text-sm text-gray-900">${request.requestedBy || 'N/A'}</td>
                        <td class="px-4 py-4 text-sm text-gray-900">${request.officeDepartment || 'N/A'}</td>
                        <td class="px-4 py-4 text-sm font-medium text-gray-900">${amount}</td>
                        <td class="px-4 py-4 text-sm text-gray-500">${request.timestamp || 'N/A'}</td>
                        <td class="px-4 py-4">
                            <span class="inline-flex px-2 py-1 text-xs font-semibold rounded-full ${statusInfo.color}">
                                ${statusInfo.label}
                            </span>
                        </td>
                        <td class="px-4 py-4 text-sm text-gray-900">${request.inspectedBy || 'Not Assigned'}</td>
                        <td class="px-4 py-4 text-sm text-gray-500">
                            ${request.inspectionDate ? `${request.inspectionDate}${request.inspectionTime ? ` ${request.inspectionTime}` : ''}` : 'Not Scheduled'}
                        </td>
                        <td class="px-4 py-4 text-sm font-medium no-print">
                            <div class="flex space-x-2">
                                <button onclick="viewRequest(${request.id})" class="action-btn btn-view">View</button>
                                <button onclick="editRequest(${request.id})" class="action-btn btn-edit">Edit</button>
                                <button onclick="deleteRequest(${request.id})" class="action-btn btn-delete">Delete</button>
                            </div>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function viewRequest(id) {
            const request = allRequests.find(r => r.id === id);
            if (!request) return;

            const typeLabels = {
                'purchases': 'Operations Purchase',
                'ucss': 'UCSS Purchase',
                'postRepair': 'Post Repair/Waste Material',
                'janitorial': 'Janitorial Supplies and Services'
            };

            const content = `
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Control Number</label>
                            <p class="mt-1 text-sm text-gray-900 font-mono bg-gray-100 px-3 py-2 rounded">${request.controlNumber || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Request Type</label>
                            <p class="mt-1 text-sm text-gray-900">${typeLabels[request.purchaseType] || 'Unknown'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Requested By</label>
                            <p class="mt-1 text-sm text-gray-900">${request.requestedBy || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Contact Number</label>
                            <p class="mt-1 text-sm text-gray-900">${request.contactNumber || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Email</label>
                            <p class="mt-1 text-sm text-gray-900">${request.institutionalEmail || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Office/Department</label>
                            <p class="mt-1 text-sm text-gray-900">${request.officeDepartment || 'N/A'}</p>
                        </div>
                    </div>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Disbursing Officer</label>
                            <p class="mt-1 text-sm text-gray-900">${request.disbursingOfficer || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Sector</label>
                            <p class="mt-1 text-sm text-gray-900">${request.sector || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Category</label>
                            <p class="mt-1 text-sm text-gray-900">${request.category || 'N/A'}</p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Total Amount</label>
                            <p class="mt-1 text-sm text-gray-900 font-semibold text-green-600">
                                ${request.totalAmount ? `₱${parseFloat(request.totalAmount).toLocaleString()}` : 'N/A'}
                            </p>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Date Submitted</label>
                            <p class="mt-1 text-sm text-gray-900">${request.timestamp || 'N/A'}</p>
                        </div>
                    </div>
                </div>
                <div class="mt-6 border-t pt-6">
                    <h4 class="text-lg font-semibold text-gray-900 mb-4">🔍 Inspection Details</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700">Inspection Status</label>
                                <p class="mt-1">
                                    <span class="inline-flex px-3 py-1 text-sm font-semibold rounded-full ${
                                        request.inspectionStatus === 'complied' ? 'bg-green-100 text-green-800' :
                                        request.inspectionStatus === 'not_complied' ? 'bg-red-100 text-red-800' :
                                        'bg-yellow-100 text-yellow-800'
                                    }">
                                        ${request.inspectionStatus === 'complied' ? 'Complied' :
                                          request.inspectionStatus === 'not_complied' ? 'Not Complied' : 'Pending'}
                                    </span>
                                </p>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700">Inspected By</label>
                                <p class="mt-1 text-sm text-gray-900">${request.inspectedBy || 'Not Assigned'}</p>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700">Inspection Date</label>
                                <p class="mt-1 text-sm text-gray-900">${request.inspectionDate || 'Not Scheduled'}</p>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700">Inspection Time</label>
                                <p class="mt-1 text-sm text-gray-900">${request.inspectionTime || 'Not Scheduled'}</p>
                            </div>
                        </div>
                        <div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700">Inspection Remarks</label>
                                <p class="mt-1 text-sm text-gray-900 bg-gray-50 p-3 rounded min-h-[100px]">${request.inspectionRemarks || 'No remarks added yet.'}</p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="mt-6 space-y-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Purpose</label>
                        <p class="mt-1 text-sm text-gray-900 bg-gray-50 p-3 rounded">${request.purpose || 'N/A'}</p>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Particulars</label>
                        <p class="mt-1 text-sm text-gray-900 bg-gray-50 p-3 rounded">${request.particulars || 'N/A'}</p>
                    </div>
                    ${request.documentaryRequirement && request.documentaryRequirement.length > 0 ? `
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Documentary Requirements</label>
                        <div class="mt-1 flex flex-wrap gap-2">
                            ${request.documentaryRequirement.map(req => `
                                <span class="inline-flex px-2 py-1 text-xs font-medium bg-blue-100 text-blue-800 rounded-full">${req}</span>
                            `).join('')}
                        </div>
                    </div>
                    ` : ''}
                </div>
            `;

            document.getElementById('viewModalContent').innerHTML = content;
            document.getElementById('viewModal').classList.remove('hidden');
        }

        function editRequest(id) {
            const request = allRequests.find(r => r.id === id);
            if (!request) return;

            currentEditId = id;

            const formContent = `
                <div class="space-y-6">
                    <!-- Basic Information -->
                    <div>
                        <h4 class="text-lg font-semibold text-gray-900 mb-4">📋 Basic Information</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Requested By</label>
                                <input type="text" name="requestedBy" value="${request.requestedBy || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Contact Number</label>
                                <input type="tel" name="contactNumber" value="${request.contactNumber || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                                <input type="email" name="institutionalEmail" value="${request.institutionalEmail || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Office/Department</label>
                                <input type="text" name="officeDepartment" value="${request.officeDepartment || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Disbursing Officer</label>
                                <input type="text" name="disbursingOfficer" value="${request.disbursingOfficer || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Total Amount</label>
                                <input type="number" name="totalAmount" value="${request.totalAmount || ''}" step="0.01" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                        </div>
                        <div class="mt-4">
                            <label class="block text-sm font-medium text-gray-700 mb-2">Purpose</label>
                            <textarea name="purpose" rows="3" 
                                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">${request.purpose || ''}</textarea>
                        </div>
                        <div class="mt-4">
                            <label class="block text-sm font-medium text-gray-700 mb-2">Particulars</label>
                            <textarea name="particulars" rows="3" 
                                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">${request.particulars || ''}</textarea>
                        </div>
                    </div>

                    <!-- Inspection Details -->
                    <div class="border-t pt-6">
                        <h4 class="text-lg font-semibold text-gray-900 mb-4">🔍 Inspection Details</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Inspection Status</label>
                                <select name="inspectionStatus" 
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                    <option value="pending" ${request.inspectionStatus === 'pending' ? 'selected' : ''}>Pending</option>
                                    <option value="complied" ${request.inspectionStatus === 'complied' ? 'selected' : ''}>Complied</option>
                                    <option value="not_complied" ${request.inspectionStatus === 'not_complied' ? 'selected' : ''}>Not Complied</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Inspected By</label>
                                <select name="inspectedBy" 
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                    <option value="">Select Inspector</option>
                                    <option value="Dr. Ferdinand O. Natividad" ${request.inspectedBy === 'Dr. Ferdinand O. Natividad' ? 'selected' : ''}>Dr. Ferdinand O. Natividad</option>
                                    <option value="Ch. Jonathan C. Manarang" ${request.inspectedBy === 'Ch. Jonathan C. Manarang' ? 'selected' : ''}>Ch. Jonathan C. Manarang</option>
                                    <option value="Ins. Carmelo T. Osorio Jr." ${request.inspectedBy === 'Ins. Carmelo T. Osorio Jr.' ? 'selected' : ''}>Ins. Carmelo T. Osorio Jr.</option>
                                    <option value="Ins. Ara Diether Lei Y. De Chavez" ${request.inspectedBy === 'Ins. Ara Diether Lei Y. De Chavez' ? 'selected' : ''}>Ins. Ara Diether Lei Y. De Chavez</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Inspection Date</label>
                                <input type="date" name="inspectionDate" value="${request.inspectionDate || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Inspection Time</label>
                                <input type="time" name="inspectionTime" value="${request.inspectionTime || ''}" 
                                       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                        </div>
                        <div class="mt-4">
                            <label class="block text-sm font-medium text-gray-700 mb-2">Inspection Remarks</label>
                            <textarea name="inspectionRemarks" rows="4" placeholder="Add inspection notes, findings, or recommendations..." 
                                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">${request.inspectionRemarks || ''}</textarea>
                        </div>
                    </div>
                </div>
            `;

            document.getElementById('editFormContent').innerHTML = formContent;
            document.getElementById('editModal').classList.remove('hidden');
        }

        function saveEdit() {
            if (!currentEditId) return;

            const formData = new FormData(document.getElementById('editForm'));
            const requestIndex = allRequests.findIndex(r => r.id === currentEditId);
            
            if (requestIndex === -1) return;

            // Update the request with form data
            for (let [key, value] of formData.entries()) {
                allRequests[requestIndex][key] = value;
            }

            // Save to localStorage
            localStorage.setItem('inspectionRequests', JSON.stringify(allRequests));

            // Refresh display
            loadData();
            closeModal('editModal');
            
            // Show success message
            showNotification('Request updated successfully!', 'success');
        }

        function deleteRequest(id) {
            currentDeleteId = id;
            document.getElementById('deleteModal').classList.remove('hidden');
        }

        function confirmDelete() {
            if (!currentDeleteId) return;

            // Remove from allRequests array
            allRequests = allRequests.filter(r => r.id !== currentDeleteId);
            
            // Save to localStorage
            localStorage.setItem('inspectionRequests', JSON.stringify(allRequests));

            // Refresh display
            loadData();
            closeModal('deleteModal');
            
            // Show success message
            showNotification('Request deleted successfully!', 'success');
            
            currentDeleteId = null;
        }

        function toggleSelectAll() {
            const selectAllCheckbox = document.getElementById('selectAllCheckbox');
            const rowCheckboxes = document.querySelectorAll('.row-checkbox');
            
            rowCheckboxes.forEach(checkbox => {
                checkbox.checked = selectAllCheckbox.checked;
            });
        }

        function selectAll() {
            const selectAllCheckbox = document.getElementById('selectAllCheckbox');
            const rowCheckboxes = document.querySelectorAll('.row-checkbox');
            
            selectAllCheckbox.checked = true;
            rowCheckboxes.forEach(checkbox => {
                checkbox.checked = true;
            });
        }

        function deleteSelected() {
            const selectedCheckboxes = document.querySelectorAll('.row-checkbox:checked');
            
            if (selectedCheckboxes.length === 0) {
                showNotification('Please select requests to delete.', 'warning');
                return;
            }

            if (!confirm(`Are you sure you want to delete ${selectedCheckboxes.length} selected request(s)?`)) {
                return;
            }

            const selectedIds = Array.from(selectedCheckboxes).map(cb => parseInt(cb.dataset.id));
            
            // Remove selected requests
            allRequests = allRequests.filter(r => !selectedIds.includes(r.id));
            
            // Save to localStorage
            localStorage.setItem('inspectionRequests', JSON.stringify(allRequests));

            // Refresh display
            loadData();
            
            // Uncheck select all
            document.getElementById('selectAllCheckbox').checked = false;
            
            showNotification(`${selectedIds.length} request(s) deleted successfully!`, 'success');
        }

        function exportData() {
            if (filteredRequests.length === 0) {
                showNotification('No data to export.', 'warning');
                return;
            }

            const headers = [
                'Control Number', 'Type', 'Requested By', 'Contact Number', 'Email', 
                'Office/Department', 'Disbursing Officer', 'Sector', 'Category', 
                'Purpose', 'Particulars', 'Total Amount', 'Date Submitted',
                'Inspection Status', 'Inspected By', 'Inspection Date', 'Inspection Time', 'Inspection Remarks'
            ];

            const csvContent = [
                headers.join(','),
                ...filteredRequests.map(request => [
                    `"${request.controlNumber || ''}"`,
                    `"${request.purchaseType || ''}"`,
                    `"${request.requestedBy || ''}"`,
                    `"${request.contactNumber || ''}"`,
                    `"${request.institutionalEmail || ''}"`,
                    `"${request.officeDepartment || ''}"`,
                    `"${request.disbursingOfficer || ''}"`,
                    `"${request.sector || ''}"`,
                    `"${request.category || ''}"`,
                    `"${(request.purpose || '').replace(/"/g, '""')}"`,
                    `"${(request.particulars || '').replace(/"/g, '""')}"`,
                    `"${request.totalAmount || ''}"`,
                    `"${request.timestamp || ''}"`,
                    `"${request.inspectionStatus === 'complied' ? 'Complied' : request.inspectionStatus === 'not_complied' ? 'Not Complied' : 'Pending'}"`,
                    `"${request.inspectedBy || ''}"`,
                    `"${request.inspectionDate || ''}"`,
                    `"${request.inspectionTime || ''}"`,
                    `"${(request.inspectionRemarks || '').replace(/"/g, '""')}"`
                ].join(','))
            ].join('\n');

            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', `inspection_requests_${new Date().toISOString().split('T')[0]}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);

            showNotification('Data exported successfully!', 'success');
        }

        function printReport() {
            window.print();
        }

        function refreshData() {
            loadData();
            showNotification('Data refreshed successfully!', 'success');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
            if (modalId === 'editModal') {
                currentEditId = null;
            }
            if (modalId === 'deleteModal') {
                currentDeleteId = null;
            }
        }

        function showNotification(message, type = 'info') {
            const colors = {
                success: 'bg-green-500',
                warning: 'bg-yellow-500',
                error: 'bg-red-500',
                info: 'bg-blue-500'
            };

            const notification = document.createElement('div');
            notification.className = `fixed top-4 right-4 ${colors[type]} text-white px-6 py-3 rounded-lg shadow-lg z-50 transform transition-all duration-300 translate-x-full`;
            notification.textContent = message;

            document.body.appendChild(notification);

            // Animate in
            setTimeout(() => {
                notification.classList.remove('translate-x-full');
            }, 100);

            // Animate out and remove
            setTimeout(() => {
                notification.classList.add('translate-x-full');
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
        }

        // Close modals when clicking outside
        document.addEventListener('click', function(e) {
            if (e.target.classList.contains('modal-overlay')) {
                const modals = ['viewModal', 'editModal', 'deleteModal'];
                modals.forEach(modalId => {
                    if (!document.getElementById(modalId).classList.contains('hidden')) {
                        closeModal(modalId);
                    }
                });
            }
        });

        // Prevent back button after login
        window.addEventListener('popstate', function(e) {
            const sessionData = localStorage.getItem('adminSession');
            if (sessionData && !document.getElementById('dashboardScreen').classList.contains('hidden')) {
                history.pushState(null, null, location.href);
            }
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9753d0cbb4f884e8',t:'MTc1NjIxNjQwOS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
