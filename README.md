
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MAG Industries | Пошаговая кастомизация</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Roboto:wght@300;400&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #F3A000;
            --red: #FF0000;
            --bg: #CCE1FE;
            --text: #222;
            --shadow: 0 4px 15px rgba(0,0,0,0.1);
            --light-yellow: #FFFFE0;
        }
        * { margin:0; padding:0; box-sizing:border-box; }
        body { font-family: 'Roboto', sans-serif; background: var(--bg); color: var(--text); line-height: 1.5; }
       
        .header-content { max-width: 1200000px; margin: 0 auto; text-align: center; }
        .logo { max-height: 80px; width: auto; display: block; margin: 0 auto; }
        .wizard { max-width: 1000px; margin: 40px auto; padding: 0 20px; }
        .steps { display: flex; justify-content: space-between; margin-bottom: 30px; gap: 10px; }
        .step { flex: 1; text-align: center; padding: 15px; background: white; border-radius: 12px; box-shadow: var(--shadow); cursor: pointer; transition: all 0.3s; font-weight: 600; }
        .step.active { background: var(--primary); color: white; }
        .step.completed { background: #4caf50; color: white; }
        .content { background: white; border-radius: 16px; padding: 30px; box-shadow: var(--shadow); }
        .preview-container { position: relative; text-align: center; margin: 20px 0; min-height: 380px; }
        #preview-base { max-width: 320px; height: auto; transition: filter 0.4s; }
        .back-text-overlay { position: absolute; bottom: 12%; left: 50%; transform: translateX(-50%); color: white; font-size: 1.25rem; text-shadow: 1px 1px 4px black; font-weight: bold; pointer-events: none; white-space: pre; text-align: center; }
        .color-picker-group { display: flex; align-items: center; gap: 20px; margin: 24px 0 24px 40px; justify-content: flex-start; }
        .color-label { font-weight: 600; min-width: 140px; text-align: right; flex-shrink: 0; }
        input[type="color"] {
            width: 90px; height: 90px; padding: 0; border: none; border-radius: 50%; cursor: pointer;
            box-shadow: 0 3px 12px rgba(0,0,0,0.18); appearance: none;
        }
        input[type="color"]::-webkit-color-swatch-wrapper { padding: 0; }
        input[type="color"]::-webkit-color-swatch { border: none; border-radius: 50%; }
        .option-container { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; margin: 24px 0; }
        .option-btn {
            padding: 12px 28px; font-size: 1.05rem; border: 2px solid #ddd; background: #f8f8f8;
            border-radius: 10px; cursor: pointer; transition: all 0.2s;
        }
        .option-btn:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
        .option-btn.active { background: var(--primary); color: white; border-color: var(--primary); }
        .nav-buttons { display: flex; justify-content: space-between; margin-top: 40px; gap: 20px; }
        button { padding: 14px 36px; font-size: 1.1rem; border: none; border-radius: 12px; cursor: pointer; font-weight: 600; transition: all 0.2s; }
        button:hover { transform: translateY(-2px); }
        .next-btn { background: var(--primary); color: white; }
        .prev-btn { background: #ddd; color: #333; }
        .no-engrave-btn { background: #6c757d; color: white; }
        #backText {
            width: 100%; max-width: 400px; padding: 14px 18px; font-size: 1.1rem;
            border: 2px solid #ccc; border-radius: 12px; margin: 20px auto; display: block; text-align: center;
            transition: all 0.3s;
        }
        #backText:focus {
            border-color: var(--primary); box-shadow: 0 0 0 4px rgba(243,160,0,0.2); outline: none;
        }

        /* ====================== ФОРМА ЗАКАЗА ПО ЦЕНТРУ ====================== */
        .order-form {
            display: none;
            margin-top: 40px;
            padding: 40px 20px;
            background: #f9f9f9;
            border-radius: 16px;
            text-align: center;
        }
        .order-form input,
        .order-form textarea {
            width: 100%;
            max-width: 420px;
            padding: 14px 18px;
            margin: 12px auto;
            display: block;
            border: 2px solid #ddd;
            border-radius: 12px;
            font-size: 1rem;
            transition: all 0.3s;
        }
        .order-form input:focus,
        .order-form textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 4px rgba(243,160,0,0.2);
            outline: none;
        }
        .buy-btn {
            background: #4caf50;
            color: white;
            padding: 16px 60px;
            font-size: 1.25rem;
            margin: 30px auto 0;
            display: block;
        }
        #finalSummary {
            margin: 20px auto;
            padding: 20px;
            background: #f0f8ff;
            border-radius: 12px;
            max-width: 500px;
            text-align: left;
            display: inline-block;
        }
    </style>
