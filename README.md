# Mowky-files-<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MOWKY Files - Community Prototype</title>
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent-color: #8b5cf6;
            --accent-hover: #7c3aed;
            --text-color: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --danger-color: #ef4444;
            --success-color: #22c55e;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            border-bottom: 2px solid var(--border-color);
            margin-bottom: 30px;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--accent-color);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-badge {
            background: var(--card-bg);
            padding: 8px 16px;
            border-radius: 20px;
            border: 1px solid var(--border-color);
            font-size: 0.9rem;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
        }

        @media (min-width: 768px) {
            .grid {
                grid-template-columns: 2fr 1fr;
            }
        }

        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 20px;
            border: 1px solid var(--border-color);
            margin-bottom: 25px;
        }

        .card h2 {
            font-size: 1.3rem;
            margin-bottom: 15px;
            color: var(--accent-color);
        }

        input[type="text"], textarea, select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
            background: var(--bg-color);
            color: var(--text-color);
            margin-bottom: 12px;
            font-size: 0.95rem;
        }

        button {
            background: var(--accent-color);
            color: white;
            border: none;
            padding: 10px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
        }

        button:hover {
            background: var(--accent-hover);
        }

        button.btn-danger {
            background: var(--danger-color);
        }

        .post {
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 15px;
        }

        .post:last-child {
            border-bottom: none;
        }

        .post-author {
            font-weight: bold;
            font-size: 0.9rem;
            color: var(--accent-color);
        }

        .post-date {
            font-size: 0.75rem;
            color: var(--text-muted);
        }

        .quiz-option {
            display: block;
            margin: 10px 0;
            padding: 10px;
            background: var(--bg-color);
            border-radius: 8px;
            cursor: pointer;
            border: 1px solid var(--border-color);
        }

        .quiz-option:hover {
            border-color: var(--accent-color);
        }

        .quiz-result {
            margin-top: 15px;
            font-weight: bold;
        }

        .notice-box {
            background: rgba(239, 68, 68, 0.1);
            border: 1px solid var(--danger-color);
            padding: 15px;
            border-radius: 8px;
            font-size: 0.85rem;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <div class="logo">
                📂 MOWKY Files
            </div>
            <div class="user-badge" id="userDisplay">
                Angemeldet als: <strong>The Mowky Admin</strong>
            </div>
        </header>

        <div class="grid">
            <!-- Hauptspalte: Editor & Feed -->
            <main>
                <!-- Editor -->
                <div class="card">
                    <h2>Neuen Beitrag erstellen</h2>
                    <input type="text" id="postTitle" placeholder="Titel des Beitrags...">
                    <textarea id="postContent" rows="4" placeholder="Wie tief seid ihr in dem Thema drinne und was meint ihr dazu?"></textarea>
                    <button onclick="createPost()">Beitrag veröffentlichen</button>
                </div>

                <!-- Feed -->
                <div class="card">
                    <h2>Community Feed</h2>
                    <div id="postsFeed">
                        <!-- Beiträge werden hier dynamisch eingefügt -->
                    </div>
                </div>
            </main>

            <!-- Seitenleiste: Quiz & Admin Tools -->
            <aside>
                <!-- Quiz Widget -->
                <div class="card">
                    <h2>Community Quiz</h2>
                    <p><strong>Frage:</strong> Was ist das Geheimrezept für gute Laune?</p>
                    <div id="quizForm">
                        <label class="quiz-option"><input type="radio" name="quiz" value="A"> A) Viel Kaffee</label>
                        <label class="quiz-option"><input type="radio" name="quiz" value="B"> B) Ein gutes Video auf Mowky Files</label>
                        <label class="quiz-option"><input type="radio" name="quiz" value="C"> C) Den ganzen Tag schlafen</label>
                        <label class="quiz-option"><input type="radio" name="quiz" value="D"> D) Laut singen</label>
                        <button onclick="checkQuiz()">Antwort prüfen</button>
                    </div>
                    <div id="quizResult" class="quiz-result"></div>
                </div>

                <!-- Data & Backup Tools -->
                <div class="card">
                    <h2>Verwaltung & Backup</h2>
                    <button onclick="exportData()" style="width: 100%; margin-bottom: 10px;">JSON Backup Exportieren</button>
                    <button onclick="clearLocalStorage()" class="btn-danger" style="width: 100%;">Lokalen Cache leeren</button>
                    
                    <div class="notice-box">
                        <strong>Hinweis:</strong> Dies ist ein Prototyp. Alle Daten werden lokal in deinem Browser (IndexedDB/LocalStorage) gespeichert.
                    </div>
                </div>
            </aside>
        </div>
    </div>

    <script>
        // Standard-Beiträge beim ersten Laden
        const defaultPosts = [
            {
                author: "The Mowky Admin",
                date: "14.11.2026",
                title: "Wie tief seid ihr in dem Thema drinne und was meint ihr dazu?",
                content: "Willkommen auf MOWKY Files! Nutzt den Editor oben, um eure Beiträge und Gedanken zu teilen."
            }
        ];

        // Lade Beiträge aus dem LocalStorage
        function loadPosts() {
            const feed = document.getElementById('postsFeed');
            const stored = localStorage.getItem('mowky_posts');
            const posts = stored ? JSON.parse(stored) : defaultPosts;

            feed.innerHTML = posts.map(p => `
                <div class="post">
                    <div class="post-author">${escapeHtml(p.author)}</div>
                    <div class="post-date">${p.date}</div>
                    <h3 style="margin: 5px 0;">${escapeHtml(p.title)}</h3>
                    <p>${escapeHtml(p.content)}</p>
                </div>
            `).join('');
        }

        // Neuer Beitrag erstellen
        function createPost() {
            const titleInput = document.getElementById('postTitle');
            const contentInput = document.getElementById('postContent');

            if (!titleInput.value.trim() || !contentInput.value.trim()) {
                alert('Bitte Titel und Inhalt ausfüllen!');
                return;
            }

            const stored = localStorage.getItem('mowky_posts');
            const posts = stored ? JSON.parse(stored) : [...defaultPosts];

            const newPost = {
                author: "The Mowky Admin",
                date: new Date().toLocaleDateString('de-DE'),
                title: titleInput.value,
                content: contentInput.value
            };

            posts.unshift(newPost);
            localStorage.setItem('mowky_posts', JSON.stringify(posts));

            titleInput.value = '';
            contentInput.value = '';
            loadPosts();
        }

        // Quiz Prüfung
        function checkQuiz() {
            const selected = document.querySelector('input[name="quiz"]:checked');
            const resultDiv = document.getElementById('quizResult');

            if (!selected) {
                resultDiv.innerText = "Bitte wähle eine Antwort aus!";
                resultDiv.style.color = "var(--danger-color)";
                return;
            }

            if (selected.value === 'B') {
                resultDiv.innerText = "1 von 1 richtig! 🎉 Perfekt!";
                resultDiv.style.color = "var(--success-color)";
            } else {
                resultDiv.innerText = "Falsch! Versuch es noch einmal.";
                resultDiv.style.color = "var(--danger-color)";
            }
        }

        // Backup Exportieren
        function exportData() {
            const data = localStorage.getItem('mowky_posts') || JSON.stringify(defaultPosts);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'mowky_files_backup.json';
            a.click();
        }

        // Cache leeren
        function clearLocalStorage() {
            if (confirm("Möchtest du wirklich alle lokalen Beiträge zurücksetzen?")) {
                localStorage.removeItem('mowky_posts');
                loadPosts();
            }
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;");
        }

        // Initiales Laden
        loadPosts();
    </script>
</body>
</html>
