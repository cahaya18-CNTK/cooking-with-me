<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Cahaya Cooking - Game Memasak dengan Alat dan Tombol</title>
    <style>
        * {
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: linear-gradient(145deg, #2b5e3b 0%, #1e3a2f 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Poppins', system-ui, -apple-system, 'Comic Neue', sans-serif;
            margin: 0;
            padding: 20px;
        }

        /* Container utama game */
        .game-container {
            background: #fef9e6;
            border-radius: 80px 80px 60px 60px;
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.4), inset 0 1px 4px rgba(255, 255, 200, 0.8);
            padding: 20px 25px 30px 25px;
            transition: all 0.2s ease;
        }

        /* area dapur utama */
        .kitchen {
            background: #f8e3b0;
            border-radius: 60px;
            padding: 25px 30px;
            box-shadow: inset 0 0 0 2px #fff9e8, inset 0 0 0 6px #d9b48b, 0 12px 24px rgba(0,0,0,0.2);
        }

        /* header cahaya & skor */
        .header-game {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            background: #fffaec;
            padding: 15px 25px;
            border-radius: 100px;
            margin-bottom: 25px;
            box-shadow: 0 5px 0 #cb9e72;
        }

        .game-title {
            font-size: 2.1rem;
            font-weight: bold;
            background: linear-gradient(135deg, #f5b042, #e07c1f);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 2px 2px 0 #fff3cf;
            letter-spacing: 2px;
        }

        .score-board {
            background: #2e241f;
            padding: 8px 20px;
            border-radius: 40px;
            color: #ffd966;
            font-weight: bold;
            font-size: 1.8rem;
            box-shadow: inset 0 2px 3px rgba(0,0,0,0.3), 0 3px 0 #5a3e2b;
        }

        .score-label {
            font-size: 1rem;
            margin-right: 8px;
            color: #ffbc6e;
        }

        /* area tampilan resep dan bahan */
        .recipe-panel {
            background: #fff1cf;
            border-radius: 48px;
            padding: 15px 20px;
            margin-bottom: 25px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            box-shadow: inset 0 1px 5px #ffe3a3, 0 8px 12px rgba(0,0,0,0.1);
        }

        .target-dish {
            display: flex;
            align-items: center;
            gap: 15px;
            background: #fae6b3;
            padding: 8px 20px;
            border-radius: 50px;
        }

        .dish-icon {
            font-size: 3rem;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.2));
        }

        .dish-name {
            font-weight: bold;
            font-size: 1.5rem;
            color: #6b3e1c;
        }

        .ingredient-stock {
            display: flex;
            gap: 20px;
            background: #e8cf94;
            padding: 10px 20px;
            border-radius: 50px;
        }

        .stock-item {
            text-align: center;
            background: white;
            border-radius: 40px;
            padding: 5px 18px;
            box-shadow: inset 0 1px 2px #fff5cf, 0 3px 0 #aa7a4a;
        }

        .stock-emoji {
            font-size: 1.8rem;
        }

        .stock-count {
            font-weight: bold;
            font-size: 1.2rem;
            background: #4a2c1a;
            display: inline-block;
            padding: 0 10px;
            border-radius: 30px;
            color: #ffd966;
            margin-left: 6px;
        }

        /* area alat memasak interaktif */
        .tools-area {
            background: #d9b48b;
            border-radius: 65px;
            padding: 20px;
            margin-bottom: 25px;
            box-shadow: inset 0 0 0 3px #f9e1a4, 0 10px 18px rgba(0,0,0,0.2);
        }

        .tools-title {
            text-align: center;
            font-size: 1.3rem;
            font-weight: bold;
            color: #2c1a0c;
            background: #ffefbf;
            display: inline-block;
            width: auto;
            padding: 5px 20px;
            border-radius: 40px;
            margin-bottom: 18px;
            margin-top: -8px;
        }

        .tool-buttons {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 18px;
        }

        .tool-card {
            background: #fff2df;
            border-radius: 60px;
            padding: 12px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.1s linear;
            box-shadow: 0 7px 0 #936e46;
            width: 120px;
        }

        .tool-card:active {
            transform: translateY(4px);
            box-shadow: 0 3px 0 #936e46;
        }

        .tool-emoji {
            font-size: 2.8rem;
            display: block;
        }

        .tool-name {
            font-weight: bold;
            font-size: 1rem;
            background: #c58f5e;
            color: white;
            padding: 4px 8px;
            border-radius: 40px;
            margin-top: 8px;
        }

        /* area aksi & panci hasil masakan */
        .cooking-panel {
            background: #f6e2b0;
            border-radius: 50px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .pot-area {
            background: #6b4c34;
            border-radius: 70px;
            padding: 15px 25px;
            display: inline-flex;
            align-items: center;
            gap: 20px;
            box-shadow: inset 0 0 0 4px #c9a87b, 0 6px 0 #3e2a1b;
            margin-bottom: 20px;
        }

        .pot {
            font-size: 3.5rem;
            filter: drop-shadow(4px 6px 0 #4f321d);
            cursor: pointer;
            transition: 0.07s linear;
        }

        .pot:active {
            transform: scale(0.96);
        }

        .current-ingredient {
            background: #ffe1a0;
            padding: 5px 16px;
            border-radius: 50px;
            font-size: 1.3rem;
            font-weight: bold;
            color: #7b4200;
            font-family: monospace;
        }

        .cook-button {
            background: #e07c1f;
            border: none;
            font-size: 1.8rem;
            font-weight: bold;
            padding: 12px 35px;
            border-radius: 60px;
            color: white;
            box-shadow: 0 7px 0 #864e1c;
            cursor: pointer;
            transition: 0.05s linear;
            letter-spacing: 2px;
            margin-bottom: 15px;
        }

        .cook-button:active {
            transform: translateY(4px);
            box-shadow: 0 3px 0 #864e1c;
        }

        .message-area {
            background: #2d2219;
            border-radius: 40px;
            padding: 10px 20px;
            color: #ffd58c;
            font-weight: bold;
            text-align: center;
            font-size: 1rem;
            margin-top: 10px;
        }

        .reset-btn {
            background: #7c5a3e;
            border: none;
            font-size: 1rem;
            padding: 8px 20px;
            border-radius: 60px;
            margin-top: 15px;
            color: #ffefb9;
            font-weight: bold;
            cursor: pointer;
            transition: 0.1s;
            box-shadow: 0 3px 0 #4d321f;
        }

        .reset-btn:active {
            transform: translateY(2px);
            box-shadow: 0 1px 0 #4d321f;
        }

        @media (max-width: 640px) {
            .game-container { padding: 12px; }
            .tool-card { width: 90px; padding: 8px 10px; }
            .tool-emoji { font-size: 2rem; }
            .dish-name { font-size: 1.2rem; }
            .stock-item { padding: 3px 12px; }
        }

        button {
            background: none;
            border: none;
            font-family: inherit;
        }
    </style>
</head>
<body>
<div class="game-container">
    <div class="kitchen">
        <div class="header-game">
            <div class="game-title">🍳 CAHAYA COOKING ✨</div>
            <div class="score-board"><span class="score-label">⭐ SKOR</span> <span id="scoreValue">0</span></div>
        </div>

        <div class="recipe-panel">
            <div class="target-dish">
                <span class="dish-icon">🍲</span>
                <span class="dish-name">RESEP: <span id="targetRecipeName">Sup Cahaya</span></span>
            </div>
            <div class="ingredient-stock" id="ingredientStockPanel">
                <!-- stock akan diupdate via js -->
            </div>
        </div>

        <!-- ALAT MEMASAK + TOMBOL ALAT -->
        <div class="tools-area">
            <div style="text-align: center;"><span class="tools-title">🔪 ALAT DAPUR CAHAYA 🥄</span></div>
            <div class="tool-buttons" id="toolButtonsContainer">
                <!-- alat dinamis dari js -->
            </div>
        </div>

        <!-- PANCI & AKSI MASAK -->
        <div class="cooking-panel">
            <div class="pot-area">
                <div class="pot" id="potClickZone">🍲</div>
                <div class="current-ingredient" id="currentIngredientDisplay">🍽️ Kosong</div>
            </div>
            <button class="cook-button" id="cookBtn">🔥 MASAK! 🔥</button>
            <div class="message-area" id="gameMessage">✨ Klik alat untuk menyiapkan bahan! Lalu masak ✨</div>
            <button class="reset-btn" id="resetBtn">🔄 RESET GAME</button>
        </div>
    </div>
</div>

<script>
    // ----- KONSEP GAME CAHAYA -----
    // Tema: Memasak dengan alat (Pisau, Wajan, Sendok kayu, Blender)
    // Setiap alat menghasilkan bahan yang berbeda (bahan dasar)
    // Bahan yang dihasilkan dapat ditampung di "panci" (slot persiapan)
    // Saat menekan tombol MASAK! akan menggabungkan bahan saat ini di panci dengan resep target
    // Jika bahan di panci sesuai dengan resep -> tambah skor +1, resep berganti, bahan habis (panci kosong)
    // Jika salah -> pesan gagal, panci tetap kosong, skor tidak berubah.
    // Stok bahan (jumlah bahan yang tersedia) terbatas, tapi alat akan mengurangi stok saat digunakan
    // Player bisa mengklik alat untuk "menyiapkan" bahan ke dalam panci (jika panci kosong, bisa simpan 1 jenis bahan)
    // Karena ini game sederhana dan seru: setiap kali memakai alat, jika panci kosong maka bahan masuk panci, jika panci sudah terisi, maka akan menimpa (memberi kebebasan)
    
    // Data resep & bahan:
    const RECIPES = [
        { name: "Sup Cahaya", requiredIngredient: "wortel", displayEmoji: "🥕✨", score: 10 },
        { name: "Nasi Goreng Spesial", requiredIngredient: "nasi", displayEmoji: "🍚🔥", score: 12 },
        { name: "Jus Pelangi", requiredIngredient: "buah", displayEmoji: "🍹🌈", score: 15 },
        { name: "Telur Dadar Cahaya", requiredIngredient: "telur", displayEmoji: "🍳⭐", score: 10 },
        { name: "Ayam Kremes", requiredIngredient: "ayam", displayEmoji: "🍗✨", score: 18 }
    ];
    
    // mapping alat -> hasil bahan & stok & nama
    const TOOLS_DATA = [
        { id: "knife", name: "Pisau", emoji: "🔪", ingredient: "wortel", stockName: "Wortel 🥕", stockEmoji: "🥕" },
        { id: "pan", name: "Wajan", emoji: "🍳", ingredient: "nasi", stockName: "Nasi 🍚", stockEmoji: "🍚" },
        { id: "spoon", name: "Sendok Kayu", emoji: "🥄", ingredient: "telur", stockName: "Telur 🥚", stockEmoji: "🥚" },
        { id: "blender", name: "Blender", emoji: "🥤", ingredient: "buah", stockName: "Buah 🍎", stockEmoji: "🍎" },
        { id: "grill", name: "Panggangan", emoji: "🍗", ingredient: "ayam", stockName: "Ayam 🍗", stockEmoji: "🍗" }
    ];
    
    // state game
    let currentScore = 0;
    let currentRecipeIndex = 0;      // resep aktif
    let currentPotIngredient = null;  // bahan yg sedang disiapkan di panci (string)
    // stok bahan (key: ingredient name, value: jumlah)
    let stock = {
        wortel: 3,
        nasi: 3,
        telur: 3,
        buah: 3,
        ayam: 3
    };
    
    // DOM Elements
    const scoreSpan = document.getElementById("scoreValue");
    const targetRecipeNameSpan = document.getElementById("targetRecipeName");
    const ingredientStockPanel = document.getElementById("ingredientStockPanel");
    const toolButtonsContainer = document.getElementById("toolButtonsContainer");
    const currentIngredientDisplay = document.getElementById("currentIngredientDisplay");
    const cookBtn = document.getElementById("cookBtn");
    const gameMessageDiv = document.getElementById("gameMessage");
    const resetBtn = document.getElementById("resetBtn");
    const potZone = document.getElementById("potClickZone");
    
    // helper: update tampilan stok & skor & resep
    function updateUI() {
        // update skor
        scoreSpan.innerText = currentScore;
        // update nama resep dengan emoji tambahan
        const recipe = RECIPES[currentRecipeIndex];
        targetRecipeNameSpan.innerHTML = `${recipe.name} ${recipe.displayEmoji}`;
        
        // update panel stok bahan
        ingredientStockPanel.innerHTML = "";
        for (let tool of TOOLS_DATA) {
            const ing = tool.ingredient;
            const count = stock[ing] || 0;
            const stockDiv = document.createElement("div");
            stockDiv.className = "stock-item";
            stockDiv.innerHTML = `<span class="stock-emoji">${tool.stockEmoji}</span> <span class="stock-count">${count}</span>`;
            ingredientStockPanel.appendChild(stockDiv);
        }
        
        // update display panci
        if (currentPotIngredient) {
            const foundTool = TOOLS_DATA.find(t => t.ingredient === currentPotIngredient);
            const emoji = foundTool ? foundTool.stockEmoji : "🍽️";
            currentIngredientDisplay.innerHTML = `${emoji} ${currentPotIngredient.toUpperCase()} siap 🔥`;
        } else {
            currentIngredientDisplay.innerHTML = `🍽️ Kosong, gunakan alat!`;
        }
    }
    
    // generate tombol alat (dinamis berdasarkan TOOLS_DATA)
    function buildToolsButtons() {
        toolButtonsContainer.innerHTML = "";
        TOOLS_DATA.forEach(tool => {
            const btn = document.createElement("div");
            btn.className = "tool-card";
            btn.setAttribute("data-ingredient", tool.ingredient);
            btn.innerHTML = `<span class="tool-emoji">${tool.emoji}</span><span class="tool-name">${tool.name}</span>`;
            btn.addEventListener("click", (e) => {
                e.stopPropagation();
                useTool(tool.ingredient, tool.stockName);
            });
            toolButtonsContainer.appendChild(btn);
        });
    }
    
    // fungsi menggunakan alat (mengambil bahan, mengurangi stok, menaruh di panci)
    function useTool(ingredientKey, ingredientDisplayName) {
        // cek stok apakah masih ada
        if (stock[ingredientKey] <= 0) {
            gameMessageDiv.innerHTML = `⚠️ Stok ${ingredientDisplayName} habis! Belanja dulu (reset game mengembalikan stok). ⚠️`;
            return;
        }
        
        // kurangi stok
        stock[ingredientKey]--;
        // masukkan bahan ke panci (timpa jika sudah ada)
        currentPotIngredient = ingredientKey;
        // pesan sukses
        gameMessageDiv.innerHTML = `✨ ${ingredientDisplayName} berhasil disiapkan menggunakan alat! Sekarang di panci: ${ingredientDisplayName}. Tekan MASAK! ✨`;
        updateUI();
        // animasi singkat
        potZone.style.transform = "scale(0.98)";
        setTimeout(() => { if(potZone) potZone.style.transform = ""; }, 120);
    }
    
    // Memasak: cocokkan currentPotIngredient dengan resep aktif
    function performCooking() {
        if (!currentPotIngredient) {
            gameMessageDiv.innerHTML = "🍳 Panci kosong! Gunakan alat dulu untuk menyiapkan bahan! 🍳";
            return;
        }
        
        const currentRecipe = RECIPES[currentRecipeIndex];
        const required = currentRecipe.requiredIngredient;
        
        if (currentPotIngredient === required) {
            // MASAK BERHASIL!
            const gainedScore = currentRecipe.score;
            currentScore += gainedScore;
            // pesan sukses
            gameMessageDiv.innerHTML = `🎉 BERHASIL! ${currentRecipe.name} selesai! +${gainedScore} poin. Resep baru muncul! 🎉`;
            // pindah ke resep berikutnya (acak atau berurutan, biar seru cycle)
            currentRecipeIndex = (currentRecipeIndex + 1) % RECIPES.length;
            // kosongkan panci setelah masak
            currentPotIngredient = null;
            updateUI();
            // efek gemuruh kecil
            cookBtn.style.transform = "scale(0.96)";
            setTimeout(() => { cookBtn.style.transform = ""; }, 100);
        } else {
            // gagal
            let requiredName = getIngredientDisplayName(required);
            let currentName = getIngredientDisplayName(currentPotIngredient);
            gameMessageDiv.innerHTML = `💔 Gagal! ${currentName} tidak cocok untuk ${currentRecipe.name}. Butuh ${requiredName}. Panci dibersihkan... 💔`;
            // panci kosong karena gagal (bahan terbuang)
            currentPotIngredient = null;
            updateUI();
        }
    }
    
    function getIngredientDisplayName(ingredientKey) {
        const found = TOOLS_DATA.find(t => t.ingredient === ingredientKey);
        return found ? found.stockName : ingredientKey;
    }
    
    // reset game (skor 0, stok penuh, resep index 0, panci kosong)
    function resetGame() {
        currentScore = 0;
        currentRecipeIndex = 0;
        currentPotIngredient = null;
        stock = {
            wortel: 3,
            nasi: 3,
            telur: 3,
            buah: 3,
            ayam: 3
        };
        updateUI();
        gameMessageDiv.innerHTML = "🔄 GAME DIRESET! Stok bahan penuh! Selamat memasak bersama Cahaya! 🔄";
        // sedikit vibrasi tombol reset
    }
    
    // interaksi tambahan: klik panci bisa membersihkan panci (optional)
    function clearPot() {
        if (currentPotIngredient) {
            currentPotIngredient = null;
            gameMessageDiv.innerHTML = "🧽 Panci dibersihkan! Bahan lama dibuang. Siapkan bahan baru dengan alat.";
            updateUI();
        } else {
            gameMessageDiv.innerHTML = "Panci sudah kosong, gunakan alat untuk menyiapkan bahan ya!";
        }
    }
    
    // event binding
    function bindEvents() {
        cookBtn.addEventListener("click", performCooking);
        resetBtn.addEventListener("click", resetGame);
        potZone.addEventListener("click", clearPot);
    }
    
    // tambahan untuk memberikan kesan alat yang interaktif dan cahaya
    function initGame() {
        buildToolsButtons();
        bindEvents();
        updateUI();
        // tambahan dekorasi nama "Cahaya" di judul game & efek psikologis
        document.querySelector('.game-title').innerHTML = '🍳 CAHAYA COOKING ✨';
        // set initial message
        gameMessageDiv.innerHTML = "✨ Selamat datang di dapur Cahaya! ✨<br>Klik alat ➕ taruh di panci ➡️ lalu MASAK! Ikuti resep & jaga stok.";
    }
    
    // Eksekusi awal
    initGame();
</script>
</body>
</html>