</head>
<body>
<header>
    <div class="header-content">
        <img src="logo_2.jpeg" alt="Логотип" class="logo">
        <!-- Замени src на свой логотип -->
    </div>
</header>

<div class="wizard">
    <div class="steps">
        <div class="step active" data-step="1">1. Модель</div>
        <div class="step" data-step="2">2. Цвет</div>
        <div class="step" data-step="3">3. Гравировка</div>
        <div class="step" data-step="4">4. Заказ</div>
    </div>

    <div class="content">
        <div class="preview-container">
            <img id="preview-base" src="https://img.freepik.com/free-psd/smartwatch-mockup_1314-117.jpg" alt="Часы">
            <div id="backTextOverlay" class="back-text-overlay"></div>
        </div>

        <!-- Шаг 1 -->
        <div id="step1">
            <h2>1. Выберите модель часов</h2>
            <div class="option-container">
                <button class="option-btn active" onclick="selectModel('clock5pro', 'сюда фото часов.jpg', this)">Clock - 5 Pro</button>
                <button class="option-btn" onclick="selectModel('clock5', 'clock-5.jpg', this)">Clock - 5</button>
                <button class="option-btn" onclick="selectModel('clock4p', 'clock-4(P).png', this)">Clock - 4(P)</button>
            </div>
            <div class="nav-buttons">
                <div></div>
                <button class="next-btn" onclick="goToStep(2)">Далее →</button>
            </div>
        </div>

        <!-- Шаг 2 -->
        <div id="step2" style="display:none;">
            <h2>2. Выберите цвета</h2>
            <div class="color-picker-group">
                <label class="color-label">Корпус:</label>
                <input type="color" id="bodyColor" value="#c0c0c0" oninput="updateColor('body', this.value)">
            </div>
            <div class="color-picker-group">
                <label class="color-label">Крышка:</label>
                <input type="color" id="coverColor" value="#a0a0a0" oninput="updateColor('cover', this.value)">
            </div>
            <div class="nav-buttons">
                <button class="prev-btn" onclick="goToStep(1)">← Назад</button>
                <button class="next-btn" onclick="goToStep(3)">Далее →</button>
            </div>
        </div>

        <!-- Шаг 3 -->
        <div id="step3" style="display:none;">
            <h2>3. Текст на задней крышке</h2>
            <input type="text" id="backText" placeholder="Например: MAG-2026 или имя" maxlength="25" oninput="updateBackText()">
            <div class="nav-buttons">
                <button class="prev-btn" onclick="goToStep(2)">← Назад</button>
                <button class="no-engrave-btn" onclick="clearEngraveAndNext()">Без гравировки</button>
                <button class="next-btn" onclick="finishOrder()">Завершить →</button>
            </div>
        </div>

        <!-- Форма заказа — всё по центру -->
        <div class="order-form" id="orderForm">
            <h2>Готово! Оформление заказа</h2>
            <div id="finalSummary"></div>

            <form action="https://formspree.io/f/ТВОЙ_FORMSPREE_ID" method="POST">
                <input type="hidden" name="Модель" id="hiddenModel">
                <input type="hidden" name="Цвет_корпуса" id="hiddenBodyColor">
                <input type="hidden" name="Цвет_крышки" id="hiddenCoverColor">
                <input type="hidden" name="Гравировка" id="hiddenBackText">

                <input type="text" name="Имя" placeholder="Имя *" required>
                <input type="email" name="Email" placeholder="Email *" required>
                <input type="tel" name="Телефон" placeholder="Телефон *" required>
                <input type="text" name="Адрес" placeholder="Адрес доставки *" required>
                <textarea name="Комментарий" rows="4" placeholder="Комментарий (размер ремешка и т.д.)"></textarea>

                <button type="submit" class="buy-btn">Отправить заказ</button>
            </form>
        </div>
    </div>
