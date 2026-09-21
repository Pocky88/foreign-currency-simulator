<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>アライアンス・バーンスタイン Dコース スマホ専用シミュレーター</title>
    <style>
        :root {
            --bg-main: #0b0f19;
            --bg-card: #151c2c;
            --bg-card-hover: #1e293b;
            --bg-input: #0f172a;
            --primary-red: #be123c;
            --primary-red-light: #f43f5e;
            --primary-blue: #2563eb;
            --primary-blue-light: #38bdf8;
            --accent-gold: #f59e0b;
            --accent-green: #10b981;
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --border-color: #1e293b;
            --border-highlight: #334155;
            --radius-xl: 20px;
            --radius-lg: 14px;
            --radius-md: 10px;
            --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            --sab: env(safe-area-inset-bottom, 0px);
            --sat: env(safe-area-inset-top, 0px);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: var(--font-sans);
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-primary);
            line-height: 1.5;
            padding-top: var(--sat);
            padding-bottom: calc(75px + var(--sab));
            overflow-x: hidden;
            min-height: 100vh;
        }

        .app-header {
            position: sticky;
            top: 0;
            z-index: 100;
            background: rgba(11, 15, 25, 0.92);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border-color);
            padding: 12px 16px;
        }

        .header-title-box {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .header-title {
            font-size: 1.05rem;
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 6px;
            color: #ffffff;
        }

        .header-badge {
            background: linear-gradient(135deg, var(--primary-red), #881337);
            color: white;
            font-size: 0.68rem;
            font-weight: 700;
            padding: 2px 8px;
            border-radius: 12px;
            letter-spacing: 0.02em;
        }

        /* コース切替セグメントコントロール */
        .course-tabs {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            background: var(--bg-input);
            padding: 3px;
            border-radius: var(--radius-lg);
            border: 1px solid var(--border-color);
        }

        .course-tab {
            background: transparent;
            border: none;
            color: var(--text-secondary);
            padding: 8px 4px;
            font-size: 0.8rem;
            font-weight: 700;
            border-radius: var(--radius-md);
            cursor: pointer;
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            text-align: center;
        }

        .course-tab.active {
            background: var(--primary-red);
            color: #ffffff;
            box-shadow: 0 4px 12px rgba(190, 18, 60, 0.4);
        }

        .content-area {
            padding: 16px;
            max-width: 600px;
            margin: 0 auto;
        }

        .view-section {
            display: none;
            animation: fadeIn 0.25s ease-in-out;
        }

        .view-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(6px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ボトムナビゲーションバー */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            background: rgba(21, 28, 44, 0.95);
            backdrop-filter: blur(16px);
            border-top: 1px solid var(--border-color);
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            padding-bottom: var(--sab);
            box-shadow: 0 -4px 20px rgba(0, 0, 0, 0.4);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 8px 0;
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 0.72rem;
            font-weight: 600;
            cursor: pointer;
            transition: color 0.2s;
        }

        .nav-item .icon {
            font-size: 1.25rem;
            margin-bottom: 2px;
        }

        .nav-item.active {
            color: var(--primary-blue-light);
        }

        .nav-item.active .icon {
            transform: scale(1.1);
            transition: transform 0.2s;
        }

        .metric-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 16px;
        }

        .metric-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-lg);
            padding: 14px;
            position: relative;
            overflow: hidden;
        }

        .metric-card.full-width {
            grid-column: span 2;
        }

        .metric-card::before {
            content: "";
            position: absolute;
            top: 0; left: 0; width: 100%; height: 3px;
            background: var(--primary-blue);
        }

        .metric-card.gold::before { background: var(--accent-gold); }
        .metric-card.red::before { background: var(--primary-red); }
        .metric-card.green::before { background: var(--accent-green); }

        .metric-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
            font-weight: 600;
            margin-bottom: 4px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .metric-val {
            font-size: 1.35rem;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: -0.02em;
        }

        .metric-val.large {
            font-size: 1.6rem;
        }

        .metric-sub {
            font-size: 0.72rem;
            color: var(--text-secondary);
            margin-top: 4px;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-xl);
            padding: 16px;
            margin-bottom: 16px;
        }

        .card-title {
            font-size: 0.95rem;
            font-weight: 700;
            margin-bottom: 14px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            color: #ffffff;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 8px;
        }

        .input-group {
            margin-bottom: 18px;
        }

        .input-header {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 6px;
        }

        .input-label {
            font-size: 0.82rem;
            font-weight: 600;
            color: #cbd5e1;
        }

        .input-value {
            font-size: 1rem;
            font-weight: 800;
            color: var(--primary-blue-light);
        }

        input[type="range"] {
            width: 100%;
            height: 8px;
            background: var(--bg-input);
            border-radius: 4px;
            accent-color: var(--primary-red-light);
            outline: none;
            margin: 6px 0;
        }

        /* クイック微調整ボタン群 */
        .quick-btn-row {
            display: flex;
            gap: 6px;
            margin-top: 6px;
        }

        .btn-quick {
            flex: 1;
            min-height: 38px;
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            color: #e2e8f0;
            font-size: 0.75rem;
            font-weight: 700;
            border-radius: var(--radius-md);
            cursor: pointer;
            transition: all 0.15s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .btn-quick:active {
            background: var(--primary-red);
            border-color: var(--primary-red);
            color: white;
            transform: scale(0.96);
        }

        select {
            width: 100%;
            min-height: 44px;
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            color: white;
            padding: 0 12px;
            font-size: 0.88rem;
            font-weight: 600;
            outline: none;
        }

        .tax-toggle {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            background: var(--bg-input);
            padding: 4px;
            border-radius: var(--radius-md);
        }

        .tax-btn {
            min-height: 40px;
            border: none;
            background: transparent;
            color: var(--text-secondary);
            font-size: 0.82rem;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
        }

        .tax-btn.active {
            background: var(--bg-card-hover);
            color: white;
            box-shadow: 0 2px 8px rgba(0,0,0,0.3);
        }

        .canvas-container {
            position: relative;
            width: 100%;
            height: 280px;
            margin-top: 8px;
            touch-action: none; /* タッチでのスクロール干渉を防止 */
        }

        canvas {
            width: 100% !important;
            height: 100% !important;
            display: block;
        }

        .chart-tooltip-popup {
            position: absolute;
            top: 10px;
            left: 10px;
            right: 10px;
            background: rgba(15, 23, 42, 0.95);
            border: 1px solid var(--primary-blue-light);
            border-radius: var(--radius-md);
            padding: 8px 12px;
            font-size: 0.75rem;
            pointer-events: none;
            display: none;
            backdrop-filter: blur(8px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.6);
            z-index: 10;
        }

        .chart-legend {
            display: flex;
            flex-wrap: wrap;
            gap: 10px 14px;
            justify-content: center;
            margin-top: 12px;
            font-size: 0.75rem;
            font-weight: 600;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .legend-dot {
            width: 10px;
            height: 10px;
            border-radius: 3px;
        }

        .table-wrapper {
            overflow-x: auto;
            border-radius: var(--radius-md);
            border: 1px solid var(--border-color);
            -webkit-overflow-scrolling: touch;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.78rem;
            text-align: right;
            white-space: nowrap;
        }

        th, td {
            padding: 10px 12px;
            border-bottom: 1px solid var(--border-color);
        }

        th {
            background: var(--bg-input);
            color: var(--text-secondary);
            font-weight: 700;
            position: sticky;
            top: 0;
        }

        th:first-child, td:first-child {
            text-align: center;
            position: sticky;
            left: 0;
            background: var(--bg-card);
            z-index: 2;
        }

        th:first-child { background: var(--bg-input); }

        .btn-csv {
            width: 100%;
            min-height: 48px;
            background: linear-gradient(135deg, var(--primary-red), #9f1239);
            color: white;
            border: none;
            border-radius: var(--radius-lg);
            font-size: 0.9rem;
            font-weight: 800;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            box-shadow: 0 4px 15px rgba(190, 18, 60, 0.4);
            margin-top: 14px;
        }

        .btn-csv:active {
            transform: scale(0.98);
        }

        .info-box {
            background: rgba(30, 41, 59, 0.6);
            border: 1px solid rgba(56, 189, 248, 0.2);
            border-radius: var(--radius-md);
            padding: 12px;
            font-size: 0.75rem;
            color: #cbd5e1;
            margin-bottom: 14px;
            line-height: 1.6;
        }
    </style>
</head>
<body>

<header class="app-header">
    <div class="header-title-box">
        <div class="header-title">
            AB米国成長株 Dコース
            <span class="header-badge">毎月分配</span>
        </div>
    </div>
    <div class="course-tabs">
        <button class="course-tab active" id="tabModeReceive" onclick="setCourseMode('receive')">受取コース</button>
        <button class="course-tab" id="tabModeReinvest" onclick="setCourseMode('reinvest')">再投資コース</button>
        <button class="course-tab" id="tabModeCompare" onclick="setCourseMode('compare')">2コース比較</button>
    </div>
</header>

<main class="content-area">
    <section id="viewResult" class="view-section active">
        <!-- メトリックダッシュボード -->
        <div class="metric-grid">
            <div class="metric-card gold full-width">
                <div class="metric-label">
                    <span>毎月の平均受取分配金（手取り）</span>
                    <span style="color:var(--accent-gold);">不労所得</span>
                </div>
                <div class="metric-val large" id="resMonthlyDiv">0.0 万円</div>
                <div class="metric-sub" id="resMonthlyDivSub">運用終了時の月額受取見込み</div>
            </div>

            <div class="metric-card red">
                <div class="metric-label" id="lblTotalDiv">累計受取分配金</div>
                <div class="metric-val" id="resTotalDiv">0 万円</div>
                <div class="metric-sub">期間中に口口座へ振込</div>
            </div>

            <div class="metric-card blue">
                <div class="metric-label">基準価額評価残高</div>
                <div class="metric-val" id="resFundAsset">0 万円</div>
                <div class="metric-sub">元本: <span id="resPrincipal">0</span> 万円</div>
            </div>

            <div class="metric-card green full-width">
                <div class="metric-label">総合トータルリターン</div>
                <div class="metric-val" id="resTotalEval">0 万円</div>
                <div class="metric-sub" id="resTotalEvalSub">評価額 ＋ 累計分配金</div>
            </div>
        </div>

        <!-- インタラクティブCanvasグラフ -->
        <div class="card">
            <div class="card-title">
                <span id="chartTitle">資産推移グラフ</span>
                <span style="font-size:0.7rem; color:var(--text-secondary);">※グラフタップで詳細</span>
            </div>
            <div class="canvas-container">
                <canvas id="mobileChart"></canvas>
                <div class="chart-tooltip-popup" id="chartTooltip"></div>
            </div>
            <div class="chart-legend" id="chartLegend"></div>
        </div>
    </section>

    <section id="viewSettings" class="view-section">
        <div class="info-box">
            💡 <strong>Dコース（予想分配金提示型）の特長</strong><br>
            基準価額に応じて分配金が毎月自動調整されます。「基準価額連動」を選ぶと実際のファンド提示ルールに基づいて精密計算します。
        </div>

        <div class="card">
            <div class="card-title">投資条件の編集</div>

            <!-- 初期投資額 -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">初期投資額（一括）</span>
                    <span class="input-value" id="valInitAsset">300万円</span>
                </div>
                <input type="range" id="inputInitAsset" min="0" max="3000" step="10" value="300">
                <div class="quick-btn-row">
                    <button class="btn-quick" onclick="adjustInput('inputInitAsset', -100)">-100万</button>
                    <button class="btn-quick" onclick="adjustInput('inputInitAsset', -10)">-10万</button>
                    <button class="btn-quick" onclick="adjustInput('inputInitAsset', 10)">+10万</button>
                    <button class="btn-quick" onclick="adjustInput('inputInitAsset', 100)">+100万</button>
                </div>
            </div>

            <!-- 毎月積立額 -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">毎月の積立額</span>
                    <span class="input-value" id="valMonthly">5.0万円</span>
                </div>
                <input type="range" id="inputMonthly" min="0" max="30" step="0.5" value="5.0">
                <div class="quick-btn-row">
                    <button class="btn-quick" onclick="adjustInput('inputMonthly', -1.0)">-1万円</button>
                    <button class="btn-quick" onclick="adjustInput('inputMonthly', -0.5)">-0.5万</button>
                    <button class="btn-quick" onclick="adjustInput('inputMonthly', 0.5)">+0.5万</button>
                    <button class="btn-quick" onclick="adjustInput('inputMonthly', 1.0)">+1万円</button>
                </div>
            </div>

            <!-- 運用期間 -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">運用期間</span>
                    <span class="input-value" id="valYears">15年</span>
                </div>
                <input type="range" id="inputYears" min="1" max="30" step="1" value="15">
                <div class="quick-btn-row">
                    <button class="btn-quick" onclick="adjustInput('inputYears', -5)">-5年</button>
                    <button class="btn-quick" onclick="adjustInput('inputYears', -1)">-1年</button>
                    <button class="btn-quick" onclick="adjustInput('inputYears', 1)">+1年</button>
                    <button class="btn-quick" onclick="adjustInput('inputYears', 5)">+5年</button>
                </div>
            </div>

            <!-- 想定リターン -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">想定トータルリターン（年利）</span>
                    <span class="input-value" id="valReturnRate">13.0%</span>
                </div>
                <input type="range" id="inputReturnRate" min="1.0" max="25.0" step="0.5" value="13.0">
                <div class="quick-btn-row">
                    <button class="btn-quick" onclick="adjustInput('inputReturnRate', -1.0)">-1.0%</button>
                    <button class="btn-quick" onclick="adjustInput('inputReturnRate', -0.5)">-0.5%</button>
                    <button class="btn-quick" onclick="adjustInput('inputReturnRate', 0.5)">+0.5%</button>
                    <button class="btn-quick" onclick="adjustInput('inputReturnRate', 1.0)">+1.0%</button>
                </div>
            </div>

            <!-- 予想分配金ルール -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">1万口あたりの予想分配金</span>
                </div>
                <select id="selectDivRule" onchange="recalculate()">
                    <option value="auto" selected>基準価額連動（Dコース公式提示ルール）</option>
                    <option value="200">固定：200円 / 1万口</option>
                    <option value="300">固定：300円 / 1万口</option>
                    <option value="400">固定：400円 / 1万口</option>
                    <option value="500">固定：500円 / 1万口</option>
                </select>
            </div>

            <!-- 口座区分（税金） -->
            <div class="input-group">
                <div class="input-header">
                    <span class="input-label">税金区分</span>
                </div>
                <div class="tax-toggle">
                    <button class="tax-btn active" id="btnTaxNisa" onclick="setTaxSetting('nisa')">NISA（非課税）</button>
                    <button class="tax-btn" id="btnTaxGeneral" onclick="setTaxSetting('general')">課税 (20.315%)</button>
                </div>
            </div>
        </div>
    </section>

    <section id="viewTable" class="view-section">
        <div class="card">
            <div class="card-title">
                <span>年別資産推移一覧</span>
            </div>
            <div class="table-wrapper">
                <table>
                    <thead>
                        <tr id="tableHeaderRow">
                            <!-- JS挿入 -->
                        </tr>
                    </thead>
                    <tbody id="tableBody">
                        <!-- JS挿入 -->
                    </tbody>
                </table>
            </div>
            <button class="btn-csv" id="btnDownloadCsv">
                <span>📥 CSVデータをダウンロード</span>
            </button>
        </div>
    </section>
</main>

<nav class="bottom-nav">
    <button class="nav-item active" id="navBtnResult" onclick="switchNavTab('Result')">
        <span class="icon">📊</span>
        <span>成果グラフ</span>
    </button>
    <button class="nav-item" id="navBtnSettings" onclick="switchNavTab('Settings')">
        <span class="icon">⚙️</span>
        <span>条件設定</span>
    </button>
    <button class="nav-item" id="navBtnTable" onclick="switchNavTab('Table')">
        <span class="icon">📋</span>
        <span>年別データ</span>
    </button>
</nav>

<script>
let currentCourseMode = 'receive'; // 'receive', 'reinvest', 'compare'
let currentTaxSetting = 'nisa'; // 'nisa', 'general'
let currentNavTab = 'Result';

const inputs = {
    initAsset: document.getElementById('inputInitAsset'),
    monthly: document.getElementById('inputMonthly'),
    years: document.getElementById('inputYears'),
    returnRate: document.getElementById('inputReturnRate'),
    divRule: document.getElementById('selectDivRule')
};

const labels = {
    initAsset: document.getElementById('valInitAsset'),
    monthly: document.getElementById('valMonthly'),
    years: document.getElementById('valYears'),
    returnRate: document.getElementById('valReturnRate')
};

const canvas = document.getElementById('mobileChart');
const ctx = canvas.getContext('2d');
const tooltip = document.getElementById('chartTooltip');

let cachedRecData = [];
let cachedReinvData = [];

Object.keys(inputs).forEach(key => {
    if (inputs[key].tagName === 'INPUT') {
        inputs[key].addEventListener('input', () => {
            updateLabelDisplays();
            recalculate();
        });
    }
});

function updateLabelDisplays() {
    labels.initAsset.innerText = `${inputs.initAsset.value}万円`;
    labels.monthly.innerText = `${parseFloat(inputs.monthly.value).toFixed(1)}万円`;
    labels.years.innerText = `${inputs.years.value}年`;
    labels.returnRate.innerText = `${parseFloat(inputs.returnRate.value).toFixed(1)}%`;
}

function adjustInput(id, delta) {
    const el = document.getElementById(id);
    let val = parseFloat(el.value) + delta;
    const min = parseFloat(el.min);
    const max = parseFloat(el.max);
    if (val < min) val = min;
    if (val > max) val = max;
    el.value = val;
    updateLabelDisplays();
    recalculate();
}

function switchNavTab(tabName) {
    currentNavTab = tabName;
    document.querySelectorAll('.view-section').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));

    document.getElementById(`view${tabName}`).classList.add('active');
    document.getElementById(`navBtn${tabName}`).classList.add('active');

    if (tabName === 'Result') {
        // グラフの再描画（タブ切替時のサイズ崩れ防止）
        setTimeout(renderChart, 50);
    }
}

function setCourseMode(mode) {
    currentCourseMode = mode;
    document.getElementById('tabModeReceive').classList.toggle('active', mode === 'receive');
    document.getElementById('tabModeReinvest').classList.toggle('active', mode === 'reinvest');
    document.getElementById('tabModeCompare').classList.toggle('active', mode === 'compare');
    recalculate();
}

function setTaxSetting(tax) {
    currentTaxSetting = tax;
    document.getElementById('btnTaxNisa').classList.toggle('active', tax === 'nisa');
    document.getElementById('btnTaxGeneral').classList.toggle('active', tax === 'general');
    recalculate();
}

function getDCourseDivPer10k(nav, ruleSetting) {
    if (ruleSetting !== 'auto') {
        return parseFloat(ruleSetting);
    }
    // アライアンス・バーンスタイン Dコース公式予想分配金提示ルール
    if (nav >= 14000) return 500;
    if (nav >= 13000) return 400;
    if (nav >= 12000) return 300;
    if (nav >= 11000) return 200;
    if (nav >= 10000) return 100;
    return 0; // 10,000円未満は分配金なし
}

function simulate(isReinvest) {
    const initYen = parseFloat(inputs.initAsset.value) * 10000;
    const monthlyYen = parseFloat(inputs.monthly.value) * 10000;
    const totalYears = parseInt(inputs.years.value);
    const annualReturn = parseFloat(inputs.returnRate.value) / 100;
    const monthlyReturn = annualReturn / 12;
    const rule = inputs.divRule.value;
    const taxRate = currentTaxSetting === 'general' ? 0.20315 : 0;

    const baseNAV = 10000;
    let currentNAV = baseNAV;
    let units = (initYen / baseNAV) * 10000;
    let principal = initYen;

    let cumDivYen = 0;
    const monthlyData = [];

    const totalMonths = totalYears * 12;
    for (let m = 1; m <= totalMonths; m++) {
        // 月初積立
        if (monthlyYen > 0) {
            units += (monthlyYen / currentNAV) * 10000;
            principal += monthlyYen;
        }

        // 月中運用成長
        currentNAV = currentNAV * (1 + monthlyReturn);

        // 月末分配金
        const divPer10k = getDCourseDivPer10k(currentNAV, rule);
        const grossDiv = units * (divPer10k / 10000);
        const netDiv = grossDiv * (1 - taxRate);

        if (isReinvest) {
            // 再投資：分配落ち後NAVで再投資買付
            currentNAV = Math.max(100, currentNAV - divPer10k);
            units += (netDiv / currentNAV) * 10000;
            cumDivYen += netDiv;
        } else {
            // 受取：現金として受取
            currentNAV = Math.max(100, currentNAV - divPer10k);
            cumDivYen += netDiv;
        }

        const fundAsset = units * (currentNAV / 10000);

        monthlyData.push({
            month: m,
            year: m / 12,
            principal: principal,
            nav: currentNAV,
            units: units,
            monthlyDivNet: netDiv,
            cumDivNet: cumDivYen,
            fundAsset: fundAsset,
            totalEval: fundAsset + (isReinvest ? 0 : cumDivYen)
        });
    }

    return monthlyData;
}

function recalculate() {
    cachedRecData = simulate(false);
    cachedReinvData = simulate(true);

    const finalRec = cachedRecData[cachedRecData.length - 1];
    const finalReinv = cachedReinvData[cachedReinvData.length - 1];

    const elResMonthly = document.getElementById('resMonthlyDiv');
    const elResMonthlySub = document.getElementById('resMonthlyDivSub');
    const elResTotalDiv = document.getElementById('resTotalDiv');
    const elLblTotalDiv = document.getElementById('lblTotalDiv');
    const elResFundAsset = document.getElementById('resFundAsset');
    const elResPrincipal = document.getElementById('resPrincipal');
    const elResTotalEval = document.getElementById('resTotalEval');
    const elResTotalEvalSub = document.getElementById('resTotalEvalSub');

    if (currentCourseMode === 'receive') {
        const last12 = cachedRecData.slice(-12);
        const avgMonthly = last12.reduce((acc, d) => acc + d.monthlyDivNet, 0) / 12;

        elResMonthly.innerText = `${(avgMonthly / 10000).toFixed(1)} 万円`;
        elResMonthlySub.innerText = "運用終了時の手取り月額分配金";
        elLblTotalDiv.innerText = "累計受取分配金";
        elResTotalDiv.innerText = `${Math.round(finalRec.cumDivNet / 10000)} 万円`;
        elResFundAsset.innerText = `${Math.round(finalRec.fundAsset / 10000)} 万円`;
        elResPrincipal.innerText = `${Math.round(finalRec.principal / 10000)}`;
        elResTotalEval.innerText = `${Math.round(finalRec.totalEval / 10000)} 万円`;
        elResTotalEvalSub.innerText = `元本差額: +${Math.round((finalRec.totalEval - finalRec.principal) / 10000)} 万円`;

        document.getElementById('chartTitle').innerText = "受取コース 資産成長内訳";
        document.getElementById('chartLegend').innerHTML = `
            <div class="legend-item"><div class="legend-dot" style="background:#f59e0b;"></div><span>累計受取分配金</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#2563eb;"></div><span>基準価額残高</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#94a3b8;"></div><span>元本累計</span></div>
        `;
    } else if (currentCourseMode === 'reinvest') {
        elResMonthly.innerText = "0.0 万円 (再投資)";
        elResMonthlySub.innerText = "分配金は全額自動再投資されます";
        elLblTotalDiv.innerText = "通算運用益";
        elResTotalDiv.innerText = `${Math.round((finalReinv.fundAsset - finalReinv.principal) / 10000)} 万円`;
        elResFundAsset.innerText = `${Math.round(finalReinv.fundAsset / 10000)} 万円`;
        elResPrincipal.innerText = `${Math.round(finalReinv.principal / 10000)}`;
        elResTotalEval.innerText = `${Math.round(finalReinv.fundAsset / 10000)} 万円`;
        elResTotalEvalSub.innerText = "全分配金を再投資した複利トータル資産";

        document.getElementById('chartTitle').innerText = "再投資コース 複利資産成長";
        document.getElementById('chartLegend').innerHTML = `
            <div class="legend-item"><div class="legend-dot" style="background:#be123c;"></div><span>再投資 総資産額</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#94a3b8;"></div><span>元本累計</span></div>
        `;
    } else {
        // 2コース比較
        const diff = finalReinv.fundAsset - finalRec.totalEval;
        elResMonthly.innerText = `差額: ${(diff / 10000).toFixed(1)} 万円`;
        elResMonthlySub.innerText = "再投資コースがどれだけ上回るか";
        elLblTotalDiv.innerText = "受取: 累計分配金";
        elResTotalDiv.innerText = `${Math.round(finalRec.cumDivNet / 10000)} 万円`;
        elResFundAsset.innerText = `${Math.round(finalRec.fundAsset / 10000)} 万円`;
        elResPrincipal.innerText = `${Math.round(finalRec.principal / 10000)}`;
        elResTotalEval.innerText = `${Math.round(finalReinv.fundAsset / 10000)} 万円 (再投資)`;
        elResTotalEvalSub.innerText = `受取コース総合: ${Math.round(finalRec.totalEval / 10000)} 万円`;

        document.getElementById('chartTitle').innerText = "受取 vs 再投資 資産比較";
        document.getElementById('chartLegend').innerHTML = `
            <div class="legend-item"><div class="legend-dot" style="background:#be123c;"></div><span>再投資コース</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#f59e0b;"></div><span>受取総合評価</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#2563eb;"></div><span>受取 基準価額残高</span></div>
            <div class="legend-item"><div class="legend-dot" style="background:#94a3b8;"></div><span>元本累計</span></div>
        `;
    }

    renderChart();
    renderTable();
}

let activePointIndex = -1;

function renderChart() {
    if (!canvas) return;
    const dpr = window.devicePixelRatio || 1;
    const rect = canvas.getBoundingClientRect();
    if (rect.width === 0 || rect.height === 0) return;

    canvas.width = rect.width * dpr;
    canvas.height = rect.height * dpr;
    ctx.scale(dpr, dpr);

    const w = rect.width;
    const h = rect.height;
    ctx.clearRect(0, 0, w, h);

    const padL = 48;
    const padB = 30;
    const padT = 15;
    const padR = 15;
    const chartW = w - padL - padR;
    const chartH = h - padT - padB;

    const years = parseInt(inputs.years.value);
    const filteredRec = [cachedRecData[0], ...cachedRecData.filter(d => d.month % 12 === 0)];
    const filteredReinv = [cachedReinvData[0], ...cachedReinvData.filter(d => d.month % 12 === 0)];

    // 最大値決定
    let maxVal = 0;
    if (currentCourseMode === 'receive') {
        maxVal = Math.max(...filteredRec.map(d => d.totalEval));
    } else if (currentCourseMode === 'reinvest') {
        maxVal = Math.max(...filteredReinv.map(d => d.fundAsset));
    } else {
        maxVal = Math.max(...filteredRec.map(d => d.totalEval), ...filteredReinv.map(d => d.fundAsset));
    }
    maxVal = Math.ceil((maxVal * 1.08) / 100000) * 100000;

    // Y軸グリッド
    const rows = 4;
    ctx.strokeStyle = '#1e293b';
    ctx.lineWidth = 1;
    ctx.fillStyle = '#94a3b8';
    ctx.font = '10px sans-serif';
    ctx.textAlign = 'right';

    for (let i = 0; i <= rows; i++) {
        const y = padT + (chartH / rows) * i;
        const val = Math.round((maxVal * (rows - i) / rows) / 10000);
        ctx.beginPath();
        ctx.moveTo(padL, y);
        ctx.lineTo(w - padR, y);
        ctx.stroke();
        ctx.fillText(`${val}万`, padL - 6, y + 3);
    }

    // X軸（年数）
    ctx.textAlign = 'center';
    const stepX = chartW / years;
    const xInterval = years > 15 ? 5 : (years > 8 ? 2 : 1);

    for (let yr = 0; yr <= years; yr++) {
        if (yr % xInterval === 0 || yr === years) {
            const x = padL + yr * stepX;
            ctx.fillText(`${yr}年`, x, h - padB + 16);
        }
    }

    function getX(yr) { return padL + yr * stepX; }
    function getY(val) { return padT + chartH - (val / maxVal) * chartH; }

    if (currentCourseMode === 'receive') {
        // 積層面グラフ
        drawArea(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.totalEval) })), 'rgba(245, 158, 11, 0.2)');
        drawArea(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), 'rgba(37, 99, 235, 0.3)');
        drawArea(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.principal) })), 'rgba(148, 163, 184, 0.15)');

        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.totalEval) })), '#f59e0b', 2.5);
        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), '#2563eb', 2.5);
        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.principal) })), '#94a3b8', 1.5, true);
    } else if (currentCourseMode === 'reinvest') {
        drawArea(filteredReinv.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), 'rgba(190, 18, 60, 0.25)');
        drawLine(filteredReinv.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), '#be123c', 2.5);
        drawLine(filteredReinv.map(d => ({ x: getX(d.year), y: getY(d.principal) })), '#94a3b8', 1.5, true);
    } else {
        drawLine(filteredReinv.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), '#be123c', 2.5);
        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.totalEval) })), '#f59e0b', 2.5);
        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.fundAsset) })), '#2563eb', 1.5, true);
        drawLine(filteredRec.map(d => ({ x: getX(d.year), y: getY(d.principal) })), '#94a3b8', 1.5, true);
    }

    // タッチ選択中の垂直ガイドバー描画
    if (activePointIndex >= 0 && activePointIndex <= years) {
        const activeX = getX(activePointIndex);
        ctx.strokeStyle = '#38bdf8';
        ctx.lineWidth = 1.5;
        ctx.setLineDash([4, 4]);
        ctx.beginPath();
        ctx.moveTo(activeX, padT);
        ctx.lineTo(activeX, padT + chartH);
        ctx.stroke();
        ctx.setLineDash([]);
    }
}

