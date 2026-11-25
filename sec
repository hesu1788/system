<!DOCTYPE html>
<html lang="zh-TW" class="h-full bg-slate-50">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>松山高中失物尋回 AI 系統 - SSMH Campus AI Lost & Found</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#16a34a',
                            600: '#15803d',
                            700: '#166534',
                            800: '#14532d',
                            900: '#052e16',
                        },
                        ssmh: {
                            green: '#007A3d',
                            lightgreen: '#10B981',
                            accent: '#F59E0B'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Lucide Icons & FontAwesome CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .glass-effect {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(8px);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        @keyframes pulse-subtle {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        .animate-pulse-subtle {
            animation: pulse-subtle 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-6px); }
            75% { transform: translateX(6px); }
        }
        .animate-shake {
            animation: shake 0.3s ease-in-out;
        }
    </style>
</head>
<body class="h-full font-sans text-slate-800 flex flex-col custom-scrollbar">

    <!-- Top Navigation Header -->
    <header class="sticky top-0 z-40 w-full border-b border-emerald-200/60 bg-white/95 backdrop-blur shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <!-- Songshan High School Crest & Title -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('explore')">
                <div class="w-11 h-11 rounded-xl bg-slate-50 border border-emerald-200 p-1 shadow-sm flex items-center justify-center shrink-0">
                    <img src="https://upload.wikimedia.org/wikipedia/zh/b/b3/Songshan_Senior_High_School_logo.svg"
                         alt="松山高中校徽"
                         class="w-full h-full object-contain"
                         onerror="this.onerror=null; this.src='https://placehold.co/100x100/007A3D/FFFFFF?text=SSMH';">
                </div>
                <div>
                    <div class="flex items-center space-x-2">
                        <span class="font-bold text-base sm:text-lg text-slate-900 tracking-tight">松山高中 AI 失物尋回系統</span>
                        <span class="px-2 py-0.5 text-xs font-semibold bg-emerald-100 text-emerald-800 rounded-full border border-emerald-200 hidden sm:inline-block">SSMH AI Engine</span>
                    </div>
                    <p class="text-[11px] text-slate-500 hidden sm:block">臺北市立松山高級中學 • 智能多模態特徵比對平台</p>
                </div>
            </div>

            <!-- Main Navigation Links -->
            <nav class="hidden md:flex space-x-1 lg:space-x-2">
                <button onclick="switchTab('explore')" id="nav-explore" class="nav-btn px-3 py-2 rounded-lg text-sm font-medium transition-colors flex items-center space-x-2 bg-emerald-50 text-emerald-800">
                    <i class="fa-solid fa-compass text-emerald-600"></i>
                    <span>失物廣場</span>
                </button>
                <button onclick="switchTab('ai-search')" id="nav-ai-search" class="nav-btn px-3 py-2 rounded-lg text-sm font-medium text-slate-600 hover:text-slate-900 hover:bg-slate-100 transition-colors flex items-center space-x-2">
                    <i class="fa-solid fa-magnifying-glass font-bold text-emerald-600"></i>
                    <span>以圖/語意檢索</span>
                </button>
                <button onclick="switchTab('report')" id="nav-report" class="nav-btn px-3 py-2 rounded-lg text-sm font-medium text-slate-600 hover:text-slate-900 hover:bg-slate-100 transition-colors flex items-center space-x-2">
                    <i class="fa-solid fa-circle-plus text-amber-500"></i>
                    <span>AI 發布通報</span>
                </button>
                <button onclick="switchTab('map')" id="nav-map" class="nav-btn px-3 py-2 rounded-lg text-sm font-medium text-slate-600 hover:text-slate-900 hover:bg-slate-100 transition-colors flex items-center space-x-2">
                    <i class="fa-solid fa-map-location-dot text-emerald-600"></i>
                    <span>松山校園地圖與數據</span>
                </button>
            </nav>

            <!-- Role & Profile Toggle -->
            <div class="flex items-center space-x-3">
                <button id="role-toggle-btn" onclick="openPasswordModal()" class="flex items-center space-x-2 px-3 py-1.5 rounded-lg border border-slate-300 text-xs font-medium text-slate-700 hover:bg-slate-50 transition">
                    <span id="role-badge" class="w-2 h-2 rounded-full bg-emerald-500"></span>
                    <span id="role-text">前台模式 (松山學生)</span>
                    <i class="fa-solid fa-lock text-slate-400 text-xs ml-1"></i>
                </button>

                <!-- User Avatar / Admin Badge -->
                <div class="flex items-center space-x-2 border-l border-slate-200 pl-3">
                    <div class="w-8 h-8 rounded-full bg-emerald-100 border border-emerald-400 flex items-center justify-center text-emerald-800 font-semibold text-xs" id="user-avatar">
                        松
                    </div>
                </div>
            </div>
        </div>

        <!-- Mobile Navigation Bottom Bar -->
        <div class="md:hidden flex justify-around border-t border-slate-200 bg-white py-2 text-xs">
            <button onclick="switchTab('explore')" class="mobile-nav-btn text-emerald-700 font-medium flex flex-col items-center">
                <i class="fa-solid fa-compass text-base mb-0.5"></i>廣場
            </button>
            <button onclick="switchTab('ai-search')" class="mobile-nav-btn text-slate-600 flex flex-col items-center">
                <i class="fa-solid fa-magnifying-glass text-base mb-0.5"></i>AI搜尋
            </button>
            <button onclick="switchTab('report')" class="mobile-nav-btn text-slate-600 flex flex-col items-center">
                <i class="fa-solid fa-circle-plus text-base mb-0.5"></i>通報
            </button>
            <button onclick="switchTab('map')" class="mobile-nav-btn text-slate-600 flex flex-col items-center">
                <i class="fa-solid fa-chart-pie text-base mb-0.5"></i>數據
            </button>
        </div>
    </header>

    <!-- Global Banner: Songshan High School Branding -->
    <div id="ai-banner" class="bg-gradient-to-r from-emerald-950 via-green-900 to-slate-900 text-white text-xs sm:text-sm py-2 px-4 shadow-inner hidden md:block border-b border-emerald-800/40">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <div class="flex items-center space-x-2">
                <span class="inline-flex items-center px-2 py-0.5 rounded text-xs font-medium bg-emerald-500/30 text-emerald-200 border border-emerald-400/30">
                    <i class="fa-solid fa-graduation-cap mr-1.5 text-emerald-300"></i> 松山高中 AI 專屬系統
                </span>
                <span class="text-slate-300">AI 多模態向量索引庫已即時同步松山高中全校區，支援特徵防冒領驗證。</span>
            </div>
            <div class="flex items-center space-x-4 text-xs text-emerald-300/80">
                <span><i class="fa-solid fa-shield-halved text-emerald-400 mr-1"></i>學術與校務保護機制</span>
            </div>
        </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- TAB 1: Lost & Found List (失物廣場) -->
        <section id="tab-explore" class="tab-content space-y-6">
            <!-- Filter & Search Controls -->
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200 flex flex-col md:flex-row gap-4 justify-between items-center">
                <!-- Search Bar -->
                <div class="relative w-full md:w-96">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400"></i>
                    <input type="text" id="filter-search-input" onkeyup="filterItems()" placeholder="搜尋關鍵字（例如：水壺、耳機、圖書館）..." class="w-full pl-10 pr-4 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-sky-500 focus:bg-white transition">
                </div>

                <!-- Filters -->
                <div class="flex flex-wrap items-center gap-2 w-full md:w-auto justify-start md:justify-end">
                    <select id="filter-type" onchange="filterItems()" class="text-xs sm:text-sm bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-slate-700 focus:ring-2 focus:ring-sky-500 outline-none">
                        <option value="all">全部類型 (遺失/拾獲)</option>
                        <option value="lost">🔴 遺失物 (尋找中)</option>
                        <option value="found">🟢 拾獲物 (等待認領)</option>
                    </select>

                    <select id="filter-category" onchange="filterItems()" class="text-xs sm:text-sm bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-slate-700 focus:ring-2 focus:ring-sky-500 outline-none">
                        <option value="all">所有類別</option>
                        <option value="3C電子">3C 電子配件</option>
                        <option value="證件皮夾">證件 / 皮夾</option>
                        <option value="日常用品">水壺 / 日常用品</option>
                        <option value="書籍文具">書籍 / 文具</option>
                        <option value="衣物配件">衣物 / 配件</option>
                    </select>

                    <select id="filter-status" onchange="filterItems()" class="text-xs sm:text-sm bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-slate-700 focus:ring-2 focus:ring-sky-500 outline-none">
                        <option value="all">狀態：全部</option>
                        <option value="open">招領/尋找中</option>
                        <option value="claiming">審核中</option>
                        <option value="resolved">已尋回/已發還</option>
                    </select>
                </div>
            </div>

            <!-- Items Counter & Dynamic Indicator -->
            <div class="flex justify-between items-center px-1">
                <p class="text-xs font-medium text-slate-500">
                    顯示 <span id="item-count" class="font-bold text-slate-800">0</span> 筆紀錄
                </p>
                <span class="text-xs text-sky-600 bg-sky-50 px-2.5 py-1 rounded-full border border-sky-100 flex items-center gap-1">
                    <i class="fa-solid fa-sparkles text-xs"></i> 系統定時自動比對特徵資料庫
                </span>
            </div>

            <!-- Grid of Lost/Found Cards -->
            <div id="items-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
                <!-- Cards injected dynamically via JS -->
            </div>
        </section>

        <!-- TAB 2: AI Multimodal Search (以圖/語意檢索) -->
        <section id="tab-ai-search" class="tab-content hidden space-y-6">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 md:p-8">
                <div class="max-w-3xl mx-auto text-center space-y-3 mb-8">
                    <span class="px-3 py-1 rounded-full bg-indigo-50 text-indigo-600 text-xs font-semibold uppercase tracking-wider border border-indigo-100">
                        <i class="fa-solid fa-brain mr-1"></i> AI 多模態向量比對 (Multimodal Embeddings)
                    </span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900">描述特徵或上傳照片，快速對齊失物庫</h2>
                    <p class="text-sm text-slate-500">系統將運用語意模型與視覺卷積神經網路提取特徵，跨資料庫計算餘弦相似度 (Cosine Similarity)。</p>
                </div>

                <!-- Input Zone -->
                <div class="max-w-2xl mx-auto space-y-5">
                    <!-- Text Semantic Input -->
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase tracking-wider mb-2">自然語言語意描述搜尋</label>
                        <div class="relative">
                            <textarea id="ai-search-text" rows="3" placeholder="例如：「藍色保護套 AirPods Pro 無線耳機，昨天下午遺失在圖書館四樓...」" class="w-full px-4 py-3 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:bg-white transition resize-none"></textarea>
                        </div>
                    </div>

                    <!-- Image Upload Simulation Area -->
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase tracking-wider mb-2">上傳相似照片 (以圖搜圖)</label>
                        <div id="drop-zone" class="border-2 border-dashed border-slate-300 hover:border-indigo-500 rounded-xl p-6 text-center bg-slate-50 hover:bg-indigo-50/30 transition cursor-pointer relative" onclick="triggerFileInput()">
                            <input type="file" id="ai-search-file" accept="image/*" class="hidden" onchange="handleFileSelect(event)">
                            <div id="upload-placeholder" class="space-y-2">
                                <div class="w-12 h-12 rounded-full bg-indigo-100 text-indigo-600 flex items-center justify-center mx-auto">
                                    <i class="fa-solid fa-cloud-arrow-up text-xl"></i>
                                </div>
                                <p class="text-sm font-medium text-slate-700">點擊上傳照片或將檔案拖曳至此</p>
                                <p class="text-xs text-slate-400">支援 JPG, PNG, WEBP (將在本地進行 AI 特徵向量運算)</p>
                            </div>
                            <div id="upload-preview" class="hidden flex flex-col items-center space-y-2">
                                <img id="uploaded-img-element" src="" class="h-32 object-contain rounded-lg border border-slate-200 shadow-sm">
                                <span class="text-xs text-indigo-600 font-medium">照片已載入特徵緩衝區</span>
                            </div>
                        </div>
                    </div>

                    <!-- Search Button -->
                    <button onclick="runAISearch()" class="w-full py-3.5 bg-gradient-to-r from-indigo-600 to-sky-600 hover:from-indigo-700 hover:to-sky-700 text-white font-semibold rounded-xl shadow-lg shadow-indigo-500/20 flex items-center justify-center space-x-2 transition">
                        <i class="fa-solid fa-wand-magic-sparkles"></i>
                        <span>執行 AI 多模態特徵比對</span>
                    </button>
                </div>
            </div>

            <!-- Search Results Area -->
            <div id="ai-results-container" class="space-y-4 hidden">
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                        <i class="fa-solid fa-list-check text-indigo-600"></i> AI 向量匹配結果排序
                    </h3>
                    <span class="text-xs text-slate-500" id="ai-time-benchmark">耗時約 42ms | 相似度 > 60%</span>
                </div>
                <div id="ai-results-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
                    <!-- Dynamic Result Cards -->
                </div>
            </div>
        </section>

        <!-- TAB 3: AI Smart Report / Publish (發布通報) -->
        <section id="tab-report" class="tab-content hidden max-w-3xl mx-auto space-y-6">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 md:p-8">
                <div class="border-b border-slate-200 pb-5 mb-6">
                    <span class="px-2.5 py-1 rounded-md bg-sky-100 text-sky-800 text-xs font-semibold">AI 自動標籤提取</span>
                    <h2 class="text-xl font-bold text-slate-900 mt-2">新增遺失物或拾獲通報</h2>
                    <p class="text-xs text-slate-500 mt-1">請填寫基本細節，系統 AI 將自動提煉特徵向量，並即時比對現有庫存。</p>
                </div>

                <form id="report-form" onsubmit="handleFormSubmit(event)" class="space-y-6">
                    <!-- Mode Choice: Lost vs Found -->
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-2">通報類型</label>
                        <div class="grid grid-cols-2 gap-4">
                            <label class="cursor-pointer">
                                <input type="radio" name="report_type" value="lost" checked class="peer hidden" onchange="toggleFormMode()">
                                <div class="p-3 text-center border-2 border-slate-200 rounded-xl peer-checked:border-red-500 peer-checked:bg-red-50/40 font-semibold text-slate-600 peer-checked:text-red-600 transition flex items-center justify-center space-x-2">
                                    <i class="fa-solid fa-circle-exclamation"></i>
                                    <span>我掉了東西 (遺失物)</span>
                                </div>
                            </label>
                            <label class="cursor-pointer">
                                <input type="radio" name="report_type" value="found" class="peer hidden" onchange="toggleFormMode()">
                                <div class="p-3 text-center border-2 border-slate-200 rounded-xl peer-checked:border-emerald-500 peer-checked:bg-emerald-50/40 font-semibold text-slate-600 peer-checked:text-emerald-600 transition flex items-center justify-center space-x-2">
                                    <i class="fa-solid fa-hand-holding-heart"></i>
                                    <span>我撿到東西 (拾獲物)</span>
                                </div>
                            </label>
                        </div>
                    </div>

                    <!-- Title & Category -->
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <div class="sm:col-span-2">
                            <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">物品名稱 / 簡述 *</label>
                            <input type="text" id="report-title" oninput="autoMatchPresetImage()" required placeholder="例如：黑綠色象印水壺" class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">物品類別 *</label>
                            <select id="report-category" onchange="autoMatchPresetImage()" required class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none">
                                <option value="3C電子">3C 電子配件</option>
                                <option value="證件皮夾">證件 / 皮夾</option>
                                <option value="日常用品" selected>水壺 / 日常用品</option>
                                <option value="書籍文具">書籍 / 文具</option>
                                <option value="衣物配件">衣物 / 配件</option>
                            </select>
                        </div>
                    </div>

                    <!-- Location & Date -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">校園地點 *</label>
                            <select id="report-location" required class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none">
                                <option value="圖書館總館">圖書館總館</option>
                                <option value="學生活動中心">學生活動中心</option>
                                <option value="綜合教學大樓">綜合教學大樓</option>
                                <option value="體育館/田徑場">體育館 / 田徑場</option>
                                <option value="學生第一餐廳">學生第一餐廳</option>
                                <option value="理學院大樓">理學院大樓</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">日期與時間 *</label>
                            <input type="date" id="report-date" required class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none">
                        </div>
                    </div>

                    <!-- Description & Image Mock -->
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">外觀特徵描述</label>
                        <textarea id="report-desc" rows="3" placeholder="儘量詳細描述外觀顏色、磨損痕跡、貼紙圖樣等..." class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none resize-none"></textarea>
                    </div>

                    <!-- Secret Features for Anti-Fraud Claim Validation -->
                    <div class="bg-amber-50 border border-amber-200 rounded-xl p-4 space-y-2">
                        <div class="flex items-center space-x-2 text-amber-800 font-semibold text-xs uppercase">
                            <i class="fa-solid fa-lock"></i>
                            <span>設定「隱密防冒領特徵」（僅認領審核時對比，不公開顯示）</span>
                        </div>
                        <input type="text" id="report-secret" placeholder="例如：皮夾內含有學生證學號 110xxxx、背面有一張粉紅貼紙、底部刻名字" class="w-full px-3 py-2 text-sm bg-white border border-amber-300 rounded-lg focus:ring-2 focus:ring-amber-500 outline-none">
                        <p class="text-xs text-amber-600">※ 認領申請者必須準確回答此細節才能通過 AI 第一階段防冒領驗證。</p>
                    </div>

                    <!-- Image URL / Preset Selection for Prototype -->
                    <div class="space-y-2">
                        <label class="block text-xs font-semibold text-slate-700 uppercase mb-1">物品照片預覽設定 (AI 自動依描述匹配)</label>
                        <div class="flex items-center gap-4">
                            <select id="report-image-preset" onchange="updateReportImgPreview()" class="flex-grow px-3 py-2 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-sky-500 focus:bg-white outline-none">
                                <option value="https://images.unsplash.com/photo-1602143407151-7111542de6e8?auto=format&fit=crop&w=600&q=80">綠色保溫水壺 / 隨身瓶</option>
                                <option value="https://images.unsplash.com/photo-1610465299993-e6675c9f9efa?auto=format&fit=crop&w=600&q=80">藍色保護套 AirPods / 無線耳機</option>
                                <option value="https://images.unsplash.com/photo-1627123424574-724758594e93?auto=format&fit=crop&w=600&q=80">黑色皮革男用長夾 / 證件皮夾</option>
                                <option value="https://images.unsplash.com/photo-1531346878377-a5be20888e57?auto=format&fit=crop&w=600&q=80">藍色硬皮筆記本 / 講義書籍</option>
                                <option value="https://images.unsplash.com/photo-1521369909029-2afed882baee?auto=format&fit=crop&w=600&q=80">米白色棒球帽 / 運動配件</option>
                            </select>
                            <img id="report-img-preview" src="https://images.unsplash.com/photo-1602143407151-7111542de6e8?auto=format&fit=crop&w=600&q=80" alt="預覽圖" class="w-16 h-16 rounded-xl object-cover border border-slate-200 shrink-0">
                        </div>
                    </div>

                    <!-- Submit Button -->
                    <button type="submit" class="w-full py-3 bg-sky-600 hover:bg-sky-700 text-white font-semibold rounded-xl shadow-md transition flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-paper-plane"></i>
                        <span>立即提交通報並觸發 AI 實時比對</span>
                    </button>
                </form>
            </div>

            <!-- Live Match Preview Box (Shows instantly after submitting or during form typing mock) -->
            <div id="instant-match-box" class="hidden bg-gradient-to-br from-indigo-900 to-slate-900 text-white rounded-2xl p-6 shadow-xl space-y-4">
                <div class="flex items-center justify-between border-b border-indigo-700/50 pb-3">
                    <div class="flex items-center space-x-2">
                        <span class="w-3 h-3 rounded-full bg-emerald-400 animate-pulse"></span>
                        <h3 class="font-bold text-base text-indigo-100">AI 即時比對引擎推薦結果</h3>
                    </div>
                    <span class="text-xs bg-indigo-500/30 text-indigo-200 px-2.5 py-1 rounded-full border border-indigo-400/30">Matches Found</span>
                </div>
                <p class="text-xs text-slate-300">發現資料庫中有極高相似度的相關記錄！若為您遺失/拾獲的物品，可直接進行聯繫或驗證認領：</p>
               
                <div id="instant-matches-list" class="space-y-3">
                    <!-- Dynamic Live Matches Inserted Here -->
                </div>
            </div>
        </section>

        <!-- TAB 4: Campus Map & Analytics (熱點地圖與數據) -->
        <section id="tab-map" class="tab-content hidden space-y-6">
            <!-- Summary Stats Widgets -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-xl bg-sky-100 text-sky-600 flex items-center justify-center text-xl shrink-0">
                        <i class="fa-solid fa-box-archive"></i>
                    </div>
                    <div>
                        <p class="text-xs text-slate-500 font-medium">總通報件數</p>
                        <h4 class="text-xl font-extrabold text-slate-900" id="stat-total-items">128</h4>
                    </div>
                </div>

                <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-xl bg-emerald-100 text-emerald-600 flex items-center justify-center text-xl shrink-0">
                        <i class="fa-solid fa-circle-check"></i>
                    </div>
                    <div>
                        <p class="text-xs text-slate-500 font-medium">成功尋回率</p>
                        <h4 class="text-xl font-extrabold text-slate-900" id="stat-match-rate">76.4%</h4>
                    </div>
                </div>

                <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-xl bg-indigo-100 text-indigo-600 flex items-center justify-center text-xl shrink-0">
                        <i class="fa-solid fa-bolt"></i>
                    </div>
                    <div>
                        <p class="text-xs text-slate-500 font-medium">AI 匹配成功數</p>
                        <h4 class="text-xl font-extrabold text-slate-900" id="stat-ai-matches">98 件</h4>
                    </div>
                </div>

                <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-xl bg-amber-100 text-amber-600 flex items-center justify-center text-xl shrink-0">
                        <i class="fa-solid fa-hourglass-half"></i>
                    </div>
                    <div>
                        <p class="text-xs text-slate-500 font-medium">平均認領天數</p>
                        <h4 class="text-xl font-extrabold text-slate-900">1.8 天</h4>
                    </div>
                </div>
            </div>

            <!-- Campus Interactive Map & Heatmap -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Visual Campus Map Mock -->
                <div class="lg:col-span-2 bg-white rounded-2xl p-6 border border-slate-200 shadow-sm space-y-4">
                    <div class="flex justify-between items-center">
                        <div>
                            <h3 class="text-base font-bold text-slate-900 flex items-center gap-2">
                                <i class="fa-solid fa-map text-emerald-600"></i> 校園遺失物遺落熱點地圖
                            </h3>
                            <p class="text-xs text-slate-500">顏色越紅區域代表該地點發生的遺失/拾獲事件頻率越高</p>
                        </div>
                        <span class="px-2.5 py-1 bg-slate-100 text-slate-600 text-xs font-semibold rounded-md">即時動態繪製</span>
                    </div>

                    <!-- Simulated Canvas/SVG Campus Layout -->
                    <div class="relative w-full h-80 sm:h-96 bg-slate-100 rounded-xl overflow-hidden border border-slate-200 flex items-center justify-center">
                        <!-- Stylized Campus Layout Graphics -->
                        <div class="absolute inset-0 opacity-40 bg-[radial-gradient(#cbd5e1_1px,transparent_1px)] [background-size:16px_16px]"></div>
                       
                        <!-- Main Buildings UI Nodes - Songshan High School Locations -->
                        <!-- 1. 圖書館大樓 -->
                        <div onclick="filterByLocation('圖書館總館')" class="absolute top-[20%] left-[25%] -translate-x-1/2 -translate-y-1/2 group cursor-pointer">
                            <div class="w-20 h-20 rounded-full bg-red-500/20 border-2 border-red-500 flex items-center justify-center animate-pulse-subtle">
                                <div class="w-12 h-12 rounded-full bg-red-600 text-white flex flex-col items-center justify-center text-xs font-bold shadow-lg">
                                    <i class="fa-solid fa-book text-sm"></i>
                                    <span>38件</span>
                                </div>
                            </div>
                            <span class="absolute top-full left-1/2 -translate-x-1/2 mt-1 px-2 py-0.5 bg-slate-900/80 text-white text-xs rounded whitespace-nowrap shadow">圖書館大樓</span>
                        </div>

                        <!-- 2. 學生活動中心/體育館 -->
                        <div onclick="filterByLocation('學生活動中心')" class="absolute top-[35%] left-[70%] -translate-x-1/2 -translate-y-1/2 group cursor-pointer">
                            <div class="w-16 h-16 rounded-full bg-amber-500/20 border-2 border-amber-500 flex items-center justify-center">
                                <div class="w-10 h-10 rounded-full bg-amber-600 text-white flex flex-col items-center justify-center text-xs font-bold shadow-lg">
                                    <i class="fa-solid fa-users text-xs"></i>
                                    <span>24件</span>
                                </div>
                            </div>
                            <span class="absolute top-full left-1/2 -translate-x-1/2 mt-1 px-2 py-0.5 bg-slate-900/80 text-white text-xs rounded whitespace-nowrap shadow">學生活動中心</span>
                        </div>

                        <!-- 3. 操場與司令台 -->
                        <div onclick="filterByLocation('體育館/田徑場')" class="absolute top-[70%] left-[30%] -translate-x-1/2 -translate-y-1/2 group cursor-pointer">
                            <div class="w-14 h-14 rounded-full bg-emerald-500/20 border-2 border-emerald-600 flex items-center justify-center">
                                <div class="w-9 h-9 rounded-full bg-emerald-700 text-white flex flex-col items-center justify-center text-xs font-bold shadow-lg">
                                    <i class="fa-solid fa-running text-xs"></i>
                                    <span>19件</span>
                                </div>
                            </div>
                            <span class="absolute top-full left-1/2 -translate-x-1/2 mt-1 px-2 py-0.5 bg-slate-900/80 text-white text-xs rounded whitespace-nowrap shadow">操場 / 司令台</span>
                        </div>

                        <!-- 4. 學生熱食部/餐廳 -->
                        <div onclick="filterByLocation('學生第一餐廳')" class="absolute top-[65%] left-[75%] -translate-x-1/2 -translate-y-1/2 group cursor-pointer">
                            <div class="w-12 h-12 rounded-full bg-amber-500/20 border-2 border-amber-500 flex items-center justify-center">
                                <div class="w-8 h-8 rounded-full bg-amber-600 text-white flex flex-col items-center justify-center text-xs font-bold shadow-lg">
                                    <i class="fa-solid fa-utensils text-xs"></i>
                                    <span>15件</span>
                                </div>
                            </div>
                            <span class="absolute top-full left-1/2 -translate-x-1/2 mt-1 px-2 py-0.5 bg-slate-900/80 text-white text-xs rounded whitespace-nowrap shadow">熱食部</span>
                        </div>

                        <!-- 5. 綜合教學大樓 -->
                        <div onclick="filterByLocation('綜合教學大樓')" class="absolute top-[45%] left-[45%] -translate-x-1/2 -translate-y-1/2 group cursor-pointer">
                            <div class="w-16 h-16 rounded-full bg-emerald-500/20 border-2 border-emerald-500 flex items-center justify-center">
                                <div class="w-10 h-10 rounded-full bg-emerald-800 text-white flex flex-col items-center justify-center text-xs font-bold shadow-lg">
                                    <i class="fa-solid fa-graduation-cap text-xs"></i>
                                    <span>32件</span>
                                </div>
                            </div>
                            <span class="absolute top-full left-1/2 -translate-x-1/2 mt-1 px-2 py-0.5 bg-slate-900/80 text-white text-xs rounded whitespace-nowrap shadow">綜合教學大樓</span>
                        </div>

                        <!-- Legend Prompt -->
                        <div class="absolute bottom-3 right-3 bg-white/90 backdrop-blur px-3 py-1.5 rounded-lg border border-slate-200 text-[11px] text-slate-600 shadow-sm">
                            點擊松山高中區域地標即可篩選失物
                        </div>
                    </div>
                </div>

                <!-- Hotspot Category Breakdowns -->
                <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm space-y-4 flex flex-col justify-between">
                    <div>
                        <h3 class="text-base font-bold text-slate-900 mb-4 flex items-center gap-2">
                            <i class="fa-solid fa-chart-pie text-indigo-600"></i> 失物遺失類別比例分析
                        </h3>
                        <div class="space-y-4">
                            <div>
                                <div class="flex justify-between text-xs font-semibold mb-1">
                                    <span class="text-slate-700">3C 電子與配件</span>
                                    <span class="text-indigo-600">35%</span>
                                </div>
                                <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                    <div class="bg-indigo-600 h-2.5 rounded-full" style="width: 35%"></div>
                                </div>
                            </div>

                            <div>
                                <div class="flex justify-between text-xs font-semibold mb-1">
                                    <span class="text-slate-700">證件 / 皮夾</span>
                                    <span class="text-sky-600">28%</span>
                                </div>
                                <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                    <div class="bg-sky-500 h-2.5 rounded-full" style="width: 28%"></div>
                                </div>
                            </div>

                            <div>
                                <div class="flex justify-between text-xs font-semibold mb-1">
                                    <span class="text-slate-700">水壺 / 日常用品</span>
                                    <span class="text-emerald-600">18%</span>
                                </div>
                                <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                    <div class="bg-emerald-500 h-2.5 rounded-full" style="width: 18%"></div>
                                </div>
                            </div>

                            <div>
                                <div class="flex justify-between text-xs font-semibold mb-1">
                                    <span class="text-slate-700">書籍 / 文具</span>
                                    <span class="text-amber-600">12%</span>
                                </div>
                                <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                    <div class="bg-amber-500 h-2.5 rounded-full" style="width: 12%"></div>
                                </div>
                            </div>

                            <div>
                                <div class="flex justify-between text-xs font-semibold mb-1">
                                    <span class="text-slate-700">衣物 / 配件</span>
                                    <span class="text-slate-500">7%</span>
                                </div>
                                <div class="w-full bg-slate-100 rounded-full h-2.5 overflow-hidden">
                                    <div class="bg-slate-400 h-2.5 rounded-full" style="width: 7%"></div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="bg-indigo-50 border border-indigo-100 rounded-xl p-4 text-xs text-indigo-900 space-y-1">
                        <div class="font-bold flex items-center gap-1.5">
                            <i class="fa-solid fa-lightbulb text-amber-500"></i> AI 數據洞察：
                        </div>
                        <p class="leading-relaxed">每週五下午在「圖書館總館」與「學生活動中心」為 3C 配件遺失的高峰期。建議加強宣導離開前確認個人隨身物品。</p>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- ROLE SWITCH PASSWORD MODAL (密碼: 1133) -->
    <div id="password-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div id="password-modal-card" class="bg-white rounded-2xl max-w-sm w-full overflow-hidden shadow-2xl border border-slate-200 flex flex-col">
            <div class="px-6 py-4 bg-emerald-950 text-white flex justify-between items-center">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-key text-emerald-400"></i>
                    <h3 class="font-bold text-sm">前後台身分切換驗證</h3>
                </div>
                <button onclick="closePasswordModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-base"></i>
                </button>
            </div>
            <div class="p-6 space-y-4">
                <p id="password-modal-desc" class="text-xs text-slate-600 leading-relaxed">
                    切換系統前／後台權限需進行身分驗證，請輸入管理員密碼：
                </p>
                <div>
                    <input type="password" id="role-password-input" maxlength="12" placeholder="請輸入密碼..." class="w-full px-4 py-2.5 text-sm text-center tracking-widest font-mono bg-slate-50 border border-slate-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-600 focus:bg-white transition">
                    <p id="password-error-msg" class="hidden text-xs text-red-600 mt-1.5 font-medium flex items-center gap-1">
                        <i class="fa-solid fa-circle-exclamation"></i> 密碼錯誤，請重新輸入！
                    </p>
                </div>
            </div>
            <div class="px-6 py-3 bg-slate-50 border-t border-slate-200 flex justify-end space-x-2">
                <button onclick="closePasswordModal()" class="px-4 py-2 text-xs font-semibold text-slate-600 hover:text-slate-800">取消</button>
                <button onclick="verifyRolePassword()" class="px-4 py-2 bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-semibold rounded-lg shadow transition">
                    確認切換
                </button>
            </div>
        </div>
    </div>

    <!-- CLAIM & VERIFICATION MODAL -->
    <div id="claim-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-lg w-full overflow-hidden shadow-2xl border border-slate-100 flex flex-col max-h-[90vh]">
            <!-- Header -->
            <div class="px-6 py-4 bg-slate-900 text-white flex justify-between items-center">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-shield-halved text-sky-400"></i>
                    <h3 class="font-bold text-base">AI 隱密特徵防冒領驗證</h3>
                </div>
                <button onclick="closeClaimModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <!-- Content Container -->
            <div class="p-6 overflow-y-auto space-y-5 custom-scrollbar">
                <!-- Target Item Preview -->
                <div class="flex items-center space-x-4 bg-slate-50 p-3 rounded-xl border border-slate-200">
                    <img id="modal-item-img" src="" class="w-16 h-16 rounded-lg object-cover border">
                    <div>
                        <span id="modal-item-badge" class="px-2 py-0.5 rounded text-[10px] font-bold"></span>
                        <h4 id="modal-item-title" class="font-bold text-sm text-slate-900 mt-0.5"></h4>
                        <p id="modal-item-sub" class="text-xs text-slate-500"></p>
                    </div>
                </div>

                <!-- AI Verification Warning -->
                <div class="text-xs text-slate-600 bg-amber-50 border border-amber-200 p-3 rounded-xl space-y-1">
                    <p class="font-bold text-amber-800"><i class="fa-solid fa-triangle-exclamation mr-1"></i>系統防冒領告示</p>
                    <p>拾獲者已為此物品設定隱密特徵問題。請準確填寫細節，AI 模型將對比答案語意重合度，通過後方可聯繫拾獲者或至管理處領取。</p>
                </div>

                <!-- Verification Form Inputs -->
                <div class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">認領者學號 / 教職員編號 *</label>
                        <input type="text" id="claim-student-id" placeholder="例如：11050123" class="w-full px-3 py-2 text-sm border border-slate-200 rounded-lg outline-none focus:ring-2 focus:ring-sky-500">
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">特徵驗證答覆 (請詳細說明物品隱密細節) *</label>
                        <textarea id="claim-answer" rows="3" placeholder="例如：皮夾內部有一張黃色悠遊卡、背面有刻微小的字母K、或是手機桌面保護色為星空..." class="w-full px-3 py-2 text-sm border border-slate-200 rounded-lg outline-none focus:ring-2 focus:ring-sky-500 resize-none"></textarea>
                    </div>
                </div>

                <!-- Dynamic AI Validation Score Display -->
                <div id="ai-score-box" class="hidden bg-slate-900 text-white p-4 rounded-xl space-y-2">
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-slate-300">AI 特徵語意重合度判讀:</span>
                        <span id="ai-score-val" class="font-extrabold text-emerald-400 text-sm">94% (高吻合)</span>
                    </div>
                    <div class="w-full bg-slate-800 rounded-full h-2">
                        <div id="ai-score-bar" class="bg-emerald-500 h-2 rounded-full transition-all duration-500" style="width: 94%"></div>
                    </div>
                    <p id="ai-score-msg" class="text-[11px] text-slate-400">特徵驗證成功！已確認您具備極高擁有者可能性。</p>
                </div>
            </div>

            <!-- Modal Actions Footer -->
            <div class="px-6 py-3 bg-slate-50 border-t border-slate-200 flex justify-end space-x-3">
                <button onclick="closeClaimModal()" class="px-4 py-2 text-xs font-semibold text-slate-600 hover:text-slate-800">取消</button>
                <button id="modal-submit-btn" onclick="submitClaimVerification()" class="px-4 py-2 bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold rounded-lg shadow transition">
                    提交 AI 防偽審核
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification Widget -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 bg-slate-900 text-white px-4 py-3 rounded-xl shadow-xl flex items-center space-x-3 text-sm transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message">操作已完成</span>
    </div>

    <!-- JAVASCRIPT LOGIC & ENGINE -->
    <script>
        // 前後台切換密碼設定
        const ROLE_SWITCH_PASSWORD = "1133";

        // 預設遺失物/拾獲物資料庫（圖片已精準配對文字描述）
        let itemsData = [
            {
                id: "ITEM-101",
                type: "found",
                title: "AirPods Pro 第二代 (藍色耳機套)",
                category: "3C電子",
                location: "圖書館總館",
                date: "2026-11-10",
                status: "open",
                // 藍色保護套 AirPods 無線耳機
                img: "https://images.unsplash.com/photo-1610465299993-e6675c9f9efa?auto=format&fit=crop&w=600&q=80",
                desc: "在 4 樓自習室桌上拾獲，殼上有皮卡丘吊飾。",
                secret: "耳機保護套內側有一張姓名貼紙，寫著「Alex」",
                publisher: "圖書館管理員",
                similarity: 95
            },
            {
                id: "ITEM-102",
                type: "lost",
                title: "黑色皮革男用長夾",
                category: "證件皮夾",
                location: "學生活動中心",
                date: "2026-11-09",
                status: "open",
                // 黑色皮革男用皮夾
                img: "https://images.unsplash.com/photo-1627123424574-724758594e93?auto=format&fit=crop&w=600&q=80",
                desc: "內有學生證及悠遊卡，運動後疑似遺落於一樓大廳。",
                secret: "皮夾內夾層有一張舊版 50 元紀念硬幣",
                publisher: "陳同學 (110403)",
                similarity: 88
            },
            {
                id: "ITEM-103",
                type: "found",
                title: "象印黑綠色漸層水壺 750ml",
                category: "日常用品",
                location: "體育館/田徑場",
                date: "2026-11-11",
                status: "open",
                // 深綠色不鏽鋼保溫水壺
                img: "https://images.unsplash.com/photo-1602143407151-7111542de6e8?auto=format&fit=crop&w=600&q=80",
                desc: "羽球場邊看台拾獲，瓶身有少許刮痕。",
                secret: "水壺底部貼有「籃球社 12 號」的防偽標籤",
                publisher: "體育館器材室",
                similarity: 91
            },
            {
                id: "ITEM-104",
                type: "lost",
                title: "微積分講義與精裝筆記本",
                category: "書籍文具",
                location: "綜合教學大樓",
                date: "2026-11-08",
                status: "claiming",
                // 藍色硬皮封面筆記本與講義
                img: "https://images.unsplash.com/photo-1531346878377-a5be20888e57?auto=format&fit=crop&w=600&q=80",
                desc: "藍色硬皮封面，夾有期中考考古題題庫。",
                secret: "第一頁有教授的親筆簽名與紅筆評語",
                publisher: "林同學",
                similarity: 82
            },
            {
                id: "ITEM-105",
                type: "found",
                title: "米白色棒球帽 (Nike)",
                category: "衣物配件",
                location: "學生第一餐廳",
                date: "2026-11-07",
                status: "resolved",
                // 米白色棒球帽
                img: "https://images.unsplash.com/photo-1521369909029-2afed882baee?auto=format&fit=crop&w=600&q=80",
                desc: "二樓餐桌旁拾獲，帽簷有微小咖啡漬。",
                secret: "帽圍調整帶上有黑色代針筆畫的心形標記",
                publisher: "餐廳服務台",
                similarity: 78
            }
        ];

        let currentRole = 'user'; // 'user' or 'admin'
        let selectedItemForClaim = null;

        // Initialize App
        document.addEventListener('DOMContentLoaded', () => {
            renderItems(itemsData);
            updateStats();

            // 密碼輸入框支援 Enter 送出與 Esc 關閉
            const pwdInput = document.getElementById('role-password-input');
            if (pwdInput) {
                pwdInput.addEventListener('keydown', (e) => {
                    if (e.key === 'Enter') {
                        e.preventDefault();
                        verifyRolePassword();
                    } else if (e.key === 'Escape') {
                        closePasswordModal();
                    }
                });
            }
        });

        // 開啟前後台切換密碼驗證彈窗
        function openPasswordModal() {
            const modal = document.getElementById('password-modal');
            const input = document.getElementById('role-password-input');
            const errorMsg = document.getElementById('password-error-msg');
            const desc = document.getElementById('password-modal-desc');

            desc.innerText = currentRole === 'user'
                ? "即將切換至「後台模式 (松山教務/總務處)」，請輸入驗證密碼："
                : "即將切換回「前台模式 (松山學生)」，請輸入驗證密碼：";

            input.value = '';
            errorMsg.classList.add('hidden');
            modal.classList.remove('hidden');
            setTimeout(() => input.focus(), 50);
        }

        function closePasswordModal() {
            document.getElementById('password-modal').classList.add('hidden');
        }

        function verifyRolePassword() {
            const input = document.getElementById('role-password-input');
            const errorMsg = document.getElementById('password-error-msg');
            const card = document.getElementById('password-modal-card');

            if (input.value.trim() === ROLE_SWITCH_PASSWORD) {
                closePasswordModal();
                executeRoleSwitch();
            } else {
                errorMsg.classList.remove('hidden');
                card.classList.remove('animate-shake');
                void card.offsetWidth; // 觸發重繪以重播動畫
                card.classList.add('animate-shake');
                input.value = '';
                input.focus();
            }
        }

        // 通過密碼驗證後實際執行前後台切換
        function executeRoleSwitch() {
            if (currentRole === 'user') {
                currentRole = 'admin';
                document.getElementById('role-badge').className = "w-2 h-2 rounded-full bg-emerald-500 animate-ping";
                document.getElementById('role-text').innerText = "後台模式 (松山教務/總務處)";
                document.getElementById('user-avatar').className = "w-8 h-8 rounded-full bg-emerald-800 text-white flex items-center justify-center font-bold text-xs";
                document.getElementById('user-avatar').innerText = "教";
                showToast("驗證通過！已切換至「松山高中後台管理模式」", "fa-user-shield");
            } else {
                currentRole = 'user';
                document.getElementById('role-badge').className = "w-2 h-2 rounded-full bg-emerald-500";
                document.getElementById('role-text').innerText = "前台模式 (松山學生)";
                document.getElementById('user-avatar').className = "w-8 h-8 rounded-full bg-emerald-100 text-emerald-800 flex items-center justify-center font-semibold text-xs border border-emerald-300";
                document.getElementById('user-avatar').innerText = "松";
                showToast("驗證通過！已切換至「松山學生前台模式」", "fa-user");
            }
            renderItems(itemsData);
        }

        // Tab Switching Logic
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-${tabId}`).classList.remove('hidden');

            // Update Nav Desktop Styles
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-50', 'text-emerald-800');
                btn.classList.add('text-slate-600');
            });
            const activeNav = document.getElementById(`nav-${tabId}`);
            if (activeNav) {
                activeNav.classList.add('bg-emerald-50', 'text-emerald-800');
                activeNav.classList.remove('text-slate-600');
            }
        }

        // 依物品標題或類別自動配對相符圖片
        function autoMatchPresetImage() {
            const title = document.getElementById('report-title').value.toLowerCase();
            const category = document.getElementById('report-category').value;
            const select = document.getElementById('report-image-preset');

            const imgMap = {
                waterBottle: "https://images.unsplash.com/photo-1602143407151-7111542de6e8?auto=format&fit=crop&w=600&q=80",
                earphone: "https://images.unsplash.com/photo-1610465299993-e6675c9f9efa?auto=format&fit=crop&w=600&q=80",
                wallet: "https://images.unsplash.com/photo-1627123424574-724758594e93?auto=format&fit=crop&w=600&q=80",
                book: "https://images.unsplash.com/photo-1531346878377-a5be20888e57?auto=format&fit=crop&w=600&q=80",
                hat: "https://images.unsplash.com/photo-1521369909029-2afed882baee?auto=format&fit=crop&w=600&q=80"
            };

            if (title.includes('耳機') || title.includes('airpods') || title.includes('充電') || category === '3C電子') {
                select.value = imgMap.earphone;
            } else if (title.includes('皮夾') || title.includes('長夾') || title.includes('錢包') || title.includes('證') || category === '證件皮夾') {
                select.value = imgMap.wallet;
            } else if (title.includes('水壺') || title.includes('保溫') || title.includes('象印') || category === '日常用品') {
                select.value = imgMap.waterBottle;
            } else if (title.includes('筆記') || title.includes('講義') || title.includes('書') || category === '書籍文具') {
                select.value = imgMap.book;
            } else if (title.includes('帽') || title.includes('衣') || title.includes('外套') || category === '衣物配件') {
                select.value = imgMap.hat;
            }

            updateReportImgPreview();
        }

        function updateReportImgPreview() {
            const select = document.getElementById('report-image-preset');
            const preview = document.getElementById('report-img-preview');
            if (select && preview) {
                preview.src = select.value;
            }
        }

        // Render Cards in Lost & Found Explore Tab
        function renderItems(data) {
            const container = document.getElementById('items-grid');
            document.getElementById('item-count').innerText = data.length;
            container.innerHTML = '';

            if (data.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full py-12 text-center text-slate-400">
                        <i class="fa-regular fa-folder-open text-4xl mb-2"></i>
                        <p>未找到符合條件的失物/拾獲物紀錄</p>
                    </div>
                `;
                return;
            }

            data.forEach(item => {
                const isLost = item.type === 'lost';
                const statusBadge = getStatusBadgeHTML(item.status);

                const card = document.createElement('div');
                card.className = "bg-white rounded-2xl border border-slate-200 overflow-hidden shadow-sm hover:shadow-md transition flex flex-col justify-between";
               
                card.innerHTML = `
                    <div>
                        <!-- Image Container with Badges -->
                        <div class="relative h-44 w-full bg-slate-100 overflow-hidden">
                            <img src="${item.img}" alt="${item.title}" class="w-full h-full object-cover transition duration-300 hover:scale-105">
                           
                            <!-- Type Badge (Lost vs Found) -->
                            <span class="absolute top-3 left-3 px-2.5 py-1 rounded-full text-xs font-bold text-white shadow ${isLost ? 'bg-red-500' : 'bg-emerald-600'}">
                                ${isLost ? '<i class="fa-solid fa-circle-exclamation mr-1"></i>遺失物' : '<i class="fa-solid fa-hand-holding-heart mr-1"></i>拾獲物'}
                            </span>

                            <!-- AI Feature Match Chip -->
                            <span class="absolute top-3 right-3 px-2 py-0.5 rounded-md text-[11px] font-semibold bg-slate-900/80 text-sky-300 backdrop-blur border border-sky-500/30">
                                <i class="fa-solid fa-wand-magic-sparkles mr-1"></i>特徵極似
                            </span>
                        </div>

                        <!-- Content Details -->
                        <div class="p-4 space-y-2">
                            <div class="flex justify-between items-start gap-2">
                                <h3 class="font-bold text-slate-900 text-sm leading-snug line-clamp-1">${item.title}</h3>
                                ${statusBadge}
                            </div>
                           
                            <p class="text-xs text-slate-500 line-clamp-2">${item.desc}</p>
                           
                            <div class="pt-2 border-t border-slate-100 flex flex-wrap gap-y-1 gap-x-3 text-[11px] text-slate-500">
                                <span><i class="fa-solid fa-location-dot text-slate-400 mr-1"></i>${item.location}</span>
                                <span><i class="fa-solid fa-calendar text-slate-400 mr-1"></i>${item.date}</span>
                                <span><i class="fa-solid fa-tag text-slate-400 mr-1"></i>${item.category}</span>
                            </div>
                        </div>
                    </div>

                    <!-- Footer Actions -->
                    <div class="px-4 py-3 bg-slate-50 border-t border-slate-100 flex justify-between items-center">
                        <span class="text-[11px] text-slate-400">發布者: ${item.publisher}</span>
                        ${getActionButtonHTML(item)}
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Helper: Status Badges
        function getStatusBadgeHTML(status) {
            if (status === 'open') {
                return `<span class="px-2 py-0.5 bg-emerald-100 text-emerald-700 text-[10px] font-bold rounded">尋找/招領中</span>`;
            } else if (status === 'claiming') {
                return `<span class="px-2 py-0.5 bg-amber-100 text-amber-700 text-[10px] font-bold rounded">AI 驗證中</span>`;
            } else {
                return `<span class="px-2 py-0.5 bg-slate-200 text-slate-600 text-[10px] font-bold rounded">已發還結案</span>`;
            }
        }

        // Helper: Action Buttons depending on role and status
        function getActionButtonHTML(item) {
            if (currentRole === 'admin') {
                return `
                    <button onclick="adminResolve('${item.id}')" class="px-3 py-1 bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-semibold rounded-lg shadow transition">
                        後台審核處置
                    </button>
                `;
            }

            if (item.status === 'resolved') {
                return `<span class="text-xs text-slate-400 font-medium">已完成結案</span>`;
            }

            return `
                <button onclick="openClaimModal('${item.id}')" class="px-3 py-1 bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold rounded-lg shadow transition flex items-center gap-1">
                    <i class="fa-solid fa-shield-halved text-[10px]"></i> 申請驗證認領
                </button>
            `;
        }

        // Filter Logic
        function filterItems() {
            const keyword = document.getElementById('filter-search-input').value.toLowerCase();
            const type = document.getElementById('filter-type').value;
            const category = document.getElementById('filter-category').value;
            const status = document.getElementById('filter-status').value;

            const filtered = itemsData.filter(item => {
                const matchKeyword = item.title.toLowerCase().includes(keyword) ||
                                     item.desc.toLowerCase().includes(keyword) ||
                                     item.location.toLowerCase().includes(keyword);
                const matchType = (type === 'all') || (item.type === type);
                const matchCategory = (category === 'all') || (item.category === category);
                const matchStatus = (status === 'all') || (item.status === status);

                return matchKeyword && matchType && matchCategory && matchStatus;
            });

            renderItems(filtered);
        }

        function filterByLocation(locName) {
            switchTab('explore');
            document.getElementById('filter-search-input').value = locName;
            filterItems();
            showToast(`已自動篩選地點：「${locName}」的物品`, 'fa-filter');
        }

        // AI Multimodal Search Simulator
        function runAISearch() {
            const queryText = document.getElementById('ai-search-text').value;
            const resultsContainer = document.getElementById('ai-results-container');
            const resultsGrid = document.getElementById('ai-results-grid');

            if (!queryText && document.getElementById('upload-preview').classList.contains('hidden')) {
                showToast("請輸入特徵描述或上傳照片以進行 AI 檢索！", "fa-triangle-exclamation");
                return;
            }

            showToast("正在計算跨庫神經網絡向量距離...", "fa-microchip");

            setTimeout(() => {
                resultsContainer.classList.remove('hidden');
                resultsGrid.innerHTML = '';

                const scoredItems = itemsData.map(item => {
                    let score = Math.floor(Math.random() * 25) + 70;
                    if (queryText && (item.title.includes(queryText.substring(0, 2)) || item.desc.includes(queryText.substring(0, 2)))) {
                        score = 96;
                    }
                    return { ...item, score };
                }).sort((a, b) => b.score - a.score);

                scoredItems.forEach(item => {
                    const card = document.createElement('div');
                    card.className = "bg-white p-4 rounded-xl border border-indigo-100 shadow-sm space-y-3 relative overflow-hidden";
                    card.innerHTML = `
                        <div class="absolute top-0 right-0 bg-indigo-600 text-white text-[10px] font-bold px-3 py-1 rounded-bl-lg">
                            向量相似度: ${item.score}%
                        </div>
                        <div class="flex items-center space-x-3">
                            <img src="${item.img}" class="w-16 h-16 rounded-lg object-cover border">
                            <div>
                                <h4 class="font-bold text-sm text-slate-900">${item.title}</h4>
                                <p class="text-xs text-slate-500">${item.location} | ${item.date}</p>
                                <span class="inline-block mt-1 px-2 py-0.5 rounded text-[10px] font-bold ${item.type === 'lost' ? 'bg-red-100 text-red-700' : 'bg-emerald-100 text-emerald-700'}">
                                    ${item.type === 'lost' ? '遺失物' : '拾獲物'}
                                </span>
                            </div>
                        </div>
                        <p class="text-xs text-slate-600 bg-slate-50 p-2 rounded border border-slate-100">${item.desc}</p>
                        <button onclick="openClaimModal('${item.id}')" class="w-full py-1.5 bg-indigo-50 hover:bg-indigo-100 text-indigo-700 text-xs font-semibold rounded-lg transition">
                            進行特徵比對認領
                        </button>
                    `;
                    resultsGrid.appendChild(card);
                });

                resultsContainer.scrollIntoView({ behavior: 'smooth' });
            }, 600);
        }

        // Image Drop Zone Simulator
        function triggerFileInput() {
            document.getElementById('ai-search-file').click();
        }

        function handleFileSelect(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(evt) {
                    document.getElementById('uploaded-img-element').src = evt.target.result;
                    document.getElementById('upload-placeholder').classList.add('hidden');
                    document.getElementById('upload-preview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        // Report Form Submission & Live AI Match Engine Mock
        function handleFormSubmit(e) {
            e.preventDefault();

            const title = document.getElementById('report-title').value;
            const category = document.getElementById('report-category').value;
            const location = document.getElementById('report-location').value;
            const date = document.getElementById('report-date').value;
            const desc = document.getElementById('report-desc').value;
            const secret = document.getElementById('report-secret').value;
            const img = document.getElementById('report-image-preset').value;
            const type = document.querySelector('input[name="report_type"]:checked').value;

            const newItem = {
                id: `ITEM-${Date.now().toString().slice(-3)}`,
                type,
                title,
                category,
                location,
                date,
                status: "open",
                img,
                desc: desc || "無詳細描述",
                secret: secret || "未設定隱密特徵",
                publisher: currentRole === 'admin' ? "校務管理員" : "匿名同學",
                similarity: 92
            };

            itemsData.unshift(newItem);
            renderItems(itemsData);
            updateStats();

            showToast("通報成功！AI 已自動提取語意向量並上架失物庫", "fa-circle-check");

            const instantBox = document.getElementById('instant-match-box');
            const instantList = document.getElementById('instant-matches-list');
            instantBox.classList.remove('hidden');

            const oppositeType = type === 'lost' ? 'found' : 'lost';
            const potentialMatches = itemsData.filter(i => i.type === oppositeType && i.id !== newItem.id);

            instantList.innerHTML = '';
            if (potentialMatches.length > 0) {
                potentialMatches.slice(0, 2).forEach(m => {
                    const div = document.createElement('div');
                    div.className = "bg-white/10 p-3 rounded-xl border border-white/10 flex items-center justify-between text-xs";
                    div.innerHTML = `
                        <div class="flex items-center space-x-3">
                            <img src="${m.img}" class="w-10 h-10 rounded-lg object-cover">
                            <div>
                                <p class="font-bold text-white">${m.title}</p>
                                <p class="text-slate-300 text-[11px]">${m.location} • ${m.date}</p>
                            </div>
                        </div>
                        <div class="text-right">
                            <span class="text-emerald-400 font-extrabold text-sm">93% Match</span>
                            <button onclick="openClaimModal('${m.id}')" class="block mt-1 px-2.5 py-1 bg-sky-500 hover:bg-sky-600 text-white text-[10px] font-bold rounded">
                                對比認領
                            </button>
                        </div>
                    `;
                    instantList.appendChild(div);
                });
            } else {
                instantList.innerHTML = `<p class="text-xs text-slate-400">目前暫無極高重複度之歷史反向通報，系統將持續監控新資料。</p>`;
            }

            instantBox.scrollIntoView({ behavior: 'smooth' });
        }

        function toggleFormMode() {}

        // Claim Verification Modal Logic
        function openClaimModal(itemId) {
            const item = itemsData.find(i => i.id === itemId);
            if (!item) return;

            selectedItemForClaim = item;

            document.getElementById('modal-item-img').src = item.img;
            document.getElementById('modal-item-title').innerText = item.title;
            document.getElementById('modal-item-sub').innerText = `${item.location} • ${item.date}`;
           
            const badge = document.getElementById('modal-item-badge');
            badge.innerText = item.type === 'lost' ? '遺失物尋找' : '拾獲物招領';
            badge.className = `px-2 py-0.5 rounded text-[10px] font-bold ${item.type === 'lost' ? 'bg-red-100 text-red-700' : 'bg-emerald-100 text-emerald-700'}`;

            document.getElementById('ai-score-box').classList.add('hidden');
            document.getElementById('claim-answer').value = '';
            document.getElementById('claim-modal').classList.remove('hidden');
        }

        function closeClaimModal() {
            document.getElementById('claim-modal').classList.add('hidden');
            selectedItemForClaim = null;
        }

        function submitClaimVerification() {
            const answer = document.getElementById('claim-answer').value;
            const studentId = document.getElementById('claim-student-id').value;

            if (!answer || !studentId) {
                showToast("請填寫完整學號與防偽特徵說明！", "fa-circle-exclamation");
                return;
            }

            const scoreBox = document.getElementById('ai-score-box');
            scoreBox.classList.remove('hidden');

            const isMatch = answer.length > 5;
            const score = isMatch ? Math.floor(Math.random() * 15) + 85 : 42;

            document.getElementById('ai-score-val').innerText = `${score}% (${score > 80 ? '高度吻合' : '吻合度低'})`;
            document.getElementById('ai-score-bar').style.width = `${score}%`;
            document.getElementById('ai-score-bar').className = score > 80 ? "bg-emerald-500 h-2 rounded-full transition-all duration-500" : "bg-red-500 h-2 rounded-full transition-all duration-500";
           
            if (score > 80) {
                document.getElementById('ai-score-msg').innerText = "特徵經 AI 驗證比對完全無誤！已發送通知至拾獲者與管理處審核。";
                setTimeout(() => {
                    if (selectedItemForClaim) {
                        selectedItemForClaim.status = 'claiming';
                        renderItems(itemsData);
                    }
                    closeClaimModal();
                    showToast("認領申請成功！已進入 AI 快速覆核階段", "fa-shield-halved");
                }, 1500);
            } else {
                document.getElementById('ai-score-msg').innerText = "特徵答覆與拾獲人備註差距過大，請重新確定物品細節或聯繫管理員。";
            }
        }

        // Admin quick actions
        function adminResolve(itemId) {
            const item = itemsData.find(i => i.id === itemId);
            if (!item) return;

            item.status = item.status === 'resolved' ? 'open' : 'resolved';
            renderItems(itemsData);
            updateStats();
            showToast(`管理員操作成功：物品 [${item.title}] 狀態已更新為「${item.status === 'resolved' ? '已發還結案' : '開放中'}」`, "fa-user-gear");
        }

        // Global Dynamic Stats Updater
        function updateStats() {
            document.getElementById('stat-total-items').innerText = itemsData.length;
            const resolvedCount = itemsData.filter(i => i.status === 'resolved').length;
            const rate = itemsData.length ? ((resolvedCount / itemsData.length) * 100).toFixed(1) : 0;
            document.getElementById('stat-match-rate').innerText = `${rate}%`;
        }

        // Toast Notification Helper
        function showToast(msg, iconClass = "fa-circle-check") {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = msg;
            document.getElementById('toast-icon').className = `fa-solid ${iconClass} text-emerald-400`;
           
            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
