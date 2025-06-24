<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>曲红绡分线体验设计</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #b76e79;
            --secondary: #e6b0aa;
            --tragic: #d98880;
            --love: #f5b7b1;
            --need: #d7bde2;
            --relation: #e8daef;
            --dark: #0a0e1a;
            --light: #e0d7e9;
            --card-bg: rgba(19, 24, 48, 0.8);
            --shadow: 0 8px 30px rgba(0, 0, 0, 0.5);
            --transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            --visual: #b76e79;
            --emotion: #e6b0aa;
            --decision: #5d8aa8;
            --feedback: #98bf64;
            --starry-bg: #0a0e1a;
            --lotus-pink: #f8c6d9;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Noto Sans SC', sans-serif;
            background: var(--starry-bg);
            color: var(--light);
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
            position: relative;
        }

        .starry-sky {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            overflow: hidden;
        }

        .star {
            position: absolute;
            background-color: #fff;
            border-radius: 50%;
            animation: twinkle var(--duration, 4s) infinite ease-in-out;
        }

        .lotus-pond {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 150px;
            z-index: -1;
            overflow: hidden;
        }

        .lotus {
            position: absolute;
            bottom: 0;
            filter: drop-shadow(0 0 8px var(--lotus-pink));
            animation: sway 8s infinite ease-in-out;
            opacity: 0.7;
            z-index: -1;
        }

        .lotus::before, .lotus::after {
            content: "";
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, var(--lotus-pink) 0%, transparent 70%);
        }

        .lotus::before {
            width: 60px;
            height: 60px;
            top: 0;
            left: 0;
        }

        .lotus::after {
            width: 40px;
            height: 40px;
            top: 10px;
            left: 30px;
        }

        .lotus-leaf {
            position: absolute;
            bottom: 0;
            width: 80px;
            height: 60px;
            border-radius: 50%;
            background: rgba(0, 128, 0, 0.3);
            filter: blur(2px);
            animation: leaf-sway 10s infinite ease-in-out;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }

        @keyframes sway {
            0%, 100% { transform: translateX(0) rotate(0deg); }
            25% { transform: translateX(5px) rotate(2deg); }
            75% { transform: translateX(-5px) rotate(-2deg); }
        }

        @keyframes leaf-sway {
            0%, 100% { transform: translateX(0) rotate(0deg) scale(1); }
            25% { transform: translateX(8px) rotate(3deg) scale(1.05); }
            75% { transform: translateX(-8px) rotate(-3deg) scale(0.95); }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
        }

        .header-section {
            text-align: center;
            padding: 40px 20px;
            margin-bottom: 40px;
            background: var(--card-bg);
            border-radius: 20px;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(183, 110, 121, 0.3);
            backdrop-filter: blur(10px);
        }

        .header-section::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 6px;
            background: linear-gradient(90deg, var(--primary), var(--secondary), var(--tragic), var(--love), var(--need), var(--relation));
            z-index: 1;
        }

        h1 {
            font-size: 2.8rem;
            font-weight: 700;
            margin-bottom: 15px;
            color: var(--light);
            position: relative;
            z-index: 2;
            text-shadow: 0 0 15px rgba(183, 110, 121, 0.7);
        }

        .subtitle {
            font-size: 1.3rem;
            color: #b0a0c0;
            margin: 0 auto 25px;
            font-weight: 400;
            max-width: 800px;
        }

        .designer-info {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 25px;
            flex-wrap: wrap;
        }

        .designer-card {
            background: rgba(40, 45, 70, 0.8);
            padding: 15px 25px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.1rem;
            color: #d0c0e0;
            transition: var(--transition);
        }

        .designer-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(183, 110, 121, 0.4);
        }

        .designer-card i {
            color: var(--primary);
        }

        .chart-section {
            background: var(--card-bg);
            border-radius: 20px;
            box-shadow: var(--shadow);
            padding: 40px;
            margin-bottom: 50px;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(183, 110, 121, 0.3);
            backdrop-filter: blur(10px);
        }

        .section-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .section-title {
            font-size: 2rem;
            font-weight: 700;
            color: var(--light);
            position: relative;
            display: inline-block;
            margin-bottom: 20px;
            text-shadow: 0 0 10px rgba(183, 110, 121, 0.5);
        }

        .section-title::after {
            content: "";
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: var(--primary);
            border-radius: 2px;
            box-shadow: 0 0 10px var(--primary);
        }

        .chart-description {
            color: #b0a0c0;
            max-width: 700px;
            font-size: 1.1rem;
            line-height: 1.7;
            margin: 0 auto;
        }

        .chart-container {
            position: relative;
            height: 400px;
            margin: 40px 0;
        }

        #emotionCoaster, #heartFlowChart {
            width: 100%;
            height: 100%;
        }

        .legend-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 25px;
            margin-top: 30px;
            padding: 15px;
            background: rgba(40, 45, 70, 0.6);
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 15px;
            border-radius: 20px;
            background: rgba(50, 55, 80, 0.8);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
            transition: var(--transition);
            cursor: pointer;
            color: #e0d0f0;
        }

        .legend-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(183, 110, 121, 0.4);
        }

        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 50%;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            animation: fadeIn 0.3s ease;
        }

        .modal-content {
            background: linear-gradient(135deg, rgba(30, 35, 60, 0.9) 0%, rgba(40, 45, 75, 0.9) 100%);
            border-radius: 20px;
            width: 90%;
            max-width: 700px;
            padding: 40px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
            position: relative;
            animation: slideUp 0.5s ease;
            max-height: 90vh;
            overflow-y: auto;
            border: 1px solid rgba(183, 110, 121, 0.3);
            backdrop-filter: blur(10px);
        }

        .close-modal {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 1.8rem;
            color: var(--primary);
            cursor: pointer;
            transition: var(--transition);
            text-shadow: 0 0 8px var(--primary);
        }

        .close-modal:hover {
            transform: rotate(90deg);
            color: var(--tragic);
        }

        .modal-header {
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(183, 110, 121, 0.3);
        }

        .modal-title {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--light);
            margin-bottom: 5px;
            text-shadow: 0 0 8px rgba(183, 110, 121, 0.5);
        }

        .modal-subtitle {
            font-size: 1.2rem;
            color: var(--primary);
            font-weight: 600;
            text-shadow: 0 0 5px rgba(183, 110, 121, 0.5);
        }

        .modal-body {
            padding: 20px 0;
        }

        .section-card {
            background: rgba(50, 55, 80, 0.6);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(183, 110, 121, 0.2);
        }

        .section-title-card {
            font-size: 1.3rem;
            font-weight: 600;
            color: var(--light);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            text-shadow: 0 0 5px rgba(183, 110, 121, 0.3);
        }

        .section-title-card i {
            margin-right: 10px;
            color: var(--primary);
            text-shadow: 0 0 8px var(--primary);
        }

        .emotion-section {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .emotion-card {
            text-align: center;
            padding: 15px;
            border-radius: 10px;
            flex: 1;
            min-width: 120px;
            max-width: 30%;
            background: rgba(183, 110, 121, 0.15);
            box-shadow: inset 0 0 15px rgba(183, 110, 121, 0.2);
            margin: 0 5px;
        }

        .emotion-emoji {
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }

        .emotion-text {
            font-size: 1.1rem;
            font-weight: 500;
            color: var(--light);
        }

        .emotion-arrow {
            font-size: 2rem;
            color: var(--primary);
            padding: 0 10px;
            text-shadow: 0 0 8px var(--primary);
        }

        .intensity-section {
            margin: 20px 0;
            padding: 15px;
            background: rgba(183, 110, 121, 0.15);
            border-radius: 12px;
            box-shadow: inset 0 0 15px rgba(183, 110, 121, 0.2);
        }

        .intensity-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .intensity-label {
            font-weight: 600;
            color: var(--light);
        }

        .intensity-value {
            font-weight: 700;
            color: var(--primary);
            font-size: 1.2rem;
            text-shadow: 0 0 5px var(--primary);
        }

        .intensity-bar {
            height: 10px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
            overflow: hidden;
        }

        .intensity-fill {
            height: 100%;
            border-radius: 5px;
            box-shadow: 0 0 10px var(--primary);
        }

        .design-target {
            margin: 25px 0;
            line-height: 1.7;
            font-size: 1.1rem;
            color: #d0c0e0;
        }

        .design-intent {
            background: rgba(183, 110, 121, 0.15);
            border-left: 4px solid var(--primary);
            padding: 15px;
            border-radius: 0 8px 8px 0;
            margin: 20px 0;
            font-style: italic;
            position: relative;
            color: #e0d0f0;
            box-shadow: inset 0 0 15px rgba(183, 110, 121, 0.2);
        }

        .design-intent::before {
            content: "设计意图";
            position: absolute;
            top: -12px;
            left: 15px;
            background: var(--primary);
            color: white;
            padding: 3px 10px;
            border-radius: 4px;
            font-size: 0.9rem;
            font-style: normal;
            box-shadow: 0 0 10px var(--primary);
        }

        .key-points {
            margin-top: 20px;
        }

        .key-point {
            display: flex;
            margin-bottom: 15px;
            align-items: flex-start;
            position: relative;
        }

        .point-icon {
            width: 28px;
            height: 28px;
            background: var(--primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            flex-shrink: 0;
            font-size: 14px;
            box-shadow: 0 0 8px var(--primary);
        }

        .point-content {
            flex: 1;
            color: #d0c0e0;
        }

        .point-content strong {
            color: var(--light);
        }

        .flow-analysis {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px dashed rgba(183, 110, 121, 0.3);
        }
        
        .flow-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }
        
        .flow-card {
            background: rgba(50, 55, 80, 0.6);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease;
            border: 1px solid rgba(183, 110, 121, 0.2);
        }
        
        .flow-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(183, 110, 121, 0.4);
        }
        
        .flow-card-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--light);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            text-shadow: 0 0 5px rgba(183, 110, 121, 0.3);
        }
        
        .flow-card-title i {
            margin-right: 10px;
            width: 30px;
            height: 30px;
            background: var(--primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 8px var(--primary);
        }
        
        .flow-card-content {
            font-size: 1rem;
            color: #c0b0d0;
            line-height: 1.6;
        }
        
        .flow-card-content ul {
            padding-left: 20px;
            margin-top: 10px;
        }
        
        .flow-card-content li {
            margin-bottom: 8px;
            position: relative;
        }
        
        .flow-card-content li::before {
            content: "•";
            color: var(--primary);
            font-weight: bold;
            position: absolute;
            left: -15px;
            text-shadow: 0 0 5px var(--primary);
        }
        
        .flow-analysis-title {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--light);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            text-shadow: 0 0 8px rgba(183, 110, 121, 0.5);
        }
        
        .flow-analysis-title i {
            margin-right: 10px;
            color: var(--primary);
            text-shadow: 0 0 8px var(--primary);
        }

        footer {
            text-align: center;
            padding: 40px 0;
            color: #a090b0;
            font-size: 1.05rem;
            margin-top: 50px;
            border-top: 1px solid rgba(183, 110, 121, 0.3);
        }

        .detail-container {
            margin-top: 15px;
            background: rgba(183, 110, 121, 0.15);
            border-radius: 8px;
            padding: 0;
            max-height: 0;
            overflow: hidden;
            transition: all 0.5s ease;
            box-shadow: inset 0 0 8px rgba(183, 110, 121, 0.2);
        }
        
        .detail-container.active {
            max-height: 1000px;
            padding: 15px;
        }
        
        .detail-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        
        .detail-title {
            font-weight: 600;
            color: var(--light);
            font-size: 1.1rem;
        }
        
        .detail-content {
            color: #d0c0e0;
            line-height: 1.7;
            font-size: 1rem;
            padding: 10px 0;
        }
        
        .detail-toggle-btn {
            background: var(--primary);
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 8px var(--primary);
            border: none;
            outline: none;
            font-size: 0.9rem;
        }
        
        .detail-toggle-btn:hover {
            transform: scale(1.05);
            background: #c47b86;
        }
        
        .point-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
        }
        
        .point-title {
            display: flex;
            align-items: center;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            from { 
                opacity: 0;
                transform: translateY(30px);
            }
            to { 
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .chart-container {
                height: 300px;
            }
            
            .modal-content {
                padding: 30px 20px;
            }
            
            .emotion-section {
                flex-direction: column;
            }
            
            .emotion-card {
                max-width: 100%;
                width: 100%;
                margin-bottom: 15px;
            }
            
            .emotion-arrow {
                transform: rotate(90deg);
                margin: 10px 0;
                padding: 10px 0;
            }
            
            .flow-grid {
                grid-template-columns: 1fr;
            }
            
            .lotus {
                transform: scale(0.8);
            }
            
            .detail-toggle-btn {
                padding: 5px 10px;
                font-size: 0.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- 星空背景 -->
    <div class="starry-sky" id="starrySky"></div>
    
    <!-- 荷花池 -->
    <div class="lotus-pond" id="lotusPond"></div>
    
    <div class="container">
        <!-- 头部区域 -->
        <section class="header-section">
            <h1>曲红绡·分线体验</h1>
            <p class="subtitle">野心与救赎-从初见到结局的体验旅程</p>
            
            <div class="designer-info">
                <div class="designer-card">
                    <i class="fas fa-user"></i>
                    <span>策划：郭慧杰（Sevy）</span>
                </div>
                <div class="designer-card">
                    <i class="fas fa-calendar"></i>
                    <span>版本：1.2.0</span>
                </div>
                <div class="designer-card">
                    <i class="fas fa-tags"></i>
                    <span>标签：NPC设计、情感曲线、玩家体验</span>
                </div>
            </div>
        </section>

        <!-- 图表区域 -->
        <section class="chart-section">
            <div class="section-header">
                <h2 class="section-title">情感体验曲线</h2>
                <p class="chart-description">玩家在体验曲红绡分线中的情绪波动可视化，展示关键情绪锚点与体验设计节点</p>
            </div>
            
            <div class="chart-container">
                <canvas id="emotionCoaster"></canvas>
            </div>
            
            <div class="legend-container">
                <div class="legend-item" data-phase="0">
                    <div class="legend-color" style="background-color: #b76e79;"></div>
                    <span>初见阶段</span>
                </div>
                <div class="legend-item" data-phase="1">
                    <div class="legend-color" style="background-color: #e6b0aa;"></div>
                    <span>再见阶段</span>
                </div>
                <div class="legend-item" data-phase="2">
                    <div class="legend-color" style="background-color: #d98880;"></div>
                    <span>成长阶段</span>
                </div>
                <div class="legend-item" data-phase="3">
                    <div class="legend-color" style="background-color: #f5b7b1;"></div>
                    <span>高潮阶段</span>
                </div>
                <div class="legend-item" data-phase="4">
                    <div class="legend-color" style="background-color: #d7bde2;"></div>
                    <span>循环阶段</span>
                </div>
                <div class="legend-item" data-phase="5">
                    <div class="legend-color" style="background-color: #e8daef;"></div>
                    <span>结局阶段</span>
                </div>
            </div>
        </section>
        
        <!-- 新增的心流体验分析图表 -->
        <section class="chart-section">
            <div class="section-header">
                <h2 class="section-title">心流体验定量分析</h2>
                <p class="chart-description">玩家在不同任务阶段的多维度体验设定，展示视觉冲击、情感共鸣、决策压力与操作反馈的强度变化</p>
            </div>
            
            <div class="chart-container">
                <canvas id="heartFlowChart"></canvas>
            </div>
            
            <div class="legend-container">
                <div class="legend-item">
                    <div class="legend-color" style="background-color: var(--visual);"></div>
                    <span>视觉冲击</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: var(--emotion);"></div>
                    <span>情感共鸣</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: var(--decision);"></div>
                    <span>决策压力</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: var(--feedback);"></div>
                    <span>操作反馈</span>
                </div>
            </div>
            
            <!-- 心流体验分析 -->
            <div class="flow-analysis">
                <div class="flow-analysis-title">
                    <i class="fas fa-brain"></i>
                    <span>心流体验层次解析</span>
                </div>
                
                <div class="flow-grid">
                    <div class="flow-card">
                        <div class="flow-card-title">
                            <i class="fas fa-eye"></i>
                            <span>视觉冲击设计</span>
                        </div>
                        <div class="flow-card-content">
                            <p>通过强烈的视觉元素建立第一印象，形成玩家记忆锚点：</p>
                            <ul>
                                <li>红唇骨剑的视觉冲击</li>
                                <li>荷花池畔的性感形象</li>
                                <li>高潮期战损共修的情欲表现</li>
                                <li>血色丝带与骨剑特效</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="flow-card">
                        <div class="flow-card-title">
                            <i class="fas fa-heart"></i>
                            <span>情感共鸣设计</span>
                        </div>
                        <div class="flow-card-content">
                            <p>通过角色背景与玩家互动建立情感连接：</p>
                            <ul>
                                <li>邪修+长生的悲情背景</li>
                                <li>为玩家牺牲的剧情设计</li>
                                <li>功法反噬的宿命矛盾</li>
                                <li>生日、纪念日等情感事件</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="flow-card">
                        <div class="flow-card-title">
                            <i class="fas fa-balance-scale"></i>
                            <span>决策压力设计</span>
                        </div>
                        <div class="flow-card-content">
                            <p>关键抉择点增加玩家参与感：</p>
                            <ul>
                                <li>合作或对抗的初始选择</li>
                                <li>战损状态下的情感抉择</li>
                                <li>正邪立场的道德困境</li>
                                <li>多结局分支的抉择权重</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="flow-card">
                        <div class="flow-card-title">
                            <i class="fas fa-gamepad"></i>
                            <span>操作反馈设计</span>
                        </div>
                        <div class="flow-card-content">
                            <p>玩法机制强化情感体验：</p>
                            <ul>
                                <li>追逐战QTE操作设计</li>
                                <li>双人配合的潜入玩法</li>
                                <li>血契共修的音阶副本</li>
                                <li>好感度影响互动反馈</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <footer>
            <p>曲红绡·体验设计 | NPC分线 | © 2025 郭慧杰（Sevy）</p>
        </footer>
    </div>

    <!-- 模态框 -->
    <div class="modal" id="phaseModal">
        <div class="modal-content">
            <span class="close-modal" id="closeModal">&times;</span>
            
            <div class="modal-header">
                <h3 class="modal-title" id="modalTitle">初见阶段</h3>
                <div class="modal-subtitle" id="modalSubtitle">危险魅力引探索</div>
            </div>
            
            <div class="modal-body">
                <div class="section-card">
                    <div class="section-title-card">
                        <i class="fas fa-heartbeat"></i> 核心情绪变化
                    </div>
                    <div class="emotion-section" id="emotionFlow">
                        <!-- 动态生成情绪卡片 -->
                    </div>
                    
                    <div class="intensity-section">
                        <div class="intensity-header">
                            <div class="intensity-label">情绪强度目标</div>
                            <div class="intensity-value" id="intensityValue">30%</div>
                        </div>
                        <div class="intensity-bar">
                            <div class="intensity-fill" id="intensityFill" style="width: 30%; background: #b76e79;"></div>
                        </div>
                    </div>
                </div>
                
                <div class="section-card">
                    <div class="section-title-card">
                        <i class="fas fa-bullseye"></i> 体验设计目标
                    </div>
                    <div class="design-target" id="designTarget">
                        建立角色第一印象，通过危险与魅力的矛盾组合激发玩家探索欲望，为后续情感发展奠定基础。
                    </div>
                    
                    <div class="design-intent" id="designIntent">
                        通过强烈的视觉冲击和悬念设计，在玩家心中建立"危险且迷人"的第一印象。娇柔跌倒与性感幕后黑手的矛盾组合，配合异常任务线索，为后续关系发展埋下伏笔。
                    </div>
                </div>
                
                <div class="section-card">
                    <div class="section-title-card">
                        <i class="fas fa-lightbulb"></i> 关键体验设计
                    </div>
                    
                    <div class="key-points" id="keyPoints">
                        <!-- 动态填充 -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 创建星空背景
        function createStarrySky() {
            const container = document.getElementById('starrySky');
            const starCount = 150;
            
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                
                // 随机大小（1-3px）
                const size = Math.random() * 3 + 1;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                
                // 随机位置
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                
                // 随机闪烁时间
                star.style.setProperty('--duration', `${Math.random() * 5 + 3}s`);
                
                container.appendChild(star);
            }
        }
        
        // 创建荷花池
        function createLotusPond() {
            const container = document.getElementById('lotusPond');
            const lotusCount = 8;
            const leafCount = 12;
            
            // 创建荷花
            for (let i = 0; i < lotusCount; i++) {
                const lotus = document.createElement('div');
                lotus.classList.add('lotus');
                
                // 随机位置
                lotus.style.left = `${Math.random() * 100}%`;
                
                // 随机大小
                const scale = Math.random() * 0.5 + 0.7;
                lotus.style.transform = `scale(${scale})`;
                
                // 随机动画延迟
                lotus.style.animationDelay = `${Math.random() * 5}s`;
                
                container.appendChild(lotus);
            }
            
            // 创建荷叶
            for (let i = 0; i < leafCount; i++) {
                const leaf = document.createElement('div');
                leaf.classList.add('lotus-leaf');
                
                // 随机位置
                leaf.style.left = `${Math.random() * 100}%`;
                
                // 随机大小
                const scale = Math.random() * 0.8 + 0.5;
                leaf.style.transform = `scale(${scale})`;
                
                // 随机动画延迟
                leaf.style.animationDelay = `${Math.random() * 5}s`;
                
                container.appendChild(leaf);
            }
        }
        
        // 情绪数据 - 每个阶段都有独特的设计意图和详细流程
        const emotions = [
            { 
                phase: '初见阶段', 
                subtitle: '危险魅力引探索',
                emotionFlow: [
                    { emoji: '😯', emotion: '好奇' },
                    { emoji: '😨', emotion: '紧张' },
                    { emoji: '🤩', emotion: '期待' }
                ],
                intensity: 30,
                color: '#b76e79',
                designTarget: '建立角色第一印象，通过危险与性感的矛盾组合激发玩家探索欲望，为后续情感发展奠定基础。',
                designIntent: '通过强烈的视觉冲击和悬念设计，在玩家心中建立"危险且迷人"的第一印象。娇柔跌倒与性感幕后黑手的矛盾组合，配合异常任务线索，为后续关系发展埋下伏笔。',
                keyPoints: [
                    {
                        title: '悬念钩子',
                        content: '任务异常引发玩家推理欲望，神秘消失留下线索道具，为二次接触创造契机',
                        details: '玩家完成高额报酬任务时发现从不同的发布者处发布的任务相同，任务描述完全一致，任务发布者还总是谈起师姐、月亮之类的话。由此产生"何人指使"的好奇，激活沟通任务。'
                    },
                    {
                        title: '视觉冲击',
                        content: '红色主题视觉设计，骨剑道具突出危险特质，性感形象与危险动作形成反差魅力',
                        details: '通过星空下的红唇骨剑飘飘倩影的视觉冲击和荷花池畔的性感形象设计，配合血色丝带与骨剑特效，建立强烈的第一印象。'
                    },
                    {
                        title: '肢体语言设计',
                        content: '近距离接触时的微妙肢体语言，传达角色复杂性格与潜在情感可能性',
                        details: '在情感追踪中，曲红绮娇嗔："你这小子倒还有两下子～"，又言"人家脚崴了，还不快来帮帮人家～～"，顺势欲倒入玩家怀中。'
                    },
                    {
                        title: '突然结束的相遇',
                        content: '追逐战到投怀送抱再到突然离开，钓足玩家胃口，增强角色吸引力',
                        details: '玩家误以为还有后续时仙子会突然飞走，留下一方香帕与一些赠礼，并留下仙音："若能下次相遇，姐姐便给你些答案～（笑）"，初见任务结束。'
                    }
                ]
            },
            { 
                phase: '再见阶段', 
                subtitle: '线索试探寻合作',
                emotionFlow: [
                    { emoji: '🕵️', emotion: '怀疑' },
                    { emoji: '😏', emotion: '兴奋' },
                    { emoji: '🤩', emotion: '期待' }
                ],
                intensity: 53,
                color: '#e6b0aa',
                designTarget: '通过剧情反转建立合作关系，利用信息差创造博弈空间，深化角色神秘感。',
                designIntent: '意在于创造戏剧性转折，将敌对关系转化为合作可能。通过信息不对称设计，让玩家在危险与利益之间权衡，增强角色神秘感和玩家探索欲望。',
                keyPoints: [
                    {
                        title: '剧情反转设计',
                        content: '从敌对关系到合作邀约的转变，创造戏剧性转折点',
                        details: '玩家发现三具正道弟子尸体，现场残留血色丝绢与骨粉痕迹。还在低头研究尸体，空谷传来一阵突声，还未来得及格挡，那女子手持骨剑抵死玩家脖颈："小弟弟，深夜探案，不怕被灭口吗？"'
                    },
                    {
                        title: '信息不对称',
                        content: '角色掌握更多信息，形成权力不对等关系，增加博弈感',
                        details: '曲红绡逗弄玩家说几人都是她杀的，模糊真相，玩家见招拆招，获得曲红绡的任何和合作邀约。'
                    },
                    {
                        title: '暧昧氛围营造',
                        content: '近距离低语、肢体接触等设计强化危险又迷人的氛围',
                        details: '玩家追回"噬灵体"，曲红绮眼神闪烁，短暂沉默后冷笑："知道太多，可是会被灭口的哦～不过……"（突然贴近玩家耳边低语）"你以为这些功法是怎么来的？那些老东西杀人的时候，可比我狠多了。"'
                    },
                    {
                        title: '利益共同体',
                        content: '建立共同目标，为后续合作提供合理动机',
                        details: '曲红绮："算你聪明，看到这令牌了吗？元洪长老争抢的【噬灵体秘术】残卷，就在我手里——正道长老又如何长生路上哪有无辜……角色沉吟一阵，只要你帮我打探到镇门功法《XXX》的线索，这残卷就是你的，我也不杀你，如何？"'
                    }
                ]
            },
            { 
                phase: '成长阶段', 
                subtitle: '合作战斗增羁绊',
                emotionFlow: [
                    { emoji: '🤝', emotion: '合作' },
                    { emoji: '😢', emotion: '感动' }
                ],
                intensity: 70,
                color: '#d98880',
                designTarget: '通过协同挑战建立情感连接，利用牺牲情节深化角色羁绊，激发玩家保护欲。',
                designIntent: '通过共同经历创造情感纽带。牺牲情节的设计旨在引发玩家情感共鸣，让玩家从利益合作转向情感投入，为后续关系质变奠定基础。',
                keyPoints: [
                    {
                        title: '协同玩法设计',
                        content: '双人配合的解谜与战斗机制，创造合作成就感',
                        details: '玩家与曲红绡组队（邪修形象），深夜潜入藏经阁。通过五行相克逻辑做个表演小游戏，破解机关阵，两人配合击碎符文；利用曲红绡的迷烟干扰巡逻长老，完成潜行。'
                    },
                    {
                        title: '牺牲情节设计',
                        content: '关键情节中的自我牺牲行为，引发玩家情感共鸣',
                        details: '成功拿到《XXX》时，藏经阁警钟骤响，亲主与三位长老包围现场。曲红绡突然将功法塞给玩家："呆子快跑！"（触发战斗：曲红绡独自对抗长老，玩家需携带功法突围）。'
                    },
                    {
                        title: '情感转折点',
                        content: '从利益合作到情感连接的转变，建立真正羁绊',
                        details: '玩家突围后回头，看到曲红绡被长老重创，骨剑断裂，嘴角溢血却仍在笑："愣着干嘛？我一会儿就来。"（背景音乐为角色曲，好感度++）。' 
                    },
                    {
                        title: '背景故事揭露',
                        content: '逐步揭示角色背景，增加情感深度与玩家认同',
                        details: '本次追杀结束后，曲红绡重伤昏迷，玩家发现【罗刹族族谱】与【噬灵体诅咒卷轴】，解锁角色宿命诅咒背景故事（可通过动画呈现）。'
                    }
                ]
            },
            { 
                phase: '高潮阶段', 
                subtitle: '战损喂药赴巫山',
                emotionFlow: [
                    { emoji: '💘', emotion: '抉择' },
                    { emoji: '🔥', emotion: '激情' }
                ],
                intensity: 95,
                color: '#f5b7b1',
                designTarget: '创造情感爆发点，通过关键抉择推动关系质变，实现情感与玩法的高潮融合。',
                designIntent: '创造情感与玩法融合的巅峰体验。通过战损状态突破角色心理防线，让玩家在关键抉择中决定关系走向，将情感突破与游戏机制完美结合。',
                keyPoints: [
                    {
                        title: '战损状态设计',
                        content: '角色脆弱状态突破心理防线，创造情感突破契机',
                        details: '玩家靠近倒地的曲红绡，出现【安抚】【喂药】按钮。喂药动画中，曲红绡脆弱易碎，并暴露自身嗜灵体缺陷，触发隐藏线索【噬灵体血痕】（影响结局）。'
                    },
                    {
                        title: '关键抉择点',
                        content: '玩家选择决定关系走向，增强参与感与情感投入',
                        details: '曲红绡抓住玩家手腕："你知道吗？每动一次情，我的骨剑就会啃食我的精血……" 玩家可选择【推开地】或【吻地】，分别开启不同结局分支。'
                    },
                    {
                        title: '双修玩法融合',
                        content: '将情感突破与游戏机制结合，创造独特体验',
                        details: '选择【吻地】后触发动画演出：灵泉洞符文亮起，血色丝带环绕，骨剑分裂融入双方眉心，解锁【血契共修】系统，近距离抚摸交互加入，后续玩家获得【噬灵共鸣】技能。'
                    },
                    {
                        title: '情感记忆点',
                        content: '设计强烈的情感符号，形成玩家记忆锚点',
                        details: '共修后开启【血契共修】音阶机制副本，播放角色曲，道出角色一生宿命与挣扎，玩家需在角色曲时间内击中曲红绡负面情绪幻化的「背叛之影」「孤独之傲」「杀戮之心」，救赎角色。'
                    }
                ]
            },
            { 
                phase: '循环阶段', 
                subtitle: '日常互动深感情',
                emotionFlow: [
                    { emoji: '💞', emotion: '甜蜜' },
                    { emoji: '☺️', emotion: '温馨' }
                ],
                intensity: 80,
                color: '#d7bde2',
                designTarget: '通过日常互动巩固情感连接，创造稳定陪伴感，增强玩家长期投入意愿。',
                designIntent: '通过日常互动维持情感热度。动态反馈系统让玩家感受到真实的关系进展，特殊事件设计深化情感连接，为最终结局创造情感基础。',
                keyPoints: [
                    {
                        title: '日常互动系统',
                        content: '设计多样化日常互动，维持情感热度',
                        details: '曲红绡每周发布3次秘密任务（如窃取某宗门灵药、刺杀背叛者），完成后获得【血罗刹信仰】（可兑换限定外观【血色轻纱】）。'
                    },
                    {
                        title: '动态情感反馈',
                        content: '基于好感度的角色反应变化，创造真实关系体验',
                        details: '可触发"曲红绡的问候"（如"今天天气不错，要不要陪姐姐看月亮？"），选择"同意"可增加好感度并获得随机丹药。'
                    },
                    {
                        title: '专属事件设计',
                        content: '生日、纪念日等特殊事件，深化情感连接',
                        details: '玩家在曲红绡生日前拿到对话的通中角色的礼物需求（说些从未过过生辰，不知道凡人究竟是怎么生活的之类的话引发玩家的心疼和共鸣），玩家可能选择与角色【正态】（需收集材料链接）并触发对应剧情。'
                    },
                    {
                        title: '成长可视化',
                        content: '情感进展的视觉化反馈，增强成就感',
                        details: '好感度满值后开启「血契共修」模式，玩家彻底击败角色心魔，解锁双人技能【生生世世】，结成情侣关系，获得成就。'
                    }
                ]
            },
            { 
                phase: '结局阶段', 
                subtitle: '宿命抉择定结局',
                emotionFlow: [
                    { emoji: '🎭', emotion: '抉择' },
                    { emoji: '💖', emotion: '满足' }
                ],
                intensity: 85,
                color: '#e8daef',
                designTarget: '提供情感闭环，通过多结局设计满足不同玩家情感需求，创造完整体验。',
                designIntent: '为情感旅程提供圆满闭环。多结局设计尊重玩家选择，强调决策影响力，部分结局融入修仙悲剧元素，强化世界观一致性，让玩家获得深度情感满足。',
                keyPoints: [
                    {
                        title: '多结局分支',
                        content: '设计4种情感结局，满足不同玩家期待',
                        details: '1. 决裂结局：曲红绡会因未玩家断情绝爱，被拆穿后悲情自白，最终死于玩家之手。<br>2. 觉醒结局：曲红绡以成长性依旧无法解决的问题，报复正道后消失，留装备给玩家。<br>3. 智别结局：曲红绡每日功法后留在这里已无意义，修为提升后回归邪修游戏恢复家族，等待与玩家重逢。<br>4. 救赎结局：玩家与曲红绡双修后弥补BUG，角色跟随玩家一段时间后根据两人的成长需求，决定回归邪修拉取资源，玩家留在水芸宗，继续合作恋爱。'
                    },
                    {
                        title: '情感闭环设计',
                        content: '解决核心矛盾，提供情感满足感',
                        details: '结局事件随版本或玩家中后期剧情推进，符合玩家长线游玩需求，不改变主线，仅为分线体验。'
                    },
                    {
                        title: '玩家影响力',
                        content: '强调玩家选择对结局的决定性作用',
                        details: '在高潮阶段的关键抉择（如是否吻地）以及后续的互动选择，会直接影响最终结局走向，增强玩家的参与感和责任感。'
                    },
                    {
                        title: '悲剧美学',
                        content: '部分结局融入修仙悲剧元素，强化世界观',
                        details: '在决裂结局和觉醒结局中，融入修仙世界的残酷性和宿命感，体现"修仙长生万民皆苦"的主题，增强世界观深度。'
                    }
                ]
            }
        ];
        
        // 心流体验数据
        const flowData = {
            phases: ['初见阶段', '再见阶段', '成长阶段', '高潮阶段', '循环阶段', '结局阶段'],
            visualImpact: [90, 70, 60, 95, 50, 80],
            emotionalResonance: [30, 50, 80, 85, 70, 90],
            decisionPressure: [40, 60, 50, 85, 40, 75],
            feedbackIntensity: [60, 75, 80, 90, 85, 70]
        };
        
        // 初始化页面
        document.addEventListener('DOMContentLoaded', function() {
            // 创建星空和荷花
            createStarrySky();
            createLotusPond();
            
            // 创建情感体验图表
            const ctx = document.getElementById('emotionCoaster').getContext('2d');
            
            // 图表数据
            const data = {
                labels: emotions.map(e => e.phase),
                datasets: [
                    {
                        label: '情绪强度',
                        data: emotions.map(e => e.intensity),
                        backgroundColor: emotions.map(e => e.color + '40'),
                        borderColor: '#b76e79',
                        borderWidth: 4,
                        tension: 0.4,
                        pointRadius: 8,
                        pointHoverRadius: 12,
                        pointBackgroundColor: '#fff',
                        pointBorderColor: emotions.map(e => e.color),
                        pointBorderWidth: 3,
                        fill: true
                    }
                ]
            };
            
            // 图表配置
            const config = {
                type: 'line',
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(30, 35, 60, 0.95)',
                            titleColor: '#e0d7e9',
                            bodyColor: '#b0a0c0',
                            borderColor: 'rgba(183, 110, 121, 0.5)',
                            borderWidth: 1,
                            padding: 30,
                            displayColors: false,
                            titleFont: {
                                size: 26
                            },
                            bodyFont: {
                                size: 24
                            },
                            callbacks: {
                                title: function(tooltipItems) {
                                    const index = tooltipItems[0].dataIndex;
                                    return `${emotions[index].phase} (${emotions[index].intensity}%)`;
                                },
                                label: function(context) {
                                    const index = context.dataIndex;
                                    const emotionsText = emotions[index].emotionFlow.map(e => e.emotion).join(' → ');
                                    return `${emotionsText}: 玩家情绪变化`;
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#b0a0c0',
                                callback: function(value) {
                                    return value + '%';
                                }
                            },
                            title: {
                                display: true,
                                text: '情绪强度',
                                color: '#e0d7e9',
                                font: {
                                    weight: 'bold'
                                }
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            },
                            ticks: {
                                color: '#e0d7e9',
                                font: {
                                    weight: '500'
                                }
                            }
                        }
                    },
                    interaction: {
                        mode: 'index',
                        intersect: false
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    },
                    onClick: (e, elements) => {
                        if (elements.length > 0) {
                            const index = elements[0].index;
                            showPhaseModal(index);
                        }
                    }
                }
            };
            
            // 创建情感体验图表
            const emotionChart = new Chart(ctx, config);
            
            // 创建心流体验图表
            const flowCtx = document.getElementById('heartFlowChart').getContext('2d');
            const flowConfig = {
                type: 'line',
                data: {
                    labels: flowData.phases,
                    datasets: [
                        {
                            label: '视觉冲击',
                            data: flowData.visualImpact,
                            borderColor: 'var(--visual)',
                            backgroundColor: 'rgba(183, 110, 121, 0.1)',
                            borderWidth: 3,
                            tension: 0.3,
                            pointRadius: 6,
                            pointHoverRadius: 10,
                            pointBackgroundColor: '#fff',
                            pointBorderWidth: 2,
                            fill: true
                        },
                        {
                            label: '情感共鸣',
                            data: flowData.emotionalResonance,
                            borderColor: 'var(--emotion)',
                            backgroundColor: 'rgba(230, 176, 170, 0.1)',
                            borderWidth: 3,
                            tension: 0.3,
                            pointRadius: 6,
                            pointHoverRadius: 10,
                            pointBackgroundColor: '#fff',
                            pointBorderWidth: 2,
                            fill: true
                        },
                        {
                            label: '决策压力',
                            data: flowData.decisionPressure,
                            borderColor: 'var(--decision)',
                            backgroundColor: 'rgba(93, 138, 168, 0.1)',
                            borderWidth: 3,
                            tension: 0.3,
                            pointRadius: 6,
                            pointHoverRadius: 10,
                            pointBackgroundColor: '#fff',
                            pointBorderWidth: 2,
                            fill: true
                        },
                        {
                            label: '操作反馈',
                            data: flowData.feedbackIntensity,
                            borderColor: 'var(--feedback)',
                            backgroundColor: 'rgba(152, 191, 100, 0.1)',
                            borderWidth: 3,
                            tension: 0.3,
                            pointRadius: 6,
                            pointHoverRadius: 10,
                            pointBackgroundColor: '#fff',
                            pointBorderWidth: 2,
                            fill: true
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        tooltip: {
                            backgroundColor: 'rgba(30, 35, 60, 0.95)',
                            titleColor: '#e0d7e9',
                            bodyColor: '#b0a0c0',
                            borderColor: 'rgba(183, 110, 121, 0.5)',
                            borderWidth: 1,
                            padding: 30,
                            displayColors: true,
                            titleFont: {
                                size: 26
                            },
                            bodyFont: {
                                size: 24
                            },
                            callbacks: {
                                title: function(tooltipItems) {
                                    return tooltipItems[0].label;
                                },
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.raw}%`;
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#b0a0c0',
                                callback: function(value) {
                                    return value + '%';
                                }
                            },
                            title: {
                                display: true,
                                text: '体验强度',
                                color: '#e0d7e9',
                                font: {
                                    weight: 'bold'
                                }
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            },
                            ticks: {
                                color: '#e0d7e9',
                                font: {
                                    weight: '500'
                                }
                            }
                        }
                    },
                    interaction: {
                        mode: 'index',
                        intersect: false
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                }
            };
            
            // 创建心流体验图表
            const heartFlowChart = new Chart(flowCtx, flowConfig);
            
            // 存储数据集可见状态
            const datasetVisibility = {
                visualImpact: true,
                emotionalResonance: true,
                decisionPressure: true,
                feedbackIntensity: true
            };
            
            // 为图例项添加切换功能
            document.querySelectorAll('.legend-item').forEach(item => {
                const type = item.querySelector('span').textContent;
                const icon = document.createElement('i');
                icon.className = 'fas fa-eye';
                icon.style.marginLeft = '10px';
                icon.style.cursor = 'pointer';
                item.appendChild(icon);
                
                icon.addEventListener('click', function(e) {
                    e.stopPropagation();
                    
                    // 切换可见状态
                    let datasetIndex;
                    switch(type) {
                        case '视觉冲击':
                            datasetVisibility.visualImpact = !datasetVisibility.visualImpact;
                            datasetIndex = 0;
                            break;
                        case '情感共鸣':
                            datasetVisibility.emotionalResonance = !datasetVisibility.emotionalResonance;
                            datasetIndex = 1;
                            break;
                        case '决策压力':
                            datasetVisibility.decisionPressure = !datasetVisibility.decisionPressure;
                            datasetIndex = 2;
                            break;
                        case '操作反馈':
                            datasetVisibility.feedbackIntensity = !datasetVisibility.feedbackIntensity;
                            datasetIndex = 3;
                            break;
                    }
                    
                    // 更新图表
                    heartFlowChart.setDatasetVisibility(datasetIndex, datasetVisibility[Object.keys(datasetVisibility)[datasetIndex]]);
                    heartFlowChart.update();
                    
                    // 更新图标
                    if (icon.classList.contains('fa-eye')) {
                        icon.classList.remove('fa-eye');
                        icon.classList.add('fa-eye-slash');
                        icon.style.color = '#999';
                    } else {
                        icon.classList.remove('fa-eye-slash');
                        icon.classList.add('fa-eye');
                        icon.style.color = '';
                    }
                });
            });
            
            // 模态框操作
            const modal = document.getElementById('phaseModal');
            const closeModal = document.getElementById('closeModal');
            
            // 关闭模态框
            closeModal.addEventListener('click', () => {
                modal.style.display = 'none';
            });
            
            // 点击外部关闭模态框
            window.addEventListener('click', (e) => {
                if (e.target === modal) {
                    modal.style.display = 'none';
                }
            });
            
            // 显示阶段模态框
            function showPhaseModal(index) {
                const phase = emotions[index];
                
                // 更新模态框内容
                document.getElementById('modalTitle').textContent = phase.phase;
                document.getElementById('modalSubtitle').textContent = phase.subtitle;
                document.getElementById('intensityValue').textContent = `${phase.intensity}%`;
                document.getElementById('intensityFill').style.width = `${phase.intensity}%`;
                document.getElementById('intensityFill').style.backgroundColor = phase.color;
                document.getElementById('designTarget').textContent = phase.designTarget;
                document.getElementById('designIntent').textContent = phase.designIntent;
                
                // 更新情绪变化展示
                const emotionFlowContainer = document.getElementById('emotionFlow');
                emotionFlowContainer.innerHTML = '';
                
                phase.emotionFlow.forEach((emotion, idx) => {
                    // 添加情绪卡片
                    const emotionCard = document.createElement('div');
                    emotionCard.className = 'emotion-card';
                    emotionCard.innerHTML = `
                        <div class="emotion-emoji">${emotion.emoji}</div>
                        <div class="emotion-text">${emotion.emotion}</div>
                    `;
                    emotionFlowContainer.appendChild(emotionCard);
                    
                    // 如果不是最后一个情绪，添加箭头
                    if (idx < phase.emotionFlow.length - 1) {
                        const arrow = document.createElement('div');
                        arrow.className = 'emotion-arrow';
                        arrow.innerHTML = '→';
                        emotionFlowContainer.appendChild(arrow);
                    }
                });
                
                // 更新关键点
                const keyPointsContainer = document.getElementById('keyPoints');
                keyPointsContainer.innerHTML = '';
                
                phase.keyPoints.forEach((point, idx) => {
                    const pointElement = document.createElement('div');
                    pointElement.className = 'key-point';
                    
                    pointElement.innerHTML = `
                        <div class="point-icon">
                            <i class="fas fa-${idx + 1}"></i>
                        </div>
                        <div class="point-content">
                            <div class="point-header">
                                <div class="point-title">
                                    <strong>${point.title}</strong>
                                </div>
                                <button class="detail-toggle-btn" data-index="${idx}">展开</button>
                            </div>
                            <p>${point.content}</p>
                            <div class="detail-container" id="detail-${idx}">
                                <div class="detail-header">
                                    <div class="detail-title">${point.title}详细流程</div>
                                </div>
                                <div class="detail-content">
                                    ${point.details}
                                </div>
                            </div>
                        </div>
                    `;
                    keyPointsContainer.appendChild(pointElement);
                });
                
                // 为所有详情按钮添加事件监听
                document.querySelectorAll('.detail-toggle-btn').forEach(button => {
                    button.addEventListener('click', function() {
                        const index = this.getAttribute('data-index');
                        const detailContainer = document.getElementById(`detail-${index}`);
                        const isActive = detailContainer.classList.contains('active');
                        
                        if (isActive) {
                            detailContainer.classList.remove('active');
                            this.textContent = '展开';
                        } else {
                            detailContainer.classList.add('active');
                            this.textContent = '收起';
                        }
                    });
                });
                
                // 显示模态框
                modal.style.display = 'flex';
                
                // 重置滚动条位置
                document.querySelector('.modal-content').scrollTop = 0;
            }
            
            // 为图例添加点击事件
            document.querySelectorAll('.legend-item').forEach(item => {
                item.addEventListener('click', () => {
                    const phaseIndex = parseInt(item.getAttribute('data-phase'));
                    if (!isNaN(phaseIndex)) {
                        showPhaseModal(phaseIndex);
                    }
                });
            });
        });
    </script>
</body>
</html>
</html>
