```html
<!DOCTYPE html>
<html lang="ar" dir="rtl" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الحاسبة الرياضية الشاملة | Math Matrix Pro</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            500: '#0284c7',
                            600: '#0284c7',
                            700: '#0369a1',
                            800: '#075985',
                            900: '#0c4a6e',
                        },
                        darkbg: '#0f172a',
                        darkcard: '#1e293b',
                    },
                    fontFamily: {
                        cairo: ['Cairo', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    
    <!-- Google Fonts Cairo -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&family=Fira+Code:wght@400;500;600&display=swap" rel="stylesheet">
    
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Math.js Library for Advanced Calculations -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.8.0/math.js"></script>

    <style>
        * {
            font-family: 'Cairo', sans-serif;
            touch-action: manipulation;
        }
        .font-mono {
            font-family: 'Fira Code', monospace;
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(15, 23, 42, 0.6);
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
        
        .glass-panel {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        
        .calc-btn {
            transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
            user-select: none;
            -webkit-user-select: none;
        }
        .calc-btn:active {
            transform: scale(0.95);
        }
        .calc-btn-primary {
            background: linear-gradient(135deg, #2563eb, #1d4ed8);
            color: white;
        }
        .calc-btn-primary:hover {
            background: linear-gradient(135deg, #3b82f6, #2563eb);
            box-shadow: 0 0 15px rgba(37, 99, 235, 0.4);
        }
        .calc-btn-op {
            background: rgba(51, 65, 85, 0.8);
            color: #38bdf8;
        }
        .calc-btn-op:hover {
            background: rgba(71, 85, 105, 0.9);
            color: #7dd3fc;
        }
        .calc-btn-num {
            background: rgba(30, 41, 59, 0.9);
            color: #f1f5f9;
        }
        .calc-btn-num:hover {
            background: rgba(51, 65, 85, 0.9);
        }
        .calc-btn-danger {
            background: rgba(225, 29, 72, 0.15);
            color: #fda4af;
            border: 1px solid rgba(225, 29, 72, 0.3);
        }
        .calc-btn-danger:hover {
            background: rgba(225, 29, 72, 0.3);
            color: #fff;
        }
        .calc-btn-sci {
            background: rgba(15, 23, 42, 0.6);
            color: #a7f3d0;
            font-size: 0.85rem;
        }
        .calc-btn-sci:hover {
            background: rgba(30, 41, 59, 0.8);
            color: #34d399;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col justify-between selection:bg-sky-500 selection:text-white">

    <!-- Header -->
    <header class="border-b border-slate-800 bg-slate-900/80 sticky top-0 z-50 backdrop-blur-md">
        <div class="max-w-7xl mx-auto px-4 py-3 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-500 to-indigo-600 flex items-center justify-center shadow-lg shadow-sky-500/20">
                    <i class="fa-solid font-mono font-bold text-xl text-white">∑</i>
                </div>
                <div>
                    <h1 class="text-xl font-bold bg-gradient-to-r from-sky-400 via-indigo-300 to-emerald-400 bg-clip-text text-transparent">
                        الحاسبة الرياضية الشاملة
                    </h1>
                    <p class="text-xs text-slate-400">منصة الحسابات العلمية والبيانية المتكاملة</p>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <button id="toggleHistoryBtn" class="p-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 transition-colors flex items-center gap-2 text-sm" title="سجل الحسابات">
                    <i class="fa-solid fa-clock-rotate-left text-sky-400"></i>
                    <span class="hidden sm:inline">السجل</span>
                </button>
                <button id="infoModalBtn" class="p-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 transition-colors text-sm" title="إرشادات الاستخدام">
                    <i class="fa-solid fa-circle-info"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto w-full px-2 sm:px-4 py-4 flex-1 flex flex-col">
        <!-- Navigation Tabs -->
        <nav class="flex overflow-x-auto gap-2 p-1.5 mb-4 bg-slate-900/90 rounded-2xl border border-slate-800 scrollbar-none">
            <button data-tab="scientific" class="nav-tab active flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all whitespace-nowrap bg-sky-600 text-white shadow-md shadow-sky-600/30">
                <i class="fa-solid fa-calculator"></i>
                <span>الحاسبة العلمية</span>
            </button>
            <button data-tab="graphing" class="nav-tab flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all whitespace-nowrap text-slate-400 hover:text-white hover:bg-slate-800">
                <i class="fa-solid fa-chart-line"></i>
                <span>الرسوم البيانية</span>
            </button>
            <button data-tab="equations" class="nav-tab flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all whitespace-nowrap text-slate-400 hover:text-white hover:bg-slate-800">
                <i class="fa-solid fa-square-root-variable"></i>
                <span>حل المعادَلَات</span>
            </button>
            <button data-tab="matrix" class="nav-tab flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all whitespace-nowrap text-slate-400 hover:text-white hover:bg-slate-800">
                <i class="fa-solid fa-table-cells font-mono"></i>
                <span>المصفوفات</span>
            </button>
            <button data-tab="converter" class="nav-tab flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-semibold transition-all whitespace-nowrap text-slate-400 hover:text-white hover:bg-slate-800">
                <i class="fa-solid fa-right-left"></i>
                <span>المحول والنظم</span>
            </button>
        </nav>

        <!-- TAB 1: Scientific Calculator -->
        <div id="tab-scientific" class="tab-content flex-1 grid grid-cols-1 lg:grid-cols-12 gap-4">
            <!-- Left/Center Display & Buttons -->
            <div class="lg:col-span-8 flex flex-col gap-4">
                <!-- Calculator Screen -->
                <div class="glass-panel p-4 rounded-3xl flex flex-col justify-between shadow-xl min-h-[160px] border border-slate-700/60 relative overflow-hidden">
                    <div class="flex items-center justify-between text-xs text-slate-400 mb-1">
                        <div class="flex items-center gap-2">
                            <span id="angleModeBadge" class="px-2 py-0.5 rounded bg-sky-950 text-sky-400 border border-sky-800 font-mono font-bold">DEG</span>
                            <span id="memoryBadge" class="px-2 py-0.5 rounded bg-amber-950 text-amber-400 border border-amber-800 font-mono hidden">M</span>
                        </div>
                        <div id="calcStatus" class="text-emerald-400 text-xs font-mono">جاهز</div>
                    </div>

                    <!-- Expression Input Screen -->
                    <div class="w-full overflow-x-auto text-right py-1 scrollbar-none">
                        <div id="expressionDisplay" class="text-slate-400 font-mono text-lg sm:text-xl min-h-[28px] whitespace-nowrap tracking-wider"></div>
                    </div>

                    <!-- Result Screen -->
                    <div class="w-full overflow-x-auto text-right py-1">
                        <div id="resultDisplay" class="text-3xl sm:text-4xl font-extrabold font-mono text-white tracking-wide min-h-[48px] flex items-center justify-end">0</div>
                    </div>
                </div>

                <!-- Memory & Mode Toolbar -->
                <div class="grid grid-cols-6 gap-2">
                    <button id="btnDegRad" class="calc-btn calc-btn-sci py-2 rounded-xl font-bold">DEG / RAD</button>
                    <button onclick="handleMemory('MC')" class="calc-btn calc-btn-sci py-2 rounded-xl">MC</button>
                    <button onclick="handleMemory('MR')" class="calc-btn calc-btn-sci py-2 rounded-xl">MR</button>
                    <button onclick="handleMemory('M+')" class="calc-btn calc-btn-sci py-2 rounded-xl">M+</button>
                    <button onclick="handleMemory('M-')" class="calc-btn calc-btn-sci py-2 rounded-xl">M-</button>
                    <button onclick="handleMemory('MS')" class="calc-btn calc-btn-sci py-2 rounded-xl">MS</button>
                </div>

                <!-- Keypad Grid -->
                <div class="grid grid-cols-5 sm:grid-cols-6 gap-2 flex-1">
                    <!-- Row 1 Scientific Functions -->
                    <button onclick="appendFunc('sin')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">sin</button>
                    <button onclick="appendFunc('cos')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">cos</button>
                    <button onclick="appendFunc('tan')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">tan</button>
                    <button onclick="appendFunc('asin')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">sin⁻¹</button>
                    <button onclick="appendFunc('acos')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">cos⁻¹</button>
                    <button onclick="appendFunc('atan')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">tan⁻¹</button>

                    <!-- Row 2 -->
                    <button onclick="appendFunc('log10')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">log</button>
                    <button onclick="appendFunc('log')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">ln</button>
                    <button onclick="appendFunc('sqrt')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">√x</button>
                    <button onclick="appendValue('^2')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">x²</button>
                    <button onclick="appendValue('^')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">xʸ</button>
                    <button onclick="appendFunc('cbrt')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">∛x</button>

                    <!-- Row 3 -->
                    <button onclick="appendValue('pi')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">π</button>
                    <button onclick="appendValue('e')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">e</button>
                    <button onclick="appendValue('(')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">(</button>
                    <button onclick="appendValue(')')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">)</button>
                    <button onclick="appendValue('!')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono">x!</button>
                    <button onclick="appendValue('%')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">%</button>

                    <!-- Row 4 Standard Controls -->
                    <button onclick="clearAll()" class="calc-btn calc-btn-danger p-3 rounded-2xl font-bold">AC</button>
                    <button onclick="deleteLast()" class="calc-btn calc-btn-danger p-3 rounded-2xl font-bold"><i class="fa-solid fa-delete-left"></i></button>
                    <button onclick="appendValue('/')" class="calc-btn calc-btn-op p-3 rounded-2xl text-xl font-mono">÷</button>
                    <button onclick="appendValue('*')" class="calc-btn calc-btn-op p-3 rounded-2xl text-xl font-mono">×</button>
                    <button onclick="appendValue('mod')" class="calc-btn calc-btn-op p-3 rounded-2xl font-mono text-sm">mod</button>
                    <button onclick="appendValue('abs')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">|x|</button>

                    <!-- Row 5 Numpad 7-9 -->
                    <button onclick="appendValue('7')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">7</button>
                    <button onclick="appendValue('8')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">8</button>
                    <button onclick="appendValue('9')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">9</button>
                    <button onclick="appendValue('-')" class="calc-btn calc-btn-op p-3 rounded-2xl text-xl font-mono">-</button>
                    <button onclick="appendFunc('exp')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono text-sm">EXP</button>
                    <button onclick="appendAns()" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">Ans</button>

                    <!-- Row 6 Numpad 4-6 -->
                    <button onclick="appendValue('4')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">4</button>
                    <button onclick="appendValue('5')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">5</button>
                    <button onclick="appendValue('6')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">6</button>
                    <button onclick="appendValue('+')" class="calc-btn calc-btn-op p-3 rounded-2xl text-xl font-mono">+</button>
                    <button onclick="appendValue('1/')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono text-sm">1/x</button>
                    <button onclick="appendValue('10^')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono text-xs hidden sm:block">10ˣ</button>

                    <!-- Row 7 Numpad 1-3 -->
                    <button onclick="appendValue('1')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">1</button>
                    <button onclick="appendValue('2')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">2</button>
                    <button onclick="appendValue('3')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">3</button>
                    <button onclick="calculateResult()" class="calc-btn calc-btn-primary p-3 rounded-2xl text-2xl font-bold font-mono row-span-2 flex items-center justify-center shadow-lg">=</button>
                    <button onclick="appendValue('e^')" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono text-xs">eˣ</button>
                    <button onclick="toggleSign()" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono hidden sm:block">±</button>

                    <!-- Row 8 Numpad 0 & Dot -->
                    <button onclick="appendValue('0')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono col-span-2">0</button>
                    <button onclick="appendValue('.')" class="calc-btn calc-btn-num p-3 rounded-2xl text-xl font-bold font-mono">.</button>
                    <button onclick="appendAns()" class="calc-btn calc-btn-sci p-3 rounded-2xl font-mono text-sm sm:hidden">Ans</button>
                </div>
            </div>

            <!-- Right Sidebar: Fast Quick Math Tips / Memory / Mini History -->
            <div class="lg:col-span-4 flex flex-col gap-4">
                <div class="glass-panel p-4 rounded-3xl flex flex-col flex-1 border border-slate-800">
                    <div class="flex items-center justify-between pb-3 border-b border-slate-800 mb-3">
                        <h3 class="font-bold text-slate-200 flex items-center gap-2">
                            <i class="fa-solid fa-clock-rotate-left text-sky-400"></i>
                            <span>السجل السريع</span>
                        </h3>
                        <button onclick="clearHistory()" class="text-xs text-rose-400 hover:underline">مسح</button>
                    </div>
                    <div id="quickHistoryList" class="flex-1 overflow-y-auto space-y-2 pr-1 max-h-[420px]">
                        <p class="text-slate-500 text-sm text-center py-6">لا يوجد عمليات سابقة</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- TAB 2: Graphing Calculator -->
        <div id="tab-graphing" class="tab-content hidden flex-1 flex flex-col lg:flex-row gap-4">
            <!-- Controls Panel -->
            <div class="w-full lg:w-80 flex flex-col gap-4">
                <div class="glass-panel p-4 rounded-3xl border border-slate-800 space-y-4">
                    <h3 class="font-bold text-lg text-slate-200 flex items-center gap-2">
                        <i class="fa-solid fa-chart-simple text-sky-400"></i>
                        <span>إدخال الدوال</span>
                    </h3>

                    <div class="space-y-3">
                        <div>
                            <label class="text-xs text-slate-400 mb-1 block">الدالة الأولى f1(x)</label>
                            <div class="flex items-center gap-2">
                                <span class="w-3 h-3 rounded-full bg-sky-400 flex-shrink-0"></span>
                                <input type="text" id="funcInput1" value="x^2 - 4" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm font-mono text-white focus:outline-none focus:border-sky-500" placeholder="مثال: sin(x)">
                            </div>
                        </div>

                        <div>
                            <label class="text-xs text-slate-400 mb-1 block">الدالة الثانية f2(x) (اختياري)</label>
                            <div class="flex items-center gap-2">
                                <span class="w-3 h-3 rounded-full bg-emerald-400 flex-shrink-0"></span>
                                <input type="text" id="funcInput2" value="2*x + 1" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-sm font-mono text-white focus:outline-none focus:border-emerald-500" placeholder="مثال: 2*x + 1">
                            </div>
                        </div>
                    </div>

                    <button id="plotBtn" class="w-full py-2.5 rounded-xl bg-sky-600 hover:bg-sky-500 text-white font-bold text-sm shadow-lg shadow-sky-600/30 transition-all flex items-center justify-center gap-2">
                        <i class="fa-solid fa-pen-nib"></i>
                        <span>رسم البياني</span>
                    </button>

                    <!-- View Controls -->
                    <div class="pt-3 border-t border-slate-800 space-y-2">
                        <span class="text-xs font-semibold text-slate-400">أدوات التحكم بالقماش</span>
                        <div class="grid grid-cols-3 gap-2">
                            <button id="zoomInBtn" class="bg-slate-800 hover:bg-slate-700 text-slate-200 py-2 rounded-xl text-sm"><i class="fa-solid fa-magnifying-glass-plus"></i></button>
                            <button id="zoomOutBtn" class="bg-slate-800 hover:bg-slate-700 text-slate-200 py-2 rounded-xl text-sm"><i class="fa-solid fa-magnifying-glass-minus"></i></button>
                            <button id="resetGraphBtn" class="bg-slate-800 hover:bg-slate-700 text-slate-200 py-2 rounded-xl text-sm" title="إعادة ضبط"><i class="fa-solid fa-arrows-rotate"></i></button>
                        </div>
                    </div>

                    <div class="p-3 bg-slate-900/60 rounded-xl border border-slate-800 text-xs text-slate-400 space-y-1">
                        <p><i class="fa-solid fa-lightbulb text-amber-400 ml-1"></i> يمكنك السحب والتحريك على الرسم أو استخدام عجلة الماوس لتكبير وتصغير الشبكة.</p>
                    </div>
                </div>
            </div>

            <!-- Graph Canvas Area -->
            <div class="flex-1 glass-panel p-2 rounded-3xl border border-slate-800 relative min-h-[450px] flex flex-col">
                <canvas id="graphCanvas" class="w-full h-full rounded-2xl bg-slate-950 cursor-crosshair flex-1"></canvas>
                <div id="graphCoords" class="absolute bottom-4 left-4 bg-slate-900/90 border border-slate-700 px-3 py-1.5 rounded-xl font-mono text-xs text-sky-400 pointer-events-none">
                    X: 0.00 | Y: 0.00
                </div>
            </div>
        </div>

        <!-- TAB 3: Equation Solver -->
        <div id="tab-equations" class="tab-content hidden flex-1 grid grid-cols-1 md:grid-cols-2 gap-4">
            <!-- Quadratic Solver -->
            <div class="glass-panel p-5 rounded-3xl border border-slate-800 flex flex-col justify-between">
                <div>
                    <h3 class="font-bold text-lg text-slate-200 mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-superscript text-sky-400"></i>
                        <span>المعادلة التربيعية (ax² + bx + c = 0)</span>
                    </h3>
                    <p class="text-xs text-slate-400 mb-4">أدخل معاملات المعادلة التربيعية لحساب الجذرين والمميز مع خطوات الحل.</p>

                    <div class="grid grid-cols-3 gap-3 mb-4">
                        <div>
                            <label class="text-xs text-slate-400 block mb-1">المعامل a</label>
                            <input type="number" id="quadA" value="1" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-center font-mono text-white focus:outline-none focus:border-sky-500">
                        </div>
                        <div>
                            <label class="text-xs text-slate-400 block mb-1">المعامل b</label>
                            <input type="number" id="quadB" value="-5" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-center font-mono text-white focus:outline-none focus:border-sky-500">
                        </div>
                        <div>
                            <label class="text-xs text-slate-400 block mb-1">المعامل c</label>
                            <input type="number" id="quadC" value="6" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 text-center font-mono text-white focus:outline-none focus:border-sky-500">
                        </div>
                    </div>

                    <button onclick="solveQuadratic()" class="w-full py-2.5 rounded-xl bg-sky-600 hover:bg-sky-500 text-white font-bold text-sm shadow-lg shadow-sky-600/30 transition-all">
                        حل المعادلة
                    </button>
                </div>

                <!-- Quad Result -->
                <div id="quadOutput" class="mt-4 p-4 bg-slate-900/80 rounded-2xl border border-slate-800 min-h-[140px] text-sm space-y-2">
                    <p class="text-slate-500 text-center py-4">أدخل المعاملات واضغط على "حل المعادلة"</p>
                </div>
            </div>

            <!-- 2x2 System Solver -->
            <div class="glass-panel p-5 rounded-3xl border border-slate-800 flex flex-col justify-between">
                <div>
                    <h3 class="font-bold text-lg text-slate-200 mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-arrows-split-up-and-left text-emerald-400"></i>
                        <span>جملة معادلتين خطيتين بمتغيرين</span>
                    </h3>
                    <p class="text-xs text-slate-400 mb-4">a1·x + b1·y = c1 <br> a2·x + b2·y = c2</p>

                    <div class="space-y-3 mb-4">
                        <div class="grid grid-cols-3 gap-2 items-center">
                            <input type="number" id="sysA1" value="2" placeholder="a1" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                            <input type="number" id="sysB1" value="3" placeholder="b1" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                            <input type="number" id="sysC1" value="13" placeholder="c1" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                        </div>
                        <div class="grid grid-cols-3 gap-2 items-center">
                            <input type="number" id="sysA2" value="1" placeholder="a2" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                            <input type="number" id="sysB2" value="-1" placeholder="b2" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                            <input type="number" id="sysC2" value="-1" placeholder="c2" class="bg-slate-900 border border-slate-700 rounded-xl p-2 text-center font-mono text-white">
                        </div>
                    </div>

                    <button onclick="solveLinearSystem()" class="w-full py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm shadow-lg shadow-emerald-600/30 transition-all">
                        حل النظام (طريقة كرامر)
                    </button>
                </div>

                <!-- System Result -->
                <div id="sysOutput" class="mt-4 p-4 bg-slate-900/80 rounded-2xl border border-slate-800 min-h-[140px] text-sm space-y-2">
                    <p class="text-slate-500 text-center py-4">اضغط لحساب قيم x و y</p>
                </div>
            </div>
        </div>

        <!-- TAB 4: Matrix Calculator -->
        <div id="tab-matrix" class="tab-content hidden flex-1 flex flex-col gap-4">
            <div class="glass-panel p-5 rounded-3xl border border-slate-800">
                <div class="flex flex-wrap items-center justify-between gap-4 mb-4">
                    <h3 class="font-bold text-lg text-slate-200 flex items-center gap-2">
                        <i class="fa-solid fa-table-cells text-indigo-400"></i>
                        <span>حاسبة المصفوفات (2x2 / 3x3)</span>
                    </h3>

                    <div class="flex items-center gap-2 bg-slate-900 p-1 rounded-xl border border-slate-800">
                        <button id="dim2Btn" onclick="setMatrixDimension(2)" class="px-3 py-1.5 rounded-lg text-xs font-bold bg-indigo-600 text-white">2 × 2</button>
                        <button id="dim3Btn" onclick="setMatrixDimension(3)" class="px-3 py-1.5 rounded-lg text-xs font-bold text-slate-400 hover:text-white">3 × 3</button>
                    </div>
                </div>

                <!-- Matrices Container -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                    <!-- Matrix A -->
                    <div>
                        <h4 class="text-sm font-bold text-indigo-400 mb-2">المصفوفة (أ / A)</h4>
                        <div id="matrixAGrid" class="grid grid-cols-2 gap-2 bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                            <!-- JS Populated Inputs -->
                        </div>
                    </div>

                    <!-- Matrix B -->
                    <div>
                        <h4 class="text-sm font-bold text-indigo-400 mb-2">المصفوفة (ب / B)</h4>
                        <div id="matrixBGrid" class="grid grid-cols-2 gap-2 bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                            <!-- JS Populated Inputs -->
                        </div>
                    </div>
                </div>

                <!-- Matrix Operations Buttons -->
                <div class="flex flex-wrap gap-2 mb-6">
                    <button onclick="calcMatrixOp('add')" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold">A + B</button>
                    <button onclick="calcMatrixOp('sub')" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold">A - B</button>
                    <button onclick="calcMatrixOp('mul')" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold">A × B</button>
                    <button onclick="calcMatrixOp('detA')" class="px-4 py-2 rounded-xl bg-indigo-900/50 hover:bg-indigo-900 text-indigo-300 border border-indigo-700/50 text-xs font-bold">محدد (det A)</button>
                    <button onclick="calcMatrixOp('invA')" class="px-4 py-2 rounded-xl bg-indigo-900/50 hover:bg-indigo-900 text-indigo-300 border border-indigo-700/50 text-xs font-bold">معكوس (A⁻¹)</button>
                    <button onclick="calcMatrixOp('transA')" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold">مدور (Aᵀ)</button>
                </div>

                <!-- Matrix Output Result -->
                <div class="p-4 bg-slate-900/90 rounded-2xl border border-slate-800">
                    <span class="text-xs text-slate-400 block mb-2">النتيجة:</span>
                    <div id="matrixResult" class="font-mono text-emerald-400 text-sm overflow-x-auto min-h-[60px] flex items-center">
                        اختر عملية للحساب.
                    </div>
                </div>
            </div>
        </div>

        <!-- TAB 5: Unit & Base Converter -->
        <div id="tab-converter" class="tab-content hidden flex-1 grid grid-cols-1 md:grid-cols-2 gap-4">
            <!-- Number Bases Converter -->
            <div class="glass-panel p-5 rounded-3xl border border-slate-800">
                <h3 class="font-bold text-lg text-slate-200 mb-4 flex items-center gap-2">
                    <i class="fa-solid fa-binary text-amber-400"></i>
                    <span>تحويل النظم العددية</span>
                </h3>

                <div class="space-y-4">
                    <div>
                        <label class="text-xs text-slate-400 block mb-1">عشري (Decimal)</label>
                        <input type="text" id="baseDec" oninput="convertBases('dec')" value="255" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-white focus:outline-none focus:border-amber-500">
                    </div>

                    <div>
                        <label class="text-xs text-slate-400 block mb-1">ثنائي (Binary)</label>
                        <input type="text" id="baseBin" oninput="convertBases('bin')" value="11111111" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-amber-400 focus:outline-none focus:border-amber-500">
                    </div>

                    <div>
                        <label class="text-xs text-slate-400 block mb-1">ست عشري (Hexadecimal)</label>
                        <input type="text" id="baseHex" oninput="convertBases('hex')" value="FF" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-sky-400 focus:outline-none focus:border-amber-500">
                    </div>

                    <div>
                        <label class="text-xs text-slate-400 block mb-1">ثثماني (Octal)</label>
                        <input type="text" id="baseOct" oninput="convertBases('oct')" value="377" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-emerald-400 focus:outline-none focus:border-amber-500">
                    </div>
                </div>
            </div>

            <!-- Angle & Unit Converter -->
            <div class="glass-panel p-5 rounded-3xl border border-slate-800">
                <h3 class="font-bold text-lg text-slate-200 mb-4 flex items-center gap-2">
                    <i class="fa-solid fa-compass text-rose-400"></i>
                    <span>تحويل قياس الزوايا</span>
                </h3>

                <div class="space-y-4">
                    <div>
                        <label class="text-xs text-slate-400 block mb-1">بالدرجات (Degrees °)</label>
                        <input type="number" id="angleDeg" oninput="convertAngles('deg')" value="180" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-white focus:outline-none focus:border-rose-500">
                    </div>

                    <div>
                        <label class="text-xs text-slate-400 block mb-1">بالراديان (Radians rad)</label>
                        <input type="text" id="angleRad" oninput="convertAngles('rad')" value="3.14159265" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-rose-400 focus:outline-none focus:border-rose-500">
                    </div>

                    <div>
                        <label class="text-xs text-slate-400 block mb-1">بالغراديان (Gradians grad)</label>
                        <input type="number" id="angleGrad" oninput="convertAngles('grad')" value="200" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2 font-mono text-amber-300 focus:outline-none focus:border-rose-500">
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- Info Modal -->
    <div id="infoModal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="glass-panel p-6 rounded-3xl border border-slate-700 max-w-md w-full space-y-4">
            <div class="flex items-center justify-between pb-2 border-b border-slate-800">
                <h3 class="font-bold text-lg text-white">حول تطبيق الحاسبة الرياضية</h3>
                <button id="closeInfoBtn" class="text-slate-400 hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>
            <div class="text-sm text-slate-300 space-y-2 leading-relaxed">
                <p>تطبيق حاسبة رياضيات متقدم وشامل مصمم بالكامل للعمل المباشر بدون إنترنت.</p>
                <ul class="list-disc list-inside space-y-1 text-xs text-slate-400">
                    <li>يدعم الحسابات العلمية المتقدمة والدوال المثلثية.</li>
                    <li>رسم الدوال البيانية $f(x)$ وتكبير/تصغير الشبكة.</li>
                    <li>حل المعادلات التربيعية ونظم المعادلتين الخطيتين.</li>
                    <li>عمليات المصفوفات ومحدداتها والمعكوس.</li>
                    <li>تحويل القواعد العددية (Binary, Hex, Oct, Dec).</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="border-t border-slate-900 py-3 text-center text-xs text-slate-500 bg-slate-950">
        <p>الحاسبة الرياضية الشاملة &copy; 2026 - تم التطوير لخدمة الرياضيات والتعليم</p>
    </footer>

    <script>
        // App State
        let currentExpression = '';
        let lastAnswer = '0';
        let isDeg = true; // true for DEG, false for RAD
        let memoryValue = 0;
        let history = JSON.parse(localStorage.getItem('math_history') || '[]');
        let matrixDim = 2;

        // Navigation Tabs Handling
        document.querySelectorAll('.nav-tab').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.nav-tab').forEach(b => {
                    b.classList.remove('bg-sky-600', 'text-white', 'shadow-md', 'shadow-sky-600/30');
                    b.classList.add('text-slate-400', 'hover:text-white');
                });
                btn.classList.add('bg-sky-600', 'text-white', 'shadow-md', 'shadow-sky-600/30');
                btn.classList.remove('text-slate-400');

                const targetTab = btn.getAttribute('data-tab');
                document.querySelectorAll('.tab-content').forEach(tc => tc.classList.add('hidden'));
                document.getElementById(`tab-${targetTab}`).classList.remove('hidden');

                if (targetTab === 'graphing') {
                    initCanvas();
                    drawGraph();
                }
            });
        });

        // Toggle Angle Mode
        document.getElementById('btnDegRad').addEventListener('click', () => {
            isDeg = !isDeg;
            document.getElementById('angleModeBadge').textContent = isDeg ? 'DEG' : 'RAD';
        });

        // Info Modal Toggle
        document.getElementById('infoModalBtn').addEventListener('click', () => {
            document.getElementById('infoModal').classList.remove('hidden');
        });
        document.getElementById('closeInfoBtn').addEventListener('click', () => {
            document.getElementById('infoModal').classList.add('hidden');
        });

        function updateDisplay() {
            const expEl = document.getElementById('expressionDisplay');
            expEl.textContent = currentExpression || '0';
        }

        function appendValue(val) {
            currentExpression += val;
            updateDisplay();
        }

        function appendFunc(func) {
            currentExpression += `${func}(`;
            updateDisplay();
        }

        function appendAns() {
            currentExpression += lastAnswer;
            updateDisplay();
        }

        function clearAll() {
            currentExpression = '';
            document.getElementById('resultDisplay').textContent = '0';
            updateDisplay();
        }

        function deleteLast() {
            currentExpression = currentExpression.slice(0, -1);
            updateDisplay();
        }

        function toggleSign() {
            if (currentExpression.startsWith('-')) {
                currentExpression = currentExpression.substring(1);
            } else {
                currentExpression = '-' + currentExpression;
            }
            updateDisplay();
        }

        // Evaluate Math Expression with Math.js
        function calculateResult() {
            if (!currentExpression.trim()) return;

            try {
                let parsedExp = currentExpression;

                // Adjust trigonometric evaluation for DEG mode
                if (isDeg) {
                    parsedExp = parsedExp.replace(/sin\(([^)]+)\)/g, 'sin(($1) * deg)');
                    parsedExp = parsedExp.replace(/cos\(([^)]+)\)/g, 'cos(($1) * deg)');
                    parsedExp = parsedExp.replace(/tan\(([^)]+)\)/g, 'tan(($1) * deg)');
                }

                const result = math.evaluate(parsedExp);
                
                // Format Result
                let formattedRes;
                if (typeof result === 'number') {
                    formattedRes = Math.abs(result) < 1e-10 ? '0' : math.format(result, { precision: 10 });
                } else {
                    formattedRes = result.toString();
                }

                document.getElementById('resultDisplay').textContent = formattedRes;
                
                // Save to history
                addHistory(currentExpression, formattedRes);
                lastAnswer = formattedRes;
            } catch (err) {
                document.getElementById('resultDisplay').textContent = 'خطأ رياضي';
            }
        }

        // Memory Functions
        function handleMemory(op) {
            const currentRes = parseFloat(document.getElementById('resultDisplay').textContent) || 0;
            const badge = document.getElementById('memoryBadge');

            switch (op) {
                case 'MC':
                    memoryValue = 0;
                    badge.classList.add('hidden');
                    break;
                case 'MR':
                    currentExpression += memoryValue.toString();
                    updateDisplay();
                    break;
                case 'M+':
                    memoryValue += currentRes;
                    badge.classList.remove('hidden');
                    break;
                case 'M-':
                    memoryValue -= currentRes;
                    badge.classList.remove('hidden');
                    break;
                case 'MS':
                    memoryValue = currentRes;
                    badge.classList.remove('hidden');
                    break;
            }
        }

        // History Management
        function addHistory(exp, res) {
            history.unshift({ exp, res, time: new Date().toLocaleTimeString('ar-EG') });
            if (history.length > 20) history.pop();
            localStorage.setItem('math_history', JSON.stringify(history));
            renderHistory();
        }

        function renderHistory() {
            const list = document.getElementById('quickHistoryList');
            if (history.length === 0) {
                list.innerHTML = '<p class="text-slate-500 text-sm text-center py-6">لا يوجد عمليات سابقة</p>';
                return;
            }

            list.innerHTML = history.map((item, idx) => `
                <div onclick="useHistoryItem('${item.exp}')" class="p-2.5 rounded-xl bg-slate-900/60 hover:bg-slate-800/80 border border-slate-800 cursor-pointer transition-colors group">
                    <div class="text-xs text-slate-400 font-mono flex justify-between">
                        <span>${item.exp}</span>
                        <span class="text-slate-600">${item.time}</span>
                    </div>
                    <div class="text-sm font-bold font-mono text-sky-400 text-right group-hover:text-sky-300">
                        = ${item.res}
                    </div>
                </div>
            `).join('');
        }

        function useHistoryItem(exp) {
            currentExpression = exp;
            updateDisplay();
        }

        function clearHistory() {
            history = [];
            localStorage.removeItem('math_history');
            renderHistory();
        }

        // Graphing Engine variables
        let canvas, ctx;
        let scale = 30; // Pixels per unit
        let offsetX = 0;
        let offsetY = 0;
        let isDragging = false;
        let startX, startY;

        function initCanvas() {
            canvas = document.getElementById('graphCanvas');
            ctx = canvas.getContext('2d');
            resizeCanvas();

            window.addEventListener('resize', resizeCanvas);

            // Drag / Pan Graph Events
            canvas.onmousedown = (e) => {
                isDragging = true;
                startX = e.clientX - offsetX;
                startY = e.clientY - offsetY;
            };

            window.onmouseup = () => isDragging = false;

            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;

                // Update Coordinates Display
                const unitX = (mouseX - (canvas.width / 2 + offsetX)) / scale;
                const unitY = -(mouseY - (canvas.height / 2 + offsetY)) / scale;
                document.getElementById('graphCoords').textContent = `X: ${unitX.toFixed(2)} | Y: ${unitY.toFixed(2)}`;

                if (isDragging) {
                    offsetX = e.clientX - startX;
                    offsetY = e.clientY - startY;
                    drawGraph();
                }
            };

            // Wheel Zoom
            canvas.onwheel = (e) => {
                e.preventDefault();
                const zoomFactor = e.deltaY < 0 ? 1.15 : 0.85;
                scale *= zoomFactor;
                scale = Math.max(5, Math.min(scale, 300));
                drawGraph();
            };
        }

        function resizeCanvas() {
            if (!canvas) return;
            const parent = canvas.parentElement;
            canvas.width = parent.clientWidth;
            canvas.height = parent.clientHeight || 450;
            drawGraph();
        }

        function drawGraph() {
            if (!ctx) return;
            const w = canvas.width;
            const h = canvas.height;
            const originX = w / 2 + offsetX;
            const originY = h / 2 + offsetY;

            // Clear Canvas
            ctx.fillStyle = '#020617';
            ctx.fillRect(0, 0, w, h);

            // Grid Lines
            ctx.lineWidth = 1;
            ctx.strokeStyle = '#1e293b';

            const startGridX = Math.floor(-originX / scale);
            const endGridX = Math.ceil((w - originX) / scale);
            const startGridY = Math.floor(-(h - originY) / scale);
            const endGridY = Math.ceil(originY / scale);

            for (let x = startGridX; x <= endGridX; x++) {
                const px = originX + x * scale;
                ctx.beginPath();
                ctx.moveTo(px, 0);
                ctx.lineTo(px, h);
                ctx.stroke();
            }

            for (let y = startGridY; y <= endGridY; y++) {
                const py = originY - y * scale;
                ctx.beginPath();
                ctx.moveTo(0, py);
                ctx.lineTo(w, py);
                ctx.stroke();
            }

            // Main Axes
            ctx.lineWidth = 2;
            ctx.strokeStyle = '#475569';

            // X Axis
            ctx.beginPath();
            ctx.moveTo(0, originY);
            ctx.lineTo(w, originY);
            ctx.stroke();

            // Y Axis
            ctx.beginPath();
            ctx.moveTo(originX, 0);
            ctx.lineTo(originX, h);
            ctx.stroke();

            // Plot Function 1 (Sky Blue)
            const f1Str = document.getElementById('funcInput1').value.trim();
            if (f1Str) plotFunctionCurve(f1Str, '#38bdf8', originX, originY, w);

            // Plot Function 2 (Emerald Green)
            const f2Str = document.getElementById('funcInput2').value.trim();
            if (f2Str) plotFunctionCurve(f2Str, '#34d399', originX, originY, w);
        }

        function plotFunctionCurve(funcStr, color, originX, originY, width) {
            try {
                const compiled = math.compile(funcStr);
                ctx.lineWidth = 2.5;
                ctx.strokeStyle = color;
                ctx.beginPath();

                let isFirstPoint = true;

                for (let px = 0; px <= width; px += 2) {
                    const x = (px - originX) / scale;
                    try {
                        const y = compiled.evaluate({ x: x });
                        if (typeof y === 'number' && !isNaN(y) && isFinite(y)) {
                            const py = originY - y * scale;
                            if (isFirstPoint) {
                                ctx.moveTo(px, py);
                                isFirstPoint = false;
                            } else {
                                ctx.lineTo(px, py);
                            }
                        } else {
                            isFirstPoint = true;
                        }
                    } catch (e) {
                        isFirstPoint = true;
                    }
                }
                ctx.stroke();
            } catch (err) {
                // Invalid math expression
            }
        }

        document.getElementById('plotBtn').addEventListener('click', drawGraph);
        document.getElementById('zoomInBtn').addEventListener('click', () => { scale *= 1.2; drawGraph(); });
        document.getElementById('zoomOutBtn').addEventListener('click', () => { scale /= 1.2; drawGraph(); });
        document.getElementById('resetGraphBtn').addEventListener('click', () => { scale = 30; offsetX = 0; offsetY = 0; drawGraph(); });

        // Quadratic Solver
        function solveQuadratic() {
            const a = parseFloat(document.getElementById('quadA').value);
            const b = parseFloat(document.getElementById('quadB').value);
            const c = parseFloat(document.getElementById('quadC').value);
            const out = document.getElementById('quadOutput');

            if (isNaN(a) || isNaN(b) || isNaN(c)) {
                out.innerHTML = `<span class="text-rose-400">يرجى إدخال أرقام صحيحة للمعاملات.</span>`;
                return;
            }

            if (a === 0) {
                out.innerHTML = `<span class="text-amber-400">المعامل (a) لا يمكن أن يساوي الصفر في المعادلة التربيعية.</span>`;
                return;
            }

            // Delta = b^2 - 4ac
            const delta = b * b - 4 * a * c;
            let html = `<div class="font-bold text-slate-200">المميز (Δ) = b² - 4ac = <span class="text-sky-400 font-mono">${delta}</span></div>`;

            if (delta > 0) {
                const x1 = (-b + Math.sqrt(delta)) / (2 * a);
                const x2 = (-b - Math.sqrt(delta
