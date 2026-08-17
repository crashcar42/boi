# boi
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Hub</title>
    <style>
        body { margin: 0; background: #0b0b0b; color: #fff; text-align: center; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; overflow: hidden; }
        .nav { height: 8vh; background: #161616; display: flex; align-items: center; justify-content: center; gap: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.5); }
        .nav a { color: #aaa; text-decoration: none; font-weight: 600; font-size: 15px; cursor: pointer; transition: 0.2s; padding: 5px 10px; border-radius: 4px; }
        .nav a:hover, .nav a.active { color: #00ffcc; background: #222; }
        
        .container { display: flex; height: 92vh; }
        .sidebar { width: 20%; background: #121212; display: flex; flex-direction: column; gap: 10px; padding: 15px; box-sizing: border-box; overflow-y: auto; border-right: 1px solid #222; }
        .sidebar button { background: #1e1e1e; border: 1px solid #333; color: #fff; padding: 12px; border-radius: 6px; cursor: pointer; text-align: left; transition: 0.2s; font-size: 14px; }
        .sidebar button:hover { background: #00ffcc; color: #000; font-weight: bold; }
        
        .main-content { width: 80%; height: 100%; background: #000; position: relative; }
        iframe { width: 100%; height: 100%; border: none; }
        
        .movie-search-box { position: absolute; top: 20px; left: 50%; transform: translateX(-50%); background: rgba(20,20,20,0.95); padding: 20px; border-radius: 8px; border: 1px solid #333; display: none; z-index: 10; width: 300px; box-shadow: 0 4px 20px rgba(0,0,0,0.8); }
        .movie-search-box input { width: 90%; padding: 8px; margin-bottom: 10px; background: #222; border: 1px solid #444; color: #fff; border-radius: 4px; }
        .movie-search-box button { width: 96%; background: #00ffcc; border: none; color: #000; padding: 8px; border-radius: 4px; font-weight: bold; cursor: pointer; }
    </style>
</head>
<body>

    <!-- Main Navigation Top Bar -->
    <div class="nav">
        <a id="tab-games" class="active" onclick="switchMode('games')">🎮 Games</a>
        <a id="tab-movies" onclick="switchMode('movies')">🎬 Movies & Shows</a>
    </div>

    <div class="container">
        <!-- Dynamic Sidebar for Selection -->
        <div class="sidebar" id="sidebar-links">
            <!-- Default Games will load here -->
        </div>

        <!-- Main Display Frame -->
        <div class="main-content">
            <!-- Floating Movie Content Searcher -->
            <div class="movie-search-box" id="movie-panel">
                <h4 style="margin:0 0 10px 0;">Stream Dashboard</h4>
                <p style="font-size:12px; color:#aaa; margin:0 0 10px 0;">Enter IMDB Code (e.g., tt0111161 for Shawshank)</p>
                <input type="text" id="imdb-id" placeholder="tt1234567">
                <button onclick="loadMovie()">Launch Player</button>
            </div>
            <iframe id="display-frame" src="https://pacman.com"></iframe>
        </div>
    </div>

    <script>
        const frame = document.getElementById('display-frame');
        const sidebar = document.getElementById('sidebar-links');
        const moviePanel = document.getElementById('movie-panel');

        // Lists of links for both modes
        const games = [
            { name: "Pac-Man", url: "https://pacman.com" },
            { name: "Tetris", url: "https://tetris.com" }
        ];

        const movies = [
            { name: "Trending Movies Feed", url: "https://vidsrc.to" },
            { name: "Alternative Database Feed", url: "https://vidsrc.cc" }
        ];

        function populateSidebar(items, isMovieMode) {
            sidebar.innerHTML = "";
            items.forEach(item => {
                let btn = document.createElement('button');
                btn.innerText = item.name;
                btn.onclick = () => {
                    frame.src = item.url;
                };
                sidebar.appendChild(btn);
            });
        }

        function switchMode(mode) {
            document.getElementById('tab-games').classList.remove('active');
            document.getElementById('tab-movies').classList.remove('active');

            if(mode === 'games') {
                document.getElementById('tab-games').classList.add('active');
                moviePanel.style.display = 'none';
                populateSidebar(games, false);
                frame.src = games[0].url;
            } else {
                document.getElementById('tab-movies').classList.add('active');
                moviePanel.style.display = 'block';
                populateSidebar(movies, true);
                frame.src = movies[0].url;
            }
        }

        function loadMovie() {
            let id = document.getElementById('imdb-id').value.trim();
            if(id) {
                // Generates direct embed parsing stream
                frame.src = `https://vidsrc.to{id}`;
            }
        }

        // Initialize with games list loaded
        populateSidebar(games, false);
    </script>
</body>
</html>
