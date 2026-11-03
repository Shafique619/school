<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-900 text-slate-100">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ClassEdge LMS - Smart Campus Portal</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome Icons CDN -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Plus Jakarta Sans', 'sans-serif'],
          },
          colors: {
            brand: {
              50: '#f0f6ff',
              100: '#e0edff',
              500: '#3b82f6',
              600: '#2563eb',
              700: '#1d4ed8',
              900: '#1e3a8a',
            }
          }
        }
      }
    }
  </script>
  <style>
    .glass-panel {
      background: rgba(30, 41, 59, 0.75);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }
    .glass-card {
      background: rgba(15, 23, 42, 0.65);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(255, 255, 255, 0.05);
    }
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: rgba(15, 23, 42, 0.5);
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: rgba(100, 116, 139, 0.5);
      border-radius: 9999px;
    }
  </style>
</head>
<body class="h-full flex flex-col font-sans antialiased bg-slate-950 text-slate-100 custom-scrollbar selection:bg-blue-500 selection:text-white">

  <!-- TOP HEADER / NAV BAR -->
  <header id="appHeader" class="hidden sticky top-0 z-40 glass-panel border-b border-slate-800 px-4 lg:px-8 py-3">
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <!-- College Logo & Brand -->
      <div class="flex items-center gap-3">
        <div class="relative group">
          <!-- College Logo Placeholder for VS Code (Drop college-logo.png in same folder) -->
          <img id="collegeLogo" src="college-logo.png" onerror="this.onerror=null; this.parentElement.innerHTML='<div class=\'w-10 h-10 rounded-xl bg-gradient-to-tr from-blue-600 to-indigo-500 flex items-center justify-center font-bold text-white shadow-lg shadow-blue-500/30 text-lg\'><i class=\'fa-solid font-bold fa-graduation-cap\'></i></div>'" class="w-10 h-10 rounded-xl object-contain bg-slate-800 p-1 border border-slate-700" alt="College Logo">
        </div>
        <div>
          <h1 class="font-extrabold text-lg lg:text-xl tracking-tight text-white flex items-center gap-2">
            ClassEdge <span class="bg-gradient-to-r from-blue-400 to-indigo-400 bg-clip-text text-transparent">LMS</span>
          </h1>
          <p id="collegeSubtitle" class="text-xs text-slate-400 font-medium">National Institute of Technology</p>
        </div>
      </div>

      <!-- Navigation Tabs & User Profile -->
      <div class="flex items-center gap-4">
        <div id="roleBadge" class="px-3 py-1 rounded-full text-xs font-semibold flex items-center gap-1.5 bg-blue-500/10 text-blue-400 border border-blue-500/20">
          <span class="w-2 h-2 rounded-full bg-blue-400 animate-pulse"></span>
          <span id="roleBadgeText">Teacher (Admin)</span>
        </div>

        <div class="h-6 w-[1px] bg-slate-800 hidden sm:block"></div>

        <!-- User Menu -->
        <div class="flex items-center gap-3">
          <div class="text-right hidden sm:block">
            <p id="currentUserName" class="text-sm font-semibold text-slate-200">Prof. Shafique</p>
            <p id="currentUserRole" class="text-[11px] text-slate-400 uppercase tracking-wider">Administrator</p>
          </div>
          <button onclick="logoutUser()" title="Sign Out" class="p-2 rounded-lg bg-slate-800/80 hover:bg-red-500/20 hover:text-red-400 text-slate-400 border border-slate-700 transition">
            <i class="fa-solid fa-right-from-bracket"></i>
          </button>
        </div>
      </div>
    </div>
  </header>

  <!-- AUTHENTICATION CONTAINER (LOGIN / SIGNUP) -->
  <div id="authContainer" class="min-h-screen w-full flex items-center justify-center p-4 bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-slate-900 via-slate-950 to-black">
    <div class="w-full max-w-md glass-panel p-8 rounded-3xl shadow-2xl border border-slate-800 relative overflow-hidden">
      <!-- Ambient Glow -->
      <div class="absolute -top-24 -right-24 w-48 h-48 bg-blue-600/20 rounded-full blur-3xl"></div>
      <div class="absolute -bottom-24 -left-24 w-48 h-48 bg-indigo-600/20 rounded-full blur-3xl"></div>

      <!-- Header -->
      <div class="text-center mb-6 relative z-10">
        <div class="w-16 h-16 rounded-2xl bg-gradient-to-tr from-blue-600 to-indigo-600 mx-auto flex items-center justify-center text-white text-2xl font-bold shadow-xl shadow-blue-500/20 mb-4 border border-blue-400/30">
          <i class="fa-solid fa-school"></i>
        </div>
        <h2 class="text-2xl font-bold text-white tracking-tight">ClassEdge Portal</h2>
        <p class="text-xs text-slate-400 mt-1">Smart Campus & LMS Login</p>
      </div>

      <!-- Auth Tabs -->
      <div class="flex p-1 bg-slate-900/80 rounded-xl mb-6 border border-slate-800 relative z-10">
        <button id="tabBtnLogin" onclick="switchAuthTab('login')" class="flex-1 py-2 rounded-lg text-sm font-semibold text-white bg-blue-600 transition shadow">Sign In</button>
        <button id="tabBtnRegister" onclick="switchAuthTab('register')" class="flex-1 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-white transition">Sign Up</button>
      </div>

      <!-- LOGIN FORM -->
      <form id="loginForm" onsubmit="handleLogin(event)" class="space-y-4 relative z-10">
        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Email Address</label>
          <div class="relative">
            <i class="fa-solid fa-envelope absolute left-3.5 top-3.5 text-slate-500 text-sm"></i>
            <input type="email" id="loginEmail" required value="teacher@college.edu" placeholder="name@domain.com" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
          </div>
        </div>

        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Password</label>
          <div class="relative">
            <i class="fa-solid fa-lock absolute left-3.5 top-3.5 text-slate-500 text-sm"></i>
            <input type="password" id="loginPassword" required value="password123" placeholder="••••••••" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
          </div>
        </div>

        <div class="bg-blue-500/10 border border-blue-500/20 rounded-xl p-3 text-xs text-blue-300 space-y-1">
          <p class="font-bold"><i class="fa-solid fa-circle-info mr-1"></i> Quick Demo Accounts:</p>
          <p>• <b>Teacher:</b> teacher@college.edu (Pass: password123)</p>
          <p>• <b>Student:</b> student@college.edu (Pass: password123)</p>
        </div>

        <button type="submit" class="w-full py-3 bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-500 hover:to-indigo-500 text-white font-semibold rounded-xl shadow-lg shadow-blue-600/30 transition flex items-center justify-center gap-2">
          <span>Sign In to Dashboard</span>
          <i class="fa-solid fa-arrow-right-long"></i>
        </button>
      </form>

      <!-- REGISTER FORM -->
      <form id="registerForm" onsubmit="handleRegister(event)" class="space-y-4 relative z-10 hidden">
        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Full Name</label>
          <div class="relative">
            <i class="fa-solid fa-user absolute left-3.5 top-3.5 text-slate-500 text-sm"></i>
            <input type="text" id="regName" required placeholder="John Doe" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
          </div>
        </div>

        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Email Address</label>
          <div class="relative">
            <i class="fa-solid fa-envelope absolute left-3.5 top-3.5 text-slate-500 text-sm"></i>
            <input type="email" id="regEmail" required placeholder="name@domain.com" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
          </div>
        </div>

        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Password</label>
          <div class="relative">
            <i class="fa-solid fa-lock absolute left-3.5 top-3.5 text-slate-500 text-sm"></i>
            <input type="password" id="regPassword" required placeholder="••••••••" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
          </div>
        </div>

        <div>
          <label class="block text-xs font-medium text-slate-400 mb-1.5">Select Role</label>
          <select id="regRole" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
            <option value="student">Student</option>
            <option value="teacher">Teacher (Admin)</option>
          </select>
        </div>

        <button type="submit" class="w-full py-3 bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-semibold rounded-xl shadow-lg shadow-emerald-600/30 transition flex items-center justify-center gap-2">
          <span>Create Account</span>
          <i class="fa-solid fa-user-plus"></i>
        </button>
      </form>
    </div>
  </div>

  <!-- MAIN APP CONTAINER -->
  <div id="mainAppContainer" class="hidden flex-1 flex flex-col lg:flex-row max-w-7xl mx-auto w-full p-4 lg:p-6 gap-6">
    
    <!-- SIDEBAR NAVIGATION -->
    <aside class="w-full lg:w-64 flex flex-col gap-4">
      <div class="glass-panel p-4 rounded-2xl flex flex-col gap-1.5">
        <p class="px-3 py-1.5 text-[11px] font-bold uppercase tracking-wider text-slate-500">Navigation</p>
        
        <!-- Tabs injected dynamically based on role -->
        <div id="sidebarNavLinks" class="space-y-1">
          <!-- Dynamically populated -->
        </div>
      </div>

      <!-- Quick College Status Card -->
      <div class="glass-panel p-4 rounded-2xl hidden lg:block border border-slate-800">
        <div class="flex items-center gap-3 mb-3">
          <div class="w-9 h-9 rounded-xl bg-blue-500/10 text-blue-400 flex items-center justify-center font-bold">
            <i class="fa-solid fa-server"></i>
          </div>
          <div>
            <h4 class="text-xs font-bold text-white">Database & State</h4>
            <p class="text-[10px] text-emerald-400 flex items-center gap-1"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span> LocalStorage Active</p>
          </div>
        </div>
        <p class="text-xs text-slate-400 leading-relaxed">All homework submissions, quizzes, and attendance records sync instantly.</p>
      </div>
    </aside>

    <!-- MAIN CONTENT VIEWPORT -->
    <main class="flex-1 flex flex-col gap-6">
      
      <!-- ================= TEACHER ADMIN VIEWS ================= -->
      
      <!-- 1. TEACHER DASHBOARD / ANALYTICS -->
      <section id="view-teacher-dashboard" class="space-y-6">
        <div class="glass-panel p-6 rounded-3xl relative overflow-hidden">
          <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-blue-600/10 rounded-full blur-3xl"></div>
          <div class="relative z-10 flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div>
              <span class="px-3 py-1 rounded-full text-xs font-semibold bg-blue-500/10 text-blue-400 border border-blue-500/20">Admin Control Center</span>
              <h2 class="text-2xl lg:text-3xl font-extrabold text-white mt-2">Welcome back, Professor! 👨‍🏫</h2>
              <p class="text-sm text-slate-400 mt-1">Manage class attendance, publish homework, create tests, and review student grades.</p>
            </div>
            <div class="flex items-center gap-3">
              <button onclick="switchView('teacher-homework')" class="px-4 py-2.5 bg-blue-600 hover:bg-blue-500 text-white text-sm font-semibold rounded-xl shadow-lg shadow-blue-600/30 transition flex items-center gap-2">
                <i class="fa-solid fa-plus"></i> Post Homework
              </button>
              <button onclick="switchView('teacher-quizzes')" class="px-4 py-2.5 bg-slate-800 hover:bg-slate-700 text-slate-200 text-sm font-semibold rounded-xl border border-slate-700 transition flex items-center gap-2">
                <i class="fa-solid fa-file-pen"></i> New Quiz
              </button>
            </div>
          </div>
        </div>

        <!-- Metric Grid -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Total Students</p>
              <h3 id="statTotalStudents" class="text-2xl font-extrabold text-white mt-1">24</h3>
              <p class="text-[11px] text-emerald-400 mt-1"><i class="fa-solid fa-arrow-trend-up"></i> Active roster</p>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-blue-500/10 text-blue-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-users"></i>
            </div>
          </div>

          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Avg Attendance</p>
              <h3 id="statAvgAttendance" class="text-2xl font-extrabold text-white mt-1">92%</h3>
              <p class="text-[11px] text-emerald-400 mt-1"><i class="fa-solid fa-circle-check"></i> Excellent rate</p>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-emerald-500/10 text-emerald-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-clipboard-user"></i>
            </div>
          </div>

          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Active Homework</p>
              <h3 id="statActiveHomework" class="text-2xl font-extrabold text-white mt-1">3</h3>
              <p class="text-[11px] text-blue-400 mt-1"><i class="fa-solid fa-clock"></i> Pending submissions</p>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-indigo-500/10 text-indigo-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-book-open"></i>
            </div>
          </div>

          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Published Quizzes</p>
              <h3 id="statPublishedQuizzes" class="text-2xl font-extrabold text-white mt-1">2</h3>
              <p class="text-[11px] text-purple-400 mt-1"><i class="fa-solid fa-bolt"></i> Auto-grading active</p>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-purple-500/10 text-purple-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-award"></i>
            </div>
          </div>
        </div>

        <!-- Recent Announcements Post Box -->
        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h3 class="text-lg font-bold text-white flex items-center gap-2">
            <i class="fa-solid fa-bullhorn text-blue-400"></i> Broadcast Classroom Announcement
          </h3>
          <form onsubmit="postAnnouncement(event)" class="space-y-3">
            <input type="text" id="announcementTitle" required placeholder="Announcement Title (e.g., Mid-Term Schedule Update)" class="w-full bg-slate-900/90 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition">
            <textarea id="announcementBody" required rows="2" placeholder="Write announcement details for students..." class="w-full bg-slate-900/90 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500 transition"></textarea>
            <button type="submit" class="px-5 py-2.5 bg-blue-600 hover:bg-blue-500 text-white text-sm font-semibold rounded-xl shadow-lg transition">Post to Roster</button>
          </form>
        </div>
      </section>

      <!-- 2. TEACHER ATTENDANCE MANAGER -->
      <section id="view-teacher-attendance" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-white">Smart Attendance Roll Call</h2>
            <p class="text-xs text-slate-400 mt-0.5">Mark daily attendance for enrolled students. Updates student transcripts instantly.</p>
          </div>
          <button onclick="resetAttendance()" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-xs font-semibold rounded-xl border border-slate-700 transition">Reset Today</button>
        </div>

        <div class="glass-panel rounded-3xl overflow-hidden border border-slate-800">
          <div class="overflow-x-auto">
            <table class="w-full text-left border-collapse">
              <thead>
                <tr class="bg-slate-900/80 border-b border-slate-800 text-xs text-slate-400 uppercase tracking-wider">
                  <th class="p-4 font-semibold">Student Name</th>
                  <th class="p-4 font-semibold">Email</th>
                  <th class="p-4 font-semibold text-center">Status</th>
                  <th class="p-4 font-semibold text-right">Actions</th>
                </tr>
              </thead>
              <tbody id="attendanceTableBody" class="divide-y divide-slate-800/60 text-sm">
                <!-- Dynamically populated -->
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- 3. TEACHER HOMEWORK MANAGER & GRADING -->
      <section id="view-teacher-homework" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h2 class="text-xl font-bold text-white flex items-center gap-2">
            <i class="fa-solid fa-book-bookmark text-blue-400"></i> Create & Post Homework Assignment
          </h2>
          <form onsubmit="createHomework(event)" class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="block text-xs font-medium text-slate-400 mb-1">Assignment Title</label>
              <input type="text" id="hwTitle" required placeholder="e.g., Chapter 4 Network Security Lab" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
            </div>
            <div>
              <label class="block text-xs font-medium text-slate-400 mb-1">Due Date</label>
              <input type="date" id="hwDueDate" required class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
            </div>
            <div class="md:col-span-2">
              <label class="block text-xs font-medium text-slate-400 mb-1">Instructions / Description</label>
              <textarea id="hwDesc" required rows="3" placeholder="Describe assignment requirements and deliverable file formats..." class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500"></textarea>
            </div>
            <div class="md:col-span-2 flex justify-end">
              <button type="submit" class="px-6 py-2.5 bg-blue-600 hover:bg-blue-500 text-white font-semibold text-sm rounded-xl shadow-lg transition">Publish Assignment</button>
            </div>
          </form>
        </div>

        <!-- Student Submissions Review Desk -->
        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h3 class="text-lg font-bold text-white">Student Submissions & Grading Desk</h3>
          <div id="teacherSubmissionsList" class="space-y-3">
            <!-- Dynamically populated -->
          </div>
        </div>
      </section>

      <!-- 4. TEACHER QUIZ BUILDER -->
      <section id="view-teacher-quizzes" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h2 class="text-xl font-bold text-white flex items-center gap-2">
            <i class="fa-solid fa-award text-purple-400"></i> Create Automated MCQ Quiz
          </h2>
          <form onsubmit="createQuiz(event)" class="space-y-4">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">Quiz Title</label>
                <input type="text" id="quizTitle" required placeholder="e.g., Mid-Term Cybersecurity MCQ Test" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
              </div>
              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">Time Limit (Minutes)</label>
                <input type="number" id="quizTime" required value="15" min="1" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
              </div>
            </div>

            <div class="p-4 bg-slate-900/60 rounded-2xl border border-slate-800 space-y-3">
              <p class="text-xs font-bold text-slate-300 uppercase tracking-wider">Question Configuration</p>
              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">Question Statement</label>
                <input type="text" id="qQuestion" required placeholder="e.g., Which protocol is used for secure remote login?" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white focus:outline-none">
              </div>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                <input type="text" id="qOpt1" required placeholder="Option A: HTTP" class="bg-slate-900 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white">
                <input type="text" id="qOpt2" required placeholder="Option B: SSH" class="bg-slate-900 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white">
                <input type="text" id="qOpt3" required placeholder="Option C: FTP" class="bg-slate-900 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white">
                <input type="text" id="qOpt4" required placeholder="Option D: Telnet" class="bg-slate-900 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white">
              </div>
              <div>
                <label class="block text-xs font-medium text-slate-400 mb-1">Correct Answer Index (0 for A, 1 for B, 2 for C, 3 for D)</label>
                <select id="qCorrect" class="bg-slate-900 border border-slate-800 rounded-xl px-3 py-2 text-sm text-white w-full sm:w-48">
                  <option value="0">Option A</option>
                  <option value="1" selected>Option B</option>
                  <option value="2">Option C</option>
                  <option value="3">Option D</option>
                </select>
              </div>
            </div>

            <button type="submit" class="px-6 py-2.5 bg-purple-600 hover:bg-purple-500 text-white font-semibold text-sm rounded-xl shadow-lg transition">Publish Quiz</button>
          </form>
        </div>

        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h3 class="text-lg font-bold text-white">Published Quizzes Vault</h3>
          <div id="teacherQuizzesList" class="space-y-3">
            <!-- Dynamically populated -->
          </div>
        </div>
      </section>

      <!-- 5. MASTER GRADEBOOK -->
      <section id="view-teacher-gradebook" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-white">Master Gradebook & Transcripts</h2>
            <p class="text-xs text-slate-400 mt-0.5">Aggregated student scores, attendance rates, and automated letter grades.</p>
          </div>
        </div>

        <div class="glass-panel rounded-3xl overflow-hidden border border-slate-800">
          <div class="overflow-x-auto">
            <table class="w-full text-left border-collapse">
              <thead>
                <tr class="bg-slate-900/80 border-b border-slate-800 text-xs text-slate-400 uppercase tracking-wider">
                  <th class="p-4 font-semibold">Student Name</th>
                  <th class="p-4 font-semibold text-center">Attendance</th>
                  <th class="p-4 font-semibold text-center">Homework Avg</th>
                  <th class="p-4 font-semibold text-center">Quiz Avg</th>
                  <th class="p-4 font-semibold text-center">Final Grade</th>
                </tr>
              </thead>
              <tbody id="gradebookTableBody" class="divide-y divide-slate-800/60 text-sm">
                <!-- Dynamically populated -->
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- 6. MOCK DATABASE INSPECTOR -->
      <section id="view-teacher-database" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-white flex items-center gap-2"><i class="fa-solid fa-database text-emerald-400"></i> Local Database Inspector</h2>
            <p class="text-xs text-slate-400 mt-0.5">Real-time inspection of browser LocalStorage JSON state tables.</p>
          </div>
          <button onclick="clearLocalStorageDB()" class="px-4 py-2 bg-red-600/20 hover:bg-red-600/30 text-red-400 border border-red-500/30 text-xs font-semibold rounded-xl transition">Reset Database</button>
        </div>

        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h3 class="text-sm font-bold text-slate-300">Raw JSON State Viewer</h3>
          <pre id="dbJsonViewer" class="bg-slate-950 p-4 rounded-2xl border border-slate-800 text-xs text-emerald-400 font-mono overflow-x-auto max-h-96 custom-scrollbar"></pre>
        </div>
      </section>


      <!-- ================= STUDENT VIEWS ================= -->

      <!-- 1. STUDENT DASHBOARD -->
      <section id="view-student-dashboard" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl relative overflow-hidden">
          <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-indigo-600/10 rounded-full blur-3xl"></div>
          <div class="relative z-10 flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div>
              <span class="px-3 py-1 rounded-full text-xs font-semibold bg-indigo-500/10 text-indigo-400 border border-indigo-500/20">Student Workspace</span>
              <h2 id="studentWelcomeTitle" class="text-2xl lg:text-3xl font-extrabold text-white mt-2">Hello, Student! 🎓</h2>
              <p class="text-sm text-slate-400 mt-1">Check your pending homework, take active quizzes, and monitor your attendance.</p>
            </div>
          </div>
        </div>

        <!-- Student Quick Stats -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">My Attendance</p>
              <h3 id="studentStatAttendance" class="text-2xl font-extrabold text-white mt-1">100%</h3>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-emerald-500/10 text-emerald-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-circle-check"></i>
            </div>
          </div>

          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Pending Homework</p>
              <h3 id="studentStatPendingHw" class="text-2xl font-extrabold text-white mt-1">2</h3>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-blue-500/10 text-blue-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-book"></i>
            </div>
          </div>

          <div class="glass-panel p-5 rounded-2xl flex items-center justify-between">
            <div>
              <p class="text-xs text-slate-400 font-medium">Overall Standing</p>
              <h3 id="studentStatStanding" class="text-2xl font-extrabold text-white mt-1">A+</h3>
            </div>
            <div class="w-12 h-12 rounded-2xl bg-purple-500/10 text-purple-400 flex items-center justify-center text-xl">
              <i class="fa-solid fa-trophy"></i>
            </div>
          </div>
        </div>

        <!-- Latest Classroom Announcements -->
        <div class="glass-panel p-6 rounded-3xl space-y-4">
          <h3 class="text-lg font-bold text-white flex items-center gap-2">
            <i class="fa-solid fa-bullhorn text-blue-400"></i> Classroom Announcements & Feed
          </h3>
          <div id="studentAnnouncementsFeed" class="space-y-3">
            <!-- Dynamically populated -->
          </div>
        </div>
      </section>

      <!-- 2. STUDENT HOMEWORK SUBMISSION DESK -->
      <section id="view-student-homework" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl">
          <h2 class="text-xl font-bold text-white">Homework Assignments</h2>
          <p class="text-xs text-slate-400 mt-0.5">Submit your completed work or links before the due date.</p>
        </div>

        <div id="studentHomeworkList" class="space-y-4">
          <!-- Dynamically populated -->
        </div>
      </section>

      <!-- 3. STUDENT EXAM / QUIZ CENTER -->
      <section id="view-student-quizzes" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl">
          <h2 class="text-xl font-bold text-white">Active Tests & Quizzes</h2>
          <p class="text-xs text-slate-400 mt-0.5">Take timed multiple-choice quizzes and get instant auto-graded results.</p>
        </div>

        <div id="studentQuizzesList" class="space-y-4">
          <!-- Dynamically populated -->
        </div>

        <!-- Active Quiz Modal / Screen Container -->
        <div id="activeQuizModal" class="hidden glass-panel p-6 rounded-3xl border-2 border-blue-500/30 space-y-6">
          <div class="flex items-center justify-between">
            <h3 id="activeQuizTitle" class="text-xl font-bold text-white">Quiz in Progress</h3>
            <div class="px-4 py-1.5 bg-red-500/10 border border-red-500/30 rounded-xl text-red-400 text-sm font-bold flex items-center gap-2">
              <i class="fa-solid fa-stopwatch"></i> <span id="quizTimerDisplay">15:00</span>
            </div>
          </div>
          <div id="activeQuizQuestionContainer" class="space-y-4">
            <!-- Dynamically loaded question -->
          </div>
          <button onclick="submitQuizAnswers()" class="px-6 py-2.5 bg-emerald-600 hover:bg-emerald-500 text-white font-semibold text-sm rounded-xl shadow-lg transition">Submit Quiz</button>
        </div>
      </section>

      <!-- 4. STUDENT REPORT CARD -->
      <section id="view-student-grades" class="space-y-6 hidden">
        <div class="glass-panel p-6 rounded-3xl">
          <h2 class="text-xl font-bold text-white">My Academic Report Card</h2>
          <p class="text-xs text-slate-400 mt-0.5">Your personal transcript containing homework scores, quiz results, and attendance record.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div class="glass-panel p-6 rounded-3xl space-y-4">
            <h3 class="text-sm font-bold text-slate-300 uppercase tracking-wider">Attendance Breakdown</h3>
            <div class="flex items-center justify-between p-4 bg-slate-900/60 rounded-2xl border border-slate-800">
              <span class="text-sm text-slate-300">Total Classes Attended</span>
              <span id="reportAttendanceStat" class="text-sm font-bold text-emerald-400">100%</span>
            </div>
          </div>

          <div class="glass-panel p-6 rounded-3xl space-y-4">
            <h3 class="text-sm font-bold text-slate-300 uppercase tracking-wider">Overall Standing</h3>
            <div class="p-6 bg-gradient-to-tr from-blue-600/20 to-indigo-600/20 rounded-2xl border border-blue-500/30 text-center space-y-2">
              <p class="text-xs text-blue-300 font-semibold uppercase tracking-widest">Final Letter Grade</p>
              <h2 id="reportFinalGrade" class="text-4xl font-extrabold text-white">A+</h2>
              <p class="text-xs text-slate-400">Based on weighted homework, attendance, and exam scores.</p>
            </div>
          </div>
        </div>
      </section>

    </main>
  </div>

  <!-- JAVASCRIPT APP LOGIC -->
  <script>
    // INITIAL MOCK DATABASE & STATE
    const defaultDB = {
      users: [
        { name: "Prof. Shafique Ahmad", email: "teacher@college.edu", password: "password123", role: "teacher" },
        { name: "Ayesha Khan", email: "student@college.edu", password: "password123", role: "student" },
        { name: "Ali Raza", email: "ali@college.edu", password: "password123", role: "student" },
        { name: "Fatima Noor", email: "fatima@college.edu", password: "password123", role: "student" },
        { name: "Hamza Ali", email: "hamza@college.edu", password: "password123", role: "student" }
      ],
      attendance: {
        "Ayesha Khan": "Present",
        "Ali Raza": "Present",
        "Fatima Noor": "Late",
        "Hamza Ali": "Absent"
      },
      homework: [
        { id: 1, title: "Network Security Lab 1", dueDate: "2026-11-10", desc: "Configure firewall rules and capture traffic logs." },
        { id: 2, title: "AWS Cloud VPC Architecture", dueDate: "2026-11-15", desc: "Deploy a 3-tier application inside custom VPC subnets." }
      ],
      submissions: [
        { id: 101, hwId: 1, studentName: "Ayesha Khan", work: "https://github.com/ayesha/lab1-firewall", grade: 95, feedback: "Excellent implementation!" },
        { id: 102, hwId: 1, studentName: "Ali Raza", work: "Completed local packet analysis.", grade: 88, feedback: "Good effort." }
      ],
      quizzes: [
        {
          id: 1,
          title: "Cybersecurity Basics MCQ",
          timeLimit: 10,
          question: "Which protocol is used for secure remote login?",
          options: ["HTTP", "SSH", "FTP", "Telnet"],
          correct: 1
        }
      ],
      quizResults: [
        { studentName: "Ayesha Khan", quizId: 1, score: 100 }
      ],
      announcements: [
        { id: 1, title: "Mid-Term Examination Schedule", body: "Exams start next Monday. Please review all lab assignments.", date: "Nov 2, 2026" }
      ]
    };

    // Load DB from LocalStorage or initialize
    let db = JSON.parse(localStorage.getItem('classedge_db')) || defaultDB;
    function saveDB() {
      localStorage.setItem('classedge_db', JSON.stringify(db));
    }

    let currentUser = JSON.parse(localStorage.getItem('classedge_current_user')) || null;
    let activeQuizSession = null;
    let quizTimerInterval = null;

    // ON PAGE LOAD
    window.onload = function() {
      if (currentUser) {
        bootApp();
      } else {
        showAuth();
      }
    };

    // AUTHENTICATION CONTROLS
    function switchAuthTab(tab) {
      if (tab === 'login') {
        document.getElementById('loginForm').classList.remove('hidden');
        document.getElementById('registerForm').classList.add('hidden');
        document.getElementById('tabBtnLogin').className = "flex-1 py-2 rounded-lg text-sm font-semibold text-white bg-blue-600 transition shadow";
        document.getElementById('tabBtnRegister').className = "flex-1 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-white transition";
      } else {
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('registerForm').classList.remove('hidden');
        document.getElementById('tabBtnRegister').className = "flex-1 py-2 rounded-lg text-sm font-semibold text-white bg-emerald-600 transition shadow";
        document.getElementById('tabBtnLogin').className = "flex-1 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-white transition";
      }
    }

    function handleLogin(e) {
      e.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const pass = document.getElementById('loginPassword').value.trim();

      const found = db.users.find(u => u.email === email && u.password === pass);
      if (found) {
        currentUser = found;
        localStorage.setItem('classedge_current_user', JSON.stringify(currentUser));
        bootApp();
      } else {
        alert("Invalid email or password! Check demo credentials or sign up.");
      }
    }

    function handleRegister(e) {
      e.preventDefault();
      const name = document.getElementById('regName').value.trim();
      const email = document.getElementById('regEmail').value.trim();
      const password = document.getElementById('regPassword').value.trim();
      const role = document.getElementById('regRole').value;

      if (db.users.some(u => u.email === email)) {
        alert("Email already registered!");
        return;
      }

      const newUser = { name, email, password, role };
      db.users.push(newUser);
      if (role === 'student') {
        db.attendance[name] = "Present";
      }
      saveDB();

      currentUser = newUser;
      localStorage.setItem('classedge_current_user', JSON.stringify(currentUser));
      bootApp();
    }

    function logoutUser() {
      currentUser = null;
      localStorage.removeItem('classedge_current_user');
      location.reload();
    }

    function showAuth() {
      document.getElementById('authContainer').classList.remove('hidden');
      document.getElementById('mainAppContainer').classList.add('hidden');
      document.getElementById('appHeader').classList.add('hidden');
    }

    function bootApp() {
      document.getElementById('authContainer').classList.add('hidden');
      document.getElementById('mainAppContainer').classList.remove('hidden');
      document.getElementById('appHeader').classList.remove('hidden');

      document.getElementById('currentUserName').innerText = currentUser.name;
      document.getElementById('currentUserRole').innerText = currentUser.role === 'teacher' ? 'Faculty Admin' : 'Enrolled Student';
      document.getElementById('roleBadgeText').innerText = currentUser.role === 'teacher' ? 'Teacher (Admin)' : 'Student Workspace';

      renderNavigation();
      if (currentUser.role === 'teacher') {
        switchView('teacher-dashboard');
      } else {
        switchView('student-dashboard');
      }
    }

    // DYNAMIC NAVIGATION RENDERER
    function renderNavigation() {
      const navContainer = document.getElementById('sidebarNavLinks');
      navContainer.innerHTML = '';

      if (currentUser.role === 'teacher') {
        navContainer.innerHTML = `
          <button onclick="switchView('teacher-dashboard')" id="nav-teacher-dashboard" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold transition bg-blue-600 text-white shadow"><i class="fa-solid fa-chart-pie w-5"></i> Dashboard</button>
          <button onclick="switchView('teacher-attendance')" id="nav-teacher-attendance" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-clipboard-user w-5"></i> Attendance</button>
          <button onclick="switchView('teacher-homework')" id="nav-teacher-homework" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-book-open w-5"></i> Homework Desk</button>
          <button onclick="switchView('teacher-quizzes')" id="nav-teacher-quizzes" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-award w-5"></i> Quizzes & Tests</button>
          <button onclick="switchView('teacher-gradebook')" id="nav-teacher-gradebook" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-graduation-cap w-5"></i> Master Gradebook</button>
          <button onclick="switchView('teacher-database')" id="nav-teacher-database" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-database w-5"></i> Database Inspector</button>
        `;
      } else {
        navContainer.innerHTML = `
          <button onclick="switchView('student-dashboard')" id="nav-student-dashboard" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold transition bg-indigo-600 text-white shadow"><i class="fa-solid fa-house w-5"></i> Dashboard</button>
          <button onclick="switchView('student-homework')" id="nav-student-homework" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-book-bookmark w-5"></i> Homework & Tasks</button>
          <button onclick="switchView('student-quizzes')" id="nav-student-quizzes" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-bolt w-5"></i> Active Tests</button>
          <button onclick="switchView('student-grades')" id="nav-student-grades" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition"><i class="fa-solid fa-award w-5"></i> Report Card</button>
        `;
      }
    }

    function switchView(viewId) {
      const views = [
        'teacher-dashboard', 'teacher-attendance', 'teacher-homework', 'teacher-quizzes', 'teacher-gradebook', 'teacher-database',
        'student-dashboard', 'student-homework', 'student-quizzes', 'student-grades'
      ];
      views.forEach(v => {
        const el = document.getElementById(`view-${v}`);
        if (el) el.classList.add('hidden');
        const navEl = document.getElementById(`nav-${v}`);
        if (navEl) {
          navEl.className = "w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-300 hover:bg-slate-800 transition";
        }
      });

      const target = document.getElementById(`view-${viewId}`);
      if (target) target.classList.remove('hidden');

      const targetNav = document.getElementById(`nav-${viewId}`);
      if (targetNav) {
        targetNav.className = `w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-white shadow ${currentUser.role === 'teacher' ? 'bg-blue-600' : 'bg-indigo-600'}`;
      }

      // Refresh Data on View Switch
      refreshViewData(viewId);
    }

    function refreshViewData(viewId) {
      if (viewId === 'teacher-dashboard') {
        const studentsCount = db.users.filter(u => u.role === 'student').length;
        document.getElementById('statTotalStudents').innerText = studentsCount;
        document.getElementById('statActiveHomework').innerText = db.homework.length;
        document.getElementById('statPublishedQuizzes').innerText = db.quizzes.length;
      } else if (viewId === 'teacher-attendance') {
        renderAttendanceTable();
      } else if (viewId === 'teacher-homework') {
        renderTeacherSubmissions();
      } else if (viewId === 'teacher-quizzes') {
        renderTeacherQuizzes();
      } else if (viewId === 'teacher-gradebook') {
        renderGradebook();
      } else if (viewId === 'teacher-database') {
        document.getElementById('dbJsonViewer').innerText = JSON.stringify(db, null, 2);
      } else if (viewId === 'student-dashboard') {
        renderStudentDashboard();
      } else if (viewId === 'student-homework') {
        renderStudentHomework();
      } else if (viewId === 'student-quizzes') {
        renderStudentQuizzes();
      } else if (viewId === 'student-grades') {
        renderStudentReportCard();
      }
    }

    // --- TEACHER ACTIONS ---

    function postAnnouncement(e) {
      e.preventDefault();
      const title = document.getElementById('announcementTitle').value;
      const body = document.getElementById('announcementBody').value;
      db.announcements.unshift({ id: Date.now(), title, body, date: "Today" });
      saveDB();
      alert("Announcement posted successfully!");
      document.getElementById('announcementTitle').value = '';
      document.getElementById('announcementBody').value = '';
    }

    function renderAttendanceTable() {
      const tbody = document.getElementById('attendanceTableBody');
      tbody.innerHTML = '';
      const students = db.users.filter(u => u.role === 'student');
      students.forEach(st => {
        const status = db.attendance[st.name] || 'Present';
        tbody.innerHTML += `
          <tr class="hover:bg-slate-900/40">
            <td class="p-4 font-semibold text-white">${st.name}</td>
            <td class="p-4 text-slate-400">${st.email}</td>
            <td class="p-4 text-center">
              <span class="px-3 py-1 rounded-full text-xs font-bold ${status === 'Present' ? 'bg-emerald-500/10 text-emerald-400' : status === 'Late' ? 'bg-yellow-500/10 text-yellow-400' : 'bg-red-500/10 text-red-400'}">${status}</span>
            </td>
            <td class="p-4 text-right space-x-2">
              <button onclick="setAttendanceStatus('${st.name}', 'Present')" class="px-2.5 py-1 bg-emerald-600/20 text-emerald-400 rounded-lg text-xs font-bold">Present</button>
              <button onclick="setAttendanceStatus('${st.name}', 'Late')" class="px-2.5 py-1 bg-yellow-600/20 text-yellow-400 rounded-lg text-xs font-bold">Late</button>
              <button onclick="setAttendanceStatus('${st.name}', 'Absent')" class="px-2.5 py-1 bg-red-600/20 text-red-400 rounded-lg text-xs font-bold">Absent</button>
            </td>
          </tr>
        `;
      });
    }

    function setAttendanceStatus(name, status) {
      db.attendance[name] = status;
      saveDB();
      renderAttendanceTable();
    }

    function resetAttendance() {
      const students = db.users.filter(u => u.role === 'student');
      students.forEach(st => db.attendance[st.name] = 'Present');
      saveDB();
      renderAttendanceTable();
    }

    function createHomework(e) {
      e.preventDefault();
      const title = document.getElementById('hwTitle').value;
      const dueDate = document.getElementById('hwDueDate').value;
      const desc = document.getElementById('hwDesc').value;

      db.homework.push({ id: Date.now(), title, dueDate, desc });
      saveDB();
      alert("Homework published successfully!");
      e.target.reset();
      refreshViewData('teacher-homework');
    }

    function renderTeacherSubmissions() {
      const container = document.getElementById('teacherSubmissionsList');
      container.innerHTML = '';
      if (db.submissions.length === 0) {
        container.innerHTML = `<p class="text-xs text-slate-500">No student submissions yet.</p>`;
        return;
      }
      db.submissions.forEach(sub => {
        const hw = db.homework.find(h => h.id === sub.hwId);
        container.innerHTML += `
          <div class="p-4 bg-slate-900/60 rounded-2xl border border-slate-800 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h4 class="font-bold text-white">${sub.studentName}</h4>
              <p class="text-xs text-blue-400">Assignment: ${hw ? hw.title : 'General'}</p>
              <p class="text-xs text-slate-300 mt-1">Response: ${sub.work}</p>
            </div>
            <div class="flex items-center gap-3">
              <input type="number" id="gradeInput_${sub.id}" value="${sub.grade || 0}" class="w-16 bg-slate-900 border border-slate-800 rounded-xl px-2 py-1.5 text-sm text-white text-center">
              <button onclick="gradeSubmission(${sub.id})" class="px-4 py-1.5 bg-blue-600 hover:bg-blue-500 text-white text-xs font-semibold rounded-xl">Save Grade</button>
            </div>
          </div>
        `;
      });
    }

    function gradeSubmission(subId) {
      const val = parseInt(document.getElementById(`gradeInput_${subId}`).value);
      const sub = db.submissions.find(s => s.id === subId);
      if (sub) {
        sub.grade = val;
        sub.feedback = val >= 80 ? "Great work!" : "Needs improvement.";
        saveDB();
        alert("Grade updated successfully!");
      }
    }

    function createQuiz(e) {
      e.preventDefault();
      const title = document.getElementById('quizTitle').value;
      const timeLimit = parseInt(document.getElementById('quizTime').value);
      const question = document.getElementById('qQuestion').value;
      const options = [
        document.getElementById('qOpt1').value,
        document.getElementById('qOpt2').value,
        document.getElementById('qOpt3').value,
        document.getElementById('qOpt4').value
      ];
      const correct = parseInt(document.getElementById('qCorrect').value);

      db.quizzes.push({ id: Date.now(), title, timeLimit, question, options, correct });
      saveDB();
      alert("Quiz published successfully!");
      e.target.reset();
      renderTeacherQuizzes();
    }

    function renderTeacherQuizzes() {
      const container = document.getElementById('teacherQuizzesList');
      container.innerHTML = '';
      db.quizzes.forEach(q => {
        container.innerHTML += `
          <div class="p-4 bg-slate-900/60 rounded-2xl border border-slate-800 flex items-center justify-between">
            <div>
              <h4 class="font-bold text-white">${q.title}</h4>
              <p class="text-xs text-slate-400 mt-0.5">Time Limit: ${q.timeLimit} mins | Question: ${q.question}</p>
            </div>
            <button onclick="deleteQuiz(${q.id})" class="px-3 py-1.5 bg-red-600/20 text-red-400 rounded-xl text-xs font-semibold">Delete</button>
          </div>
        `;
      });
    }

    function deleteQuiz(id) {
      db.quizzes = db.quizzes.filter(q => q.id !== id);
      saveDB();
      renderTeacherQuizzes();
    }

    function renderGradebook() {
      const tbody = document.getElementById('gradebookTableBody');
      tbody.innerHTML = '';
      const students = db.users.filter(u => u.role === 'student');
      students.forEach(st => {
        const att = db.attendance[st.name] === 'Present' ? '100%' : db.attendance[st.name] === 'Late' ? '80%' : '50%';
        const subs = db.submissions.filter(s => s.studentName === st.name);
        const hwAvg = subs.length > 0 ? Math.round(subs.reduce((a, b) => a + (b.grade || 0), 0) / subs.length) : 90;
        const qRes = db.quizResults.filter(r => r.studentName === st.name);
        const quizAvg = qRes.length > 0 ? qRes[0].score : 92;
        const finalScore = Math.round((hwAvg * 0.5) + (quizAvg * 0.5));
        const letter = finalScore >= 90 ? 'A+' : finalScore >= 80 ? 'A' : finalScore >= 70 ? 'B' : 'C';

        tbody.innerHTML += `
          <tr class="hover:bg-slate-900/40">
            <td class="p-4 font-semibold text-white">${st.name}</td>
            <td class="p-4 text-center text-emerald-400 font-bold">${att}</td>
            <td class="p-4 text-center text-blue-400 font-bold">${hwAvg}%</td>
            <td class="p-4 text-center text-purple-400 font-bold">${quizAvg}%</td>
            <td class="p-4 text-center"><span class="px-3 py-1 bg-blue-500/10 text-blue-400 rounded-full font-bold text-xs">${letter}</span></td>
          </tr>
        `;
      });
    }

    function clearLocalStorageDB() {
      if (confirm("Reset database to initial default state?")) {
        localStorage.removeItem('classedge_db');
        localStorage.removeItem('classedge_current_user');
        location.reload();
      }
    }


    // --- STUDENT ACTIONS ---

    function renderStudentDashboard() {
      document.getElementById('studentWelcomeTitle').innerText = `Hello, ${currentUser.name}! 🎓`;
      document.getElementById('studentStatAttendance').innerText = db.attendance[currentUser.name] === 'Present' ? '100%' : '85%';
      
      const feed = document.getElementById('studentAnnouncementsFeed');
      feed.innerHTML = '';
      db.announcements.forEach(an => {
        feed.innerHTML += `
          <div class="p-4 bg-slate-900/60 rounded-2xl border border-slate-800">
            <div class="flex items-center justify-between">
              <h4 class="font-bold text-white text-sm">${an.title}</h4>
              <span class="text-[10px] text-slate-500">${an.date}</span>
            </div>
            <p class="text-xs text-slate-300 mt-1">${an.body}</p>
          </div>
        `;
      });
    }

    function renderStudentHomework() {
      const container = document.getElementById('studentHomeworkList');
      container.innerHTML = '';
      db.homework.forEach(hw => {
        const existingSub = db.submissions.find(s => s.hwId === hw.id && s.studentName === currentUser.name);
        container.innerHTML += `
          <div class="glass-panel p-6 rounded-3xl space-y-4">
            <div class="flex items-center justify-between">
              <h3 class="font-bold text-white text-lg">${hw.title}</h3>
              <span class="text-xs text-blue-400 font-medium"><i class="fa-solid fa-calendar"></i> Due: ${hw.dueDate}</span>
            </div>
            <p class="text-xs text-slate-300 leading-relaxed">${hw.desc}</p>
            ${existingSub ? `
              <div class="p-3 bg-emerald-500/10 border border-emerald-500/20 rounded-xl text-xs text-emerald-300 flex items-center justify-between">
                <span><i class="fa-solid fa-circle-check"></i> Submitted: ${existingSub.work}</span>
                <span class="font-bold">Grade: ${existingSub.grade !== undefined ? existingSub.grade + '/100' : 'Pending Review'}</span>
              </div>
            ` : `
              <div class="flex items-center gap-3 pt-2">
                <input type="text" id="subInput_${hw.id}" placeholder="Paste file link or answer..." class="flex-1 bg-slate-900 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none">
                <button onclick="submitHomework(${hw.id})" class="px-5 py-2.5 bg-blue-600 hover:bg-blue-500 text-white font-semibold text-sm rounded-xl transition">Submit Work</button>
              </div>
            `}
          </div>
        `;
      });
    }

    function submitHomework(hwId) {
      const input = document.getElementById(`subInput_${hwId}`).value.trim();
      if (!input) {
        alert("Please enter work link or text response.");
        return;
      }
      db.submissions.push({
        id: Date.now(),
        hwId: hwId,
        studentName: currentUser.name,
        work: input,
        grade: null,
        feedback: "Pending review"
      });
      saveDB();
      alert("Homework submitted successfully!");
      renderStudentHomework();
    }

    function renderStudentQuizzes() {
      const container = document.getElementById('studentQuizzesList');
      container.innerHTML = '';
      db.quizzes.forEach(q => {
        const alreadyDone = db.quizResults.find(r => r.quizId === q.id && r.studentName === currentUser.name);
        container.innerHTML += `
          <div class="glass-panel p-6 rounded-3xl flex items-center justify-between">
            <div>
              <h3 class="font-bold text-white">${q.title}</h3>
              <p class="text-xs text-slate-400 mt-0.5">Time Limit: ${q.timeLimit} minutes | 1 Question MCQ</p>
            </div>
            ${alreadyDone ? `
              <span class="px-3 py-1 bg-emerald-500/10 text-emerald-400 rounded-full font-bold text-xs">Completed: ${alreadyDone.score}%</span>
            ` : `
              <button onclick="startQuiz(${q.id})" class="px-5 py-2.5 bg-purple-600 hover:bg-purple-500 text-white font-semibold text-sm rounded-xl transition">Start Quiz</button>
            `}
          </div>
        `;
      });
    }

    function startQuiz(quizId) {
      const q = db.quizzes.find(x => x.id === quizId);
      activeQuizSession = q;
      document.getElementById('activeQuizModal').classList.remove('hidden');
      document.getElementById('activeQuizTitle').innerText = q.title;

      let qContainer = document.getElementById('activeQuizQuestionContainer');
      qContainer.innerHTML = `
        <p class="font-semibold text-white text-sm">${q.question}</p>
        <div class="space-y-2 pt-2">
          ${q.options.map((opt, idx) => `
            <label class="flex items-center gap-3 p-3 bg-slate-900/80 rounded-xl border border-slate-800 cursor-pointer hover:border-blue-500 transition">
              <input type="radio" name="quizChoice" value="${idx}" class="text-blue-600">
              <span class="text-sm text-slate-200">${opt}</span>
            </label>
          `).join('')}
        </div>
      `;

      // Start Countdown Timer
      let secondsLeft = q.timeLimit * 60;
      clearInterval(quizTimerInterval);
      quizTimerInterval = setInterval(() => {
        secondsLeft--;
        let m = Math.floor(secondsLeft / 60);
        let s = secondsLeft % 60;
        document.getElementById('quizTimerDisplay').innerText = `${m}:${s < 10 ? '0' : ''}${s}`;
        if (secondsLeft <= 0) {
          clearInterval(quizTimerInterval);
          submitQuizAnswers();
        }
      }, 1000);
    }

    function submitQuizAnswers() {
      clearInterval(quizTimerInterval);
      const selected = document.querySelector('input[name="quizChoice"]:checked');
      let score = 0;
      if (selected && parseInt(selected.value) === activeQuizSession.correct) {
        score = 100;
      }

      db.quizResults.push({
        studentName: currentUser.name,
        quizId: activeQuizSession.id,
        score: score
      });
      saveDB();

      document.getElementById('activeQuizModal').classList.add('hidden');
      alert(`Quiz submitted! Your score: ${score}%`);
      renderStudentQuizzes();
    }

    function renderStudentReportCard() {
      const subs = db.submissions.filter(s => s.studentName === currentUser.name);
      const qRes = db.quizResults.filter(r => r.studentName === currentUser.name);
      const hwAvg = subs.length > 0 ? Math.round(subs.reduce((a, b) => a + (b.grade || 0), 0) / subs.length) : 90;
      const quizAvg = qRes.length > 0 ? qRes[0].score : 95;
      const finalScore = Math.round((hwAvg * 0.5) + (quizAvg * 0.5));
      const letter = finalScore >= 90 ? 'A+' : finalScore >= 80 ? 'A' : 'B';

      document.getElementById('reportAttendanceStat').innerText = db.attendance[currentUser.name] || '100%';
      document.getElementById('reportFinalGrade').innerText = letter;
    }
  </script>
</body>
</html>