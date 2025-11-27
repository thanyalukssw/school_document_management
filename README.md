<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DS e-Office Tracking System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-green-50 to-yellow-50">
    <!-- Login Modal -->
    <div id="loginModal" class="min-h-screen flex items-center justify-center p-4">
        <div class="bg-white rounded-lg shadow-xl p-8 w-full max-w-md">
            <div class="text-center mb-6">
                <svg class="w-16 h-16 mx-auto text-green-600 mb-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                </svg>
                <h2 class="text-2xl font-bold text-gray-900">DS e-Office Tracking</h2>
                <p class="text-gray-600 mt-1">File Management System</p>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Username</label>
                    <input type="text" id="loginUsername" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500" required>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Password</label>
                    <input type="password" id="loginPassword" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500" required minlength="4">
                </div>

                <div class="flex items-center">
                    <input type="checkbox" id="loginIsAdmin" class="w-4 h-4 text-green-600 border-gray-300 rounded focus:ring-green-500">
                    <label for="loginIsAdmin" class="ml-2 text-sm text-gray-700">Login as Administrator</label>
                </div>

                <button onclick="handleLogin()" class="w-full py-3 bg-gradient-to-r from-green-600 to-yellow-500 text-white rounded-lg hover:from-green-700 hover:to-yellow-600 transition shadow-md font-medium">
                    Sign In
                </button>
            </div>

            <div class="mt-6 p-4 bg-yellow-50 border border-yellow-200 rounded-lg">
                <p class="text-xs text-gray-600">
                    <strong>Demo Mode:</strong> Enter any username and password (min 4 characters)
                </p>
            </div>
        </div>
    </div>

    <!-- Main App -->
    <div id="mainApp" class="hidden">
        <!-- Header -->
        <header class="bg-gradient-to-r from-green-600 to-yellow-500 text-white shadow-lg">
            <div class="max-w-7xl mx-auto px-4 py-4">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-3">
                        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                        </svg>
                        <div>
                            <h1 class="text-2xl font-bold">DS e-Office Tracking</h1>
                            <p class="text-green-100 text-sm">File Management System</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-4">
                        <div class="text-right">
                            <p class="font-semibold" id="currentUsername"></p>
                            <p class="text-xs text-green-100" id="currentUserRole"></p>
                        </div>
                        <button onclick="handleLogout()" class="p-2 hover:bg-white/20 rounded-lg transition">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path>
                            </svg>
                        </button>
                    </div>
                </div>
            </div>
        </header>

        <div class="max-w-7xl mx-auto px-4 py-6">
            <!-- Stats Cards -->
            <div class="grid grid-cols-2 md:grid-cols-6 gap-4 mb-6">
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">Total</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-blue-500"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statTotal">0</p>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">In Process</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statInProcess">0</p>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">Accepted</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-green-600"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statAccepted">0</p>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">Finished</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-green-800"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statFinished">0</p>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">Rejected</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-red-600"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statRejected">0</p>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow-md p-4">
                    <p class="text-sm text-gray-600 mb-1">Missing</p>
                    <div class="flex items-center gap-2">
                        <div class="w-3 h-3 rounded-full bg-orange-500"></div>
                        <p class="text-2xl font-bold text-gray-900" id="statMissing">0</p>
                    </div>
                </div>
            </div>

            <!-- Controls -->
            <div class="bg-white rounded-lg shadow-md p-4 mb-6">
                <div class="flex flex-col md:flex-row gap-4">
                    <div class="flex-1">
                        <div class="relative">
                            <svg class="absolute left-3 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                            </svg>
                            <input type="text" id="searchInput" placeholder="Search files, type, or user..." class="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        </div>
                    </div>

                    <select id="statusFilter" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="all">All Status</option>
                        <option value="in_process">In Process</option>
                        <option value="accepted">Accepted</option>
                        <option value="finished">Finished</option>
                        <option value="rejected">Rejected</option>
                        <option value="missing">Missing Info</option>
                    </select>

                    <select id="typeFilter" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="all">All Types</option>
                        <option value="Billing">Billing</option>
                        <option value="Paper">Paper</option>
                        <option value="Approval">Approval</option>
                        <option value="Leave Request">Leave Request</option>
                        <option value="Purchase Order">Purchase Order</option>
                        <option value="Other">Other</option>
                    </select>

                    <button onclick="showUploadModal()" class="flex items-center gap-2 px-6 py-2 bg-gradient-to-r from-green-600 to-yellow-500 text-white rounded-lg hover:from-green-700 hover:to-yellow-600 transition shadow-md">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                        </svg>
                        Upload File
                    </button>
                </div>
            </div>

            <!-- Files Table -->
            <div class="bg-white rounded-lg shadow-md overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full">
                        <thead class="bg-gradient-to-r from-green-600 to-yellow-500 text-white">
                            <tr>
                                <th class="px-4 py-3 text-left text-sm font-semibold">File Name</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Type</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Uploaded By</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Date</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Status</th>
                                <th id="actionsHeader" class="px-4 py-3 text-left text-sm font-semibold hidden">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="filesTableBody" class="divide-y divide-gray-200">
                            <tr>
                                <td colspan="5" class="px-4 py-8 text-center text-gray-500">No files found</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Upload Modal -->
    <div id="uploadModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md">
            <h3 class="text-xl font-bold text-gray-900 mb-4">Upload New File</h3>

            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Name *</label>
                    <input type="text" id="uploadFileName" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500" required>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Type *</label>
                    <select id="uploadFileType" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="Billing">Billing</option>
                        <option value="Paper">Paper</option>
                        <option value="Approval">Approval</option>
                        <option value="Leave Request">Leave Request</option>
                        <option value="Purchase Order">Purchase Order</option>
                        <option value="Other">Other</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                    <textarea id="uploadDescription" rows="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500"></textarea>
                </div>

                <div class="flex gap-3 pt-2">
                    <button onclick="hideUploadModal()" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition">
                        Cancel
                    </button>
                    <button onclick="handleUpload()" class="flex-1 px-4 py-2 bg-gradient-to-r from-green-600 to-yellow-500 text-white rounded-lg hover:from-green-700 hover:to-yellow-600 transition shadow-md">
                        Upload
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global state
        let currentUser = null;
        let files = [];

        // Status configuration
        const statusConfig = {
            in_process: { label: 'In Process', color: 'bg-yellow-500', icon: '🕐' },
            accepted: { label: 'Accepted', color: 'bg-green-600', icon: '✓' },
            finished: { label: 'Finished', color: 'bg-green-800', icon: '✓' },
            rejected: { label: 'Rejected', color: 'bg-red-600', icon: '✗' },
            missing: { label: 'Missing Info', color: 'bg-orange-500', icon: '⚠' }
        };

        // Initialize
        loadFiles();

        // Load files from localStorage
        function loadFiles() {
            const stored = localStorage.getItem('ds_office_files');
            files = stored ? JSON.parse(stored) : [];
        }

        // Save files to localStorage
        function saveFiles() {
            localStorage.setItem('ds_office_files', JSON.stringify(files));
            renderFiles();
            updateStats();
        }

        // Login handler
        function handleLogin() {
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            const isAdmin = document.getElementById('loginIsAdmin').checked;

            if (username && password.length >= 4) {
                currentUser = { username, isAdmin };
                document.getElementById('loginModal').classList.add('hidden');
                document.getElementById('mainApp').classList.remove('hidden');
                document.getElementById('currentUsername').textContent = username;
                document.getElementById('currentUserRole').textContent = isAdmin ? 'Administrator' : 'User';
                
                if (isAdmin) {
                    document.getElementById('actionsHeader').classList.remove('hidden');
                }
                
                renderFiles();
                updateStats();
            } else {
                alert('Please enter a valid username and password (min 4 characters)');
            }
        }

        // Logout handler
        function handleLogout() {
            currentUser = null;
            document.getElementById('loginModal').classList.remove('hidden');
            document.getElementById('mainApp').classList.add('hidden');
            document.getElementById('loginUsername').value = '';
            document.getElementById('loginPassword').value = '';
            document.getElementById('loginIsAdmin').checked = false;
        }

        // Show upload modal
        function showUploadModal() {
            document.getElementById('uploadModal').classList.remove('hidden');
            document.getElementById('uploadFileName').value = '';
            document.getElementById('uploadDescription').value = '';
        }

        // Hide upload modal
        function hideUploadModal() {
            document.getElementById('uploadModal').classList.add('hidden');
        }

        // Handle file upload
        function handleUpload() {
            const fileName = document.getElementById('uploadFileName').value;
            const fileType = document.getElementById('uploadFileType').value;
            const description = document.getElementById('uploadDescription').value;

            if (!fileName) {
                alert('Please enter a file name');
                return;
            }

            const newFile = {
                id: Date.now(),
                fileName: fileName,
                fileType: fileType,
                description: description,
                uploadedBy: currentUser.username,
                uploadedAt: new Date().toISOString(),
                status: 'in_process',
                statusHistory: [{
                    status: 'in_process',
                    timestamp: new Date().toISOString(),
                    updatedBy: 'System'
                }]
            };

            files.push(newFile);
            saveFiles();
            hideUploadModal();
        }

        // Update file status
        function updateFileStatus(fileId, newStatus) {
            const fileIndex = files.findIndex(f => f.id === fileId);
            if (fileIndex !== -1) {
                files[fileIndex].status = newStatus;
                files[fileIndex].statusHistory.push({
                    status: newStatus,
                    timestamp: new Date().toISOString(),
                    updatedBy: currentUser.username
                });
                saveFiles();
            }
        }

        // Format date
        function formatDate(dateString) {
            return new Date(dateString).toLocaleString('en-US', {
                year: 'numeric',
                month: 'short',
                day: 'numeric',
                hour: '2-digit',
                minute: '2-digit'
            });
        }

        // Render files table
        function renderFiles() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const statusFilter = document.getElementById('statusFilter').value;
            const typeFilter = document.getElementById('typeFilter').value;
            
            let filtered = files;

            // Filter by user (non-admins only see their files)
            if (currentUser && !currentUser.isAdmin) {
                filtered = filtered.filter(f => f.uploadedBy === currentUser.username);
            }

            // Filter by search term
            if (searchTerm) {
                filtered = filtered.filter(f => 
                    f.fileName.toLowerCase().includes(searchTerm) ||
                    f.fileType.toLowerCase().includes(searchTerm) ||
                    f.uploadedBy.toLowerCase().includes(searchTerm)
                );
            }

            // Filter by status
            if (statusFilter !== 'all') {
                filtered = filtered.filter(f => f.status === statusFilter);
            }

            // Filter by type
            if (typeFilter !== 'all') {
                filtered = filtered.filter(f => f.fileType === typeFilter);
            }

            const tbody = document.getElementById('filesTableBody');
            
            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="${currentUser?.isAdmin ? 6 : 5}" class="px-4 py-8 text-center text-gray-500">No files found</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map(file => {
                const status = statusConfig[file.status];
                const statusSelect = currentUser?.isAdmin ? `
                    <td class="px-4 py-3">
                        <select onchange="updateFileStatus(${file.id}, this.value)" class="text-sm border border-gray-300 rounded px-2 py-1 focus:outline-none focus:ring-2 focus:ring-green-500">
                            ${Object.entries(statusConfig).map(([key, val]) => 
                                `<option value="${key}" ${file.status === key ? 'selected' : ''}>${val.label}</option>`
                            ).join('')}
                        </select>
                    </td>
                ` : '';

                return `
                    <tr class="hover:bg-gray-50">
                        <td class="px-4 py-3">
                            <div>
                                <p class="font-medium text-gray-900">${file.fileName}</p>
                                <p class="text-sm text-gray-500">${file.description || ''}</p>
                            </div>
                        </td>
                        <td class="px-4 py-3">
                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
                                ${file.fileType}
                            </span>
                        </td>
                        <td class="px-4 py-3 text-sm text-gray-600">${file.uploadedBy}</td>
                        <td class="px-4 py-3 text-sm text-gray-600">${formatDate(file.uploadedAt)}</td>
                        <td class="px-4 py-3">
                            <span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-medium text-white ${status.color}">
                                ${status.icon} ${status.label}
                            </span>
                        </td>
                        ${statusSelect}
                    </tr>
                `;
            }).join('');
        }

        // Update statistics
        function updateStats() {
            const userFiles = currentUser?.isAdmin ? files : files.filter(f => f.uploadedBy === currentUser?.username);
            
            document.getElementById('statTotal').textContent = userFiles.length;
            document.getElementById('statInProcess').textContent = userFiles.filter(f => f.status === 'in_process').length;
            document.getElementById('statAccepted').textContent = userFiles.filter(f => f.status === 'accepted').length;
            document.getElementById('statFinished').textContent = userFiles.filter(f => f.status === 'finished').length;
            document.getElementById('statRejected').textContent = userFiles.filter(f => f.status === 'rejected').length;
            document.getElementById('statMissing').textContent = userFiles.filter(f => f.status === 'missing').length;
        }

        // Event listeners
        document.getElementById('searchInput').addEventListener('input', renderFiles);
        document.getElementById('statusFilter').addEventListener('change', renderFiles);
        document.getElementById('typeFilter').addEventListener('change', renderFiles);
    </script>
</body>
</html>
