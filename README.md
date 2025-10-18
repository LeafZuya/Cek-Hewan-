<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cek Hewan Dalam Jiwa</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            text-align: center;
            z-index: 10;
            position: relative;
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(255, 255, 0, 0.7);
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 30px;
            color: #e0e0e0;
        }
        
        .input-section {
            background: rgba(0, 0, 0, 0.4);
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.5);
            margin-bottom: 30px;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            margin-bottom: 15px;
            text-align: left;
        }
        
        label {
            margin-bottom: 8px;
            font-weight: 600;
        }
        
        input, select {
            padding: 12px;
            border-radius: 8px;
            border: none;
            background: rgba(255, 255, 255, 0.9);
            font-size: 1rem;
        }
        
        .date-inputs {
            display: flex;
            gap: 10px;
        }
        
        .date-inputs select {
            flex: 1;
        }
        
        button {
            background: linear-gradient(to right, #00b09b, #96c93d);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            margin-top: 10px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
        }
        
        .result-section {
            display: none;
            margin-top: 30px;
            background: rgba(0, 0, 0, 0.5);
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
        }
        
        .animal-card {
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            padding: 20px;
            border-radius: 15px;
            margin: 20px auto;
            max-width: 300px;
            box-shadow: 0 0 25px rgba(255, 215, 0, 0.7);
            animation: glow 2s infinite alternate;
        }
        
        @keyframes glow {
            from {
                box-shadow: 0 0 15px rgba(255, 215, 0, 0.7);
            }
            to {
                box-shadow: 0 0 30px rgba(255, 215, 0, 1);
            }
        }
        
        .animal-emoji {
            font-size: 4rem;
            margin-bottom: 15px;
        }
        
        .animal-name {
            font-size: 2rem;
            margin-bottom: 10px;
            color: #ffcc00;
        }
        
        .animal-description {
            font-size: 1.1rem;
            line-height: 1.5;
        }
        
        .decorations {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .leaf {
            position: absolute;
            font-size: 3rem;
            opacity: 0.7;
            animation: sway 8s infinite ease-in-out;
        }
        
        .ice {
            position: absolute;
            font-size: 3rem;
            opacity: 0.7;
            animation: sparkle 6s infinite ease-in-out;
        }
        
        @keyframes sway {
            0%, 100% {
                transform: rotate(-10deg) scale(1);
            }
            50% {
                transform: rotate(10deg) scale(1.1);
            }
        }
        
        @keyframes sparkle {
            0%, 100% {
                transform: scale(1);
                opacity: 0.7;
            }
            50% {
                transform: scale(1.2);
                opacity: 1;
            }
        }
        
        .black-hole {
            position: fixed;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: radial-gradient(circle, #000 0%, transparent 70%);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            z-index: 100;
            display: none;
            box-shadow: 0 0 50px rgba(0, 0, 0, 0.8);
        }
        
        .black-hole-glow {
            position: fixed;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: radial-gradient(circle, rgba(255, 215, 0, 0.8) 0%, transparent 70%);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            z-index: 99;
            display: none;
            filter: blur(10px);
        }
        
        .name-letter {
            position: fixed;
            font-size: 2.5rem;
            font-weight: bold;
            color: #ffcc00;
            z-index: 98;
            display: none;
            text-shadow: 0 0 10px rgba(255, 204, 0, 0.8);
        }
        
        .particle {
            position: fixed;
            width: 8px;
            height: 8px;
            background: #ffcc00;
            border-radius: 50%;
            z-index: 97;
            display: none;
            box-shadow: 0 0 10px rgba(255, 204, 0, 0.8);
        }
        
        .screen-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 90;
            display: none;
        }
    </style>
</head>
<body>
    <div class="decorations" id="decorations"></div>
    
    <div class="screen-overlay" id="screenOverlay"></div>
    <div class="black-hole-glow" id="blackHoleGlow"></div>
    <div class="black-hole" id="blackHole"></div>
    
    <div class="container">
        <h1>Cek Hewan Dalam Jiwa(~By LeafZuya)</h1>
        <p class="subtitle">Temukan hewan yang mencerminkan jiwa Kamu!(Data yang Kamu Masukkan,tidak Akan disimpan Permanen, karena Ini Hanya Bersifat Sementara 🗿🙏)</p>
        
        <div class="input-section">
            <div class="input-group">
                <label for="name">Nama Lengkap</label>
                <input type="text" id="name" placeholder="Masukkan nama Anda">
            </div>
            
            <div class="input-group">
                <label for="age">Usia</label>
                <input type="number" id="age" placeholder="Masukkan usia Anda">
            </div>
            
            <div class="input-group">
                <label for="birthDate">Tanggal Lahir</label>
                <div class="date-inputs">
                    <select id="birthDay">
                        <option value="">Hari</option>
                        <!-- Hari akan diisi dengan JavaScript -->
                    </select>
                    <select id="birthMonth">
                        <option value="">Bulan</option>
                        <!-- Bulan akan diisi dengan JavaScript -->
                    </select>
                    <select id="birthYear">
                        <option value="">Tahun</option>
                        <!-- Tahun akan diisi dengan JavaScript -->
                    </select>
                </div>
            </div>
            
            <button id="checkButton">Cek Hewan Dalam Jiwa</button>
        </div>
        
        <div class="result-section" id="resultSection">
            <h2>Hewan Dalam Jiwa Kamu Adalah:</h2>
            <div class="animal-card">
                <div class="animal-emoji" id="animalEmoji">🦁</div>
                <div class="animal-name" id="animalName">Singa</div>
                <div class="animal-description" id="animalDescription">
                    Kamu adalah pribadi yang berani, percaya diri, dan memiliki jiwa kepemimpinan yang kuat. Kamu adalah penguasa alam Kamu sendiri.
                </div>
            </div>
            <button id="resetButton">Cek Lagi</button>
        </div>
    </div>

    <script>
        // Daftar hewan dengan emoji yang lebih beragam
        const animals = [
            { name: "Harimau", emoji: "🐯", description: "Kamu adalah pribadi yang kuat, berani, dan penuh semangat. Seperti harimau, Kamu memiliki kemampuan untuk memimpin dan mengambil keputusan dengan tegas." },
            { name: "Elang", emoji: "🦅", description: "Kamu memiliki pandangan yang luas dan kemampuan untuk melihat situasi dari berbagai sudut pandang. Kamu adalah pemikir visioner yang selalu mencari kebenaran." },
            { name: "Lumba-lumba", emoji: "🐬", description: "Kamu adalah pribadi yang cerdas, ramah, dan penuh empati. Kamu mudah bergaul dan membawa kebahagiaan bagi orang di sekitar Kamu." },
            { name: "Serigala", emoji: "🐺", description: "Kamu adalah pribadi yang setia kepada kelompok dan memiliki insting yang kuat. Kamu menghargai hubungan dan selalu melindungi orang yang Kamu sayangi." },
            { name: "Kucing", emoji: "🐱", description: "Kamu adalah pribadi yang mandiri, penuh rasa ingin tahu, dan elegan. Kamu menghargai kebebasan tetapi juga bisa menjadi teman yang setia." },
            { name: "Gajah", emoji: "🐘", description: "Kamu adalah pribadi yang bijaksana, kuat, dan memiliki ingatan yang baik. Kamu menghargai keluarga dan tradisi, serta menjadi sandaran bagi banyak orang." },
            { name: "Kupu-kupu", emoji: "🦋", description: "Kamu adalah pribadi yang mengalami transformasi dan pertumbuhan yang signifikan dalam hidup. Kamu membawa keindahan dan perubahan positif ke mana pun Kamu pergi." },
            { name: "Beruang", emoji: "🐻", description: "Kamu adalah pribadi yang kuat, protektif, dan penyendiri. Kamu menghargai ketenangan tetapi siap membela apa yang penting bagi Kamu." },
            { name: "Ular", emoji: "🐍", description: "Kamu adalah pribadi yang penuh misteri, transformatif, dan penyembuh. Kamu memiliki kemampuan untuk melepaskan masa lalu dan memulai babak baru." },
            { name: "Burung Hantu", emoji: "🦉", description: "Kamu adalah pribadi yang bijaksana, intuitif, dan memiliki pengetahuan mendalam. Kamu melihat apa yang tidak dilihat oleh orang lain." },
            { name: "Anjing", emoji: "🐕", description: "Kamu adalah pribadi yang setia, protektif, dan penuh kasih sayang. Kamu adalah teman sejati yang selalu ada untuk orang yang Kamu cintai." },
            { name: "Singa", emoji: "🦁", description: "Kamu adalah pribadi yang berani, percaya diri, dan memiliki jiwa kepemimpinan yang kuat. Kamu adalah penguasa alam Kamu sendiri." },
            { name: "Merak", emoji: "🦚", description: "Kamu adalah pribadi yang percaya diri, kreatif, dan penuh pesona. Kamu tidak takut menunjukkan keunikan diri Kamu kepada dunia." },
            { name: "Rubah", emoji: "🦊", description: "Kamu adalah pribadi yang cerdik, adaptif, dan penuh akal. Kamu mampu menemukan solusi kreatif untuk masalah yang rumit." },
            { name: "Paus", emoji: "🐋", description: "Kamu adalah pribadi yang dalam, penuh kebijaksanaan, dan emosional. Kamu terhubung dengan alam dan memiliki intuisi yang kuat." },
            { name: "Panda", emoji: "🐼", description: "Kamu adalah pribadi yang lembut, penyayang, dan penuh ketenangan. Kamu membawa kedamaian bagi orang di sekitar Kamu." },
            { name: "Koala", emoji: "🐨", description: "Kamu adalah pribadi yang tenang, penyayang, dan menghargai kenyamanan. Kamu menemukan kebahagiaan dalam hal-hal sederhana." },
            { name: "Penguin", emoji: "🐧", description: "Kamu adalah pribadi yang setia, pekerja keras, dan mampu bertahan dalam kondisi sulit. Kamu menghargai keluarga dan komunitas." },
            { name: "Kelinci", emoji: "🐰", description: "Kamu adalah pribadi yang lincah, penuh energi, dan membawa keberuntungan. Kamu memiliki kemampuan untuk berkembang dalam situasi apa pun." },
            { name: "Kuda", emoji: "🐴", description: "Kamu adalah pribadi yang bebas, kuat, dan penuh semangat petualangan. Kamu menghargai kebebasan dan selalu mencari tantangan baru." },
            { name: "Zebra", emoji: "🦓", description: "Kamu adalah pribadi yang unik, seimbang, dan mampu menyesuaikan diri dengan berbagai situasi. Kamu memiliki identitas yang kuat." },
            { name: "Jerapah", emoji: "🦒", description: "Kamu adalah pribadi yang memiliki pandangan yang luas, elegan, dan unik. Kamu melihat dunia dari perspektif yang berbeda." },
            { name: "Badak", emoji: "🦏", description: "Kamu adalah pribadi yang kuat, tegas, dan memiliki kulit yang tebal. Kamu tidak mudah terpengaruh oleh pendapat orang lain." },
            { name: "Kangguru", emoji: "🦘", description: "Kamu adalah pribadi yang energik, protektif, dan selalu melompat ke peluang baru. Kamu membawa keluarga di hati Kamu." },
            { name: "Landak", emoji: "🦔", description: "Kamu adalah pribadi yang mandiri, memiliki pertahanan yang kuat, tetapi lembut di dalam. Kamu melindungi diri sendiri dengan bijak." },
            { name: "Macan Tutul", emoji: "🐆", description: "Kamu adalah pribadi yang gesit, misterius, dan penuh daya tarik. Kamu bergerak dengan penuh keyakinan dan keanggunan." },
            { name: "Orangutan", emoji: "🦧", description: "Kamu adalah pribadi yang bijaksana, introspektif, dan memiliki kedalaman emosi. Kamu menghargai kebijaksanaan dan pembelajaran." },
            { name: "Kelelawar", emoji: "🦇", description: "Kamu adalah pribadi yang intuitif, mampu melihat dalam kegelapan, dan memiliki persepsi yang unik tentang dunia." },
            { name: "Unta", emoji: "🐪", description: "Kamu adalah pribadi yang sabar, tangguh, dan mampu bertahan dalam kondisi sulit. Kamu adalah pejalan jarak jauh yang tak kenal lelah." },
            { name: "Luwak", emoji: "🐾", description: "Kamu adalah pribadi yang penuh rasa ingin tahu, mandiri, dan memiliki selera yang unik dalam banyak hal." },
            { name: "Bebek", emoji: "🦆", description: "Kamu adalah pribadi yang mudah beradaptasi, komunikatif, dan selalu menemukan cara untuk mengapung di atas masalah." },
            { name: "Flamingo", emoji: "🦩", description: "Kamu adalah pribadi yang elegan, sosial, dan tidak takut menonjol dari keramaian. Kamu membawa keindahan ke mana pun Kamu pergi." },
            { name: "Berang-berang", emoji: "🦦", description: "Kamu adalah pribadi yang pekerja keras, cerdas, dan selalu membangun fondasi yang kuat untuk masa depan." },
            { name: "Tupai", emoji: "🐿️", description: "Kamu adalah pribadi yang gesit, perencana yang baik, dan selalu siap untuk masa depan." },
            { name: "Katak", emoji: "🐸", description: "Kamu adalah pribadi yang mampu beradaptasi dengan perubahan, transformatif, dan memiliki suara yang berpengaruh." },
            { name: "Kura-kura", emoji: "🐢", description: "Kamu adalah pribadi yang sabar, bijaksana, dan memahami bahwa perjalanan panjang membutuhkan ketekunan." },
            { name: "Ikan Mas", emoji: "🐠", description: "Kamu adalah pribadi yang membawa keberuntungan, penuh warna, dan mampu berkembang dalam berbagai lingkungan." },
            { name: "Cumi-cumi", emoji: "🦑", description: "Kamu adalah pribadi yang misterius, kreatif, dan mampu menyesuaikan diri dengan situasi apa pun." },
            { name: "Laba-laba", emoji: "🕷️", description: "Kamu adalah pribadi yang kreatif, sabar, dan mampu membangun jaringan yang kuat dan kompleks." },
            { name: "Semut", emoji: "🐜", description: "Kamu adalah pribadi yang pekerja keras, disiplin, dan memahami kekuatan kerja sama dalam tim." },
            { name: "Lebah", emoji: "🐝", description: "Kamu adalah pribadi yang produktif, sosial, dan memahami pentingnya berkontribusi untuk kebaikan bersama." },
            { name: "Kepik", emoji: "🐞", description: "Kamu adalah pribadi yang membawa keberuntungan, lembut, namun memiliki kekuatan yang tersembunyi." },
            { name: "Kalajengking", emoji: "🦂", description: "Kamu adalah pribadi yang kuat, protektif, dan memiliki kemampuan untuk bertahan dalam situasi sulit." },
            { name: "Kadal", emoji: "🦎", description: "Kamu adalah pribadi yang adaptif, mampu berubah sesuai lingkungan, dan memiliki ketahanan yang luar biasa." },
            { name: "Burung Merak", emoji: "🦚", description: "Kamu adalah pribadi yang percaya diri, penuh pesona, dan tidak takut menunjukkan keindahan diri Kamu." },
            { name: "Burung Kenari", emoji: "🐤", description: "Kamu adalah pribadi yang ceria, bersuara merdu, dan membawa keceriaan ke mana pun Kamu pergi." },
            { name: "Burung Beo", emoji: "🦜", description: "Kamu adalah pribadi yang komunikatif, cerdas, dan mampu menyesuaikan diri dengan berbagai situasi sosial." },
            { name: "Hiu", emoji: "🦈", description: "Kamu adalah pribadi yang tangguh, penuh determinasi, dan selalu bergerak maju tanpa ragu." },
            { name: "Gurita", emoji: "🐙", description: "Kamu adalah pribadi yang cerdas, multi-talenta, dan mampu menangani banyak hal sekaligus dengan baik." }
        ];

        // Inisialisasi elemen DOM
        const nameInput = document.getElementById('name');
        const ageInput = document.getElementById('age');
        const birthDaySelect = document.getElementById('birthDay');
        const birthMonthSelect = document.getElementById('birthMonth');
        const birthYearSelect = document.getElementById('birthYear');
        const checkButton = document.getElementById('checkButton');
        const resultSection = document.getElementById('resultSection');
        const animalEmoji = document.getElementById('animalEmoji');
        const animalName = document.getElementById('animalName');
        const animalDescription = document.getElementById('animalDescription');
        const resetButton = document.getElementById('resetButton');
        const decorations = document.getElementById('decorations');
        const blackHole = document.getElementById('blackHole');
        const blackHoleGlow = document.getElementById('blackHoleGlow');
        const screenOverlay = document.getElementById('screenOverlay');

        // Mengisi pilihan tanggal, bulan, dan tahun
        function populateDateSelects() {
            // Hari (1-31)
            for (let i = 1; i <= 31; i++) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i;
                birthDaySelect.appendChild(option);
            }
            
            // Bulan (1-12)
            const months = [
                'Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni',
                'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'
            ];
            
            months.forEach((month, index) => {
                const option = document.createElement('option');
                option.value = index + 1;
                option.textContent = month;
                birthMonthSelect.appendChild(option);
            });
            
            // Tahun (1900-2023)
            const currentYear = new Date().getFullYear();
            for (let i = currentYear; i >= 1900; i--) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i;
                birthYearSelect.appendChild(option);
            }
        }

        // Membuat dekorasi daun dan es di sudut-sudut
        function createDecorations() {
            // Daun di kanan atas
            const leafTopRight = document.createElement('div');
            leafTopRight.className = 'leaf';
            leafTopRight.textContent = '🍃';
            leafTopRight.style.top = '20px';
            leafTopRight.style.right = '20px';
            leafTopRight.style.animationDelay = '0s';
            decorations.appendChild(leafTopRight);
            
            // Daun di kiri bawah
            const leafBottomLeft = document.createElement('div');
            leafBottomLeft.className = 'leaf';
            leafBottomLeft.textContent = '🍂';
            leafBottomLeft.style.bottom = '20px';
            leafBottomLeft.style.left = '20px';
            leafBottomLeft.style.animationDelay = '1s';
            decorations.appendChild(leafBottomLeft);
            
            // Es di kiri atas
            const iceTopLeft = document.createElement('div');
            iceTopLeft.className = 'ice';
            iceTopLeft.textContent = '❄️';
            iceTopLeft.style.top = '20px';
            iceTopLeft.style.left = '20px';
            iceTopLeft.style.animationDelay = '0.5s';
            decorations.appendChild(iceTopLeft);
            
            // Es di kanan bawah
            const iceBottomRight = document.createElement('div');
            iceBottomRight.className = 'ice';
            iceBottomRight.textContent = '🧊';
            iceBottomRight.style.bottom = '20px';
            iceBottomRight.style.right = '20px';
            iceBottomRight.style.animationDelay = '1.5s';
            decorations.appendChild(iceBottomRight);
            
            // Tambahan daun dan es untuk variasi
            const leafMiddleRight = document.createElement('div');
            leafMiddleRight.className = 'leaf';
            leafMiddleRight.textContent = '🌿';
            leafMiddleRight.style.top = '50%';
            leafMiddleRight.style.right = '40px';
            leafMiddleRight.style.transform = 'translateY(-50%)';
            leafMiddleRight.style.animationDelay = '2s';
            decorations.appendChild(leafMiddleRight);
            
            const iceMiddleLeft = document.createElement('div');
            iceMiddleLeft.className = 'ice';
            iceMiddleLeft.textContent = '🌨️';
            iceMiddleLeft.style.top = '50%';
            iceMiddleLeft.style.left = '40px';
            iceMiddleLeft.style.transform = 'translateY(-50%)';
            iceMiddleLeft.style.animationDelay = '2.5s';
            decorations.appendChild(iceMiddleLeft);
        }

        // Animasi huruf nama tersedot ke lubang hitam
        function animateNameToBlackHole(name) {
            const letters = name.split('');
            const centerX = window.innerWidth / 2;
            const centerY = window.innerHeight / 2;
            
            // Tampilkan overlay dan lubang hitam
            screenOverlay.style.display = 'block';
            blackHoleGlow.style.display = 'block';
            blackHole.style.display = 'block';
            
            // Animasi lubang hitam membesar
            setTimeout(() => {
                blackHoleGlow.style.width = '300px';
                blackHoleGlow.style.height = '300px';
                blackHoleGlow.style.transition = 'all 2s ease-out';
                
                blackHole.style.width = '250px';
                blackHole.style.height = '250px';
                blackHole.style.transition = 'all 2s ease-out';
            }, 100);
            
            // Buat elemen untuk setiap huruf
            letters.forEach((letter, index) => {
                const letterElement = document.createElement('div');
                letterElement.className = 'name-letter';
                letterElement.textContent = letter;
                
                // Posisi acak di sekitar layar
                const angle = Math.random() * Math.PI * 2;
                const distance = Math.max(window.innerWidth, window.innerHeight) * 0.6;
                const startX = centerX + Math.cos(angle) * distance;
                const startY = centerY + Math.sin(angle) * distance;
                
                letterElement.style.left = `${startX}px`;
                letterElement.style.top = `${startY}px`;
                letterElement.style.display = 'block';
                document.body.appendChild(letterElement);
                
                // Animasi huruf menuju lubang hitam dengan efek spiral
                setTimeout(() => {
                    letterElement.style.transition = 'all 2s cubic-bezier(0.2, 0.8, 0.3, 1)';
                    letterElement.style.left = `${centerX}px`;
                    letterElement.style.top = `${centerY}px`;
                    letterElement.style.fontSize = '0px';
                    letterElement.style.opacity = '0';
                    
                    // Tambahkan partikel efek
                    createParticles(startX, startY, centerX, centerY);
                }, index * 150);
                
                // Hapus elemen huruf setelah animasi selesai
                setTimeout(() => {
                    if (letterElement.parentNode) {
                        document.body.removeChild(letterElement);
                    }
                }, 2000 + index * 150);
            });
            
            // Sembunyikan lubang hitam setelah semua huruf masuk
            setTimeout(() => {
                blackHoleGlow.style.width = '0px';
                blackHoleGlow.style.height = '0px';
                blackHole.style.width = '0px';
                blackHole.style.height = '0px';
                
                setTimeout(() => {
                    blackHoleGlow.style.display = 'none';
                    blackHole.style.display = 'none';
                    screenOverlay.style.display = 'none';
                }, 2000);
            }, 1000 + letters.length * 150);
        }

        // Membuat partikel efek
        function createParticles(startX, startY, endX, endY) {
            const particleCount = 15;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                // Posisi awal partikel
                particle.style.left = `${startX}px`;
                particle.style.top = `${startY}px`;
                particle.style.display = 'block';
                document.body.appendChild(particle);
                
                // Animasi partikel menuju lubang hitam
                setTimeout(() => {
                    particle.style.transition = 'all 1.5s ease-out';
                    particle.style.left = `${endX}px`;
                    particle.style.top = `${endY}px`;
                    particle.style.width = '0px';
                    particle.style.height = '0px';
                    particle.style.opacity = '0';
                }, i * 30);
                
                // Hapus partikel setelah animasi selesai
                setTimeout(() => {
                    if (particle.parentNode) {
                        document.body.removeChild(particle);
                    }
                }, 2000 + i * 30);
            }
        }

        // Fungsi hash yang lebih baik untuk distribusi yang lebih merata
        function generateHash(str) {
            let hash = 0;
            for (let i = 0; i < str.length; i++) {
                const char = str.charCodeAt(i);
                hash = ((hash << 5) - hash) + char;
                hash = hash & hash; // Convert to 32bit integer
            }
            return Math.abs(hash);
        }

        // Menghasilkan hewan berdasarkan input pengguna
        function generateAnimal(name, age, day, month, year) {
            // Gabungkan semua data untuk membuat seed yang unik
            const seedString = `${name}${age}${day}${month}${year}`;
            
            // Gunakan hash untuk memilih hewan
            const animalIndex = generateHash(seedString) % animals.length;
            return animals[animalIndex];
        }

        // Event listener untuk tombol Cek Hewan
        checkButton.addEventListener('click', function() {
            const name = nameInput.value.trim();
            const age = ageInput.value;
            const day = birthDaySelect.value;
            const month = birthMonthSelect.value;
            const year = birthYearSelect.value;
            
            if (!name || !age || !day || !month || !year) {
                alert('Harap isi semua data dengan lengkap!');
                return;
            }
            
            // Jalankan animasi nama tersedot ke lubang hitam
            animateNameToBlackHole(name);
            
            // Tunggu animasi selesai sebelum menampilkan hasil
            setTimeout(() => {
                const animal = generateAnimal(name, age, day, month, year);
                animalEmoji.textContent = animal.emoji;
                animalName.textContent = animal.name;
                animalDescription.textContent = animal.description;
                
                // Putar suara (efek suara sederhana)
                playAnimalSound();
                
                // Tampilkan hasil
                resultSection.style.display = 'block';
                
                // Scroll ke hasil
                resultSection.scrollIntoView({ behavior: 'smooth' });
            }, 3000 + name.length * 150);
        });

        // Event listener untuk tombol Reset
        resetButton.addEventListener('click', function() {
            resultSection.style.display = 'none';
            nameInput.value = '';
            ageInput.value = '';
            birthDaySelect.value = '';
            birthMonthSelect.value = '';
            birthYearSelect.value = '';
        });

        // Efek suara sederhana
       function playAnimalSound() {
    // Ganti ".mp3" dengan file suara yang kamu mau
    const audio = new Audio('Jokowi.mp3');
    audio.volume = 0.7; // Atur volume (0.1 - 1.0)
    audio.play().catch(e => console.log('Error playing sound:', e));
}

        // Inisialisasi saat halaman dimuat
        window.addEventListener('DOMContentLoaded', function() {
            populateDateSelects();
            createDecorations();
        });
    </script>
</body>
</html>
