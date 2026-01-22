<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BLack World | Community & Projects</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root { --primary: #1b4332; --accent: #2d6a4f; --light-bg: #f8f9fa; --text: #333; }
        * { box-sizing: border-box; font-family: 'Poppins', sans-serif; }
        
        body { margin: 0; background-color: var(--light-bg); color: var(--text); }

        /* HEADER & NAVBAR (Stile Blog) */
        header { background: var(--primary); color: white; padding: 40px 20px; text-align: center; }
        header h1 { margin: 0; font-size: 2.5rem; letter-spacing: 3px; }

        nav { background: white; border-bottom: 1px solid #ddd; display: flex; justify-content: center; position: sticky; top: 0; z-index: 1000; height: 50px; }
        .nav-links { display: flex; align-items: center; gap: 20px; }
        .nav-links a { text-decoration: none; color: var(--text); font-weight: 600; font-size: 0.9rem; cursor: pointer; text-transform: uppercase; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        /* SIDEBAR (Tua Registrazione) */
        .sidebar { position: fixed; left: -100%; top: 0; width: 350px; height: 100%; background: white; z-index: 2000; transition: 0.4s; padding: 25px; box-shadow: 5px 0 25px rgba(0,0,0,0.1); overflow-y: auto; }
        .sidebar.open { left: 0; }
        .reg-field { margin-bottom: 12px; }
        .reg-field label { display: block; font-size: 0.8rem; font-weight: 600; margin-bottom: 4px; }
        .reg-field input { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 4px; }

        .btn-google { background: white; border: 1px solid #ddd; color: #555; padding: 10px; border-radius: 4px; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 10px; width: 100%; font-weight: 600; }
        .btn-main { background: var(--primary); color: white; border: none; padding: 12px; width: 100%; border-radius: 4px; cursor: pointer; font-weight: bold; }

        /* CONTENT LAYOUT */
        .main-content { max-width: 1200px; margin: 30px auto; display: grid; grid-template-columns: 1fr 300px; gap: 30px; padding: 0 20px; }
        
        .post-card { background: white; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 10px rgba(0,0,0,0.05); margin-bottom: 30px; }
        .post-card img { width: 100%; height: auto; display: block; }
        .post-info { padding: 20px; }
        .post-info h2 { margin-top: 0; color: var(--primary); }

        /* CHAT SECTION */
        #chatBox { height: 400px; overflow-y: auto; border: 1px solid #eee; padding: 15px; background: #fafafa; border-radius: 8px; margin-bottom: 10px; display: flex; flex-direction: column; gap: 10px; }
        .msg { padding: 10px; border-radius: 8px; background: white; max-width: 85%; box-shadow: 0 1px 3px rgba(0,0,0,0.1); font-size: 0.9rem; }
        .msg.me { align-self: flex-end; background: #e2f3eb; }

        .page { display: none; }
        .page.active { display: block; }
    </style>
</head>
<body>

<header>
    <h1>BLACK WORLD 🌈</h1>
    <p>Drama, Ship e Passione BL</p>
</header>

<nav>
    <div style="position: absolute; left: 20px; top: 12px; cursor: pointer;" onclick="toggleSidebar()">☰ ACCEDI</div>
    <div class="nav-links">
        <a onclick="showPage('home')">Home</a>
        <a onclick="showPage('amicizia')">Amicizia</a>
        <a onclick="showPage('chat')">Chat Live</a>
    </div>
</nav>

<div class="sidebar" id="sidebar">
    <div style="text-align:right; cursor:pointer; margin-bottom: 20px;" onclick="toggleSidebar()">✕ CHIUDI</div>
    <h2>Registrazione</h2>
    <div class="reg-field"><label>Nome *</label><input type="text" id="rNome"></div>
    <div class="reg-field"><label>Nome utente *</label><input type="text" id="rUser"></div>
    <div class="reg-field"><label>Email *</label><input type="email" id="rEmail"></div>
    <div class="reg-field"><label>Conferma Email *</label><input type="email" id="rEmailC"></div>
    <div class="reg-field"><label>Password *</label><input type="password" id="rPass"></div>
    <div class="reg-field"><label>Conferma Password *</label><input type="password" id="rPassC"></div>
    <button class="btn-main" onclick="registerManual()">REGISTRATI</button>
    <hr>
    <button class="btn-google" onclick="loginGoogle()">
        <img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg" width="18"> ACCEDI CON GOOGLE
    </button>
</div>

<div class="main-content">
    
    <main>
        <section id="home" class="page active">
            <div class="post-card">
                <img src="https://via.placeholder.com/800x400?text=Ultimi+Drama+Aggiornati" alt="Cover">
                <div class="post-info">
                    <h2>Ultimi Progetti BL</h2>
                    <p>Benvenuti nel blog! Qui troverai le traduzioni e le discussioni sulle ultime serie thailandesi, coreane e giapponesi.</p>
                </div>
            </div>
        </section>

        <section id="amicizia" class="page">
            <div class="post-card" style="padding:20px;">
                <h2>Trova il tuo Match BL 💘</h2>
                <div id="matchRes" style="background:#d4edda; padding:10px; margin-bottom:10px; display:none; border-radius:5px;"></div>
                <input type="text" id="pNick" placeholder="Nickname">
                <input type="text" id="pShip" placeholder="La tua Ship preferita">
                <textarea id="pBio" placeholder="Raccontaci di te..." rows="4"></textarea>
                <button class="btn-main" onclick="saveAndMatch()">PUBBLICA E CERCA MATCH</button>
                <div id="profilesFeed" style="margin-top:20px;"></div>
            </div>
        </section>

        <section id="chat" class="page">
            <div class="post-card" style="padding:20px;">
                <h2>Global Chat 💬</h2>
                <div id="chatBox"></div>
                <div style="display:flex; gap:10px;">
                    <input type="text" id="chatInput" placeholder="Scrivi qui..." style="flex:1; margin:0;">
                    <button class="btn-main" style="width:100px;" onclick="sendMessage()">Invia</button>
                </div>
            </div>
        </section>
    </main>

    <aside>
        <div class="post-card" style="padding:15px;">
            <h3>🔍 Cerca</h3>
            <input type="text" placeholder="Cerca drama o ship...">
        </div>
        <div class="post-card" style="padding:15px;">
            <h3>🔥 Trending</h3>
            <ul style="list-style:none; padding:0; font-size:0.9rem;">
                <li>→ Bad Buddy</li>
                <li>→ My School President</li>
                <li>→ Hidden Agenda</li>
            </ul>
        </div>
    </aside>
</div>

<script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.10/firebase-database-compat.js"></script>

<script>
    // TUA CONFIGURAZIONE ESATTA (Incluso l'URL corretto del Database)
    const firebaseConfig = {
      apiKey: "AIzaSyAr4cM8wb7kSHpaFDGjlDZcm15t1LyL4Do",
      authDomain: "black-world-91efc.firebaseapp.com",
      databaseURL: "https://black-world-91efc-default-rtdb.europe-west1.firebasedatabase.app",
      projectId: "black-world-91efc",
      storageBucket: "black-world-91efc.firebasestorage.app",
      messagingSenderId: "1075556185722",
      appId: "1:1075556185722:web:a18a5f3d7ef3b4862aedc3",
      measurementId: "G-L1TH722CGE"
    };

    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    const db = firebase.database();

    function toggleSidebar() { document.getElementById('sidebar').classList.toggle('open'); }
    function showPage(id) { 
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(id).classList.add('active');
    }

    // REGISTRAZIONE
    function registerManual() {
        const email = document.getElementById('rEmail').value;
        const pass = document.getElementById('rPass').value;
        if(email !== document.getElementById('rEmailC').value) return alert("Le email non corrispondono!");
        auth.createUserWithEmailAndPassword(email, pass).then(() => toggleSidebar()).catch(e => alert(e.message));
    }

    function loginGoogle() {
        auth.signInWithPopup(new firebase.auth.GoogleAuthProvider()).then(() => toggleSidebar());
    }

    // CHAT (SISTEMATA)
    function sendMessage() {
        const txt = document.getElementById('chatInput').value;
        if(!txt || !auth.currentUser) return alert("Devi essere loggata!");
        db.ref("messages/public").push({
            user: auth.currentUser.email,
            text: txt,
            timestamp: Date.now()
        });
        document.getElementById('chatInput').value = "";
    }

    // Caricamento Chat e Matchmaking
    let allProfiles = [];
    auth.onAuthStateChanged(user => {
        if(user) {
            // Carica Messaggi
            db.ref("messages/public").limitToLast(30).on("value", s => {
                const box = document.getElementById('chatBox');
                box.innerHTML = "";
                s.forEach(m => {
                    const data = m.val();
                    const d = document.createElement("div");
                    d.className = "msg" + (data.user === user.email ? " me" : "");
                    d.innerHTML = `<b>${data.user.split('@')[0]}</b>: ${data.text}`;
                    box.appendChild(d);
                });
                box.scrollTop = box.scrollHeight;
            });

            // Carica Profili
            db.ref("profiles").on("value", s => {
                allProfiles = [];
                s.forEach(p => allProfiles.push(p.val()));
            });
        }
    });

    function saveAndMatch() {
        const nick = document.getElementById('pNick').value;
        const ship = document.getElementById('pShip').value;
        if(!auth.currentUser || !ship) return alert("Accedi e inserisci la tua ship!");

        const match = allProfiles.find(p => p.ship.toLowerCase() === ship.toLowerCase() && p.nick !== nick);
        if(match) {
            const res = document.getElementById('matchRes');
            res.style.display = "block";
            res.innerHTML = `✨ MATCH! Anche <b>${match.nick}</b> ama questa ship!`;
        }
        db.ref("profiles/" + auth.currentUser.uid).set({ nick, ship, bio: document.getElementById('pBio').value });
    }
</script>
</body>
</html>