function drawLine(pts, color, width, isDashed = false) {
    ctx.beginPath();
    if (isDashed) ctx.setLineDash([3, 3]);
    else ctx.setLineDash([]);
    pts.forEach((p, i) => {
        if (i === 0) ctx.moveTo(p.x, p.y);
        else ctx.lineTo(p.x, p.y);
    });
    ctx.strokeStyle = color;
    ctx.lineWidth = width;
    ctx.stroke();
    ctx.setLineDash([]);

    pts.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, 3, 0, Math.PI * 2);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.strokeStyle = color;
        ctx.lineWidth = 1.5;
        ctx.stroke();
    });
}

function drawArea(pts, color) {
    if (pts.length === 0) return;
    const padT = 15;
    const padB = 30;
    const h = canvas.height / (window.devicePixelRatio || 1);
    ctx.beginPath();
    ctx.moveTo(pts[0].x, h - padB);
    pts.forEach(p => ctx.lineTo(p.x, p.y));
    ctx.lineTo(pts[pts.length - 1].x, h - padB);
    ctx.closePath();
    ctx.fillStyle = color;
    ctx.fill();
}

function handleTouchMove(e) {
    const rect = canvas.getBoundingClientRect();
    const touchX = (e.touches ? e.touches[0].clientX : e.clientX) - rect.left;
    const padL = 48;
    const padR = 15;
    const chartW = rect.width - padL - padR;
    const years = parseInt(inputs.years.value);

    let yearIdx = Math.round(((touchX - padL) / chartW) * years);
    if (yearIdx < 0) yearIdx = 0;
    if (yearIdx > years) yearIdx = years;

    activePointIndex = yearIdx;
    renderChart();

    const recItem = cachedRecData[yearIdx * 12] || cachedRecData[cachedRecData.length - 1];
    const reinvItem = cachedReinvData[yearIdx * 12] || cachedReinvData[cachedReinvData.length - 1];

    tooltip.style.display = 'block';
    if (currentCourseMode === 'receive') {
        tooltip.innerHTML = `
            <strong>【${yearIdx}年目】</strong> 元本: ${(recItem.principal/10000).toFixed(1)}万<br>
            ・基準価額評価: <span style="color:#38bdf8;font-weight:700;">${(recItem.fundAsset/10000).toFixed(1)}万円</span><br>
            ・累計受取分配金: <span style="color:#f59e0b;font-weight:700;">${(recItem.cumDivNet/10000).toFixed(1)}万円</span><br>
            ・総合評価額: <span style="color:#4ade80;font-weight:700;">${(recItem.totalEval/10000).toFixed(1)}万円</span>
        `;
    } else if (currentCourseMode === 'reinvest') {
        tooltip.innerHTML = `
            <strong>【${yearIdx}年目】</strong> 元本: ${(reinvItem.principal/10000).toFixed(1)}万<br>
            ・再投資 総資産額: <span style="color:#f43f5e;font-weight:700;">${(reinvItem.fundAsset/10000).toFixed(1)}万円</span><br>
            ・通算運用益: <span style="color:#4ade80;font-weight:700;">+${((reinvItem.fundAsset - reinvItem.principal)/10000).toFixed(1)}万円</span>
        `;
    } else {
        tooltip.innerHTML = `
            <strong>【${yearIdx}年目】</strong> 元本: ${(recItem.principal/10000).toFixed(1)}万<br>
            ・受取総合評価: <span style="color:#f59e0b;font-weight:700;">${(recItem.totalEval/10000).toFixed(1)}万円</span><br>
            ・再投資総資産: <span style="color:#f43f5e;font-weight:700;">${(reinvItem.fundAsset/10000).toFixed(1)}万円</span>
        `;
    }
}

