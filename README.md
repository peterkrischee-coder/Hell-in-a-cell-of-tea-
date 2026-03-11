# Hell-in-a-cell-of-tea-
Sip enjoy and have a tables ladders and chair <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HELL IN A CELL: THE COFFIN</title>
    <style>
        :root { 
            --deep-blue: #0000FF; 
            --crimson: #FF0000; 
            --electric-cyan: #00FFFF;
            --glass: rgba(255, 255, 255, 0.05);
        }

        /* THE COFFIN VIBE - PITCH BLACK WITH RISING NEON FOG */
        body { 
            background: #000;
            background-image: linear-gradient(to top, rgba(0, 0, 255, 0.4) 0%, rgba(255, 0, 0, 0.4) 15%, transparent 50%);
            background-attachment: fixed;
            color: #FFFFFF; /* High contrast "Teeth" white */
            font-family: 'Verdana', sans-serif; 
            padding: 20px; 
            min-height: 100vh; 
            font-weight: bold; 
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* SCREEN SHAKE */
        @keyframes shake {
            0% { transform: translate(2px, 2px); }
            25% { transform: translate(-2px, -2px); }
            50% { transform: translate(3px, -1px); }
            75% { transform: translate(-1px, 2px); }
            100% { transform: translate(2px, -2px); }
        }
        .shaking { animation: shake 0.15s infinite; }

        /* CENA BLAST */
        @keyframes cena-blast {
            0% { transform: scale(1.2); filter: brightness(3) blur(0px); }
            100% { transform: translateX(3000px) rotate(20deg); opacity: 0; filter: blur(10px); }
        }
        .blasting { animation: cena-blast 0.6s ease-in forwards; }

        /* NAVIGATION */
        nav { width: 100%; display: flex; justify-content: center; gap: 10px; margin-bottom: 30px; }
        .nav-btn { 
            background: var(--glass); 
            border: 1px solid #333; 
            color: #888; 
            padding: 12px; 
            border-radius: 5px; 
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .id-card { border-bottom: 2px solid #222; padding: 20px; width: 100%; text-align: center; margin-bottom: 30px; }
        
        /* THE CAGE */
        #cage-btn { font-size: 120px; cursor: pointer; transition: 0.2s; filter: drop-shadow(0 0 20px var(--crimson)); margin: 20px 0; }
        #cage-btn:active { transform: scale(0.7); filter: brightness(3); }

        .card { 
            background: #080808; 
            border: 1px solid #1a1a1a; 
            padding: 20px; 
            border-radius: 4px; 
            margin-top: 15px; 
            width: 90%; 
            box-shadow: 0 0 15px rgba(0,255,255,0.1);
        }
        
        textarea { 
            width: 90%; height: 100px; 
            background: #050505; 
            color: #fff; 
            border: 1px solid #222; 
            border-radius: 2px; 
            padding: 15px; 
            font-size: 1.1rem;
            outline: none;
        }
        textarea:focus { border-color: var(--electric-cyan); }
        
        #p-fill { height: 100%; background: linear-gradient(90deg, var(--deep-blue), var(--crimson)); width: 0%; transition: 0.8s; }
    </style>
</head>
<body onload="loadData()">

    <nav>
        <button class="nav-btn" onclick="showRoom('p-room')">The Cell</button>
        <button class="nav-btn" onclick="showRoom('t-room')">The Porch</button>
        <button class="nav-btn" style="color:#ff0000;" onclick="clearMem()">Reset Memory</button>
    </nav>

    <h1 id="site-title" style="color:white; letter-spacing: 15px; cursor:pointer; font-size: 1.5rem;">SANCTUARY</h1>

    <div id="p-room" class="room active-room" style="width: 100%; display: flex; flex-direction: column; align-items: center;">
        <div class="id-card">
            <h2 style="margin:0; font-size: 1.4rem; letter-spacing: 3px;">PETER KRISCHE</h2>
            <p style="color: #444; font-size: 0.6rem; margin-top: 5px;">RONKONKOMA SECTOR | CELL LEADER</p>
        </div>

        <div style="width: 100%; background: #111; height: 6px; margin-bottom: 5px;"><div id="p-fill"></div></div>
        <p style="font-size: 0.7rem; color: var(--electric-cyan); letter-spacing: 2px;">SUMMERSLAM POWER: <span id="p-pct">0</span></p>

        <div id="cage-btn">⛓️</div>
        
        <textarea id="s-input" placeholder="Confess to the Steel..."></textarea><br>
        
        <button onclick="mummify()" style="background: #fff; color: #000; border: none; padding: 18px 40px; font-weight: bold; border-radius: 0px; cursor: pointer; letter-spacing: 2px; margin-top: 10px;">YOU CAN'T SEE ME</button>

        <div id="vault-list" style="width: 100%; margin-top: 40px; display: flex; flex-direction: column; align-items: center;"></div>
    </div>

    <div id="t-room" class="room" style="display:none; width: 100%; flex-direction: column; align-items: center;">
        <h2 style="letter-spacing: 10px;">THE PORCH</h2>
        <div id="forum" style="width: 100%; display: flex; flex-direction: column; align-items: center;"></div>
    </div>

    <script>
        let data = { bags: 0 };

        function save() { localStorage.setItem('pete_cell_final', JSON.stringify(data)); }
        function loadData() {
            const s = localStorage.getItem('pete_cell_final');
            if(s) { data = JSON.parse(s); updateUI(); }
        }

        function updateUI() {
            let p = Math.min((data.bags/30)*100, 100);
            document.getElementById('p-fill').style.width = p + "%";
            document.getElementById('p-pct').innerText = Math.floor(p * 999);
        }

        function clearMem() { localStorage.removeItem('pete_cell_final'); location.reload(); }
        
        function showRoom(id) {
            document.getElementById('p-room').style.display = 'none';
            document.getElementById('t-room').style.display = 'none';
            document.getElementById(id).style.display = 'flex';
        }

        function mummify() {
            const i = document.getElementById('s-input'), v = document.getElementById('vault-list'), f = document.getElementById('forum');
            if(i.value.trim() !== "") {
                data.bags += 5;
                
                const e = document.createElement('div');
                e.className = 'card';
                e.innerHTML = `<p style="font-size:1.1rem; color:#fff;">${i.value}</p>
                               <button onclick="cenaBlast(this.parentElement)" style="background:none; border:1px solid #333; color:#555; padding:8px; cursor:pointer; width:100%; margin-top:10px; font-size:0.6rem;">👋 DISMISS FROM CELL</button>`;
                
                v.prepend(e);
                f.prepend(e.cloneNode(true));
                i.value = "";
                updateUI(); save();
            }
        }

        function cenaBlast(e) { 
            document.body.classList.add('shaking');
            e.style.borderColor = "cyan";
            e.innerHTML = "<h1 style='color:cyan; text-align:center; font-size:1rem;'>YOU CAN'T SEE ME</h1>";
            
            setTimeout(() => {
                e.classList.add('blasting'); 
                setTimeout(() => {
                    e.remove();
                    document.body.classList.remove('shaking');
                }, 600);
            }, 400);
        }

        document.getElementById('site-title').addEventListener('click', () => {
            alert("The Cell doors are locked, Pete. No escape.");
        });
    </script>
</body>
</html>

