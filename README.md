<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DS e-Office Management System</title>
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
                <h2 class="text-2xl font-bold text-gray-900">DS e-Office Management</h2>
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

                <div id="adminDepartmentSection" class="hidden">
                    <label class="block text-sm font-medium text-gray-700 mb-2">Select Department *</label>
                    <div class="space-y-2">
                        <label class="flex items-center p-3 border border-gray-300 rounded-lg hover:bg-gray-50 cursor-pointer">
                            <input type="radio" name="adminDepartment" value="Academic Affairs Department" class="w-4 h-4 text-green-600 focus:ring-green-500">
                            <span class="ml-3 text-sm text-gray-900">Academic Affairs Department</span>
                        </label>
                        <label class="flex items-center p-3 border border-gray-300 rounded-lg hover:bg-gray-50 cursor-pointer">
                            <input type="radio" name="adminDepartment" value="HR and Student Affairs Department" class="w-4 h-4 text-green-600 focus:ring-green-500">
                            <span class="ml-3 text-sm text-gray-900">HR and Student Affairs Department</span>
                        </label>
                        <label class="flex items-center p-3 border border-gray-300 rounded-lg hover:bg-gray-50 cursor-pointer">
                            <input type="radio" name="adminDepartment" value="General Administration Department" class="w-4 h-4 text-green-600 focus:ring-green-500">
                            <span class="ml-3 text-sm text-gray-900">General Administration Department</span>
                        </label>
                        <label class="flex items-center p-3 border border-gray-300 rounded-lg hover:bg-gray-50 cursor-pointer">
                            <input type="radio" name="adminDepartment" value="Budgeting and Finance Department" class="w-4 h-4 text-green-600 focus:ring-green-500">
                            <span class="ml-3 text-sm text-gray-900">Budgeting and Finance Department</span>
                        </label>
                    </div>
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
                            <h1 class="text-2xl font-bold">DS e-Office Management</h1>
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

                    <select id="departmentFilter" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="all">All Departments</option>
                        <option value="Academic Affairs Department">Academic Affairs</option>
                        <option value="HR and Student Affairs Department">HR & Student Affairs</option>
                        <option value="General Administration Department">General Administration</option>
                        <option value="Budgeting and Finance Department">Budgeting & Finance</option>
                    </select>

                    <select id="typeFilter" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="all">All Types</option>
                    </select>

                    <button onclick="showUploadModal()" class="flex items-center gap-2 px-6 py-2 bg-gradient-to-r from-green-600 to-yellow-500 text-white rounded-lg hover:from-green-700 hover:to-yellow-600 transition shadow-md">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                        </svg>
                        Upload File
                    </button>

                    <button onclick="refreshData()" class="flex items-center gap-2 px-4 py-2 bg-white border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition shadow-sm">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
                        </svg>
                        Refresh
                    </button>
                </div>
            </div>

            <!-- Files Table -->
            <div class="bg-white rounded-lg shadow-md overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full">
                        <thead class="bg-gradient-to-r from-green-600 to-yellow-500 text-black">
                            <tr>
                                <th class="px-4 py-3 text-left text-sm font-semibold">File Name</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Department</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Type</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Uploaded By</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Upload Date</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Status</th>
                                <th class="px-4 py-3 text-left text-sm font-semibold">Last Updated</th>
                                <th id="actionsHeader" class="px-4 py-3 text-left text-sm font-semibold hidden">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="filesTableBody" class="divide-y divide-gray-200">
                            <tr>
                                <td colspan="8" class="px-4 py-8 text-center text-gray-500">No files found</td>
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
                    <label class="block text-sm font-medium text-gray-700 mb-1">Department *</label>
                    <select id="uploadDepartment" onchange="updateFileTypeOptions()" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="">-- Select Department --</option>
                        <option value="Academic Affairs Department">Academic Affairs Department</option>
                        <option value="HR and Student Affairs Department">HR and Student Affairs Department</option>
                        <option value="General Administration Department">General Administration Department</option>
                        <option value="Budgeting and Finance Department">Budgeting and Finance Department</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Type *</label>
                    <select id="uploadFileType" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500">
                        <option value="">-- Select Type --</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Name *</label>
                    <input type="text" id="uploadFileName" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500" required>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                    <textarea id="uploadDescription" rows="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500"></textarea>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Attach File (Optional)</label>
                    <div class="border-2 border-dashed border-gray-300 rounded-lg p-4 text-center hover:border-green-500 transition">
                        <input type="file" id="uploadFileInput" class="hidden" onchange="handleFileSelect(this)">
                        <button type="button" onclick="document.getElementById('uploadFileInput').click()" class="text-green-600 hover:text-green-700 font-medium">
                            <svg class="w-8 h-8 mx-auto mb-2 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                            </svg>
                            Click to upload or drag and drop
                        </button>
                        <p class="text-xs text-gray-500 mt-1">PDF, DOC, DOCX, XLS, XLSX, JPG, PNG (Max 5MB)</p>
                        <div id="selectedFileName" class="mt-2 text-sm text-green-600 font-medium"></div>
                    </div>
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

    <!-- Status Note Modal -->
    <div id="statusNoteModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md">
            <h3 class="text-xl font-bold text-gray-900 mb-4">Missing Information Note</h3>

            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Please specify what information is missing:</label>
                    <textarea id="statusNoteText" rows="4" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500" placeholder="e.g., Need to attach invoice copy, Missing signature, Incomplete form..."></textarea>
                </div>

                <div class="flex gap-3 pt-2">
                    <button onclick="hideStatusNoteModal()" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition">
                        Cancel
                    </button>
                    <button onclick="saveStatusWithNote()" class="flex-1 px-4 py-2 bg-gradient-to-r from-orange-600 to-red-500 text-white rounded-lg hover:from-orange-700 hover:to-red-600 transition shadow-md">
                        Save Note
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Resubmit Modal -->
    <div id="resubmitModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md max-h-[90vh] overflow-y-auto">
            <h3 class="text-xl font-bold text-gray-900 mb-4">Resubmit File</h3>

            <div class="mb-4 p-3 bg-orange-50 border border-orange-200 rounded-lg">
                <p class="text-sm font-semibold text-orange-800 mb-1">Missing Information:</p>
                <p class="text-sm text-orange-700" id="resubmitNote"></p>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Department *</label>
                    <select id="resubmitDepartment" onchange="updateResubmitFileTypeOptions()" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500">
                        <option value="">-- Select Department --</option>
                        <option value="Academic Affairs Department">Academic Affairs Department</option>
                        <option value="HR and Student Affairs Department">HR and Student Affairs Department</option>
                        <option value="General Administration Department">General Administration Department</option>
                        <option value="Budgeting and Finance Department">Budgeting and Finance Department</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Type *</label>
                    <select id="resubmitFileType" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500">
                        <option value="">-- Select Type --</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">File Name *</label>
                    <input type="text" id="resubmitFileName" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500" required>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                    <textarea id="resubmitDescription" rows="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500"></textarea>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Update Attached File (Optional)</label>
                    <div class="border-2 border-dashed border-gray-300 rounded-lg p-4 text-center hover:border-orange-500 transition">
                        <input type="file" id="resubmitFileInput" class="hidden" onchange="handleResubmitFileSelect(this)">
                        <button type="button" onclick="document.getElementById('resubmitFileInput').click()" class="text-orange-600 hover:text-orange-700 font-medium">
                            <svg class="w-8 h-8 mx-auto mb-2 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                            </svg>
                            Click to upload new file
                        </button>
                        <p class="text-xs text-gray-500 mt-1">PDF, DOC, DOCX, XLS, XLSX, JPG, PNG (Max 5MB)</p>
                        <div id="resubmitSelectedFileName" class="mt-2 text-sm text-orange-600 font-medium"></div>
                        <div id="resubmitCurrentFile" class="mt-2 text-xs text-gray-500"></div>
                    </div>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Comment (Optional)</label>
                    <textarea id="resubmitComment" rows="2" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500" placeholder="Explain what you've fixed or updated..."></textarea>
                </div>

                <div class="flex gap-3 pt-2">
                    <button onclick="hideResubmitModal()" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition">
                        Cancel
                    </button>
                    <button onclick="handleResubmit()" class="flex-1 px-4 py-2 bg-gradient-to-r from-orange-600 to-red-500 text-white rounded-lg hover:from-orange-700 hover:to-red-600 transition shadow-md">
                        Resubmit
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Success Modal -->
    <div id="successModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-sm">
            <div class="text-center">
                <div class="mx-auto flex items-center justify-center h-16 w-16 rounded-full bg-green-100 mb-4">
                    <svg class="h-10 w-10 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                </div>
                <h3 class="text-lg font-bold text-gray-900 mb-2">สำเร็จ!</h3>
                <p class="text-sm text-gray-600 mb-4" id="successMessage">อัพโหลดเอกสารเรียบร้อยแล้ว</p>
                <button onclick="hideSuccessModal()" class="px-6 py-2 bg-gradient-to-r from-green-600 to-yellow-500 text-white rounded-lg hover:from-green-700 hover:to-yellow-600 transition shadow-md">
                    ตรวจสอบ
                </button>
            </div>
        </div>
    </div>

    <!-- Delete Confirmation Modal -->
    <div id="deleteModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-md">
            <div class="text-center">
                <div class="mx-auto flex items-center justify-center h-16 w-16 rounded-full bg-red-100 mb-4">
                    <svg class="h-10 w-10 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"></path>
                    </svg>
                </div>
                <h3 class="text-lg font-bold text-gray-900 mb-2">ยืนยันการลบเอกสาร</h3>
                <p class="text-sm text-gray-600 mb-1">คุณต้องการลบเอกสารนี้หรือไม่?</p>
                <p class="text-sm font-medium text-gray-900 mb-4" id="deleteFileName"></p>
                <p class="text-xs text-red-600 mb-4">การลบจะไม่สามารถกู้คืนได้</p>
                <div class="flex gap-3">
                    <button onclick="hideDeleteModal()" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition">
                        ยกเลิก
                    </button>
                    <button onclick="deleteFile()" class="flex-1 px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition">
                        ลบเอกสาร
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global state
        let currentUser = null;
        let files = [];
        let selectedFile = null;
        let currentFileIdForNote = null;
        let currentFileIdForResubmit = null;
        let resubmitFile = null;
        let currentFileIdForDelete = null;

        // Department and file type mapping
        const departmentFileTypes = {
            'Academic Affairs Department': [
                'Swap periods',
                'Teaching materials',
                'Research submission',
                'Others'
            ],
            'HR and Student Affairs Department': [
                'Leave request',
                'Request submission',
                'Others'
            ],
            'General Administration Department': [
                'Maintenance',
                'Request submission',
                'Others'
            ],
            'Budgeting and Finance Department': [
                'Supply request',
                'Others'
            ]
        };

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

        // Toggle admin department section
        document.getElementById('loginIsAdmin').addEventListener('change', function() {
            const adminSection = document.getElementById('adminDepartmentSection');
            if (this.checked) {
                adminSection.classList.remove('hidden');
            } else {
                adminSection.classList.add('hidden');
            }
        });

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

            if (!username || password.length < 4) {
                alert('Please enter a valid username and password (min 4 characters)');
                return;
            }

            // Get admin department if admin
            let adminDepartment = null;
            if (isAdmin) {
                const selectedDept = document.querySelector('input[name="adminDepartment"]:checked');
                if (!selectedDept) {
                    alert('Please select a department');
                    return;
                }
                adminDepartment = selectedDept.value;
            }

            currentUser = { username, isAdmin, department: adminDepartment };
            document.getElementById('loginModal').classList.add('hidden');
            document.getElementById('mainApp').classList.remove('hidden');
            document.getElementById('currentUsername').textContent = username;
            document.getElementById('currentUserRole').textContent = isAdmin ? `Administrator (${adminDepartment})` : 'User';
            
            if (isAdmin) {
                document.getElementById('actionsHeader').classList.remove('hidden');
            }
            
            renderFiles();
            updateStats();
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
            document.getElementById('uploadDepartment').value = '';
            document.getElementById('uploadFileType').innerHTML = '<option value="">-- Select Type --</option>';
            document.getElementById('uploadFileName').value = '';
            document.getElementById('uploadDescription').value = '';
            document.getElementById('uploadFileInput').value = '';
            document.getElementById('selectedFileName').textContent = '';
            selectedFile = null;
        }

        // Update file type options based on department
        function updateFileTypeOptions() {
            const department = document.getElementById('uploadDepartment').value;
            const fileTypeSelect = document.getElementById('uploadFileType');
            
            fileTypeSelect.innerHTML = '<option value="">-- Select Type --</option>';
            
            if (department && departmentFileTypes[department]) {
                departmentFileTypes[department].forEach(type => {
                    const option = document.createElement('option');
                    option.value = type;
                    option.textContent = type;
                    fileTypeSelect.appendChild(option);
                });
            }
        }

        // Hide upload modal
        function hideUploadModal() {
            document.getElementById('uploadModal').classList.add('hidden');
            selectedFile = null;
        }

        // Handle file selection
        function handleFileSelect(input) {
            const file = input.files[0];
            if (!file) {
                selectedFile = null;
                document.getElementById('selectedFileName').textContent = '';
                return;
            }

            // Validate file size (5MB)
            if (file.size > 5 * 1024 * 1024) {
                alert('File size must be less than 5MB');
                input.value = '';
                return;
            }

            // Validate file type
            const allowedTypes = [
                'application/pdf',
                'application/msword',
                'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
                'application/vnd.ms-excel',
                'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
                'image/jpeg',
                'image/png'
            ];

            if (!allowedTypes.includes(file.type)) {
                alert('Only PDF, DOC, DOCX, XLS, XLSX, JPG, PNG files are allowed');
                input.value = '';
                return;
            }

            // Read file as base64
            const reader = new FileReader();
            reader.onload = function(e) {
                selectedFile = {
                    name: file.name,
                    type: file.type,
                    size: file.size,
                    data: e.target.result
                };
                document.getElementById('selectedFileName').textContent = `✓ ${file.name} (${(file.size / 1024).toFixed(1)} KB)`;
            };
            reader.readAsDataURL(file);
        }

        // Handle file upload
        function handleUpload() {
            const department = document.getElementById('uploadDepartment').value;
            const fileType = document.getElementById('uploadFileType').value;
            const fileName = document.getElementById('uploadFileName').value;
            const description = document.getElementById('uploadDescription').value;

            if (!department) {
                alert('Please select a department');
                return;
            }

            if (!fileType) {
                alert('Please select a file type');
                return;
            }

            if (!fileName) {
                alert('Please enter a file name');
                return;
            }

            const newFile = {
                id: Date.now(),
                department: department,
                fileType: fileType,
                fileName: fileName,
                description: description,
                uploadedBy: currentUser.username,
                uploadedAt: new Date().toISOString(),
                status: 'in_process',
                attachedFile: selectedFile,
                statusHistory: [{
                    status: 'in_process',
                    timestamp: new Date().toISOString(),
                    updatedBy: 'System'
                }]
            };

            files.push(newFile);
            saveFiles();
            hideUploadModal();
            showSuccessModal('อัพโหลดเอกสารเรียบร้อยแล้ว');
        }

        // Show success modal
        function showSuccessModal(message) {
            document.getElementById('successMessage').textContent = message;
            document.getElementById('successModal').classList.remove('hidden');
        }

        // Hide success modal
        function hideSuccessModal() {
            document.getElementById('successModal').classList.add('hidden');
        }

        // Refresh data
        function refreshData() {
            loadFiles();
            renderFiles();
            updateStats();
            showSuccessModal('รีเฟรชข้อมูลเรียบร้อยแล้ว');
        }

        // Confirm delete file
        function confirmDeleteFile(fileId) {
            const file = files.find(f => f.id === fileId);
            if (!file) return;

            currentFileIdForDelete = fileId;
            document.getElementById('deleteFileName').textContent = file.fileName;
            document.getElementById('deleteModal').classList.remove('hidden');
        }

        // Hide delete modal
        function hideDeleteModal() {
            document.getElementById('deleteModal').classList.add('hidden');
            currentFileIdForDelete = null;
        }

        // Delete file
        function deleteFile() {
            if (currentFileIdForDelete) {
                const fileIndex = files.findIndex(f => f.id === currentFileIdForDelete);
                if (fileIndex !== -1) {
                    files.splice(fileIndex, 1);
                    saveFiles();
                    hideDeleteModal();
                    showSuccessModal('ลบเอกสารเรียบร้อยแล้ว');
                }
            }
        }

        // Download attached file
        function downloadFile(fileId) {
            const file = files.find(f => f.id === fileId);
            if (file && file.attachedFile) {
                const link = document.createElement('a');
                link.href = file.attachedFile.data;
                link.download = file.attachedFile.name;
                link.click();
            }
        }

        // Show resubmit modal
        function showResubmitModal(fileId) {
            const file = files.find(f => f.id === fileId);
            if (!file) return;

            currentFileIdForResubmit = fileId;
            resubmitFile = null;

            // Pre-fill with existing data
            document.getElementById('resubmitDepartment').value = file.department;
            updateResubmitFileTypeOptions();
            document.getElementById('resubmitFileType').value = file.fileType;
            document.getElementById('resubmitFileName').value = file.fileName;
            document.getElementById('resubmitDescription').value = file.description || '';
            document.getElementById('resubmitNote').textContent = file.statusNote || 'No note provided';
            document.getElementById('resubmitComment').value = '';
            document.getElementById('resubmitFileInput').value = '';
            document.getElementById('resubmitSelectedFileName').textContent = '';
            
            // Show current file if exists
            if (file.attachedFile) {
                document.getElementById('resubmitCurrentFile').textContent = `Current file: ${file.attachedFile.name}`;
            } else {
                document.getElementById('resubmitCurrentFile').textContent = '';
            }

            document.getElementById('resubmitModal').classList.remove('hidden');
        }

        // Update resubmit file type options
        function updateResubmitFileTypeOptions() {
            const department = document.getElementById('resubmitDepartment').value;
            const fileTypeSelect = document.getElementById('resubmitFileType');
            
            fileTypeSelect.innerHTML = '<option value="">-- Select Type --</option>';
            
            if (department && departmentFileTypes[department]) {
                departmentFileTypes[department].forEach(type => {
                    const option = document.createElement('option');
                    option.value = type;
                    option.textContent = type;
                    fileTypeSelect.appendChild(option);
                });
            }
        }

        // Hide resubmit modal
        function hideResubmitModal() {
            document.getElementById('resubmitModal').classList.add('hidden');
            currentFileIdForResubmit = null;
            resubmitFile = null;
        }

        // Handle resubmit file selection
        function handleResubmitFileSelect(input) {
            const file = input.files[0];
            if (!file) {
                resubmitFile = null;
                document.getElementById('resubmitSelectedFileName').textContent = '';
                return;
            }

            // Validate file size (5MB)
            if (file.size > 5 * 1024 * 1024) {
                alert('File size must be less than 5MB');
                input.value = '';
                return;
            }

            // Validate file type
            const allowedTypes = [
                'application/pdf',
                'application/msword',
                'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
                'application/vnd.ms-excel',
                'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
                'image/jpeg',
                'image/png'
            ];

            if (!allowedTypes.includes(file.type)) {
                alert('Only PDF, DOC, DOCX, XLS, XLSX, JPG, PNG files are allowed');
                input.value = '';
                return;
            }

            // Read file as base64
            const reader = new FileReader();
            reader.onload = function(e) {
                resubmitFile = {
                    name: file.name,
                    type: file.type,
                    size: file.size,
                    data: e.target.result
                };
                document.getElementById('resubmitSelectedFileName').textContent = `✓ New file: ${file.name} (${(file.size / 1024).toFixed(1)} KB)`;
            };
            reader.readAsDataURL(file);
        }

        // Handle resubmit
        function handleResubmit() {
            const department = document.getElementById('resubmitDepartment').value;
            const fileType = document.getElementById('resubmitFileType').value;
            const fileName = document.getElementById('resubmitFileName').value;
            const description = document.getElementById('resubmitDescription').value;
            const comment = document.getElementById('resubmitComment').value;

            if (!department) {
                alert('Please select a department');
                return;
            }

            if (!fileType) {
                alert('Please select a file type');
                return;
            }

            if (!fileName) {
                alert('Please enter a file name');
                return;
            }

            const fileIndex = files.findIndex(f => f.id === currentFileIdForResubmit);
            if (fileIndex !== -1) {
                // Update file information
                files[fileIndex].department = department;
                files[fileIndex].fileType = fileType;
                files[fileIndex].fileName = fileName;
                files[fileIndex].description = description;
                
                // Update attached file if new one is provided
                if (resubmitFile) {
                    files[fileIndex].attachedFile = resubmitFile;
                }
                
                // Update status to in_process
                files[fileIndex].status = 'in_process';
                files[fileIndex].statusNote = null; // Clear the missing info note
                
                // Add to history
                files[fileIndex].statusHistory.push({
                    status: 'in_process',
                    timestamp: new Date().toISOString(),
                    updatedBy: currentUser.username,
                    action: 'resubmit',
                    comment: comment || 'File resubmitted after missing info'
                });

                saveFiles();
                hideResubmitModal();
                showSuccessModal('ส่งเอกสารใหม่เรียบร้อยแล้ว');
            }
        }

        // Handle status change
        function handleStatusChange(fileId, newStatus) {
            if (newStatus === 'missing') {
                // Show note modal for missing info
                currentFileIdForNote = fileId;
                document.getElementById('statusNoteModal').classList.remove('hidden');
                document.getElementById('statusNoteText').value = '';
            } else {
                // Update status directly
                updateFileStatus(fileId, newStatus, null);
            }
        }

        // Hide status note modal
        function hideStatusNoteModal() {
            document.getElementById('statusNoteModal').classList.add('hidden');
            currentFileIdForNote = null;
            renderFiles(); // Reset select if cancelled
        }

        // Save status with note
        function saveStatusWithNote() {
            const note = document.getElementById('statusNoteText').value.trim();
            if (!note) {
                alert('Please enter a note explaining what information is missing');
                return;
            }
            updateFileStatus(currentFileIdForNote, 'missing', note);
            hideStatusNoteModal();
        }

        // Update file status
        function updateFileStatus(fileId, newStatus, note) {
            const fileIndex = files.findIndex(f => f.id === fileId);
            if (fileIndex !== -1) {
                files[fileIndex].status = newStatus;
                if (note !== null) {
                    files[fileIndex].statusNote = note;
                }
                files[fileIndex].statusHistory.push({
                    status: newStatus,
                    timestamp: new Date().toISOString(),
                    updatedBy: currentUser.username,
                    note: note || undefined
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
            const departmentFilter = document.getElementById('departmentFilter').value;
            const typeFilter = document.getElementById('typeFilter').value;
            
            let filtered = files;

            // Filter by user (non-admins only see their files)
            if (currentUser && !currentUser.isAdmin) {
                filtered = filtered.filter(f => f.uploadedBy === currentUser.username);
            }

            // Filter by admin department (admins only see files from their department)
            if (currentUser && currentUser.isAdmin && currentUser.department) {
                filtered = filtered.filter(f => f.department === currentUser.department);
            }

            // Filter by search term
            if (searchTerm) {
                filtered = filtered.filter(f => 
                    f.fileName.toLowerCase().includes(searchTerm) ||
                    f.fileType.toLowerCase().includes(searchTerm) ||
                    f.department.toLowerCase().includes(searchTerm) ||
                    f.uploadedBy.toLowerCase().includes(searchTerm)
                );
            }

            // Filter by status
            if (statusFilter !== 'all') {
                filtered = filtered.filter(f => f.status === statusFilter);
            }

            // Filter by department
            if (departmentFilter !== 'all') {
                filtered = filtered.filter(f => f.department === departmentFilter);
            }

            // Filter by type
            if (typeFilter !== 'all') {
                filtered = filtered.filter(f => f.fileType === typeFilter);
            }

            // Update type filter options based on current filters
            updateTypeFilterOptions();

            const tbody = document.getElementById('filesTableBody');
            
            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="${currentUser?.isAdmin ? 8 : 7}" class="px-4 py-8 text-center text-gray-500">No files found</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map(file => {
                const status = statusConfig[file.status];
                
                // Get last status update timestamp
                const lastUpdate = file.statusHistory[file.statusHistory.length - 1];
                const lastUpdateTime = formatDate(lastUpdate.timestamp);
                const lastUpdateBy = lastUpdate.updatedBy;
                
                const statusSelect = currentUser?.isAdmin ? `
                    <td class="px-4 py-3">
                        <select onchange="handleStatusChange(${file.id}, this.value)" class="text-sm border border-gray-300 rounded px-2 py-1 focus:outline-none focus:ring-2 focus:ring-green-500">
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
                                <p class="text-sm text-gray-600">${file.description || ''}</p>
                                ${file.attachedFile ? `
                                    <button onclick="downloadFile(${file.id})" class="text-xs text-blue-600 hover:text-blue-800 mt-1 flex items-center gap-1">
                                        <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                                        </svg>
                                        ${file.attachedFile.name}
                                    </button>
                                ` : ''}
                                ${file.statusNote ? `
                                    <div class="mt-2 p-2 bg-orange-50 border border-orange-200 rounded text-xs">
                                        <p class="font-semibold text-orange-800">Note:</p>
                                        <p class="text-orange-700">${file.statusNote}</p>
                                    </div>
                                ` : ''}
                            </div>
                        </td>
                        <td class="px-4 py-3">
                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-purple-100 text-purple-800">
                                ${file.department.replace(' Department', '')}
                            </span>
                        </td>
                        <td class="px-4 py-3">
                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
                                ${file.fileType}
                            </span>
                        </td>
                        <td class="px-4 py-3 text-sm text-gray-900">${file.uploadedBy}</td>
                        <td class="px-4 py-3 text-sm text-gray-900">${formatDate(file.uploadedAt)}</td>
                        <td class="px-4 py-3">
                            <span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-medium text-white ${status.color}">
                                ${status.icon} ${status.label}
                            </span>
                            ${file.status === 'missing' && file.uploadedBy === currentUser.username ? `
                                <button onclick="showResubmitModal(${file.id})" class="mt-2 w-full text-xs px-3 py-1.5 bg-orange-600 hover:bg-orange-700 text-white rounded-lg transition flex items-center justify-center gap-1">
                                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
                                    </svg>
                                    Resubmit
                                </button>
                            ` : ''}
                            ${file.uploadedBy === currentUser.username && (file.status === 'in_process' || file.status === 'missing') ? `
                                <button onclick="confirmDeleteFile(${file.id})" class="mt-2 w-full text-xs px-3 py-1.5 bg-red-600 hover:bg-red-700 text-white rounded-lg transition flex items-center justify-center gap-1">
                                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                    </svg>
                                    Delete
                                </button>
                            ` : ''}
                        </td>
                        <td class="px-4 py-3">
                            <div class="text-sm">
                                <p class="text-gray-900">${lastUpdateTime}</p>
                                <p class="text-xs text-gray-600">by ${lastUpdateBy}</p>
                            </div>
                        </td>
                        ${statusSelect}
                    </tr>
                `;
            }).join('');
        }

        // Update type filter options based on selected department
        function updateTypeFilterOptions() {
            const departmentFilter = document.getElementById('departmentFilter').value;
            const typeFilterSelect = document.getElementById('typeFilter');
            const currentValue = typeFilterSelect.value;
            
            typeFilterSelect.innerHTML = '<option value="all">All Types</option>';
            
            if (departmentFilter !== 'all' && departmentFileTypes[departmentFilter]) {
                departmentFileTypes[departmentFilter].forEach(type => {
                    const option = document.createElement('option');
                    option.value = type;
                    option.textContent = type;
                    typeFilterSelect.appendChild(option);
                });
                typeFilterSelect.value = currentValue;
            } else if (departmentFilter === 'all') {
                // Show all types from all departments
                const allTypes = new Set();
                Object.values(departmentFileTypes).forEach(types => {
                    types.forEach(type => allTypes.add(type));
                });
                allTypes.forEach(type => {
                    const option = document.createElement('option');
                    option.value = type;
                    option.textContent = type;
                    typeFilterSelect.appendChild(option);
                });
                typeFilterSelect.value = currentValue;
            }
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
        document.getElementById('departmentFilter').addEventListener('change', renderFiles);
        document.getElementById('typeFilter').addEventListener('change', renderFiles);
    </script>
</body>
</html>
