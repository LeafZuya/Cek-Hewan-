<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Cek Hewan Dalam Jiwa — LeafZuya</title>
<link rel="icon" href="Favicon.png" />
<style>
 :root{
  --g1:#00c16b; --g2:#27a2ff; --r1:#ff6b6b; --yellow: #ffd54d;
}
*{box-sizing:border-box; margin:0; padding:0;}
html, body{width:100%; height:100%;}

body{
  font-family:Inter, "Poppins", Arial, sans-serif;
  min-height:100vh;
  background: radial-gradient(circle at 20% 20%, rgba(255,255,200,0.06), transparent 10%),
              linear-gradient(135deg, var(--g1), var(--g2), var(--r1));
  display:flex; align-items:center; justify-content:center;
  color:#033;
  overflow-x:hidden; /* ✅ biar tidak bisa geser kanan-kiri */
  overflow-y:auto; /* ✅ tetap bisa scroll vertikal */
  padding: clamp(12px, 4vw, 28px); /* ✅ auto adaptif untuk semua layar */
}

/* Kartu utama */
.card{
  width:960px; max-width:96%;
  background: linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.88));
  border-radius:20px;
  padding:18px;
  box-shadow:0 20px 60px rgba(0,0,0,0.18);
  display:grid;
  grid-template-columns: 1fr 420px;
  gap:18px;
  align-items:start;
  margin:auto; /* ✅ pastikan tetap di tengah */
  position:relative;
}