</div>

<script>
    let currentStep = 1;
    const config = {
        model: 'clock5pro',
        bodyColor: '#c0c0c0',
        coverColor: '#a0a0a0',
        backText: ''
    };

    function goToStep(step) {
        document.querySelectorAll('[id^="step"]').forEach(el => el.style.display = 'none');
        document.getElementById(`step${step}`).style.display = 'block';
        document.querySelectorAll('.step').forEach(el => {
            el.classList.remove('active', 'completed');
            if (Number(el.dataset.step) < step) el.classList.add('completed');
            if (Number(el.dataset.step) === step) el.classList.add('active');
        });
    }

    function selectModel(id, src, elem) {
        config.model = id;
        document.getElementById('preview-base').src = src;
        document.querySelectorAll('#step1 .option-btn').forEach(el => el.classList.remove('active'));
        elem.classList.add('active');
    }

    function updateColor(part, color) {
        if (part === 'body') config.bodyColor = color;
        if (part === 'cover') config.coverColor = color;
        applyColors();
    }

    function applyColors() {
        const base = document.getElementById('preview-base');
        const bodyHue = getHue(config.bodyColor);
        base.style.filter = `hue-rotate(${bodyHue}deg) saturate(1.4) brightness(1.05)`;
    }

    function getHue(hex) {
        let r = parseInt(hex.slice(1,3),16)/255;
        let g = parseInt(hex.slice(3,5),16)/255;
        let b = parseInt(hex.slice(5,7),16)/255;
        let max = Math.max(r,g,b), min = Math.min(r,g,b);
        if (max === min) return 0;
        let h = 0;
        let d = max - min;
        switch (max) {
            case r: h = (g - b) / d + (g < b ? 6 : 0); break;
            case g: h = (b - r) / d + 2; break;
            case b: h = (r - g) / d + 4; break;
        }
        return h * 60;
    }

    function updateBackText() {
        const text = document.getElementById('backText').value;
        config.backText = text;
        document.getElementById('backTextOverlay').textContent = text;
    }

    function clearEngraveAndNext() {
        document.getElementById('backText').value = '';
        config.backText = '';
        document.getElementById('backTextOverlay').textContent = '';
        finishOrder();
    }

    function finishOrder() {
        document.querySelectorAll('[id^="step"]').forEach(el => el.style.display = 'none');
        document.getElementById('orderForm').style.display = 'block';

        const modelName = {
            clock5pro: 'Clock - 5 Pro',
            clock5: 'Clock - 5',
            clock4p: 'Clock - 4(P)'
        }[config.model];

        document.getElementById('finalSummary').innerHTML = `
            <strong>Ваша кастомизация:</strong><br><br>
            Модель: ${modelName}<br>
            Цвет корпуса: <span style="background:${config.bodyColor}; width:24px; height:24px; display:inline-block; border-radius:6px; vertical-align:middle;"></span> ${config.bodyColor}<br>
            Цвет крышки: <span style="background:${config.coverColor}; width:24px; height:24px; display:inline-block; border-radius:6px; vertical-align:middle;"></span> ${config.coverColor}<br>
            Гравировка: ${config.backText || 'Нет'}
        `;

        document.getElementById('hiddenModel').value = modelName;
        document.getElementById('hiddenBodyColor').value = config.bodyColor;
        document.getElementById('hiddenCoverColor').value = config.coverColor;
        document.getElementById('hiddenBackText').value = config.backText;
    }

    goToStep(1);
</script>
</body>
</html>
