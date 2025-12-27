# meowquiz
貓咪內心世界心理測驗
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>你的貓咪內心世界 - 溫馨心理測驗</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&family=Noto+Serif+TC:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Noto Sans TC', sans-serif;
            background: linear-gradient(135deg, #ffeef8 0%, #e3f2fd 50%, #fff9e6 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .container {
            max-width: 600px;
            width: 100%;
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
            padding: 40px 30px;
            position: relative;
            overflow: hidden;
        }

        .container::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255, 182, 193, 0.1) 0%, transparent 70%);
            animation: float 20s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translate(0, 0) rotate(0deg); }
            33% { transform: translate(30px, -30px) rotate(120deg); }
            66% { transform: translate(-20px, 20px) rotate(240deg); }
        }

        .page {
            display: none;
            opacity: 0;
            animation: fadeIn 0.8s ease-in-out forwards;
            position: relative;
            z-index: 1;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        h1 {
            font-family: 'Noto Serif TC', serif;
            font-size: 2rem;
            color: #ff6b9d;
            text-align: center;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.05);
        }

        h2 {
            font-size: 1.5rem;
            color: #ff8fab;
            text-align: center;
            margin-bottom: 25px;
        }

        .subtitle {
            font-size: 0.95rem;
            color: #666;
            text-align: center;
            line-height: 1.8;
            margin-bottom: 30px;
            padding: 0 10px;
        }

        .input-group {
            margin: 30px 0;
        }

        input[type="text"] {
            width: 100%;
            padding: 15px 20px;
            border: 2px solid #ffc0cb;
            border-radius: 20px;
            font-size: 1rem;
            font-family: 'Noto Sans TC', sans-serif;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.9);
        }

        input[type="text"]:focus {
            outline: none;
            border-color: #ff6b9d;
            box-shadow: 0 0 15px rgba(255, 107, 157, 0.2);
        }

        .btn {
            width: 100%;
            padding: 15px 30px;
            background: linear-gradient(135deg, #ff6b9d 0%, #ffa6c9 100%);
            color: white;
            border: none;
            border-radius: 25px;
            font-size: 1.1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 20px rgba(255, 107, 157, 0.3);
            font-family: 'Noto Sans TC', sans-serif;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(255, 107, 157, 0.4);
        }

        .btn:active {
            transform: translateY(0);
        }

        .story-text {
            font-size: 1.05rem;
            line-height: 2;
            color: #555;
            text-align: center;
            padding: 20px;
            background: rgba(255, 255, 255, 0.6);
            border-radius: 20px;
            margin-bottom: 30px;
            font-family: 'Noto Serif TC', serif;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(255, 192, 203, 0.3);
            border-radius: 10px;
            margin-bottom: 30px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff6b9d 0%, #ffa6c9 100%);
            border-radius: 10px;
            transition: width 0.5s ease;
        }

        .progress-text {
            text-align: center;
            color: #ff6b9d;
            font-size: 0.9rem;
            margin-bottom: 15px;
            font-weight: 500;
        }

        .question-text {
            font-size: 1rem;
            color: #888;
            text-align: center;
            margin-bottom: 15px;
            font-style: italic;
            line-height: 1.6;
        }

        .question-title {
            font-size: 1.2rem;
            color: #333;
            text-align: center;
            margin-bottom: 25px;
            font-weight: 500;
            line-height: 1.8;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .option {
            padding: 18px 20px;
            background: rgba(255, 255, 255, 0.9);
            border: 2px solid #ffc0cb;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
            text-align: left;
            line-height: 1.6;
        }

        .option:hover {
            background: rgba(255, 182, 193, 0.2);
            border-color: #ff8fab;
            transform: translateX(5px);
        }

        .result-container {
            text-align: center;
        }

        .result-title {
            font-size: 1.8rem;
            color: #ff6b9d;
            margin-bottom: 20px;
            font-family: 'Noto Serif TC', serif;
        }

        .result-description {
            font-size: 1.1rem;
            line-height: 2;
            color: #555;
            padding: 25px;
            background: rgba(255, 240, 245, 0.6);
            border-radius: 20px;
            margin-bottom: 30px;
        }

        .result-images {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 30px;
        }

        .result-images img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .result-images img:hover {
            transform: scale(1.05);
        }

        .share-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .share-btn {
            flex: 1;
            min-width: 150px;
            padding: 12px 20px;
            background: linear-gradient(135deg, #a8e6cf 0%, #c8e6c9 100%);
            color: #2e7d32;
            border: none;
            border-radius: 20px;
            font-size: 0.95rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Noto Sans TC', sans-serif;
        }

        .share-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(168, 230, 207, 0.4);
        }

        .restart-btn {
            margin-top: 15px;
            background: linear-gradient(135deg, #b39ddb 0%, #ce93d8 100%);
        }

        .cat-emoji {
            font-size: 3rem;
            margin-bottom: 20px;
            display: block;
        }

        @media (max-width: 600px) {
            .container {
                padding: 30px 20px;
                border-radius: 20px;
            }

            h1 {
                font-size: 1.6rem;
            }

            h2 {
                font-size: 1.3rem;
            }

            .result-images {
                grid-template-columns: 1fr;
            }

            .result-images img {
                height: 250px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 歡迎頁 -->
        <div id="welcome-page" class="page active">
            <span class="cat-emoji">🐱</span>
            <h1>你的貓咪內心世界</h1>
            <p class="subtitle">
                歡迎來到這個溫馨的心靈旅程。讓我們一起探索你內心那隻獨特的貓咪，發現屬於你的溫暖故事。
            </p>
            
            <div class="input-group">
                <input type="text" id="userName" placeholder="請輸入你的名字..." />
            </div>
            
            <p class="subtitle" style="font-size: 0.9rem; color: #888; line-height: 1.8;">
                許多流浪貓像我一樣，渴望一個溫暖的家。只要「要餵就要紮」、「領養不棄養」，我們就能一起為喵星人的幸福努力。<br>
                <strong style="color: #ff6b9d;">有你＋有我=有我們</strong>
            </p>
            
            <button class="btn" onclick="startQuiz()">開始探索 ✨</button>
        </div>

        <!-- 開頭敘述頁 -->
        <div id="intro-page" class="page">
            <span class="cat-emoji">🌙</span>
            <h2>流浪貓的獨白</h2>
            <div class="story-text">
                我是一隻在街頭徘徊的流浪貓，夜晚的風有點涼，但月光總是那麼溫柔。<br><br>
                我常常靜靜坐著，看著來來往往的人們，心裡想著……如果有個家，會是什麼感覺呢？<br><br>
                現在，讓我們一起進入我的內心世界。你選擇的答案，將揭開你內心的貓咪模樣……
            </div>
            <button class="btn" onclick="startQuestions()">進入內心世界 🌟</button>
        </div>

        <!-- 問題頁面 -->
        <div id="question-page" class="page">
            <div class="progress-text">問題 <span id="currentQ">1</span> / 8</div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressBar"></div>
            </div>
            
            <p class="question-text" id="questionContext"></p>
            <h3 class="question-title" id="questionTitle"></h3>
            
            <div class="options" id="optionsContainer"></div>
        </div>

        <!-- 結果頁 -->
        <div id="result-page" class="page">
            <span class="cat-emoji" id="resultEmoji">🐱</span>
            <h2 class="result-title" id="resultType"></h2>
            <div class="result-description" id="resultDescription"></div>
            
            <div class="result-images" id="resultImages"></div>
            
            <div class="share-buttons">
                <button class="share-btn" onclick="shareResult()">分享你的貓咪內心 🎀</button>
                <button class="share-btn restart-btn" onclick="restartQuiz()">重新測驗 🔄</button>
            </div>
        </div>
    </div>

    <script>
        // 全局變數
        let userName = '';
        let currentQuestion = 0;
        let scores = {
            orange: 0,    // 橘貓
            black: 0,     // 黑貓
            calico: 0,    // 三花貓
            british: 0,   // 英國短毛
            siamese: 0,   // 暹羅貓
            persian: 0    // 波斯貓
        };

        // 問題數據
        const questions = [
            {
                context: "在雨後的巷子，我聞到遠處食物的香氣，心裡湧起一絲渴望……",
                question: "你會怎麼做？",
                options: [
                    { text: "A. 勇敢走近，充滿活力地探索", type: "orange" },
                    { text: "B. 靜靜觀察，等安全時再靠近", type: "black" },
                    { text: "C. 好奇地繞圈，輕輕試探", type: "calico" },
                    { text: "D. 平靜等待，享受這份寧靜", type: "british" }
                ]
            },
            {
                context: "有人伸出手，我想被觸碰，但又害怕受傷……",
                question: "你的心會？",
                options: [
                    { text: "A. 熱情迎上，渴望連接", type: "siamese" },
                    { text: "B. 先退後，但內心柔軟", type: "persian" },
                    { text: "C. 猶豫轉身，卻偷偷回頭", type: "calico" },
                    { text: "D. 溫柔接受，感受暖意", type: "british" }
                ]
            },
            {
                context: "找到一個隱蔽的角落，雨停了，我蜷起身子……",
                question: "內心的感覺是？",
                options: [
                    { text: "A. 想玩鬧，釋放能量", type: "orange" },
                    { text: "B. 享受獨處的平靜", type: "black" },
                    { text: "C. 探索周圍的一切", type: "siamese" },
                    { text: "D. 優雅休息，等待陽光", type: "persian" }
                ]
            },
            {
                context: "看到其他貓在陽光下嬉戲，我心裡羨慕那份自在……",
                question: "你會？",
                options: [
                    { text: "A. 加入其中，分享快樂", type: "calico" },
                    { text: "B. 從遠處守望，微笑", type: "british" },
                    { text: "C. 輕聲呼喚，吸引注意", type: "siamese" },
                    { text: "D. 溫柔靠近，靜靜陪伴", type: "persian" }
                ]
            },
            {
                context: "偶爾想起過去的溫暖，那種被擁抱的感覺……",
                question: "面對回憶，你會？",
                options: [
                    { text: "A. 用活力填滿現在", type: "orange" },
                    { text: "B. 靜靜品味，療癒自己", type: "black" },
                    { text: "C. 多變地轉移心情", type: "calico" },
                    { text: "D. 平靜接受，繼續前行", type: "british" }
                ]
            },
            {
                context: "夜晚的星星閃爍，我抬頭看著，夢想一個永遠的家……",
                question: "內心的渴望是？",
                options: [
                    { text: "A. 無盡的探索與陪伴", type: "siamese" },
                    { text: "B. 柔軟的安靜時光", type: "persian" },
                    { text: "C. 熱鬧的分享時刻", type: "orange" },
                    { text: "D. 深沉的獨處療癒", type: "black" }
                ]
            },
            {
                context: "風吹過樹葉，沙沙聲像輕柔的呢喃……",
                question: "你會怎麼回應？",
                options: [
                    { text: "A. 興奮追逐葉子", type: "calico" },
                    { text: "B. 安穩坐下，感受風", type: "british" },
                    { text: "C. 輕聲與風對話", type: "siamese" },
                    { text: "D. 優雅伸展，擁抱這一刻", type: "persian" }
                ]
            },
            {
                context: "終於，我閉上眼睛，內心浮現最真實的自己……",
                question: "最後的感覺是？",
                options: [
                    { text: "A. 活力滿滿的溫暖", type: "orange" },
                    { text: "B. 神秘卻柔軟的平靜", type: "black" },
                    { text: "C. 多彩有趣的自由", type: "calico" },
                    { text: "D. 穩重優雅的安心", type: "british" }
                ]
            }
        ];

        // 結果數據
        const results = {
            orange: {
                name: "橘貓型",
                emoji: "🧡",
                description: "你的內心世界像一隻充滿溫暖的橘貓，像陽光般療癒周圍的一切。你帶來快樂與希望，讓人感覺世界更明亮。",
                images: [
                    "https://images.unsplash.com/photo-1574158622682-e40e69881006?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1533738363-b7f9aef128ce?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1529778873920-4da4926a72c2?w=400&h=300&fit=crop"
                ]
            },
            black: {
                name: "黑貓型",
                emoji: "🖤",
                description: "你的內心世界像一隻神秘卻溫柔的黑貓，像月光般靜靜守護。你的內心充滿深度與療癒，給人安心的擁抱。",
                images: [
                    "https://images.unsplash.com/photo-1529257414772-1960b7bea4eb?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1516750930-93b2a4da6d14?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1518791841217-8f162f1e1131?w=400&h=300&fit=crop"
                ]
            },
            calico: {
                name: "三花貓型",
                emoji: "🌸",
                description: "你的內心世界像一隻多彩而自由的三花貓，像花朵般綻放溫馨。你帶來驚喜與療癒，讓生活充滿柔軟的美。",
                images: [
                    "https://images.unsplash.com/photo-1495360010541-f48722b34f7d?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1513360371669-4adf3dd7dff8?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1478098711619-5ab0b478d6e6?w=400&h=300&fit=crop"
                ]
            },
            british: {
                name: "英國短毛型",
                emoji: "💙",
                description: "你的內心世界像一隻穩重溫柔的英國短毛，像擁抱般可靠。你的內心是寧靜的港灣，療癒每一個靠近的人。",
                images: [
                    "https://images.unsplash.com/photo-1541781774459-bb2af2f05b55?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1596854407944-bf87f6fdd49e?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?w=400&h=300&fit=crop"
                ]
            },
            siamese: {
                name: "暹羅貓型",
                emoji: "💜",
                description: "你的內心世界像一隻優雅而親近的暹羅貓，像輕語般溫暖。你渴望連接，帶來深刻的療癒與陪伴。",
                images: [
                    "https://images.unsplash.com/photo-1513245543132-31f507417b26?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1573865526739-10c1d3a1f0e3?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1506755855567-92ff770e8d00?w=400&h=300&fit=crop"
                ]
            },
            persian: {
                name: "波斯貓型",
                emoji: "🤍",
                description: "你的內心世界像一隻柔軟奢華的波斯貓，像雲朵般舒適。你的內心充滿溫柔，療癒自己也療癒他人。",
                images: [
                    "https://images.unsplash.com/photo-1455970022149-a8f26b6902dd?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1511044568932-338cba0ad803?w=400&h=300&fit=crop",
                    "https://images.unsplash.com/photo-1543852786-1cf6624b9987?w=400&h=300&fit=crop"
                ]
            }
        };

        // 切換頁面
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        // 開始測驗
        function startQuiz() {
            const nameInput = document.getElementById('userName').value.trim();
            if (!nameInput) {
                alert('請輸入你的名字再開始 🐱');
                return;
            }
            userName = nameInput;
            showPage('intro-page');
        }

        // 開始問題
        function startQuestions() {
            currentQuestion = 0;
            scores = { orange: 0, black: 0, calico: 0, british: 0, siamese: 0, persian: 0 };
            showQuestion();
            showPage('question-page');
        }

        // 顯示問題
        function showQuestion() {
            const q = questions[currentQuestion];
            document.getElementById('currentQ').textContent = currentQuestion + 1;
            document.getElementById('progressBar').style.width = ((currentQuestion + 1) / 8 * 100) + '%';
            document.getElementById('questionContext').textContent = q.context;
            document.getElementById('questionTitle').textContent = q.question;
            
            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';
            
            q.options.forEach((option, index) => {
                const div = document.createElement('div');
                div.className = 'option';
                div.textContent = option.text;
                div.onclick = () => selectOption(option.type);
                optionsContainer.appendChild(div);
            });
        }

        // 選擇選項
        function selectOption(type) {
            scores[type]++;
            
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                setTimeout(() => {
                    showQuestion();
                }, 300);
            } else {
                setTimeout(() => {
                    showResult();
                }, 300);
            }
        }

        // 顯示結果
        function showResult() {
            // 找出最高分
            let maxScore = 0;
            let resultType = 'orange';
            
            for (let type in scores) {
                if (scores[type] > maxScore) {
                    maxScore = scores[type];
                    resultType = type;
                } else if (scores[type] === maxScore && Math.random() > 0.5) {
                    resultType = type;
                }
            }
            
            const result = results[resultType];
            
            document.getElementById('resultEmoji').textContent = result.emoji;
            document.getElementById('resultType').textContent = `${userName}，你是${result.name}`;
            document.getElementById('resultDescription').textContent = result.description;
            
            // 添加圖片
            const imagesContainer = document.getElementById('resultImages');
            imagesContainer.innerHTML = '';
            result.images.forEach(src => {
                const img = document.createElement('img');
                img.src = src;
                img.alt = result.name;
                imagesContainer.appendChild(img);
            });
            
            showPage('result-page');
        }

        // 分享結果
        function shareResult() {
            const resultText = `我完成了「貓咪內心世界」測驗！快來探索你的貓咪個性吧 🐱✨`;
            
            if (navigator.share) {
                navigator.share({*