/* left: form + result area */
.left{ padding:12px 18px; }
h1{ margin:0 0 8px 0; font-size:24px; color:#053; text-shadow:0 2px 8px rgba(0,0,0,0.06)}
p.lead{ margin:6px 0 16px 0; color:#156; }

label{ display:block; margin:8px 0 6px; font-weight:600; color:#045}
input[type="text"], input[type="number"], select{
  width:100%; padding:10px 12px; border-radius:10px; border:1px solid #d6eaf0; font-size:14px;
  background: #fff;
}

.controls-row{ display:flex; gap:10px; margin-top:12px; align-items:center; flex-wrap:wrap;}
.btn {
  background: linear-gradient(135deg,var(--g1),var(--g2)); color:white;
  border:none; padding:10px 16px; border-radius:12px; cursor:pointer; font-weight:700;
  box-shadow:0 10px 20px rgba(0,0,0,0.12);
}
.btn.secondary{
  background:linear-gradient(135deg,#fff,#f4f8ff); color:#045; border:1px solid rgba(0,0,0,0.06);
}

/* right: preview area */
.right{
  padding:12px 18px; display:flex; align-items:center; justify-content:center; position:relative;
  min-height:320px;
}
.preview-stage{
  width:360px; height:360px; border-radius:18px; background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.8));
  box-shadow: inset 0 6px 30px rgba(0,0,0,0.04);
  position:relative; overflow:visible; display:flex; align-items:center; justify-content:center;
}

/* floating result bubble */
.result-bubble{
  position:absolute; left:50%; top:50%; transform:translate(-50%,-50%) scale(0.96);
  min-width:240px; max-width:86%;
  background: linear-gradient(180deg, rgba(255,255,255,0.98), rgba(255,255,240,0.98));
  border-radius:18px; padding:18px; text-align:center;
  box-shadow:0 12px 30px rgba(0,0,0,0.18);
  transition: transform .35s cubic-bezier(.2,.9,.3,1), opacity .25s;
  opacity:0;
}
.result-bubble.show{ opacity:1; transform: translate(-50%,-50%) scale(1); }

.animal-emoji{ font-size:72px; display:block; margin-bottom:8px; filter: drop-shadow(0 8px 18px rgba(0,0,0,0.12)); }
.animal-name{ font-size:20px; font-weight:800; color:#062; margin-bottom:6px; }
.result-sub{ font-size:14px; color:#045; opacity:0.95; }

/* decorations floating (leaf/flower/ice) */
.decor{
  position:absolute; width:64px; height:64px; background-size:contain; background-repeat:no-repeat; opacity:0.95;
  animation: floaty 4s infinite ease-in-out;
}
.d-leaf{ top:12px; right:12px; background-image:url('https://cdn-icons-png.flaticon.com/512/4765/4765549.png'); transform:rotate(-10deg)}
.d-flower{ bottom:12px; right:40px; background-image:url('https://cdn-icons-png.flaticon.com/512/616/616408.png'); transform:rotate(8deg); animation-duration:5s}
.d-ice{ bottom:14px; left:12px; background-image:url('https://cdn-icons-png.flaticon.com/512/1170/1170627.png'); transform:rotate(-6deg); animation-duration:4.5s}
@keyframes floaty{
  0%,100%{ transform: translateY(0) rotate(0deg); }
  50%{ transform: translateY(-12px) rotate(6deg); }
}

/* helper note */
.note{ margin-top:10px; font-size:13px; color:#155; }

/* responsive */
@media(max-width:980px){
  .card{ grid-template-columns: 1fr; }
  .right{ order:-1; margin-bottom:12px }
}

/* glow yellow outline for highlight effect */
.glow{
  box-shadow: 0 8px 40px rgba(255,215,77,0.28), 0 2px 6px rgba(255,240,150,0.12) !important;
  border: 1px solid rgba(255,215,77,0.18);
}
</style>
</head>
<body>
  <div class="card" role="main" aria-label="Cek Hewan Dalam Jiwa">
    <div class="left">
      <h1>Cek Hewan Dalam Jiwa</h1>
      <p class="lead">Masukkan nama & tanggal lahir (data <b>tidak disimpan,Karena Itu Privasi kalian</b>) lalu klik "Cek Hewan" untuk melihat hewan dalam jiwamu ✨</p>

      <label for="name">Nama</label>
      <input id="name" type="text" placeholder="Contoh: Daffa" />

      <div style="display:flex; gap:10px; margin-top:8px;">
        <div style="flex:1">
          <label for="age">Usia</label>
          <input id="age" type="number" min="1" placeholder="Umur (tahun)" />
        </div>
        <div style="flex:1">
          <label for="dob">Tanggal Lahir</label>
          <input id="dob" type="date" />
        </div>
      </div>

      <div class="controls-row">
        <button class="btn" id="checkBtn">🔮 Cek Hewan</button>
        <button class="btn secondary" id="resetBtn">🔁 Reset (Kosongkan)</button>
        <label style="margin-left:auto; font-size:13px; color:#036; align-self:center">
          <input id="soundToggle" type="checkbox" checked /> Suara
        </label>
      </div>

      <div class="note">Keterangan: Hanya untuk hiburan. Hasil random dan tidak menyimpan informasi pribadi.</div>
    </div>

    <div class="right" aria-live="polite">
      <div class="preview-stage" id="stage">
        <div class="decor d-leaf" aria-hidden="true"></div>
        <div class="decor d-flower" aria-hidden="true"></div>
        <div class="decor d-ice" aria-hidden="true"></div>

        <div class="result-bubble" id="resultBubble" role="status" aria-hidden="true">
          <div class="animal-emoji" id="animalEmoji">🦊</div>
          <div class="animal-name" id="animalName">Serigala</div>
          <div class="result-sub" id="resultSub">Keterangan singkat akan tampil di sini.</div>
        </div>
      </div>
    </div>
  </div>

  <!-- sound: default tick/chime (kamu bisa ganti src ke file MP3 sendiri) -->
  <audio id="chime" src="Jokowi.mp3?filename=soft-chime-5945.mp3" preload="auto"></audio>

<script>
/*
  Cek Hewan Dalam Jiwa — Frontend only
  - Data TIDAK DIKIRIM / TIDAK DISIMPAN
  - Untuk menambah hewan: ubah array ANIMALS (lihat catatan di bawah)
*/

// ---------- hewan list (name + emoji or icon) ----------
const ANIMALS = [
  {n:"Serigala", e:"🐺", info:"Pemberani, setia, namun kadang menyendiri."},
  {n:"Kucing", e:"🐱", info:"Mandiri, penasaran, suka kenyamanan."},
  {n:"Anjing", e:"🐶", info:"Ramah, setia, penuh energi."},
  {n:"Kelinci", e:"🐰", info:"Lembut, lincah, penuh rasa ingin tahu."},
  {n:"Gajah", e:"🐘", info:"Bijak, ingatan kuat, penyayang."},
  {n:"Harimau", e:"🐯", info:"Kuat, percaya diri, berkarisma."},
  {n:"Rubah", e:"🦊", info:"Cerdik, lincah, kreatif."},
  {n:"Burung Hantu", e:"🦉", info:"Misterius, reflektif, bijaksana."},
  {n:"Burung", e:"🐦", info:"Bebas, enerjik, penyuka petualangan."},
  {n:"Ikan", e:"🐟", info:"Tenang, adaptif, penuh arus emosi."},
  {n:"Ikan Paus", e:"🐋", info:"Damai, besar hati, komunikatif."},
  {n:"Paus Pembunuh", e:"🐳", info:"Perlindungan kuat terhadap yang dicintai."},
  {n:"Kuda", e:"🐴", info:"Enerjik, kuat, menyukai kebebasan."},
  {n:"Kambing", e:"🐐", info:"Tangguh, gigih, sering penasaran."},
  {n:"Sapi", e:"🐮", info:"Tenang, stabil, penuh kesabaran."},
  {n:"Domba", e:"🐑", info:"Lembut, kekeluargaan, tenang."},
  {n:"Kuda Nil", e:"🦛", info:"Nyaman, kuat di kondisi berat."},
  {n:"Ular", e:"🐍", info:"Misterius, mengandalkan insting, transformasi."},
  {n:"Buaya", e:"🐊", info:"Tangguh, bertahan hidup, waspada."},
  {n:"Beo", e:"🦜", info:"Ceria, suka berekspresi, komunikatif."},
  {n:"Burung Kolibri", e:"🕊️", info:"Energi kecil, kecepatannya luar biasa."},
  {n:"Elang", e:"🦅", info:"Pengamat, fokus, penguasa pandangan jauh."},
  {n:"Badak", e:"🦏", info:"Kuat, tenang, tahan banting."},
  {n:"Koala", e:"🐨", info:"Manja, santai, menyukai kenyamanan."},
  {n:"Panda", e:"🐼", info:"Lembut, penyabar, penyuka makanan enak."},
  {n:"Kanguru", e:"🦘", info:"Enerjik, pelindung, siap melompat maju."},
  {n:"Srigala Arctic", e:"❄️🐺", info:"Tenang di kondisi sulit, tahan dingin."},
  {n:"Kura-kura", e:"🐢", info:"Santai, bijak, berjalan dengan langkah pasti."},
  {n:"Katak", e:"🐸", info:"Adaptif, melompat peluang baru."},
  {n:"Kupu-kupu", e:"🦋", info:"Perubahan, indah, mudah terpesona."},
  {n:"Lebah", e:"🐝", info:"Rajin, kerja tim, penghasil manis."},
  {n:"Semut", e:"🐜", info:"Kerja keras, disiplin, pantang menyerah."},
  {n:"Kumbang", e:"🐞", info:"Kecil tapi berarti, pembawa keberuntungan."},
  {n:"Rakun", e:"🦝", info:"Pintar mencari solusi, suka penasaran."},
  {n:"Lumba-lumba", e:"🐬", info:"Cerdas, sosial, suka bermain."},
  {n:"Landak", e:"🦔", info:"Melindungi diri, penuh keunikan."},
  {n:"Singa", e:"🦁", info:"Pemimpin, percaya diri, berkarisma."},
  {n:"Kucing Hutan", e:"🐈‍⬛", info:"Menyendiri, lincah, misterius."},
  {n:"Rusa", e:"🦌", info:"Anggun, waspada, lemah lembut."},
  {n:"Bebek", e:"🦆", info:"Santai, mengikuti arus, ramah."},
  {n:"Angsa", e:"🦢", info:"Setia, anggun, protektif."},
  {n:"Kakatua", e:"🦜", info:"Berwarna, suka diperhatikan."},
  {n:"Tupai", e:"🐿️", info:"Lincah, perencana kecil, cepat bergerak."},
  {n:"Musang", e:"🦝", info:"Hidup malam, cerdik mencari peluang."},
  {n:"Iguana", e:"🦎", info:"Santai, beradaptasi, memanfaatkan lingkungan."},
  {n:"Tokek", e:"🦎", info:"Tahan banting, suara unik, penjaga rumah."},
  {n:"Salamander", e:"🦎", info:"Regenerasi, berubah seiring waktu."},
  {n:"Kerang", e:"🐚", info:"Tertutup, indah di dalam, butuh perlindungan."},
  {n:"Cumi-cumi", e:"🦑", info:"Cerah, pintar berkamuflase, cepat bereaksi."},
  {n:"Gurita", e:"🐙", info:"Cerdas, multifungsi, penuh solusi."},
  {n:"Bintang Laut", e:"🌟", info:"Tenang, indah, misterius lautan."},
  {n:"Kakap", e:"🐠", info:"Suka bergerombol, hidup di perairan."},
  {n:"Koi", e:"🐟", info:"Keindahan, simbol keberuntungan."},
  {n:"Hiu", e:"🦈", info:"Tegas, fokus, predator alami."},
  {n:"Belut", e:"🐍", info:"Licin, cepat beradaptasi."},
  {n:"Kerbau", e:"🐂", info:"Kuat, pekerja, simbol ketabahan."},
  {n:"Kodok Pohon", e:"🐸", info:"Pemanjat, suka lingkungan hijau."},
  {n:"Kuskus", e:"🦥", info:"Santai, pelan tapi tenang."},
  {n:"Sloth (Kangguru Malas)", e:"🦥", info:"Santai, menikmati waktu perlahan."},
  {n:"Orangutan", e:"🦧", info:"Cerdas, emosional, penyayang keluarga."},
  {n:"Gorila", e:"🦍", info:"Perlindungan keluarga, kuat dan penuh kasih."},
  {n:"Kadal Gurun", e:"🦎", info:"Tangguh di kondisi ekstrem."},
  {n:"Axolotl", e:"🦎", info:"Unik, imut, simbol transformasi."},
  {n:"Lebah Madu", e:"🐝", info:"Sibuk, produktif, manis hasilnya."},
  {n:"Kupu-kupu Malam", e:"🦋", info:"Misterius, transformasi malam."},
  {n:"Walrus", e:"🦭", info:"Bersahabat, besar, kadang ceria."},
  {n:"Anjing Laut", e:"🦭", info:"Lincah di air, sosial."},
  {n:"Penguin", e:"🐧", info:"Lucu, setia, bertahan di dingin."},
  {n:"Albatros", e:"🕊️", info:"Pengembara jauh, pemandangan luas."},
  {n:"Kakatua Raja", e:"🦜", info:"Nyentrik, penuh warna."},
  {n:"Bison", e:"🐂", info:"Berasal dari padang luas, tangguh."},
  {n:"Kuda Laut", e:"🐴", info:"Langka, anggun di air."},
  {n:"Monyet", e:"🐒", info:"Lincah, nakal, sosial."},
  {n:"Lemur", e:"🐒", info:"Eksotis, suka berkumpul."},
  {n:"Tapir", e:"🦛", info:"Unik, penyendiri di hutan."},
  {n:"Antelope", e:"🦌", info:"Cepat, anggun di padang."},
  {n:"Okapi", e:"🦒", info:"Misterius, langka, elegan."},
  {n:"Jerapah", e:"🦒", info:"Tinggi, pandang luas, anggun."},
  {n:"Zebra", e:"🦓", info:"Unik motif, hidup berkelompok."},
  {n:"Hyena", e:"🦝", info:"Cerdik, suara khas, oportunis."},
  {n:"Kuda Liar", e:"🐴", info:"Bebas, tidak bisa dijinakkan dengan mudah."},
  {n:"Kuda Zapata", e:"🐎", info:"Cepat, pekerja keras."},
  {n:"Axeman Bird (imajinatif)", e:"🪶", info:"Hewan kreatif imajiner — cocok untuk ekspresi."},
  {n:"Naga (mitos)", e:"🐉", info:"Kuat, simbol keberanian dan kebijaksanaan."},
  {n:"Unicorn (mitos)", e:"🦄", info:"Murni, imajinatif, langka."},
  {n:"Phoenix (mitos)", e:"🔥", info:"Kelahiran kembali, transformasi."},
  {n:"Griffin (mitos)", e:"🦅🦁", info:"Perpaduan kekuatan dan keanggunan."},
  {n:"Minotaur (mitos)", e:"🐂", info:"Kombinasi kekuatan dan labirin batin."},
  {n:"Chimera (mitos)", e:"🐉", info:"Beragam sisi dalam satu pribadi."},
  {n:"Serigala Bulan", e:"🌕🐺", info:"Terhubung dengan intuisi malam."},
  {n:"Komet (simbolik)", e:"☄️", info:"Cepat, membawa perubahan."},
  {n:"Rubah Arktik", e:"🦊❄️", info:"Adaptif di kondisi ekstrem."},
  {n:"Merpati", e:"🕊️", info:"Simbol perdamaian dan ketenangan."},
  {n:"Kakatua Mawar", e:"🦜", info:"Warni, penuh ekspresi."},
  {n:"Sotong Raksasa", e:"🦑", info:"Misterius dan cerdas di lautan."},
  {n:"Krakens (mitos laut)", e:"🌊", info:"Misteri lautan mendalam."},
  {n:"Capung", e:"🐉", info:"Cepat, hidup singkat penuh warna."},
  {n:"Kalajengking", e:"🦂", info:"Protektif, waspada."},
  {n:"Lumba-lumba Sungai", e:"🐬", info:"Cerdas, sosial di air tawar."},
  {n:"Axolotl Pelangi", e:"🦎", info:"Unik, simbol regenerasi warna-warni."},
  {n:"Marmut", e:"🐹", info:"Imut, ramah, kecil tapi hangat."},
  {n:"Hamster", e:"🐹", info:"Lucu, bekerja mencari kenyamanan."},
  {n:"Tikus", e:"🐀", info:"Cerdik, bertahan terus-menerus."},
  {n:"Landak Laut", e:"🦔", info:"Unik, pelindung alami."},
  {n:"Ibis", e:"🕊️", info:"Anggun, penjelajah rawa."},
  {n:"Rangkong", e:"🪶", info:"Bersuara keras, terlihat bangga."},
  {n:"Kakatua Sulawesi", e:"🦜", info:"Eksotis, penuh warna."},
  {n:"Burung Unta", e:"🦤", info:"Kuat, berlari cepat di padang."},
  {n:"Kelinci Gunung", e:"🐇", info:"Tahan dingin, gesit."},
  {n:"Anakonda", e:"🐍", info:"Besar, penuh tenaga."},
  {n:"Macan Dahan", e:"🐅", info:"Lincah di pepohonan."},
  {n:"Babi Hutan", e:"🐗", info:"Keras, bertahan di alam."},
  {n:"Babi Mandi", e:"🐖", info:"Nikmat, santai, suka makanan."},
  {n:"Kucing Anggora", e:"🐱", info:"Gaya, lembut, elegan."},
  {n:"Ayam", e:"🐔", info:"Produktif, penuh rutinitas."},
  {n:"Itik Hias", e:"🦆", info:"Indah di perairan keluarga."},
  {n:"Merak", e:"🦚", info:"Pamer, penuh warna, cantik."},
  {n:"Elang Laut", e:"🦅", info:"Pengintai pantai, mata tajam."},
  {n:"Kucing Liar", e:"🐱", info:"Kemandirian, kebebasan malam."},
  {n:"Kucing Rumah", e:"🐈", info:"Teman rumahan yang hangat."},
  {n:"Serigala", e:"🐺", info:"Pemberani dan setia, namun kadang menyendiri."},
  {n:"Kucing", e:"🐱", info:"Mandiri, penasaran, suka kenyamanan."},
  {n:"Anjing", e:"🐶", info:"Ramah, setia, dan energik."},
  {n:"Kelinci", e:"🐰", info:"Lembut, gesit, dan penuh rasa ingin tahu."},
  {n:"Gajah", e:"🐘", info:"Bijak, penyayang, dan punya ingatan kuat."},
  {n:"Harimau", e:"🐯", info:"Kuat dan berkarisma, tapi suka menyendiri."},
  {n:"Rubah", e:"🦊", info:"Cerdik, kreatif, dan cepat berpikir."},
  {n:"Burung Hantu", e:"🦉", info:"Misterius dan bijaksana, teman malam sejati."},
  {n:"Burung", e:"🐦", info:"Bebas, enerjik, penyuka petualangan."},
  {n:"Ikan", e:"🐟", info:"Tenang dan adaptif, tapi penuh arus emosi."},
  {n:"Paus", e:"🐋", info:"Damai, besar hati, komunikatif."},
  {n:"Kuda", e:"🐴", info:"Kuat, enerjik, dan menyukai kebebasan."},
  {n:"Sapi", e:"🐮", info:"Tenang, stabil, penuh kesabaran."},
  {n:"Domba", e:"🐑", info:"Lembut, kekeluargaan, penuh kedamaian."},
  {n:"Kura-kura", e:"🐢", info:"Santai, bijak, dan sabar menghadapi hidup."},
  {n:"Katak", e:"🐸", info:"Adaptif, melompat peluang baru."},
  {n:"Kupu-kupu", e:"🦋", info:"Indah, bebas, dan suka perubahan."},
  {n:"Lebah", e:"🐝", info:"Rajin, pekerja keras, pembawa manis."},
  {n:"Semut", e:"🐜", info:"Disiplin dan pantang menyerah."},
  {n:"Rakun", e:"🦝", info:"Pintar dan selalu penasaran."},
  {n:"Lumba-lumba", e:"🐬", info:"Cerdas, sosial, dan suka bermain."},
  {n:"Landak", e:"🦔", info:"Lucu tapi punya pelindung alami."},
  {n:"Singa", e:"🦁", info:"Pemimpin alami yang percaya diri."},
  {n:"Rusa", e:"🦌", info:"Anggun dan waspada terhadap lingkungan."},
  {n:"Bebek", e:"🦆", info:"Santai dan menyenangkan di air."},
  {n:"Angsa", e:"🦢", info:"Setia dan anggun dalam sikapnya."},
  {n:"Koala", e:"🐨", info:"Santai, manja, dan cinta kedamaian."},
  {n:"Panda", e:"🐼", info:"Penyabar, lembut, dan cinta makanan enak."},
  {n:"Kanguru", e:"🦘", info:"Enerjik dan pelindung bagi yang disayangi."},
  {n:"Ular", e:"🐍", info:"Bijak, misterius, dan pandai beradaptasi."},
  {n:"Buaya", e:"🐊", info:"Tangguh, waspada, dan sabar menunggu peluang."},
  {n:"Elang", e:"🦅", info:"Fokus, tajam, dan pengamat hebat."},
  {n:"Badak", e:"🦏", info:"Tangguh dan kuat, tapi tenang."},
  {n:"Kambing", e:"🐐", info:"Teguh dan selalu mencari jalan."},
  {n:"Zebra", e:"🦓", info:"Unik dan mencintai kebebasan."},
  {n:"Jerapah", e:"🦒", info:"Anggun, sabar, dan berpandangan luas."},
  {n:"Beruang", e:"🐻", info:"Hangat dan pelindung, tapi suka tidur lama."},
  {n:"Babi", e:"🐷", info:"Lucu, santai, dan suka kenyamanan."},
  {n:"Ayam", e:"🐔", info:"Produktif dan suka rutinitas."},
  {n:"Burung Merak", e:"🦚", info:"Cantik dan percaya diri."},
  {n:"Kucing Hutan", e:"🐈‍⬛", info:"Misterius dan independen."},
  {n:"Musang", e:"🦝", info:"Suka malam, cerdik, dan licik sedikit 😆."},
  {n:"Bunglon", e:"🦎", info:"Adaptif dan penuh warna."},
  {n:"Tokek", e:"🦎", info:"Tangguh dan jadi penjaga rumah."},
  {n:"Cicak", e:"🦎", info:"Diam tapi selalu mengawasi."},
  {n:"Kadal Gurun", e:"🦎", info:"Sabar dan tahan panas."},
  {n:"Iguana", e:"🦎", info:"Santai dan suka sinar matahari."},
  {n:"Anjing Laut", e:"🦭", info:"Ceria dan suka bermain di air."},
  {n:"Penguin", e:"🐧", info:"Lucu, setia, dan tahan dingin."},
  {n:"Paus Pembunuh", e:"🐳", info:"Kuat dan melindungi kelompoknya."},
  {n:"Kuda Laut", e:"🐠", info:"Unik dan lembut di air."},
  {n:"Gurita", e:"🐙", info:"Cerdas dan bisa menyesuaikan diri."},
  {n:"Cumi-cumi", e:"🦑", info:"Pintar berkamuflase dan cepat tanggap."},
  {n:"Kepiting", e:"🦀", info:"Pelindung dan punya cangkang keras luar, lembut dalam."},
  {n:"Udang", e:"🦐", info:"Lucu dan aktif di dunia bawah laut."},
  {n:"Bintang Laut", e:"🌟", info:"Simbol keindahan dan kedamaian laut."},
  {n:"Kupu-kupu Malam", e:"🦋", info:"Misterius dan menawan di kegelapan."},
  {n:"Laba-laba", e:"🕷️", info:"Teliti dan ahli dalam strategi."},
  {n:"Kalajengking", e:"🦂", info:"Tegas dan waspada, tapi protektif."},
  {n:"Capung", e:"🐉", info:"Cepat, indah, dan penuh warna."},
  {n:"Lebah Madu", e:"🐝", info:"Kerja keras dan bawa hasil manis."},
  {n:"Tawon", e:"🐝", info:"Berani melindungi diri dan kelompoknya."},
  {n:"Cicada", e:"🎵", info:"Suara nyaring, penuh semangat hidup."},
  {n:"Kumbang", e:"🐞", info:"Pembawa keberuntungan dan pesona kecil."},
  {n:"Belalang", e:"🦗", info:"Lompat tinggi dan penuh semangat."},
  {n:"Kecoak", e:"🪳", info:"Tahan banting di segala kondisi."},
  {n:"Kuda Nil", e:"🦛", info:"Tenang tapi kuat bila dibutuhkan."},
  {n:"Tapir", e:"🦛", info:"Unik dan tenang di hutan tropis."},
  {n:"Bison", e:"🐂", info:"Kuat, kokoh, dan gagah."},
  {n:"Kerbau", e:"🐃", info:"Teguh dan pekerja keras."},
  {n:"Sapi Highland", e:"🐮", info:"Berbulu lebat, tenang, dan sabar."},
  {n:"Kuda Zebra", e:"🦓", info:"Unik dan suka perhatian."},
  {n:"Ayam Hutan", e:"🐔", info:"Berani dan penuh warna."},
  {n:"Burung Cendrawasih", e:"🪶", info:"Cantik, elegan, dan langka."},
  {n:"Burung Unta", e:"🦤", info:"Cepat dan tangguh di padang."},
  {n:"Burung Kakaktua", e:"🦜", info:"Ceria, suka bicara, dan warna-warni."},
  {n:"Beo", e:"🦜", info:"Ceria dan suka meniru suara."},
  {n:"Burung Kolibri", e:"🕊️", info:"Kecil tapi punya energi besar."},
  {n:"Merpati", e:"🕊️", info:"Damai, lembut, dan penuh cinta."},
  {n:"Burung Elang Laut", e:"🦅", info:"Kuat dan tajam penglihatannya."},
  {n:"Burung Pipit", e:"🐦", info:"Lucu dan suka bersosialisasi."},
  {n:"Burung Kenari", e:"🐦", info:"Ceria dan suka bernyanyi."},
  {n:"Burung Gereja", e:"🐦", info:"Biasa tapi berarti."},
  {n:"Naga", e:"🐉", info:"Kuat dan penuh kebijaksanaan."},
  {n:"Unicorn", e:"🦄", info:"Murni dan penuh imajinasi."},
  {n:"Phoenix", e:"🔥", info:"Simbol kebangkitan dan harapan baru."},
  {n:"Griffin", e:"🦅🦁", info:"Kombinasi kekuatan dan kebijaksanaan."},
  {n:"Pegasus", e:"🪽", info:"Bebas dan melayang di atas batas."},
  {n:"Minotaur", e:"🐂", info:"Kuat tapi introspektif."},
  {n:"Chimera", e:"🐉", info:"Beragam sisi dalam satu pribadi."},
  {n:"Hydra", e:"🐉", info:"Sulit dikalahkan dan regeneratif."},
  {n:"Cerberus", e:"🐕", info:"Pelindung setia dari bawah dunia."},
  {n:"Kitsune", e:"🦊", info:"Licik tapi penuh daya tarik mistis."},
  {n:"Tanuki", e:"🦝", info:"Pembawa keberuntungan dan jenaka."},
  {n:"Rubah Api", e:"🔥🦊", info:"Hangat dan penuh semangat."},
  {n:"Serigala Bulan", e:"🌕🐺", info:"Terhubung dengan energi malam."},
  {n:"Naga Es", e:"❄️🐉", info:"Dingin tapi elegan dan kuat."},
  {n:"Naga Api", e:"🔥🐉", info:"Berani dan penuh gairah."},
  {n:"Burung Petir", e:"⚡🕊️", info:"Cepat dan berenergi tinggi."},
  {n:"Burung Angin", e:"🌬️🐦", info:"Bebas dan tak terikat apa pun."},
  {n:"Kucing Ajaib", e:"✨🐈", info:"Lucu tapi penuh misteri sihir."},
  {n:"Anjing Pelangi", e:"🌈🐶", info:"Ceria dan membawa kebahagiaan."},
  {n:"Hiu", e:"🦈", info:"Fokus dan tangguh dalam perairan."},
  {n:"Belut", e:"🐍", info:"Licin dan cepat beradaptasi."},
  {n:"Ikan Koi", e:"🐟", info:"Simbol keberuntungan dan ketenangan."},
  {n:"Ikan Cupang", e:"🐠", info:"Kecil tapi berani dan penuh warna."},
  {n:"Ikan Mas", e:"🐠", info:"Tenang dan membawa rezeki."},
  {n:"Ikan Gurame", e:"🐟", info:"Damai dan penyabar."},
  {n:"Ikan Lele", e:"🐟", info:"Pekerja keras yang tahan lumpur."},
  {n:"Ikan Paus", e:"🐋", info:"Bijak dan tenang di kedalaman laut."},
  {n:"Ikan Hiu Putih", e:"🦈", info:"Tegas dan tangguh di ombak."},
  {n:"Ikan Pari", e:"🌊", info:"Lembut tapi punya kekuatan tersembunyi."},
  {n:"Ikan Lumba", e:"🐬", info:"Cerdas dan suka berinteraksi."},
  {n:"Ikan Pedang", e:"⚔️🐟", info:"Cepat dan fokus pada tujuan."},
  {n:"Kepiting Biru", e:"🦀", info:"Lucu dan bersemangat tinggi."},
  {n:"Ubur-ubur", e:"🌊", info:"Lembut tapi berbahaya bila tersentuh."},
  {n:"Cumi Raksasa", e:"🦑", info:"Tangguh dan misterius."},
  {n:"Kerang", e:"🐚", info:"Diam tapi menyimpan keindahan."},
  {n:"Karang", e:"🪸", info:"Indah dan menopang banyak kehidupan."},
  {n:"Bintang Laut Pelangi", e:"🌈⭐", info:"Penuh warna dan harapan."},
  {n:"Penyu", e:"🐢", info:"Bijak, lambat tapi pasti."},
  {n:"Buaya Muara", e:"🐊", info:"Sabar, kuat, dan fokus."},
  {n:"Komodo", e:"🦎", info:"Legenda dari tanah hangat Indonesia 🇮🇩."},
  {n:"Ayam Jago", e:"🐓", info:"Pemberani dan selalu bangun pagi."},
  {n:"Kalkun", e:"🦃", info:"Ramah dan penuh gaya."},
  {n:"Merak Putih", e:"🦚", info:"Cantik dan langka."},
  {n:"Cendrawasih Emas", e:"🪶", info:"Simbol kecantikan abadi."},
  {n:"Burung Hantu Salju", e:"🦉", info:"Bijak dan elegan di malam putih."},
  {n:"Elang Jawa", e:"🦅", info:"Bangga dan kuat seperti pejuang."},
  {n:"Burung Pipit Kuning", e:"🐦", info:"Ceria dan optimis sepanjang hari."},
  {n:"Burung Merpati", e:"🕊️", info:"Simbol cinta dan kedamaian."},
  {n:"Kucing Anggora", e:"🐈", info:"Lembut, elegan, dan penyayang."},
  {n:"Kucing Persia", e:"🐱", info:"Tenang dan mewah."},
  {n:"Kucing Hitam", e:"🐈‍⬛", info:"Misterius dan membawa keberuntungan tersendiri."},
  {n:"Kucing Jalanan", e:"🐾", info:"Bebas dan penuh petualangan."},
  {n:"Anjing Shiba", e:"🐕", info:"Lucu, cerdas, dan percaya diri."},
  {n:"Anjing Golden", e:"🐶", info:"Hangat dan penyayang tanpa syarat."},
  {n:"Anjing Siberian", e:"❄️🐶", info:"Kuat dan setia seperti serigala salju."},
  {n:"Anjing Laut Putih", e:"🦭", info:"Lucu dan gemuk, suka main salju."},
  {n:"Anjing Galaksi", e:"🌌🐕", info:"Setia dan tak terbatas imajinasinya."},
  {n:"Serigala Salju", e:"❄️🐺", info:"Tenang dan tahan segala cuaca."},
  {n:"Serigala Hitam", e:"🌑🐺", info:"Misterius tapi penuh karisma."},
  {n:"Serigala Api", e:"🔥🐺", info:"Panas semangatnya, sulit dipadamkan."},
  {n:"Serigala Hutan", e:"🌲🐺", info:"Pelindung dan pengembara alam liar."},
  {n:"Rubah Awan", e:"☁️🦊", info:"Ringan dan suka bermimpi."},
  {n:"Rubah Salju", e:"❄️🦊", info:"Anggun di dingin dan lembut di hati."},
  {n:"Rubah Bulan", e:"🌕🦊", info:"Intuitif dan peka terhadap Cuaca."},{n:"Rubah Bulan", e:"🌕🦊", info:"Intuitif dan peka terhadap emosi sekitar."},
  {n:"Rubah Petir", e:"⚡🦊", info:"Gesit, cepat berpikir, dan penuh energi."},
  {n:"Rubah Ekor Sembilan", e:"✨🦊", info:"Penuh misteri dan kekuatan dalam diam."},
  {n:"Kucing Salju", e:"❄️🐱", info:"Tenang, lembut, dan jarang marah."},
  {n:"Kucing Api", e:"🔥🐈", info:"Hangat, penuh semangat dan percaya diri."},
  {n:"Kucing Air", e:"💧🐱", info:"Tenang dan menenangkan suasana."},
  {n:"Kucing Angin", e:"🌬️🐱", info:"Gesit dan suka kebebasan."},
  {n:"Kucing Awan", e:"☁️🐱", info:"Lembut dan suka melamun."},
  {n:"Kucing Hujan", e:"🌧️🐈", info:"Melankolis tapi menenangkan hati."},
  {n:"Kucing Kilat", e:"⚡🐈", info:"Lincah dan selalu bersemangat."},
  {n:"Kucing Sakura", e:"🌸🐱", info:"Cantik dan berjiwa lembut."},
  {n:"Kucing Galaksi", e:"🌌🐈", info:"Unik dan penuh misteri alam semesta."},
  {n:"Anjing Angin", e:"🌬️🐶", info:"Cepat, kuat, dan selalu berlari menuju tujuan."},
  {n:"Anjing Air", e:"💧🐕", info:"Tenang, setia, dan damai."},
  {n:"Anjing Api", e:"🔥🐶", info:"Panas semangatnya, tak kenal lelah."},
  {n:"Anjing Salju", e:"❄️🐕", info:"Setia dan tahan segala rintangan."},
  {n:"Anjing Bulan", e:"🌕🐶", info:"Setia dan sensitif terhadap perasaan orang lain."},
  {n:"Singa Emas", e:"🌞🦁", info:"Pemimpin yang hangat dan memotivasi."},
  {n:"Singa Putih", e:"🤍🦁", info:"Langka, murni, dan berwibawa."},
  {n:"Singa Hitam", e:"🌑🦁", info:"Kuat dan misterius, tapi bijak."},
  {n:"Singa Air", e:"💧🦁", info:"Tenang tapi memiliki kekuatan besar."},
  {n:"Singa Api", e:"🔥🦁", info:"Berani dan penuh semangat hidup."},
  {n:"Elang Api", e:"🔥🦅", info:"Cepat, tegas, dan berani mengambil risiko."},
  {n:"Elang Salju", e:"❄️🦅", info:"Tenang, tajam, dan berwibawa."},
  {n:"Elang Bulan", e:"🌕🦅", info:"Bijak dan melihat jauh ke depan."},
  {n:"Elang Emas", e:"🌞🦅", info:"Menyala penuh kebanggaan dan semangat."},
  {n:"Harimau Putih", e:"❄️🐯", info:"Kuat, langka, dan elegan."},
  {n:"Harimau Api", e:"🔥🐯", info:"Berani dan penuh determinasi."},
  {n:"Harimau Emas", e:"🌞🐯", info:"Pemimpin alami dengan pesona."},
  {n:"Harimau Hitam", e:"🌑🐯", info:"Misterius dan tangguh menghadapi kesulitan."},
  {n:"Harimau Angin", e:"🌬️🐯", info:"Cepat dan tak bisa dikurung."},
  {n:"Macan Dahan", e:"🌳🐅", info:"Pendiam tapi memiliki kekuatan tersembunyi."},
  {n:"Macan Tutul", e:"🐆", info:"Gesit dan cerdik, pemburu sejati."},
  {n:"Jaguar", e:"🐆", info:"Kuat, tenang, dan misterius."},
  {n:"Cheetah", e:"🐆", info:"Cepat dan penuh fokus pada tujuan."},
  {n:"Lynx", e:"🐱", info:"Tajam dalam pengamatan dan penuh insting."},
  {n:"Puma", e:"🐈", info:"Kuat, mandiri, dan gesit."},
  {n:"Leopard Salju", e:"❄️🐆", info:"Langka dan elegan di puncak tertinggi."},
  {n:"Beruang Kutub", e:"🐻‍❄️", info:"Tangguh dan lembut dalam waktu bersamaan."},
  {n:"Beruang Madu", e:"🍯🐻", info:"Manis, santai, dan penyayang."},
  {n:"Beruang Hitam", e:"🌑🐻", info:"Kuat dan penyendiri."},
  {n:"Beruang Gunung", e:"🏔️🐻", info:"Teguh dan suka tantangan alam."},
  {n:"Kelinci Salju", e:"❄️🐇", info:"Gesit dan lucu di lingkungan dingin."},
  {n:"Kelinci Api", e:"🔥🐇", info:"Ceria dan penuh semangat kehidupan."},
  {n:"Kelinci Sakura", e:"🌸🐇", info:"Lembut dan mencintai keindahan."},
  {n:"Kelinci Bulan", e:"🌕🐇", info:"Simbol mimpi dan keajaiban malam."},
  {n:"Kelinci Galaksi", e:"🌌🐇", info:"Imut tapi penuh misteri kosmos."},
  {n:"Kuda Api", e:"🔥🐎", info:"Cepat, berani, dan tak kenal lelah."},
  {n:"Kuda Es", e:"❄️🐎", info:"Anggun dan teguh di bawah tekanan."},
  {n:"Kuda Petir", e:"⚡🐎", info:"Gesit dan sangat ambisius."},
  {n:"Kuda Angin", e:"🌬️🐎", info:"Bebas dan sulit dikendalikan."},
  {n:"Kuda Air", e:"💧🐎", info:"Tenang tapi sangat kuat bila dibutuhkan."},
  {n:"Kuda Emas", e:"🌞🐎", info:"Bersinar dengan percaya diri."},
  {n:"Kuda Hitam", e:"🌑🐎", info:"Klasik, elegan, dan penuh misteri."},
  {n:"Kuda Putih", e:"🤍🐎", info:"Murni dan berjiwa ksatria."},
  {n:"Kuda Langit", e:"☁️🐎", info:"Suka mimpi tinggi dan tidak mudah menyerah."},
  {n:"Rusa Putih", e:"🤍🦌", info:"Lembut dan membawa keberuntungan."},
  {n:"Rusa Hutan", e:"🌲🦌", info:"Damai dan menyatu dengan alam."},
  {n:"Rusa Api", e:"🔥🦌", info:"Berani dan percaya diri dalam kegelapan."},
  {n:"Rusa Es", e:"❄️🦌", info:"Tenang dan elegan di saat sulit."},
  {n:"Rusa Bulan", e:"🌕🦌", info:"Peka dan intuitif terhadap dunia."},
  {n:"Panda Merah", e:"🦊🐼", info:"Lucu, lembut, dan penuh kehangatan."},
  {n:"Sloth", e:"🦥", info:"Santai, damai, dan anti stres."},
  {n:"Koala Malam", e:"🌙🐨", info:"Santai dan suka kedamaian malam."},
  {n:"Musang Awan", e:"☁️🦝", info:"Cerdik dan suka bersantai di waktu tenang."},
  {n:"Musang Api", e:"🔥🦝", info:"Penuh semangat dan ide gila."},
  {n:"Musang Hitam", e:"🌑🦝", info:"Pendiam tapi misterius dan berani."},
  {n:"Tupai Terbang", e:"🪶🐿️", info:"Gesit dan suka kebebasan."},
  {n:"Tupai Gunung", e:"🏔️🐿️", info:"Kecil tapi penuh keberanian."},
  {n:"Tupai Emas", e:"🌞🐿️", info:"Ceria dan cepat beradaptasi."},
  {n:"Burung Phoenix", e:"🔥🕊️", info:"Bangkit dari kegagalan dengan semangat baru."},
  {n:"Burung Pelangi", e:"🌈🦜", info:"Berwarna dan penuh inspirasi."},
  {n:"Burung Malam", e:"🌙🦉", info:"Misterius dan penyendiri yang bijak."},
  {n:"Burung Awan", e:"☁️🐦", info:"Ringan, damai, dan suka melayang-layang."},
  {n:"Burung Petir", e:"⚡🐦", info:"Cepat dan berani menembus rintangan."},
  {n:"Burung Cahaya", e:"✨🕊️", info:"Membawa harapan dan ketenangan."},
  {n:"Burung Batu", e:"🪶🪨", info:"Kuat dan stabil dalam segala kondisi."},
  {n:"Burung Gelap", e:"🌑🦅", info:"Tenang dan misterius tapi setia."},
  {n:"Burung Putih", e:"🤍🕊️", info:"Simbol perdamaian sejati."},
  {n:"Naga Hujan", e:"💧🐉", info:"Menenangkan dan penuh empati."},
  {n:"Naga Petir", e:"⚡🐉", info:"Cepat dan luar biasa kuat."},
  {n:"Naga Langit", e:"☁️🐉", info:"Bijak dan spiritual."},
  {n:"Naga Bumi", e:"🌍🐉", info:"Tenang dan membawa kestabilan."},
  {n:"Naga Laut", e:"🌊🐉", info:"Dalam, misterius, dan tenang."},
  {n:"Naga Pelangi", e:"🌈🐉", info:"Kreatif dan penuh warna kehidupan."},
  {n:"Naga Gelap", e:"🌑🐉", info:"Kuat dan misterius dalam bayangan."},
  {n:"Naga Api", e:"🔥🐉", info:"Simbol kekuatan dan semangat."},
  {n:"Naga Emas", e:"🌞🐉", info:"Pemimpin sejati penuh karisma."},
  {n:"Naga Salju", e:"❄️🐉", info:"Dingin tapi indah dan berwibawa."},
  {n:"Naga Sakura", e:"🌸🐉", info:"Lembut tapi kuat dalam hati."},
  {n:"Naga Angin", e:"🌬️🐉", info:"Cepat dan bijak."},
  {n:"Naga Bintang", e:"🌌🐉", info:"Lahir dari imajinasi dan cahaya."},
  {n:"Naga Bulan", e:"🌕🐉", info:"Penuh misteri dan ketenangan batin."},
  {n:"Naga Matahari", e:"🌞🐉", info:"Penuh semangat dan vitalitas."},
  {n:"Naga Aurora", e:"🌈❄️🐉", info:"Indah dan membawa cahaya damai."},
  {n:"Phoenix Es", e:"❄️🔥", info:"Bangkit dari dingin dan panas sekaligus."},
  {n:"Phoenix Emas", e:"🌞🔥", info:"Simbol keagungan dan kebangkitan."},
  {n:"Phoenix Malam", e:"🌙🔥", info:"Penuh aura mistis dan ketenangan."},
  {n:"Phoenix Pelangi", e:"🌈🔥", info:"Penuh warna, harapan, dan kehidupan."},
  {n:"Phoenix Bumi", e:"🌍🔥", info:"Bangkit dari debu menjadi kekuatan baru."},
  {n:"Phoenix Langit", e:"☁️🔥", info:"Terlahir kembali di cahaya harapan."},
  {n:"Griffin Langit", e:"☁️🦅🦁", info:"Gabungan kebijaksanaan dan kekuatan."},
  {n:"Unicorn Air", e:"💧🦄", info:"Lembut dan menenangkan hati."},
  {n:"Unicorn Api", e:"🔥🦄", info:"Semangat dan penuh kehidupan."},
  {n:"Unicorn Es", e:"❄️🦄", info:"Tenang dan anggun di segala waktu."},
  {n:"Unicorn Pelangi", e:"🌈🦄", info:"Simbol keajaiban dan imajinasi tinggi."},
  {n:"Unicorn Bulan", e:"🌕🦄", info:"Romantis dan misterius."},
  {n:"Unicorn Galaksi", e:"🌌🦄", info:"Penuh mimpi dan keindahan kosmos."},
  {n:"Kuda Pegasus", e:"🪽🐎", info:"Terbang bebas melampaui batas dunia."},
  {n:"Pegasus Hitam", e:"🌑🪽", info:"Pemberani dalam keheningan malam."},
  {n:"Pegasus Emas", e:"🌞🪽", info:"Bersinar dan jadi inspirasi bagi semua."},
  {n:"Pegasus Awan", e:"☁️🪽", info:"Tenang dan damai di atas langit biru."},
  {n:"Kucing Nebula", e:"🌌🐱", info:"Imut tapi seluas galaksi di hatinya."},
  {n:"Serigala Aurora", e:"🌈🐺", info:"Indah, misterius, dan penuh cahaya malam."},
  {n:"Burung Kristal", e:"💎🕊️", info:"Murni dan berkilau dalam kegelapan."},
  {n:"Burung Cahaya Biru", e:"💙🕊️", info:"Menebarkan ketenangan bagi sekitar."},
  {n:"Burung Cermin", e:"🪞🕊️", info:"Reflektif dan penuh introspeksi."},
  {n:"Burung Ember", e:"🔥🐦", info:"Penuh api semangat kehidupan."},
  {n:"Burung Es", e:"❄️🐦", info:"Tenang, lembut, dan fokus."},
  {n:"Kucing Pixel", e:"🧩🐱", info:"Unik dan modern, suka teknologi."},
  {n:"Anjing Digital", e:"💾🐕", info:"Setia di dunia maya dan nyata."},
  {n:"Paus Galaksi", e:"🌌🐋", info:"Bijak dan menenangkan seperti bintang laut."},
  {n:"Paus Pelangi", e:"🌈🐋", info:"Menyebar kebahagiaan di lautan luas."},
  {n:"Kuda Laut Kristal", e:"💎🐠", info:"Halus dan indah dalam bentuk sederhana."},
  {n:"Gurita Pelangi", e:"🌈🐙", info:"Kreatif dan punya banyak cara untuk berhasil."},
  {n:"Gurita Galaksi", e:"🌌🐙", info:"Cerdas dan misterius di dunia bawah laut."},
  {n:"Kupu-kupu Aurora", e:"🌈🦋", info:"Cantik, lembut, dan simbol kebebasan."},
  {n:"Kupu-kupu Es", e:"❄️🦋", info:"Anggun dan elegan di dunia beku."},
  {n:"Kupu-kupu Sakura", e:"🌸🦋", info:"Penuh keindahan dan cinta musim semi."},
  {n:"Lebah Emas", e:"🌞🐝", info:"Berkarya keras dan membawa kebahagiaan."},
  {n:"Lebah Pelangi", e:"🌈🐝", info:"Rajin tapi juga ceria dan berwarna."},
  {n:"Semut Baja", e:"🪓🐜", info:"Kuat dan pekerja keras sejati."},
  {n:"Kumbang Besi", e:"⚙️🐞", info:"Kreatif dan tahan banting di dunia modern."},
  {n:"Kumbang Biru", e:"💙🐞", info:"Tenang dan penuh pesona kecil."},
  {n:"Lebah Digital", e:"💻🐝", info:"Cerdas dan cepat seperti teknologi."},
  {n:"Burung Emoji", e:"📱🐦", info:"Lucu dan kekinian banget 😆."},
  {n:"Kucing Cyber", e:"💽🐱", info:"Mekanis tapi punya hati hangat."},
  {n:"Anjing Cyber", e:"🔋🐶", info:"Selalu aktif dan setia 24 jam."},
  {n:"Burung Neon", e:"💡🐦", info:"Cerah dan membawa ide-ide baru."},
  {n:"Pikachu", e:"⚡🐭", info:"Ceria, penuh energi listrik, simbol semangat."},
  {n:"Charmander", e:"🔥🦎", info:"Berapi-api, tak menyerah meski kecil."},
  {n:"Bulbasaur", e:"🌿🐸", info:"Tenang, penyayang alam dan sabar."},
  {n:"Squirtle", e:"💧🐢", info:"Lucu, ceria, selalu beradaptasi dengan baik."},
  {n:"Eevee", e:"✨🦊", info:"Fleksibel, bisa berubah sesuai suasana hati."},
  {n:"Jigglypuff", e:"🎵💤", info:"Lembut, manis, tapi jangan remehkan suaranya."},
  {n:"Meowth", e:"💰🐱", info:"Cerdik, materialistis tapi punya hati hangat."},
  {n:"Psyduck", e:"💫🦆", info:"Kebingungan tapi punya kekuatan tersembunyi."},
  {n:"Machop", e:"💪", info:"Kuat, pekerja keras, bermental baja."},
  {n:"Abra", e:"🌀", info:"Tenang, misterius, memiliki kekuatan pikiran luar biasa."},
  {n:"Kadabra", e:"🔮", info:"Bijak, fokus, pemikir logis."},
  {n:"Alakazam", e:"🧠", info:"Jenius dan analitis, kekuatan pikirannya menembus batas."},
  {n:"Gastly", e:"👻", info:"Gaib, penuh rahasia, tapi lucu di hati."},
  {n:"Gengar", e:"💀", info:"Nakal, humoris, tapi setia pada teman."},
  {n:"Snorlax", e:"💤🐻", info:"Santai, damai, menikmati hidup tanpa tergesa."},
  {n:"Lucario", e:"🧘‍♂️🐺", info:"Bijak dan setia, berjiwa pejuang sejati."},
  {n:"Mew", e:"🌸🐱", info:"Misterius, lembut, penuh keajaiban."},
  {n:"Mewtwo", e:"🧬⚡", info:"Kuat, tegas, penuh tujuan dan harga diri."},
  {n:"Dragonite", e:"🐉💛", info:"Penuh kasih, melindungi dan suka membantu."},
  {n:"Lapras", e:"🌊🦕", info:"Lembut, penolong, dan cinta kedamaian."},
  {n:"Vulpix", e:"🔥🦊", info:"Manis, percaya diri, dan elegan."},
  {n:"Ninetales", e:"🔥🦊", info:"Misterius dan mempesona, memiliki aura magis."},
  {n:"Growlithe", e:"🔥🐶", info:"Setia, berani, dan protektif."},
  {n:"Arcanine", e:"🔥🦁", info:"Bangga, heroik, dan megah seperti singa."},
  {n:"Poliwag", e:"💧🐸", info:"Lucu dan suka bermain di air."},
  {n:"Tentacool", e:"🪼", info:"Tenang tapi berbahaya saat terganggu."},
  {n:"Tentacruel", e:"🪼💧", info:"Pintar dan suka menjaga keseimbangan laut."},
  {n:"Onix", e:"🪨🐍", info:"Teguh dan tahan banting, fondasi yang kokoh."},
  {n:"Geodude", e:"🪨", info:"Keras kepala tapi bisa diandalkan."},
  {n:"Golem", e:"🪨💥", info:"Kuat dan solid, melindungi yang dicintai."},
  {n:"Cubone", e:"💀🦴", info:"Melankolis tapi punya hati paling lembut."},
  {n:"Marowak", e:"🦴🔥", info:"Tabah dan penuh kenangan masa lalu."},
  {n:"Hitmonlee", e:"🥋🦵", info:"Disiplin, fokus, pengendali diri tinggi."},
  {n:"Hitmonchan", e:"🥊", info:"Protektif dan siap melawan ketidakadilan."},
  {n:"Chansey", e:"💖🥚", info:"Penyembuh dan penyayang sejati."},
  {n:"Kangaskhan", e:"🤱🦘", info:"Ibu pelindung dan pejuang sejati."},
  {n:"Tauros", e:"🐂🔥", info:"Penuh semangat dan kekuatan tak terkendali."},
  {n:"Magikarp", e:"🐟", info:"Lemah di awal tapi berpotensi besar di masa depan."},
  {n:"Gyarados", e:"🐉🌊", info:"Penuh amarah, kekuatannya luar biasa."},
  {n:"Ditto", e:"🟪", info:"Fleksibel dan mudah menyesuaikan diri."},
  {n:"Eevee", e:"✨🦊", info:"Serbaguna dan siap berubah jadi apa pun."},
  {n:"Vaporeon", e:"💧🦊", info:"Anggun dan lembut seperti ombak laut."},
  {n:"Jolteon", e:"⚡🦊", info:"Cepat, energik, dan cemerlang."},
  {n:"Flareon", e:"🔥🦊", info:"Hangat, emosional, dan penuh gairah."},
  {n:"Espeon", e:"💫🐈", info:"Sensitif, spiritual, dan elegan."},
  {n:"Umbreon", e:"🌑🐈‍⬛", info:"Kalem dan misterius, tapi setia pada hati."},
  {n:"Leafeon", e:"🌿🦊", info:"Tenang, selaras dengan alam."},
  {n:"Glaceon", e:"❄️🦊", info:"Dingin di luar tapi lembut di dalam."},
  {n:"Sylveon", e:"💗🦊", info:"Cinta dan kasih menjadi kekuatannya."},
  {n:"Porygon", e:"💻🧩", info:"Logis dan unik, dunia digital adalah rumahnya."},
  {n:"Articuno", e:"❄️🦅", info:"Dingin tapi agung, simbol kedamaian abadi."},
  {n:"Zapdos", e:"⚡🦅", info:"Cepat dan menakjubkan, penuh kekuatan listrik."},
  {n:"Moltres", e:"🔥🦅", info:"Berani, flamboyan, penuh api semangat."},
  {n:"Dratini", e:"💧🐉", info:"Lembut, penuh potensi besar."},
  {n:"Dragonair", e:"🌊🐉", info:"Anggun dan berkarisma, simbol keanggunan alami."},
  {n:"Dragonite", e:"💛🐉", info:"Pelindung dan pengembara yang baik hati."},
  {n:"Chikorita", e:"🌿🌸", info:"Lucu dan cinta damai, dekat dengan alam."},
  {n:"Totodile", e:"💧🐊", info:"Ceria, bersemangat, dan senang bersenang-senang."},
  {n:"Cyndaquil", e:"🔥🦔", info:"Pemalu tapi menyala dengan semangat jika diperlukan."},
  {n:"Typhlosion", e:"🔥🔥", info:"Kuat dan berani melindungi yang lemah."},
  {n:"Feraligatr", e:"🌊🐊", info:"Tegas dan tangguh, tapi punya sisi lembut."},
  {n:"Bayleef", e:"🌿🌼", info:"Harum, manis, dan inspiratif."},
  {n:"Meganium", e:"🌿🌸", info:"Penyembuh alami dan damai di hatinya."},
  {n:"Ampharos", e:"⚡🐏", info:"Ceria, memberi cahaya di saat gelap."},
  {n:"Espeon", e:"💫🐱", info:"Intuitif, elegan, penuh misteri."},
  {n:"Umbreon", e:"🌑🐈‍⬛", info:"Setia, kalem, berjiwa malam."},
  {n:"Scizor", e:"🔴🦗", info:"Cepat, efisien, dan fokus."},
  {n:"Heracross", e:"🐞💪", info:"Tangguh dan pekerja keras."},
  {n:"Houndoom", e:"🔥🐶", info:"Berani, kuat, dan misterius."},
  {n:"Tyranitar", e:"🪨🐉", info:"Raksasa kuat dengan jiwa pemimpin."},
  {n:"Lugia", e:"🌊🕊️", info:"Penjaga samudra dan ketenangan."},
  {n:"Ho-Oh", e:"🔥🌈", info:"Simbol harapan dan kebangkitan."},
  {n:"Celebi", e:"🌿🕊️", info:"Penjaga waktu dan alam."}
];

// ------------- logic -------------
const checkBtn = document.getElementById('checkBtn');
const resetBtn = document.getElementById('resetBtn');
const nameInp = document.getElementById('name');
const ageInp = document.getElementById('age');
const dobInp = document.getElementById('dob');
const bubble = document.getElementById('resultBubble');
const aEmoji = document.getElementById('animalEmoji');
const aName = document.getElementById('animalName');
const aSub = document.getElementById('resultSub');
const chime = document.getElementById('chime');
const soundToggle = document.getElementById('soundToggle');

// ---------- fungsi bantu ----------
function hashString(str){
  // Hash ringan agar hasil tetap sama untuk input yang sama
  let h = 0;
  for(let i = 0; i < str.length; i++){
    h = Math.imul(31, h) + str.charCodeAt(i) | 0;
  }
  return Math.abs(h);
}

function showResult(item){
  aEmoji.textContent = item.e || "🐾";
  aName.textContent = item.n;
  aSub.textContent = item.info || "Sifat singkat muncul di sini.";
  bubble.classList.add('show','glow');
  bubble.setAttribute('aria-hidden','false');

  if(soundToggle.checked){
    chime.currentTime = 0;
    chime.play().catch(()=>{});
  }

  setTimeout(()=> bubble.classList.remove('glow'), 1600);
}

function hideResult(){
  bubble.classList.remove('show');
  bubble.setAttribute('aria-hidden','true');
}

// ---------- tombol utama ----------
checkBtn.addEventListener('click', ()=>{
  hideResult();

  setTimeout(()=>{
    const name = nameInp.value.trim().toLowerCase();
    const age = ageInp.value.trim();
    const dob = dobInp.value || "";
    
    // 🔢 gabungkan data untuk seed unik
    const seedStr = `${name}|${age}|${dob}`;
    const h = hashString(seedStr);
    
    // hasil deterministik
    const idx = h % ANIMALS.length;
    const item = ANIMALS[idx];
    showResult(item);
  }, 350);
});

resetBtn.addEventListener('click', ()=>{
  nameInp.value=''; ageInp.value=''; dobInp.value='';
  hideResult();
});

[nameInp, ageInp, dobInp].forEach(el=>{
  el.addEventListener('keydown',(e)=>{
    if(e.key === 'Enter'){
      e.preventDefault();
      checkBtn.click();
    }
  });
});

nameInp.focus();
</script>
</body>
</html>
