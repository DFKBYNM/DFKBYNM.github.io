<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>LiteCode Galaxy — Космическая платформа программирования</title>
    <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Orbitron:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Inter', sans-serif;
            background: #010118;
            color: #fff;
            overflow-x: hidden;
            min-height: 100vh;
        }
        /* Космическая заставка с планетами и звёздами */
        .space-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(ellipse at 20% 30%, #0a0a2a, #010110);
        }
        .stars-layer {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(2px 2px at 15px 40px, #fff, rgba(0,0,0,0)),
                radial-gradient(1px 1px at 70px 120px, #fff, rgba(0,0,0,0)),
                radial-gradient(3px 3px at 200px 300px, #fff, rgba(0,0,0,0)),
                radial-gradient(1px 1px at 500px 800px, #fff, rgba(0,0,0,0)),
                radial-gradient(2px 2px at 900px 200px, #fff, rgba(0,0,0,0));
            background-size: 300px 300px, 500px 500px, 800px 800px, 1000px 1000px, 1200px 1200px;
            background-repeat: repeat;
            opacity: 0.8;
            pointer-events: none;
            z-index: -1;
            animation: starMove 80s linear infinite;
        }
        @keyframes starMove {
            0% { background-position: 0 0, 0 0, 0 0, 0 0, 0 0; }
            100% { background-position: 300px 300px, 500px 500px, 800px 800px, 1000px 1000px, 1200px 1200px; }
        }
        /* Планеты */
        .planet {
            position: fixed;
            border-radius: 50%;
            filter: blur(3px);
            opacity: 0.5;
            z-index: -1;
            pointer-events: none;
            animation: floatPlanet 30s infinite alternate ease-in-out;
        }
        .planet-1 { width: 220px; height: 220px; background: radial-gradient(circle at 30% 30%, #ffaa66, #aa4422); top: 5%; left: -80px; }
        .planet-2 { width: 350px; height: 350px; background: radial-gradient(circle at 60% 40%, #88aaff, #2244aa); bottom: -100px; right: -100px; animation-duration: 40s; }
        .planet-3 { width: 150px; height: 150px; background: radial-gradient(circle at 70% 20%, #aaffaa, #228844); top: 50%; left: 80%; animation-duration: 20s; }
        .planet-4 { width: 100px; height: 100px; background: radial-gradient(circle at 40% 60%, #ff88cc, #aa2266); top: 70%; left: 10%; animation-duration: 25s; }
        .planet-5 { width: 280px; height: 280px; background: radial-gradient(circle at 50% 50%, #ffcc66, #cc8822); top: 15%; right: 15%; animation-duration: 35s; opacity: 0.3; }
        @keyframes floatPlanet {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(30px, 30px) rotate(15deg); }
        }

        /* Основной стиль */
        .header {
            text-align: center;
            padding: 2.5rem 1rem;
            background: rgba(0,0,0,0.55);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(168,85,247,0.6);
            position: relative;
            z-index: 10;
        }
        .header h1 {
            font-family: 'Orbitron', monospace;
            font-size: 3rem;
            background: linear-gradient(135deg, #a855f7, #ec4899, #facc15);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .badge {
            display: inline-block;
            background: #7c3aed;
            padding: 0.3rem 1.2rem;
            border-radius: 40px;
            font-size: 0.8rem;
            margin-top: 12px;
        }
        .groups {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 12px;
            background: rgba(0,0,0,0.65);
            backdrop-filter: blur(12px);
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 20;
            border-bottom: 1px solid #a855f7;
        }
        .group-btn {
            background: #1f1a3e;
            border: none;
            padding: 10px 28px;
            border-radius: 60px;
            color: #ddd;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }
        .group-btn.active {
            background: linear-gradient(135deg, #7c3aed, #a855f7);
            color: white;
            box-shadow: 0 0 12px #a855f7;
        }
        .content {
            max-width: 1500px;
            margin: 2rem auto;
            padding: 0 20px;
            position: relative;
            z-index: 2;
        }
        .card-3d {
            background: rgba(15, 10, 35, 0.7);
            backdrop-filter: blur(12px);
            border-radius: 32px;
            padding: 2rem;
            border: 1px solid rgba(168,85,247,0.4);
            transition: 0.25s;
            transform: translateZ(10px);
            margin-bottom: 2rem;
        }
        .card-3d:hover {
            transform: translateZ(25px);
            border-color: #ec4899;
        }
        .btn-glow {
            background: linear-gradient(145deg, #4c1d95, #6d28d9);
            border: none;
            padding: 12px 28px;
            border-radius: 60px;
            color: white;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.1s;
            box-shadow: 0 6px 0 #2e1065;
        }
        .btn-glow:active { transform: translateY(2px); box-shadow: 0 2px 0 #2e1065; }
        .tasks-area { display: none; }
        .tasks-area.active-area { display: block; }
        .tasks-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(440px, 1fr));
            gap: 1.8rem;
        }
        .task-item {
            background: rgba(0,0,0,0.6);
            border-radius: 28px;
            padding: 1.5rem;
            border-left: 6px solid #a855f7;
        }
        textarea, input {
            width: 100%;
            padding: 14px;
            background: #0a0820;
            border: 1px solid #7c3aed;
            border-radius: 24px;
            color: white;
            font-family: monospace;
            font-size: 1rem;
            margin: 12px 0;
        }
        .hint-text {
            background: #1e1a3a;
            padding: 8px 12px;
            border-radius: 24px;
            font-size: 0.85rem;
        }
        .progress-bar {
            height: 20px;
            background: #2d2a4a;
            border-radius: 30px;
            overflow: hidden;
            margin: 12px 0;
        }
        .progress-fill {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #a855f7, #ec4899);
        }
        .resource-link {
            display: inline-block;
            background: rgba(168,85,247,0.2);
            padding: 8px 18px;
            border-radius: 40px;
            margin: 8px 12px 8px 0;
            transition: 0.2s;
            color: #c084fc;
            text-decoration: none;
            font-weight: 500;
        }
        .resource-link:hover {
            background: #a855f7;
            color: white;
            transform: scale(1.03);
        }
        .course-item {
            background: #0f0b2a;
            border-radius: 24px;
            padding: 12px;
            margin: 10px 0;
        }
        footer {
            text-align: center;
            padding: 2rem;
            background: rgba(0,0,0,0.6);
            margin-top: 4rem;
        }
        @media (max-width: 700px) {
            .tasks-grid { grid-template-columns: 1fr; }
            .header h1 { font-size: 2rem; }
        }
    </style>
</head>
<body>
<div class="space-bg"></div>
<div class="stars-layer"></div>
<div class="planet planet-1"></div>
<div class="planet planet-2"></div>
<div class="planet planet-3"></div>
<div class="planet planet-4"></div>
<div class="planet planet-5"></div>

<div class="header">
    <h1>🌌 LiteCode Galaxy 🌌</h1>
    <p>200+ заданий по HTML, JS, Python | Космический прогресс | Бэкап на Python и Java</p>
    <div class="badge">💾 Сохраняй прогресс в облако</div>
</div>

<div class="groups">
    <button class="group-btn active" data-group="home">🏠 Главная</button>
    <button class="group-btn" data-group="html">📄 HTML (70 заданий)</button>
    <button class="group-btn" data-group="js">⚡ JavaScript (65)</button>
    <button class="group-btn" data-group="python">🐍 Python (65)</button>
    <button class="group-btn" data-group="courses">📚 Пользовательские курсы</button>
</div>

<div class="content">
    <div id="home-group" class="tasks-area active-area">
        <div class="card-3d">
            <h2>🏆 Твой прогресс (синхронизация с бэкендом)</h2>
            <div class="progress-bar"><div class="progress-fill" id="globalProgress"></div></div>
            <p id="pointsText">⭐ Очки: 0 / 2000</p>
            <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                <button class="btn-glow" onclick="saveProgressToBackend()">💾 Сохранить прогресс в облако</button>
                <button class="btn-glow" onclick="loadProgressFromBackend()">☁️ Загрузить прогресс</button>
                <button class="btn-glow" onclick="takeScreenshot()">📸 Скриншот</button>
            </div>
            <div id="qrcode" style="margin-top: 15px;"></div>
        </div>
        <div class="card-3d">
            <h3>📚 Официальные ресурсы (десятки ссылок)</h3>
            <a class="resource-link" href="https://practicum.yandex.ru" target="_blank">Яндекс Практикум</a>
            <a class="resource-link" href="https://stepik.org" target="_blank">Stepik</a>
            <a class="resource-link" href="https://htmlacademy.ru" target="_blank">HTML Academy</a>
            <a class="resource-link" href="https://learn.microsoft.com/ru-ru/training/" target="_blank">Microsoft Learn</a>
            <a class="resource-link" href="https://thecode.media" target="_blank">Код.медиа</a>
            <a class="resource-link" href="https://ru.hexlet.io" target="_blank">Хекслет</a>
            <a class="resource-link" href="https://www.coursera.org/" target="_blank">Coursera</a>
            <a class="resource-link" href="https://www.udemy.com/" target="_blank">Udemy</a>
            <a class="resource-link" href="https://code-basics.com/ru/" target="_blank">Code Basics</a>
            <a class="resource-link" href="https://metanit.com/" target="_blank">Metanit</a>
            <a class="resource-link" href="https://developer.mozilla.org/ru/" target="_blank">MDN Web Docs</a>
            <a class="resource-link" href="https://habr.com/ru/" target="_blank">Habr</a>
            <a class="resource-link" href="https://ru.wikipedia.org/wiki/HTML" target="_blank">Википедия HTML</a>
            <a class="resource-link" href="https://www.w3schools.com/" target="_blank">W3Schools (англ.)</a>
        </div>
    </div>

    <div id="html-group" class="tasks-area"><div class="tasks-grid" id="htmlTasksList"></div></div>
    <div id="js-group" class="tasks-area"><div class="tasks-grid" id="jsTasksList"></div></div>
    <div id="python-group" class="tasks-area"><div class="tasks-grid" id="pythonTasksList"></div></div>

    <div id="courses-group" class="tasks-area">
        <div class="card-3d">
            <h3>➕ Добавить новый курс / урок</h3>
            <input type="text" id="courseTitle" placeholder="Название курса">
            <textarea id="courseDesc" rows="2" placeholder="Описание / ссылка"></textarea>
            <button class="btn-glow" onclick="addUserCourse()">➕ Добавить курс</button>
            <div id="userCoursesList" style="margin-top: 20px;">
                <h4>📖 Добавленные сообществом курсы:</h4>
                <div id="coursesContainer"></div>
            </div>
        </div>
    </div>
</div>
<footer>© LiteCode Galaxy — 200 заданий, космический дизайн, бэкап на Python/Java, хостинг GitHub Pages + Render</footer>

<script>
    // ---------- ГЕНЕРАЦИЯ 200 ЗАДАНИЙ ----------
    function generateTasks(count, lang) {
        let tasks = [];
        for (let i = 1; i <= count; i++) {
            let text, answer, hint;
            if (lang === 'html') {
                if (i <= 25) { text = `Создай заголовок h${(i%3)+1} с текстом "Заголовок ${i}"`; answer = `<h${(i%3)+1}>Заголовок ${i}</h${(i%3)+1}>`; hint = `Пример: <h${(i%3)+1}>Заголовок ${i}</h${(i%3)+1}>`; }
                else if (i <= 50) { text = `Создай абзац с классом "text-${i}" и текстом "Учу HTML"`; answer = `<p class="text-${i}">Учу HTML</p>`; hint = `<p class="text-${i}">Учу HTML</p>`; }
                else { text = `Создай ссылку на сайт "https://example.com" с текстом "Пример ${i}"`; answer = `<a href="https://example.com">Пример ${i}</a>`; hint = `<a href="...">Пример</a>`; }
            } else if (lang === 'js') {
                if (i <= 20) { text = `Объяви переменную let x${i} = ${i*2}`; answer = `let x${i} = ${i*2};`; hint = `let x${i} = ${i*2};`; }
                else if (i <= 45) { text = `Напиши функцию, которая возвращает строку "JS Уровень ${i}"`; answer = `function getMsg() { return "JS Уровень ${i}"; }`; hint = `function getMsg() { return "..."; }`; }
                else { text = `Создай массив из трёх чисел: 5, 10, 15`; answer = `let arr = [5,10,15];`; hint = `let arr = [5,10,15];`; }
            } else {
                if (i <= 20) { text = `Создай переменную var${i} = ${i*3}`; answer = `var${i} = ${i*3}`; hint = `var${i} = ${i*3}`; }
                else if (i <= 45) { text = `Напиши функцию, печатающую "Python task ${i}"`; answer = `def f():\n    print("Python task ${i}")`; hint = `def f(): print(...)`; }
                else { text = `Создай список из чисел от 1 до 5`; answer = `nums = [1,2,3,4,5]`; hint = `nums = [1,2,3,4,5]`; }
            }
            tasks.push({ id: i, text, answer, hint, completed: false, points: 10, wrongAttempts: 0 });
        }
        return tasks;
    }

    let htmlTasks = generateTasks(70, 'html');
    let jsTasks = generateTasks(65, 'js');
    let pythonTasks = generateTasks(65, 'python');

    // Прогресс (локальный + бэкап)
    let progress = {
        html: JSON.parse(localStorage.getItem('htmlProg')) || {},
        js: JSON.parse(localStorage.getItem('jsProg')) || {},
        python: JSON.parse(localStorage.getItem('pythonProg')) || {}
    };
    let userId = "user_" + Math.random().toString(36).substr(2, 8);
    if (!localStorage.getItem('userId')) {
        localStorage.setItem('userId', userId);
    } else {
        userId = localStorage.getItem('userId');
    }

    function saveProgress() {
        localStorage.setItem('htmlProg', JSON.stringify(progress.html));
        localStorage.setItem('jsProg', JSON.stringify(progress.js));
        localStorage.setItem('pythonProg', JSON.stringify(progress.python));
        updateGlobalProgress();
    }

    function updateGlobalProgress() {
        let totalPoints = 0, totalMax = 0;
        [htmlTasks, jsTasks, pythonTasks].forEach((tasks, idx) => {
            let lang = idx === 0 ? 'html' : (idx === 1 ? 'js' : 'python');
            tasks.forEach(t => {
                totalMax += t.points;
                if (progress[lang][t.id]) totalPoints += t.points;
            });
        });
        let percent = totalMax ? (totalPoints / totalMax) * 100 : 0;
        document.getElementById('globalProgress').style.width = percent + '%';
        document.getElementById('pointsText').innerHTML = `⭐ Очки: ${totalPoints} / ${totalMax}`;
    }

    function checkAnswer(userAns, correctAns) {
        let normUser = userAns.trim().toLowerCase().replace(/\s+/g, ' ');
        let normCorrect = correctAns.toLowerCase().replace(/\s+/g, ' ');
        return normUser.includes(normCorrect) || normCorrect.includes(normUser);
    }

    window.submitTask = function(lang, taskId, taskObj) {
        let input = document.getElementById(`${lang}_inp_${taskId}`);
        let fb = document.getElementById(`${lang}_fb_${taskId}`);
        let revealBtn = document.getElementById(`reveal_${lang}_${taskId}`);
        if (!input.value.trim()) { fb.innerHTML = "❌ Введи код!"; fb.style.color = "#f66"; return; }
        if (checkAnswer(input.value, taskObj.answer)) {
            if (!progress[lang][taskId]) {
                progress[lang][taskId] = { done: true, points: taskObj.points };
                saveProgress();
                fb.innerHTML = `✅ Верно! +${taskObj.points} очков!`;
                fb.style.color = "#8bc34a";
                document.getElementById(`${lang}_card_${taskId}`).classList.add('completed');
                taskObj.wrongAttempts = 0;
                if (revealBtn) revealBtn.style.display = 'none';
            } else {
                fb.innerHTML = "✅ Уже выполнено!";
                fb.style.color = "#ffd966";
            }
        } else {
            taskObj.wrongAttempts = (taskObj.wrongAttempts || 0) + 1;
            if (taskObj.wrongAttempts >= 5) {
                if (revealBtn) revealBtn.style.display = 'inline-block';
                fb.innerHTML = `❌ Ошибок: ${taskObj.wrongAttempts}. Нажми "Показать ответ"`;
            } else {
                fb.innerHTML = `❌ Неверно. Попыток до подсказки: ${5-taskObj.wrongAttempts}. Подсказка: ${taskObj.hint}`;
            }
            fb.style.color = "#f66";
        }
    };

    window.revealAnswer = function(lang, taskId, taskObj) {
        let fb = document.getElementById(`${lang}_fb_${taskId}`);
        fb.innerHTML = `💡 Правильный ответ: ${taskObj.answer}`;
        fb.style.color = "#ffd966";
    };

    function renderTasks(lang, tasks, containerId) {
        let container = document.getElementById(containerId);
        if (!container) return;
        container.innerHTML = '';
        tasks.forEach(task => {
            let completed = progress[lang][task.id];
            let card = document.createElement('div');
            card.className = `task-item ${completed ? 'completed' : ''}`;
            card.id = `${lang}_card_${task.id}`;
            card.innerHTML = `
                <div style="display:flex; justify-content:space-between;"><strong>📌 Задание ${task.id}</strong> <span class="badge" style="background:#6d28d9;">${task.points} pts</span></div>
                <div style="margin: 10px 0;">${task.text}</div>
                <textarea rows="3" id="${lang}_inp_${task.id}" placeholder="Напишите код..."></textarea>
                <div class="hint-text">💡 Подсказка: ${task.hint}</div>
                <button class="btn-glow" style="padding:6px 18px;" onclick="submitTask('${lang}', ${task.id}, ${JSON.stringify(task).replace(/"/g, '&quot;')})">✅ Проверить</button>
                <button id="reveal_${lang}_${task.id}" class="btn-glow" style="display:none; margin-left:10px;" onclick="revealAnswer('${lang}', ${task.id}, ${JSON.stringify(task).replace(/"/g, '&quot;')})">📖 Ответ</button>
                <div id="${lang}_fb_${task.id}" style="margin-top:8px;">${completed ? '✅ Выполнено' : ''}</div>
            `;
            container.appendChild(card);
        });
    }

    // Пользовательские курсы
    let userCourses = JSON.parse(localStorage.getItem('userCourses')) || [];
    function renderUserCourses() {
        let container = document.getElementById('coursesContainer');
        if (!container) return;
        container.innerHTML = '';
        userCourses.forEach((course, idx) => {
            let div = document.createElement('div');
            div.className = 'course-item';
            div.innerHTML = `<strong>${course.title}</strong><br>${course.desc}<br><button class="btn-glow" style="margin-top:6px;" onclick="removeCourse(${idx})">🗑️ Удалить</button>`;
            container.appendChild(div);
        });
    }
    window.addUserCourse = function() {
        let title = document.getElementById('courseTitle').value.trim();
        let desc = document.getElementById('courseDesc').value.trim();
        if (!title) return alert("Введите название курса");
        userCourses.push({ title, desc });
        localStorage.setItem('userCourses', JSON.stringify(userCourses));
        renderUserCourses();
        document.getElementById('courseTitle').value = '';
        document.getElementById('courseDesc').value = '';
    };
    window.removeCourse = function(idx) {
        userCourses.splice(idx,1);
        localStorage.setItem('userCourses', JSON.stringify(userCourses));
        renderUserCourses();
    };
    renderUserCourses();

    // Скриншот и QR
    window.takeScreenshot = function() {
        html2canvas(document.body).then(canvas => {
            let link = document.createElement('a');
            link.download = 'litecode_screenshot.png';
            link.href = canvas.toDataURL();
            link.click();
        });
    };
    new QRCode(document.getElementById("qrcode"), { text: window.location.href, width: 120, height: 120 });

    // ---------- БЭКАП НА PYTHON И JAVA (API) ----------
    const BACKEND_URL = "https://your-render-backend.onrender.com/api/progress"; // Замените на ваш Render URL
    // Для локального теста используйте: const BACKEND_URL = "http://localhost:5000/api/progress";

    window.saveProgressToBackend = async function() {
        let allProgress = {
            html: progress.html,
            js: progress.js,
            python: progress.python
        };
        try {
            let resp = await fetch(`${BACKEND_URL}/${userId}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(allProgress)
            });
            if (resp.ok) alert("✅ Прогресс сохранён на сервере!");
            else alert("Ошибка сохранения. Убедитесь, что бэкенд запущен.");
        } catch(e) { alert("Не удалось подключиться к серверу. Запустите бэкенд локально или на Render."); }
    };

    window.loadProgressFromBackend = async function() {
        try {
            let resp = await fetch(`${BACKEND_URL}/${userId}`);
            if (resp.ok) {
                let data = await resp.json();
                if (data.html) progress.html = data.html;
                if (data.js) progress.js = data.js;
                if (data.python) progress.python = data.python;
                saveProgress();
                renderTasks('html', htmlTasks, 'htmlTasksList');
                renderTasks('js', jsTasks, 'jsTasksList');
                renderTasks('python', pythonTasks, 'pythonTasksList');
                alert("Прогресс загружен из облака!");
            } else alert("Нет сохранённого прогресса");
        } catch(e) { alert("Ошибка загрузки"); }
    };

    // Переключение вкладок
    document.querySelectorAll('.group-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            let group = this.dataset.group;
            document.querySelectorAll('.tasks-area').forEach(area => area.classList.remove('active-area'));
            document.getElementById(`${group}-group`).classList.add('active-area');
            document.querySelectorAll('.group-btn').forEach(b => b.classList.remove('active'));
            this.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
    });

    renderTasks('html', htmlTasks, 'htmlTasksList');
    renderTasks('js', jsTasks, 'jsTasksList');
    renderTasks('python', pythonTasks, 'pythonTasksList');
    updateGlobalProgress();
</script>
</body>
</html>
