 index.html
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">  
    <title>GameNext Engine Ultra</title>  
    <style>  
        * {  
            box-sizing: border-box;  
            margin: 0;  
            padding: 0;  
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;  
            -webkit-font-smoothing: antialiased;  
        }  
  
        body {  
            background-color: #080b10;  
            color: #f1f5f9;  
            padding: 2rem 1rem;  
            display: flex;  
            flex-direction: column;  
            align-items: center;  
            min-height: 100vh;  
        }  
  
        .container {  
            width: 100%;  
            max-width: 1000px;  
            display: grid;  
            grid-template-columns: 1fr;  
            gap: 1.5rem;  
        }  
  
        header {  
            text-align: center;  
            grid-column: 1 / -1;  
            margin-bottom: 1rem;  
        }  
  
        header h1 {  
            font-size: 3rem;  
            font-weight: 900;  
            letter-spacing: -0.05em;  
            background: linear-gradient(135deg, #3b82f6 0%, #a855f7 100%);  
            -webkit-background-clip: text;  
            -webkit-text-fill-color: transparent;  
            margin-bottom: 0.5rem;  
        }  
  
        .subtitle {  
            color: #64748b;  
            font-size: 1.05rem;  
            font-weight: 500;  
        }  
  
        @media (min-width: 768px) {  
            .container {  
                grid-template-columns: 1fr 1fr;  
            }  
            .full-width {  
                grid-column: 1 / -1;  
            }  
        }  
  
        .card {  
            background: #111827;  
            border: 1px solid #1f2937;  
            padding: 1.5rem;  
            border-radius: 20px;  
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);  
            position: relative;  
            display: flex;  
            flex-direction: column;  
        }  
  
        .card h2 {  
            font-size: 1.15rem;  
            font-weight: 700;  
            color: #f8fafc;  
            margin-bottom: 1rem;  
            display: flex;  
            align-items: center;  
            gap: 0.5rem;  
        }  
  
        .search-wrapper {  
            position: relative;  
            width: 100%;  
        }  
  
        /* RESTORED FLEX LAYOUT FOR INPUT + BUTTON */  
        .form-group {  
            display: flex;  
            gap: 0.5rem;  
            width: 100%;  
        }  
  
        input {  
            flex: 1;  
            padding: 0.85rem 1.25rem;  
            border-radius: 12px;  
            border: 2px solid #1f2937;  
            background-color: #030712;  
            color: white;  
            font-size: 1rem;  
            transition: all 0.2s ease;  
        }  
  
        input:focus {  
            outline: none;  
            border-color: #3b82f6;  
            box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.15);  
        }  
  
        .suggestions-box {  
            position: absolute;  
            top: 105%;  
            left: 0;  
            right: 0;  
            background: #1f2937;  
            border: 1px solid #374151;  
            border-radius: 12px;  
            max-height: 250px;  
            overflow-y: auto;  
            z-index: 100;  
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);  
            display: none;  
        }  
  
        .suggestion-item {  
            padding: 0.85rem 1.25rem;  
            cursor: pointer;  
            border-bottom: 1px solid #374151;  
            font-size: 0.95rem;  
            display: flex;  
            align-items: center;  
            justify-content: space-between;  
            transition: background 0.15s ease;  
        }  
  
        .suggestion-item:last-child { border-bottom: none; }  
        .suggestion-item:hover, .suggestion-item:active { background: #2563eb; color: white; }  
        .suggestion-year { color: #64748b; font-size: 0.8rem; }  
  
        button {  
            padding: 0.85rem 1.5rem;  
            border-radius: 12px;  
            border: none;  
            font-weight: 700;  
            font-size: 0.95rem;  
            cursor: pointer;  
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);  
            -webkit-tap-highlight-color: transparent;  
        }  
  
        button:active { transform: scale(0.98); opacity: 0.9; }  
        button:disabled { opacity: 0.4; cursor: not-allowed; pointer-events: none; }  
  
        /* ADD BUTTON RESTORED VISUAL STYLES */  
        .add-btn { background-color: #3b82f6; color: white; }  
        .add-btn:hover { background-color: #2563eb; }  
          
        .played-btn { background-color: #10b981; color: white; width: 100%; margin-top: 0.5rem; }  
        .later-btn { background-color: #f59e0b; color: white; width: 100%; }  
        .reroll-btn { background-color: #374151; color: #9ca3af; width: 100%; }  
  
        .warning-text {  
            color: #ef4444;  
            font-size: 0.85rem;  
            margin-top: 0.6rem;  
            display: none;  
            font-weight: bold;  
            background-color: rgba(239, 68, 68, 0.1);  
            padding: 0.5rem;  
            border-radius: 8px;  
            border: 1px solid rgba(239, 68, 68, 0.2);  
        }  
  
        .flex-tags {  
            display: flex;  
            flex-wrap: wrap;  
            gap: 0.6rem;  
        }  
  
        .game-tag {  
            display: inline-flex;  
            align-items: center;  
            background-color: #030712;  
            border: 1px solid #1f2937;  
            border-radius: 30px;  
            font-size: 0.9rem;  
            font-weight: 500;  
            padding: 0.15rem 0.4rem 0.15rem 1rem;  
            transition: all 0.2s ease;  
            animation: popIn 0.25s ease-out forwards;  
        }  
  
        .game-title-link {  
            color: #f1f5f9;  
            text-decoration: none;  
            cursor: pointer;  
            display: flex;  
            align-items: center;  
            gap: 0.35rem;  
            padding: 0.4rem 0;  
        }  
  
        .game-title-link:hover { color: #60a5fa; }  
        .game-title-link::after { content: "↗"; font-size: 0.75rem; color: #64748b; }  
  
        .remove-game {  
            padding: 0.4rem 0.6rem;  
            color: #ef4444;  
            cursor: pointer;  
            font-weight: 800;  
            font-size: 1.1rem;  
            line-height: 1;  
        }  
  
        .rec-card {  
            background: linear-gradient(145deg, #0f172a 0%, #1e1b4b; 100%);  
            border: 2px solid #4f46e5;  
            box-shadow: 0 0 25px rgba(79, 70, 229, 0.25);  
            display: none;  
        }  
  
        .rec-title-wrap { display: inline-block; cursor: pointer; margin-bottom: 0.4rem; }  
        .rec-title { font-size: 1.6rem; font-weight: 800; color: #f59e0b; }  
        .rec-title-wrap:hover .rec-title { color: #60a5fa; text-decoration: underline; }  
        .rec-desc { color: #cbd5e1; font-size: 0.98rem; line-height: 1.6; margin-bottom: 1.5rem; }  
        .btn-stack { display: flex; flex-direction: column; gap: 0.6rem; margin-top: auto; }  
        .alert-box { color: #4b5563; font-style: italic; font-size: 0.95rem; text-align: center; width: 100%; padding: 1rem 0; }  
    </style>  
</head>  
<body>  
  
    <div class="container">  
        <header>  
            <h1>GAMENEXT</h1>  
            <p class="subtitle">Intelligent Global Taste Analyzer</p>  
        </header>  
  
        <div class="card full-width">  
            <h2>🎮 Add Favorite Games</h2>  
            <div class="search-wrapper">  
                <div class="form-group">  
                    <input type="text" id="gameInput" placeholder="Type a video game title..." autocomplete="off">  
                    <button class="add-btn" id="addBtn" onclick="manualAddGame()">Add</button>  
                </div>  
                <div class="suggestions-box" id="suggestionsBox"></div>  
                <div class="warning-text" id="errorWarning">⚠️ Game not found! Please type a real video game title.</div>  
            </div>  
        </div>  
  
        <div class="card">  
            <h2>📚 Your Played History</h2>  
            <div id="libraryContainer" class="flex-tags alert-box">Add 3 games to initialize engine calculation.</div>  
        </div>  
  
        <div class="card">  
            <h2>⏳ Saved Play Later Queue</h2>  
            <div id="laterContainer" class="flex-tags alert-box">Your saved shortlist items appear here.</div>  
        </div>  
  
        <div class="card rec-card full-width" id="recCard">  
            <h2>🔥 Engine Recommendation Match</h2>  
            <div class="rec-title-wrap" id="recLink" onclick="openMediaLink(document.getElementById('recTitle').innerText)">  
                <h3 class="rec-title" id="recTitle">Calculating profile weights...</h3>  
            </div>  
            <p class="rec-desc" id="recReason"></p>  
              
            <div class="btn-stack">  
                <button class="played-btn" onclick="markAsPlayed()">✅ Played It! Move to Library</button>  
                <div style="display: flex; gap: 0.5rem; width: 100%;">  
                    <button class="later-btn" onclick="addToPlayLater()">⏳ Queue Later</button>  
                    <button class="reroll-btn" id="rerollBtn" onclick="generateRecommendation()">❌ Not Satisfied? Reroll</button>  
                </div>  
            </div>  
        </div>  
  
    </div>  
  
    <script>  
        const API_URL = 'https://api.rawg.io/api/games?key=69bc8fa7dfbd44fcb278dfccb3d1b82d';  
  
        let myLibrary = JSON.parse(localStorage.getItem('absUserGames')) || [];  
        let playLaterList = JSON.parse(localStorage.getItem('absPlayLater')) || [];  
        let currentRec = null;  
        let searchTimeout = null;  
  
        updateUI();  
  
        function openMediaLink(gameName) {  
            const searchUrl = `https://www.youtube.com/results?search_query=${encodeURIComponent(gameName + ' gameplay trailer')}`;  
            window.open(searchUrl, '_blank');  
        }  
  
        // Dropdown Auto-Search Engine  
        document.getElementById('gameInput').addEventListener('input', function(e) {  
            clearTimeout(searchTimeout);  
            const query = e.target.value.trim();  
            const box = document.getElementById('suggestionsBox');  
            document.getElementById('errorWarning').style.display = 'none';  
  
            if (query.length < 2) {  
                box.style.display = 'none';  
                return;  
            }  
  
            searchTimeout = setTimeout(async () => {  
                try {  
                    const response = await fetch(`${API_URL}&search=${encodeURIComponent(query)}&page_size=5`);  
                    const data = await response.json();  
                      
                    if (data.results && data.results.length > 0) {  
                        box.innerHTML = '';  
                        data.results.forEach(game => {  
                            const year = game.released ? game.released.split('-')[0] : 'N/A';  
                            const div = document.createElement('div');  
                            div.className = 'suggestion-item';  
                            div.innerHTML = `<span>${game.name}</span> <span class="suggestion-year">(${year})</span>`;  
                            div.onclick = () => selectGame(game);  
                            box.appendChild(div);  
                        });  
                        box.style.display = 'block';  
                    } else {  
                        box.style.display = 'none';  
                    }  
                } catch(err) { console.log("Dropdown fetch drop."); }  
            }, 250);  
        });  
  
        document.addEventListener('click', function(e) {  
            if (e.target.id !== 'gameInput') {  
                document.getElementById('suggestionsBox').style.display = 'none';  
            }  
        });  
  
        // HANDLES CLICKING DIRECTLY FROM SUGGESTIONS LIST  
        function selectGame(game) {  
            if (myLibrary.some(g => g.id === game.id)) {  
                alert("This game is already sitting in your history list!");  
                document.getElementById('gameInput').value = '';  
                return;  
            }  
            myLibrary.push({  
                id: [game.id](http://game.id),  
                title: game.name,  
                genres: game.genres.map(g => g.slug)  
            });  
            saveData();  
            document.getElementById('gameInput').value = '';  
            document.getElementById('suggestionsBox').style.display = 'none';  
        }  
  
        // HANDLES MANUAL BUTTON SUBMISSIONS WITH FAKE-NAME WARNING LOGIC  
        async function manualAddGame() {  
            const input = document.getElementById('gameInput');  
            const warning = document.getElementById('errorWarning');  
            const addBtn = document.getElementById('addBtn');  
            const title = input.value.trim();  
  
            if (!title) return;  
            warning.style.display = 'none';  
            addBtn.disabled = true;  
  
            try {  
                const response = await fetch(`${API_URL}&search=${encodeURIComponent(title)}&page_size=1`);  
                const data = await response.json();  
  
                if (!data.results || data.results.length === 0) {  
                    warning.style.display = 'block';  
                    return;  
                }  
  
                const verifiedGame = data.results[0];  
  
                if (myLibrary.some(g => g.id === verifiedGame.id)) {  
                    alert("This game is already sitting in your history list!");  
                    input.value = '';  
                    return;  
                }  
  
                myLibrary.push({  
                    id: [verifiedGame.id](http://verifiedGame.id),  
                    title: verifiedGame.name,  
                    genres: verifiedGame.genres.map(g => g.slug)  
                });  
  
                saveData();  
                input.value = '';  
                document.getElementById('suggestionsBox').style.display = 'none';  
            } catch (err) {  
                warning.style.display = 'block';  
            } finally {  
                addBtn.disabled = false;  
                document.activeElement.blur();  
            }  
        }  
  
        function removeGame(index, type) {  
            if (type === 'library') myLibrary.splice(index, 1);  
            if (type === 'later') playLaterList.splice(index, 1);  
            currentRec = null;  
            saveData();  
        }  
  
        function saveData() {  
            localStorage.setItem('absUserGames', JSON.stringify(myLibrary));  
            localStorage.setItem('absPlayLater', JSON.stringify(playLaterList));  
            updateUI();  
        }  
  
        function updateUI() {  
            const libContainer = document.getElementById('libraryContainer');  
            if (myLibrary.length === 0) {  
                libContainer.className = "flex-tags alert-box";  
                libContainer.innerHTML = "Add 3 games to initialize engine calculation.";  
                document.getElementById('recCard').style.display = 'none';  
            } else {  
                libContainer.className = "flex-tags";  
                libContainer.innerHTML = "";  
                myLibrary.forEach((game, idx) => {  
                    libContainer.innerHTML += `  
                        <div class="game-tag">  
                            <span class="game-title-link" onclick="openMediaLink('${game.title.replace(/'/g, "\\'")}')">${game.title}</span>  
                            <span class="remove-game" onclick="removeGame(${idx}, 'library')">×</span>  
                        </div>`;  
                });  
            }  
  
            const laterContainer = document.getElementById('laterContainer');  
            if (playLaterList.length === 0) {  
                laterContainer.className = "flex-tags alert-box";  
                laterContainer.innerHTML = "Your saved shortlist items appear here.";  
            } else {  
                laterContainer.className = "flex-tags";  
                laterContainer.innerHTML = "";  
                playLaterList.forEach((game, idx) => {  
                    laterContainer.innerHTML += `  
                        <div class="game-tag" style="border-color:#f59e0b">  
                            <span class="game-title-link" onclick="openMediaLink('${game.title.replace(/'/g, "\\'")}')">${game.title}</span>  
                            <span class="remove-game" onclick="removeGame(${idx}, 'later')">×</span>  
                        </div>`;  
                });  
            }  
  
            if (myLibrary.length >= 3) {  
                if (!currentRec) generateRecommendation();  
            } else {  
                document.getElementById('recCard').style.display = 'none';  
                currentRec = null;  
            }  
        }  
  
        async function generateRecommendation() {  
            const recCard = document.getElementById('recCard');  
            const rerollBtn = document.getElementById('rerollBtn');  
              
            document.getElementById('recTitle').innerText = "Analyzing weights...";  
            document.getElementById('recReason').innerText = "Running multi-genre taste alignment algorithms across cloud directories...";  
            recCard.style.display = 'block';  
            rerollBtn.disabled = true;  
  
            const genreMap = {};  
            myLibrary.flatMap(g => g.genres).forEach(gen => {  
                genreMap[gen] = (genreMap[gen] || 0) + 1;  
            });  
  
            const sortedGenres = Object.keys(genreMap).sort((a, b) => genreMap[b] - genreMap[a]);  
              
            let targetGenre = sortedGenres[0] || 'action';  
            if (sortedGenres.length > 1 && Math.random() > 0.6) {  
                targetGenre = sortedGenres[1];   
            }  
  
            const randomPage = Math.floor(Math.random() * 30) + 1;  
  
            try {  
                const response = await fetch(`${API_URL}&genres=${targetGenre}&page=${randomPage}&page_size=25&ordering=-rating`);  
                const data = await response.json();  
  
                const cleanMatches = data.results.filter(game =>   
                    !myLibrary.some(owned => owned.id === game.id) &&  
                    !playLaterList.some(later => later.id === game.id)  
                );  
  
                if (cleanMatches.length > 0) {  
                    const picked = cleanMatches[Math.floor(Math.random() * cleanMatches.length)];  
                      
                    currentRec = {  
                        id: [picked.id](http://picked.id),  
                        title: picked.name,  
                        genres: picked.genres.map(g => g.slug),  
                        desc: `Engine Profile Match: High probability selection matching your logged metadata history. Globally rated at ⭐ ${picked.rating || '4.2'}/5 by players. Click the title header above to explore video coverage.`  
                    };  
  
                    document.getElementById('recTitle').innerText = currentRec.title;  
                    document.getElementById('recReason').innerText = currentRec.desc;  
                } else {  
                    currentRec = null;  
                    generateRecommendation();  
                }  
            } catch (err) {  
                document.getElementById('recTitle').innerText = "Re-routing link...";  
                generateRecommendation();  
            } finally {  
                rerollBtn.disabled = false;  
            }  
        }  
  
        function markAsPlayed() {  
            if (!currentRec) return;  
            myLibrary.push({  
                id: [currentRec.id](http://currentRec.id),  
                title: currentRec.title,  
                genres: currentRec.genres  
            });  
            currentRec = null;  
            saveData();  
        }  
  
        function addToPlayLater() {  
            if (!currentRec) return;  
            if (!playLaterList.some(g => g.id === currentRec.id)) {  
                playLaterList.push({  
                    id: currentRec.id,  
                    title: currentRec.title  
                });  
            }  
            currentRec = null;  
            saveData();  
        }  
    </script>  
</body>  
</html>  
