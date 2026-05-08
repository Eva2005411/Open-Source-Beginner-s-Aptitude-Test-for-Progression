<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>开源人格测试 | 找到你的开源超能力</title>
    <!-- html2canvas 库：用于生成海报 -->
    <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
    <!-- Google Fonts 提升字体质感 -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #f6f9fc 0%, #eef2f5 100%);
            font-family: 'Inter', sans-serif;
            color: #1a2c3e;
            padding: 2rem 1.5rem;
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
        }

        /* 头部区域 */
        .hero {
            text-align: center;
            margin-bottom: 3rem;
        }
        .hero h1 {
            font-size: 2.8rem;
            font-weight: 800;
            background: linear-gradient(135deg, #1e6f3f, #2b8c5e, #1e88e5);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.01em;
            margin-bottom: 0.5rem;
        }
        .hero .badge {
            background: #e9ecef;
            display: inline-block;
            padding: 0.3rem 1rem;
            border-radius: 40px;
            font-size: 0.85rem;
            font-weight: 600;
            color: #2c5a7a;
            margin-bottom: 1rem;
            backdrop-filter: blur(4px);
        }
        .hero p {
            font-size: 1.2rem;
            color: #2c3e4e;
            max-width: 650px;
            margin: 0 auto;
            line-height: 1.4;
        }

        /* 主卡片 */
        .card {
            background: rgba(255,255,255,0.85);
            backdrop-filter: blur(2px);
            border-radius: 2rem;
            box-shadow: 0 20px 35px -12px rgba(0,0,0,0.1);
            padding: 2rem 2rem 2rem 2rem;
            margin-bottom: 2rem;
            transition: all 0.2s;
            border: 1px solid rgba(255,255,255,0.6);
        }

        .question-block {
            margin-bottom: 2rem;
            border-bottom: 1px solid #e2edf2;
            padding-bottom: 1.5rem;
        }
        .question-text {
            font-weight: 700;
            font-size: 1.2rem;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
            color: #1e4663;
        }
        .q-num {
            background: #2b8c5e20;
            color: #1e6f3f;
            font-weight: 800;
            width: 32px;
            height: 32px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border-radius: 60px;
            font-size: 0.9rem;
        }
        .options {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-top: 0.5rem;
        }
        .option-label {
            background: #f8fafc;
            border: 1px solid #cddfe7;
            border-radius: 60px;
            padding: 0.6rem 1.2rem;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 500;
            display: inline-flex;
            align-items: center;
            gap: 0.4rem;
            flex: 1 0 auto;
            min-width: 180px;
            backdrop-filter: blur(2px);
        }
        .option-label:hover {
            background: #e3f0ec;
            border-color: #2b8c5e;
            transform: translateY(-1px);
        }
        input[type="radio"] {
            accent-color: #2b8c5e;
            width: 18px;
            height: 18px;
            margin-right: 6px;
        }
        .nickname-area {
            margin-bottom: 2rem;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 1rem;
            background: #f0f4f7;
            padding: 1rem 1.5rem;
            border-radius: 60px;
        }
        .nickname-area label {
            font-weight: 600;
            color: #1e4663;
        }
        #nickname {
            flex: 2;
            min-width: 180px;
            padding: 0.6rem 1rem;
            border-radius: 40px;
            border: 1px solid #cbdde6;
            background: white;
            font-family: inherit;
            outline: none;
            transition: 0.2s;
        }
        #nickname:focus {
            border-color: #2b8c5e;
            box-shadow: 0 0 0 2px rgba(43,140,94,0.2);
        }
        .btn-group {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 1.5rem;
            margin-bottom: 1rem;
        }
        .btn {
            border: none;
            padding: 0.8rem 2rem;
            font-weight: 600;
            font-family: inherit;
            border-radius: 60px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.2s;
            background: white;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
        }
        .btn-primary {
            background: #1e6f3f;
            color: white;
            box-shadow: 0 8px 18px rgba(30,111,63,0.25);
        }
        .btn-primary:hover {
            background: #145c34;
            transform: translateY(-2px);
        }
        .btn-secondary {
            background: #eef2f5;
            border: 1px solid #bdd3df;
        }
        .btn-secondary:hover {
            background: #e2e9ef;
        }

        /* 结果展示区 */
        .result-area {
            display: none;
            margin-top: 2rem;
            animation: fadeInUp 0.4s ease;
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(20px);}
            to { opacity: 1; transform: translateY(0px);}
        }
        .personality-card {
            background: linear-gradient(135deg, #ffffff 0%, #fef9e8 100%);
            border-radius: 2rem;
            padding: 1.8rem;
            box-shadow: 0 12px 24px -12px rgba(0,0,0,0.2);
            border: 1px solid #ffe8cf;
            margin-bottom: 1.5rem;
        }
        .personality-header {
            display: flex;
            align-items: center;
            gap: 1rem;
            flex-wrap: wrap;
            border-bottom: 2px dashed #d4e2e9;
            padding-bottom: 1rem;
            margin-bottom: 1rem;
        }
        .personality-icon {
            font-size: 3.5rem;
        }
        .personality-name {
            font-size: 2rem;
            font-weight: 800;
            background: linear-gradient(120deg, #1e6f3f, #287b5a);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
        }
        .personality-desc {
            font-size: 1rem;
            line-height: 1.5;
            color: #2c3e4e;
            background: #eef3fa;
            padding: 0.8rem 1.2rem;
            border-radius: 1.2rem;
            margin: 1rem 0;
        }
        .recommend-title {
            font-weight: 700;
            font-size: 1.2rem;
            margin: 1rem 0 0.8rem 0;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .project-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        .project-item {
            background: #f8fafc;
            padding: 1rem;
            border-radius: 1.2rem;
            transition: 0.2s;
            border-left: 5px solid #2b8c5e;
        }
        .project-name {
            font-weight: 700;
            color: #1a5d7a;
        }
        .project-link, .issue-link {
            font-size: 0.85rem;
            word-break: break-all;
            color: #2b8c5e;
            text-decoration: none;
            font-weight: 500;
            display: inline-block;
            margin-top: 6px;
            margin-right: 1rem;
        }
        .project-link:hover, .issue-link:hover {
            text-decoration: underline;
        }
        .tag {
            background: #e2eef4;
            padding: 0.2rem 0.8rem;
            border-radius: 40px;
            font-size: 0.7rem;
            font-weight: 600;
            display: inline-block;
            margin-left: 0.5rem;
        }

        .poster-btn {
            margin-top: 20px;
            text-align: center;
        }
        .footer-note {
            margin-top: 2rem;
            font-size: 0.8rem;
            text-align: center;
            color: #6a7f8f;
            border-top: 1px solid #d0dfe8;
            padding-top: 1.5rem;
        }

        @media (max-width: 700px) {
            body { padding: 1rem; }
            .card { padding: 1.2rem; }
            .option-label { min-width: 100%;}
        }
        .error-msg {
            color: #c7254e;
            background: #f9e6e9;
            border-radius: 40px;
            padding: 0.5rem 1rem;
            text-align: center;
            margin-top: 1rem;
            display: none;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="hero">
        <div class="badge">✨ 开源新人体验测试 · 趣味人格版</div>
        <h1>🧩 开源社区人格测试</h1>
        <p>从文档到代码，从流程到洞察 — 测测你是哪种开源贡献者，解锁适合你的第一个 Good First Issue</p>
    </div>

    <div class="card">
        <div class="nickname-area">
            <label>🌟 你的昵称 / ID（用于海报）</label>
            <input type="text" id="nickname" placeholder="例如：开源小萌新 / 代码浪人" autocomplete="off">
        </div>

        <!-- 问卷动态插入 -->
        <form id="quizForm">
            <div id="questionsContainer"></div>
        </form>

        <div class="btn-group">
            <button class="btn btn-primary" id="submitBtn">🚀 揭示人格 · 获取推荐</button>
            <button class="btn btn-secondary" id="resetBtn">🔄 重新测试</button>
        </div>
        <div id="errorMsg" class="error-msg"></div>
    </div>

    <!-- 结果展示区 -->
    <div id="resultArea" class="result-area"></div>

    <div class="footer-note">
        🌱 基于“开源社区新人体验测试”任务设计 | 融合资源基础观(RBV)与自组织理论 —— 你的独特“VRIN”人格是开源社区多样性的重要组成
    </div>
</div>

<script>
    // ---------- 问卷设计：10个情境问题，每个选项影响 [文档Doc, 流程Flow, 代码Code, 问题捕捉Issue] 分值 ----------
    const QUESTIONS = [
        { text: "当你第一次进入一个陌生的GitHub仓库，你最自然的做法是？", options: [
            { text: "📖 仔仔细细阅读 README，了解项目概况和使用方式", scores: { doc:3, flow:0, code:0, issue:1 } },
            { text: "🔁 找 CONTRIBUTING.md 或贡献指南，了解提交 PR 流程", scores: { doc:1, flow:3, code:0, issue:1 } },
            { text: "💻 直接克隆代码，尝试本地编译/运行，看看功能", scores: { doc:0, flow:0, code:3, issue:1 } },
            { text: "🐞 打开 Issues 列表，寻找 'good first issue' 或待处理bug", scores: { doc:0, flow:1, code:0, issue:3 } }
        ] },
        { text: "对开源贡献来说，你最享受以下哪个环节？", options: [
            { text: "📝 完善文档、补充注释、编写示例", scores: { doc:3, flow:1, code:0, issue:1 } },
            { text: "⚙️ 梳理贡献流程，设计自动化测试或PR模板", scores: { doc:1, flow:3, code:1, issue:0 } },
            { text: "🛠️ 修复小型bug，实现简单功能，编写代码", scores: { doc:0, flow:0, code:3, issue:2 } },
            { text: "🔍 复现漏洞、分类issue，帮助维护者定位问题", scores: { doc:0, flow:1, code:0, issue:3 } }
        ] },
        { text: "遇到一个复杂的Issue描述，你会优先？", options: [
            { text: "先确认项目文档有没有相关设计说明", scores: { doc:3, flow:1, code:0, issue:1 } },
            { text: "寻找社区沟通渠道（Slack/Discord）询问流程", scores: { doc:0, flow:3, code:0, issue:2 } },
            { text: "尝试在本地复现问题，阅读相关源码", scores: { doc:0, flow:0, code:3, issue:2 } },
            { text: "补充复现步骤，在issue下留言帮助理清线索", scores: { doc:1, flow:0, code:0, issue:3 } }
        ] },
        { text: "关于贡献指南（CONTRIBUTING），你通常的感觉是？", options: [
            { text: "我喜欢贡献指南清晰，会严格按照指南提交", scores: { doc:2, flow:3, code:0, issue:1 } },
            { text: "如果指南缺失，我愿意帮忙撰写或补充", scores: { doc:3, flow:2, code:0, issue:1 } },
            { text: "对于复杂的Git操作会有点头疼", scores: { doc:1, flow:0, code:1, issue:2 } },  // 偏向流程体验差变问题捕捉
            { text: "我会尝试绕过指南直接提PR，但可能不规范", scores: { doc:0, flow:0, code:2, issue:1 } }
        ] },
        { text: "在本地搭建开发环境时，你更关注？", options: [
            { text: "README如果有setup步骤就完美", scores: { doc:3, flow:1, code:0, issue:1 } },
            { text: "我习惯快速搞定环境，关注编译流程的自动化", scores: { doc:1, flow:3, code:1, issue:0 } },
            { text: "喜欢折腾，即使指引不完善也能搞定", scores: { doc:0, flow:0, code:3, issue:1 } },
            { text: "遇到环境问题会记录并分享给社区改进", scores: { doc:1, flow:1, code:0, issue:3 } }
        ] },
        { text: "如果让你选择第一个开源贡献，你会选？", options: [
            { text: "📄 修复文档拼写错误或更新过时说明", scores: { doc:3, flow:0, code:0, issue:1 } },
            { text: "📌 改进PR模版或 issue 分类标签指导", scores: { doc:1, flow:3, code:0, issue:1 } },
            { text: "🧪 修复一个 tagged with 'good first issue' 的简单代码bug", scores: { doc:0, flow:0, code:3, issue:2 } },
            { text: "🗂️ 帮维护者 triage issue，重现或补充必要信息", scores: { doc:1, flow:1, code:0, issue:3 } }
        ] },
        { text: "对于Git和GitHub协作流程，你的熟悉度？", options: [
            { text: "还在学习，希望有清晰的指引", scores: { doc:2, flow:1, code:0, issue:2 } },
            { text: "比较熟悉 PR 规范，乐意帮忙完善社区流程", scores: { doc:1, flow:3, code:1, issue:1 } },
            { text: "熟练使用Git，但更享受代码层面的协作", scores: { doc:0, flow:0, code:3, issue:0 } },
            { text: "可以帮新人解答 Git 疑问，发现流程痛点", scores: { doc:0, flow:2, code:0, issue:3 } }
        ] },
        { text: "当你发现一个潜在可贡献的改进点时，第一步是？", options: [
            { text: "确认相关文档是否需要协同更新", scores: { doc:3, flow:0, code:0, issue:2 } },
            { text: "搜索有没有类似讨论或贡献规则", scores: { doc:1, flow:2, code:0, issue:2 } },
            { text: "直接写代码demo证明可行性", scores: { doc:0, flow:0, code:3, issue:1 } },
            { text: "创建issue详细描述问题和方案", scores: { doc:0, flow:0, code:1, issue:3 } }
        ] },
        { text: "在社区中，你认为你最突出的价值是？", options: [
            { text: "文档驱动，让项目更容易上手", scores: { doc:3, flow:1, code:0, issue:1 } },
            { text: "建立清晰治理规则和工作流", scores: { doc:1, flow:3, code:0, issue:1 } },
            { text: "产出可靠代码，解决技术债", scores: { doc:0, flow:0, code:3, issue:1 } },
            { text: "发现隐藏bug和新手障碍，提升社区体验", scores: { doc:1, flow:1, code:0, issue:3 } }
        ] },
        { text: "对于未知项目，你觉得最阻碍你贡献的因素是？ (反向但映射优势)', options: [
            { text: "文档不清晰不知道如何开始 → 我想改进文档", scores: { doc:3, flow:1, code:0, issue:1 } },
            { text: "贡献流程复杂 → 我愿意梳理流程", scores: { doc:0, flow:3, code:0, issue:2 } },
            { text: "代码难以理解 → 我会尝试重构或写注释", scores: { doc:1, flow:0, code:2, issue:1 } },
            { text: "缺少友好issue → 可帮忙筛选新人任务", scores: { doc:0, flow:1, code:0, issue:3 } }
        ] }
    ];

    // 人格映射数据 + 推荐内容 (项目 + Good First Issue 示例)
    const PERSONALITY_MAP = {
        docMaster: {
            name: "📚 文档整理官",
            icon: "📖✨",
            description: "你拥有天生的文档敏感度，擅长将复杂信息结构清晰，提升项目可读性。开源社区离不开高质量的文档，你是新人的引路灯。",
            tags: ["Markdown大师", "信息架构", "极强同理心"],
            projects: [
                { name: "github/docs", desc: "GitHub 官方文档仓库，大量 good first issue", url: "https://github.com/github/docs", exampleIssue: "https://github.com/github/docs/issues?q=label%3A%22good+first+issue%22" },
                { name: "freeCodeCamp 翻译协作", desc: "帮助翻译课程/文档，友好入门", url: "https://github.com/freeCodeCamp/freeCodeCamp", exampleIssue: "https://github.com/freeCodeCamp/freeCodeCamp/issues?q=label%3A%22first-timers-only%22" },
                { name: "first-contributions", desc: "专为新人准备的指南型项目", url: "https://github.com/firstcontributions/first-contributions", exampleIssue: "https://github.com/firstcontributions/first-contributions/issues" }
            ]
        },
        flowMaster: {
            name: "⚙️ 流程开拓者",
            icon: "🔧🧩",
            description: "你对规则和协作流程高度敏锐，能够优化贡献指南、CI流程、PR模板。为社区建立高效的自组织机制，减少摩擦。",
            tags: ["自动化控", "流程设计", "治理推动"],
            projects: [
                { name: "Homebrew", desc: "贡献指南极客，参与维护 brew 流程", url: "https://github.com/Homebrew/brew", exampleIssue: "https://github.com/Homebrew/brew/issues?q=label%3A%22help+wanted%22" },
                { name: "Kubernetes SIG Contributor Experience", desc: "参与社区流程建设", url: "https://github.com/kubernetes/community", exampleIssue: "https://github.com/kubernetes/community/issues?q=label%3A%22good+first+issue%22" },
                { name: "Jenkins infra", desc: "基础设施流程优化", url: "https://github.com/jenkins-infra", exampleIssue: "https://github.com/jenkins-infra/helpdesk/issues" }
            ]
        },
        codeMaster: {
            name: "🛠️ 代码实干家",
            icon: "💻⚡",
            description: "你享受编码，直面bug与功能实现，乐于提供高质量代码贡献。开源世界因你的每一行代码而强大。",
            tags: ["Bug Hunter", "算法能力", "快速落地"],
            projects: [
                { name: "VS Code", desc: "微软顶级开源，适合初学者的good first issue", url: "https://github.com/microsoft/vscode", exampleIssue: "https://github.com/microsoft/vscode/issues?q=label%3A%22good+first+issue%22" },
                { name: "Rust Language", desc: "系统语言开源，有很多入门级任务", url: "https://github.com/rust-lang/rust", exampleIssue: "https://github.com/rust-lang/rust/issues?q=label%3A%22E-easy%22" },
                { name: "TensorFlow", desc: "机器学习框架，标记易于上手的issue", url: "https://github.com/tensorflow/tensorflow", exampleIssue: "https://github.com/tensorflow/tensorflow/issues?q=label%3A%22stat%3Acontributions+welcome%22" }
            ]
        },
        issueMaster: {
            name: "🔍 问题捕手",
            icon: "🐛🧲",
            description: "你拥有锐利的观察力，擅长复现bug、提炼关键信息，优化新人体验和社区响应。让开源项目更健康！",
            tags: ["Quality Guardian", "用户体验分析师", "Triager"],
            projects: [
                { name: "Godot Engine", desc: "游戏引擎，Issue 分类欢迎贡献者", url: "https://github.com/godotengine/godot", exampleIssue: "https://github.com/godotengine/godot/issues?q=label%3A%22good+first+issue%22" },
                { name: "Mozilla 基础设施", desc: "bug triage 和测试", url: "https://github.com/mozilla", exampleIssue: "https://github.com/mozilla-mobile/firefox-ios/issues?q=label%3A%22good+first+issue%22" },
                { name: "OpenRefine", desc: "开源数据处理，需要测试和issue分类", url: "https://github.com/OpenRefine/OpenRefine", exampleIssue: "https://github.com/OpenRefine/OpenRefine/issues?q=label%3A%22good+first+issue%22" }
            ]
        },
        allRounder: {
            name: "🌈 全能潜力新人",
            icon: "🌟🚀",
            description: "你博学且适应力极强！兼具文档、流程、代码、洞察多维潜能，是社区最渴望的新星。任何入门任务都能轻松驾驭。",
            tags: ["多面手", "快速学习", "领导者潜力"],
            projects: [
                { name: "CNCF  landscape", desc: "云原生全景图，适合全栈新手", url: "https://github.com/cncf/landscape", exampleIssue: "https://github.com/cncf/landscape/issues?q=label%3A%22good+first+issue%22" },
                { name: "First Contributions 全球教程", desc: "任何人都能成为贡献者", url: "https://github.com/firstcontributions/first-contributions", exampleIssue: "https://github.com/firstcontributions/first-contributions/issues" },
                { name: "EddieHub 社区", desc: "开源多样性社区，新手友好", url: "https://github.com/EddieHubCommunity", exampleIssue: "https://github.com/EddieHubCommunity/LinkFree/issues?q=label%3A%22good+first+issue%22" }
            ]
        }
    };

    let currentScores = { doc:0, flow:0, code:0, issue:0 };
    let questionsRendered = false;

    // 渲染问卷
    function renderQuestions() {
        const container = document.getElementById('questionsContainer');
        if (!container) return;
        let html = '';
        QUESTIONS.forEach((q, idx) => {
            html += `<div class="question-block" data-qidx="${idx}">
                        <div class="question-text"><span class="q-num">${idx+1}</span> ${q.text}</div>
                        <div class="options">`;
            q.options.forEach((opt, optIdx) => {
                const optionId = `q${idx}_opt${optIdx}`;
                html += `<label class="option-label" for="${optionId}">
                            <input type="radio" name="q${idx}" value="${optIdx}" id="${optionId}"> 
                            ${opt.text}
                         </label>`;
            });
            html += `</div></div>`;
        });
        container.innerHTML = html;
    }

    // 收集分数并计算人格
    function computeScores() {
        let scores = { doc:0, flow:0, code:0, issue:0 };
        for (let i = 0; i < QUESTIONS.length; i++) {
            const selected = document.querySelector(`input[name="q${i}"]:checked`);
            if (!selected) return null;
            const optIndex = parseInt(selected.value);
            const optScores = QUESTIONS[i].options[optIndex].scores;
            scores.doc += optScores.doc || 0;
            scores.flow += optScores.flow || 0;
            scores.code += optScores.code || 0;
            scores.issue += optScores.issue || 0;
        }
        return scores;
    }

    // 决定人格
    function getPersonality(scores) {
        const { doc, flow, code, issue } = scores;
        const values = { doc, flow, code, issue };
        const maxVal = Math.max(doc, flow, code, issue);
        const sorted = Object.values(values).sort((a,b)=>b-a);
        const isBalanced = (sorted[0] - sorted[3] <= 4) && (doc >= 12 && flow >= 12 && code >= 12 && issue >= 12);
        if (isBalanced || (maxVal - sorted[1] <= 2 && doc+flow+code+issue >= 45)) {
            return 'allRounder';
        }
        if (maxVal === doc) return 'docMaster';
        if (maxVal === flow) return 'flowMaster';
        if (maxVal === code) return 'codeMaster';
        if (maxVal === issue) return 'issueMaster';
        return 'docMaster';
    }

    // 构建推荐html
    function renderResult(personalityType, nickname, scores) {
        const personality = PERSONALITY_MAP[personalityType];
        if (!personality) return;
        const nameDisplay = nickname.trim() ? nickname.trim() : "开源探索者";
        const projectItems = personality.projects.map(proj => `
            <div class="project-item">
                <div class="project-name">📦 ${proj.name} <span class="tag">推荐</span></div>
                <div>${proj.desc}</div>
                <div>
                    <a href="${proj.url}" target="_blank" class="project-link">🔗 项目地址 →</a>
                    <a href="${proj.exampleIssue}" target="_blank" class="issue-link">🎯 Good First Issue 列表 →</a>
                </div>
            </div>
        `).join('');
        
        return `
            <div class="personality-card" id="posterCapture">
                <div class="personality-header">
                    <div class="personality-icon">${personality.icon}</div>
                    <div class="personality-name">${personality.name}</div>
                </div>
                <div><strong>🧑‍💻 ${nameDisplay}</strong> 的人格画像</div>
                <div class="personality-desc">✨ ${personality.description}</div>
                <div>🏷️ 优势标签: ${personality.tags.map(t=>`#${t}`).join(' · ')}</div>
                <div class="recommend-title">🎯 最适合你的开源任务 & 项目推荐</div>
                <div class="project-list">${projectItems}</div>
                <div style="margin-top: 1rem; font-size:0.85rem; background:#e9f3ee; border-radius:1rem; padding:0.7rem;">
                💡 小贴士：点击以上「Good First Issue 列表」即可筛选适合你的入门议题，大胆迈出开源第一步！
                </div>
                <div style="margin-top:0.8rem; font-size:0.7rem; color:#3c6e5f;">📊 能力维度: 文档 ${scores.doc} · 流程 ${scores.flow} · 代码 ${scores.code} · 问题洞察 ${scores.issue}</div>
            </div>
            <div class="poster-btn">
                <button class="btn btn-secondary" id="generatePosterBtn">📸 生成分享海报</button>
            </div>
        `;
    }

    // 全局提交逻辑
    function onSubmit() {
        const errorDiv = document.getElementById('errorMsg');
        errorDiv.style.display = 'none';
        // 验证全选
        let allSelected = true;
        for (let i = 0; i < QUESTIONS.length; i++) {
            if (!document.querySelector(`input[name="q${i}"]:checked`)) {
                allSelected = false;
                break;
            }
        }
        if (!allSelected) {
            errorDiv.innerText = '⚠️ 请完成全部 10 个问题，才能解锁你的开源人格哟！';
            errorDiv.style.display = 'block';
            return;
        }
        const scores = computeScores();
        if (!scores) return;
        const personalityKey = getPersonality(scores);
        const nickname = document.getElementById('nickname').value || '';
        const resultHtml = renderResult(personalityKey, nickname, scores);
        const resultArea = document.getElementById('resultArea');
        resultArea.style.display = 'block';
        resultArea.innerHTML = resultHtml;
        // 平滑滚动到结果
        resultArea.scrollIntoView({ behavior: 'smooth', block: 'start' });
        // 绑定海报事件
        setTimeout(() => {
            const posterBtn = document.getElementById('generatePosterBtn');
            if (posterBtn) {
                posterBtn.addEventListener('click', generatePoster);
            }
        }, 100);
    }

    async function generatePoster() {
        const element = document.getElementById('posterCapture');
        if (!element) return;
        try {
            const canvas = await html2canvas(element, {
                scale: 2,
                backgroundColor: '#ffffff',
                logging: false,
                useCORS: false
            });
            const link = document.createElement('a');
            const nickname = document.getElementById('nickname').value.trim() || 'opensource';
            link.download = `opensource_personality_${nickname}.png`;
            link.href = canvas.toDataURL();
            link.click();
        } catch(e) {
            alert("生成海报失败，可手动截图保存");
        }
    }

    function resetQuiz() {
        const radios = document.querySelectorAll('input[type="radio"]');
        radios.forEach(radio => radio.checked = false);
        document.getElementById('resultArea').style.display = 'none';
        document.getElementById('errorMsg').style.display = 'none';
        document.getElementById('nickname').value = '';
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // 初次加载渲染
    renderQuestions();
    document.getElementById('submitBtn').addEventListener('click', onSubmit);
    document.getElementById('resetBtn').addEventListener('click', resetQuiz);
</script>
</body>
</html>