canvas.addEventListener('touchstart', handleTouchMove, { passive: true });
canvas.addEventListener('touchmove', handleTouchMove, { passive: true });
canvas.addEventListener('mousemove', handleTouchMove);

canvas.addEventListener('touchend', () => {
    setTimeout(() => {
        tooltip.style.display = 'none';
        activePointIndex = -1;
        renderChart();
    }, 2500);
});

function renderTable() {
    const headerRow = document.getElementById('tableHeaderRow');
    const body = document.getElementById('tableBody');

    if (currentCourseMode === 'compare') {
        headerRow.innerHTML = `
            <th>経過年</th>
            <th>元本</th>
            <th>受取残高</th>
            <th>受取分配金</th>
            <th>受取総合</th>
            <th>再投資資産</th>
        `;
    } else if (currentCourseMode === 'reinvest') {
        headerRow.innerHTML = `
            <th>経過年</th>
            <th>元本</th>
            <th>基準価額残高</th>
            <th>通算運用益</th>
            <th>総資産額</th>
        `;
    } else {
        headerRow.innerHTML = `
            <th>経過年</th>
            <th>元本</th>
            <th>基準価額残高</th>
            <th>年間分配金</th>
            <th>累計分配金</th>
            <th>総合評価額</th>
        `;
    }

    const filteredRec = cachedRecData.filter(d => d.month % 12 === 0);
    const filteredReinv = cachedReinvData.filter(d => d.month % 12 === 0);

    let html = '';
    for (let i = 0; i < filteredRec.length; i++) {
        const r = filteredRec[i];
        const rv = filteredReinv[i];
        const prevCum = i === 0 ? 0 : filteredRec[i - 1].cumDivNet;
        const annualDiv = r.cumDivNet - prevCum;

        if (currentCourseMode === 'compare') {
            html += `
                <tr>
                    <td>${r.year}年目</td>
                    <td>${(r.principal / 10000).toFixed(1)}万</td>
                    <td style="color:#38bdf8;">${(r.fundAsset / 10000).toFixed(1)}万</td>
                    <td style="color:#f59e0b;">${(r.cumDivNet / 10000).toFixed(1)}万</td>
                    <td style="font-weight:700;">${(r.totalEval / 10000).toFixed(1)}万</td>
                    <td style="color:#f43f5e; font-weight:700;">${(rv.fundAsset / 10000).toFixed(1)}万</td>
                </tr>
            `;
        } else if (currentCourseMode === 'reinvest') {
            html += `
                <tr>
                    <td>${rv.year}年目</td>
                    <td>${(rv.principal / 10000).toFixed(1)}万</td>
                    <td style="color:#f43f5e; font-weight:700;">${(rv.fundAsset / 10000).toFixed(1)}万</td>
                    <td style="color:#4ade80;">+${((rv.fundAsset - rv.principal) / 10000).toFixed(1)}万</td>
                    <td style="font-weight:700;">${(rv.fundAsset / 10000).toFixed(1)}万</td>
                </tr>
            `;
        } else {
            html += `
                <tr>
                    <td>${r.year}年目</td>
                    <td>${(r.principal / 10000).toFixed(1)}万</td>
                    <td style="color:#38bdf8;">${(r.fundAsset / 10000).toFixed(1)}万</td>
                    <td style="color:#f59e0b;">${(annualDiv / 10000).toFixed(1)}万</td>
                    <td style="color:#f59e0b; font-weight:700;">${(r.cumDivNet / 10000).toFixed(1)}万</td>
                    <td style="font-weight:700; color:#4ade80;">${(r.totalEval / 10000).toFixed(1)}万</td>
                </tr>
            `;
        }
    }
    body.innerHTML = html;
}

// CSVダウンロード処理（UTF-8 BOM付き）
document.getElementById('btnDownloadCsv').addEventListener('click', () => {
    const filteredRec = cachedRecData.filter(d => d.month % 12 === 0);
    const filteredReinv = cachedReinvData.filter(d => d.month % 12 === 0);

    let csv = "\uFEFF経過年,元本(円),受取_基準価額残高(円),受取_累計分配金(円),受取_総合評価(円),再投資_総資産(円)\n";

    for (let i = 0; i < filteredRec.length; i++) {
        const r = filteredRec[i];
        const rv = filteredReinv[i];
        csv += `${r.year},${Math.round(r.principal)},${Math.round(r.fundAsset)},${Math.round(r.cumDivNet)},${Math.round(r.totalEval)},${Math.round(rv.fundAsset)}\n`;
    }

    const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = `AB米国成長株Dコース_試算結果.csv`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
});

window.addEventListener('resize', () => {
    renderChart();
});

window.onload = function() {
    updateLabelDisplays();
    recalculate();
};
</script>
</body>
</html>
