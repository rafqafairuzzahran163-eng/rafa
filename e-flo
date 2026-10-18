<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Inventaris Tanaman Adiwiyata SMAN 30 Jakarta</title>
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- React & ReactDOM CDN -->
    <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
    
    <!-- Babel CDN (for JSX) -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <!-- QRCode.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

    <!-- Google Fonts: Plus Jakarta Sans -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">

    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #F4F7F5;
        }
        .canva-shadow {
            box-shadow: 0 10px 30px -5px rgba(0, 77, 64, 0.08);
        }
        .canva-shadow-hover:hover {
            box-shadow: 0 20px 35px -10px rgba(0, 77, 64, 0.15);
            transform: translateY(-4px);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #10b981;
            border-radius: 10px;
        }
    </style>
</head>
<body class="text-slate-800 antialiased selection:bg-emerald-200 selection:text-emerald-900">
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useMemo, useRef } = React;

        // Raw plant data list (114 items)
        const INITIAL_PLANTS = [
            { id: 1, name: "Pakis rem Cina", latin: "Pteris vittata", spec: "Pakis sejati dengan ental menyirip dan anak daun sempit.", flower: "Tidak berbunga; spora tumbuh pada sori di bawah daun.", habitat: "Tropis/subtropis; celah batu, tembok dan lahan terbuka.", care: "Cahaya terang tersaring, media lembap porous; buang ental tua.", fact: "Diteliti untuk fitoremediasi arsenik; jangan dimakan.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 2, name: "Cabai", latin: "Capsicum spp.", spec: "Herba/perdu pendek; varietas pada inventaris tidak dirinci.", flower: "Bunga putih kecil, penyerbukan membentuk buah.", habitat: "Asal genus dari Amerika tropis; kini dibudidayakan luas.", care: "Matahari penuh, tanah subur porous, siram tanpa genangan.", fact: "Pedasnya bergantung spesies dan kultivar.", location: "Depan labkim; Belakang labkim; Bagian Kanan Masjid; Gang kantin; Kebun; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 3, name: "Andong / hanjuang", latin: "Cordyline fruticosa", spec: "Perdu tegak berdaun pita; kultivar merah/hijau beragam.", flower: "Bunga kecil pada malai menarik serangga.", habitat: "Asli Papuasia hingga Pasifik barat; iklim tropis lembap.", care: "Cahaya terang/matahari pagi, tanah porous lembap; pangkas daun tua.", fact: "Daunnya memiliki pemakaian budaya dan hias di Pasifik.", location: "Depan labkim; Ruang wakil (L); Mulmed (L) ; Parkiran guru; Koperasi", ref: "Kew POWO|rujukan tambahan" },
            { id: 4, name: "Lidah mertua", latin: "Dracaena trifasciata", spec: "Daun tegak seperti pedang tumbuh dari rimpang; pola bergantung kultivar.", flower: "Bunga putih kehijauan harum, jarang muncul di pot.", habitat: "Asal Afrika tropis barat-tengah; kini ditanam luas.", care: "Cahaya terang tersaring, media porous; siram setelah kering.", fact: "Nama lama Sansevieria berubah menjadi Dracaena dalam taksonomi modern.", location: "Depan labkim; Belakang labkim; Bagian Kanan Masjid; Belakang kantin; Kebun; Depan lemari piala (L); Ruang wakil (L); Depan perpus; Depan mulmed; Mulmed (L) ; Parkiran guru; Dekat air mancur; Lapangan bultang; Gerbang belakang; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 5, name: "Pepaya", latin: "Carica papaya", spec: "Herba berkayu lunak berdaun menjari besar dan buah pada batang.", flower: "Bunga jantan/betina dapat terpisah; penyerbukan membentuk buah.", habitat: "Asal Amerika tropis; kini umum di kawasan hangat.", care: "Matahari penuh, tanah dalam porous; lindungi dari angin.", fact: "Batangnya lunak dan berongga, tidak sekeras pohon berkayu.", location: "Depan labkim; Gang kantin; Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 6, name: "Resam", latin: "Dicranopteris linearis", spec: "Paku berumpun dengan daun bercabang berulang seperti garpu.", flower: "Tidak berbunga; berkembang biak dengan spora.", habitat: "Daerah tropis; lereng terbuka, tanah asam dan lahan terganggu.", care: "Cahaya terang, media lembap; batasi rimpang menjalar.", fact: "Sering menutup lahan terbuka sebagai vegetasi awal.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 7, name: "Pakis monyet", latin: "Cibotium barometz (dugaan)", spec: "Kemungkinan pakis pohon dengan ental besar dan rimpang berbulu.", flower: "Tidak berbunga; spora tumbuh di bawah daun.", habitat: "Dugaan ini hidup di hutan lembap Asia; perlu foto untuk memastikan.", care: "Teduh lembap, media kaya humus dan tidak kering.", fact: "Beberapa pakis pohon rentan dipanen berlebihan dari alam.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 8, name: "Kuping gajah", latin: "Anthurium sp.", spec: "Daun lebar berbentuk hati dengan urat menonjol.", flower: "Tongkol dan seludang khas Araceae berfungsi dalam reproduksi.", habitat: "Anthurium daun umumnya dari hutan tropis Amerika.", care: "Cahaya tersaring, media organik porous dan lembap tanpa genangan.", fact: "Tulang daun kontras menjadi ciri hias populer.", location: "Depan labkim; Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 9, name: "Adam hawa", latin: "Tradescantia spathacea", spec: "Herba roset berdaun pita tebal, sisi bawah sering ungu.", flower: "Bunga putih kecil tumbuh di dalam seludang seperti perahu.", habitat: "Asal Meksiko/Amerika Tengah; taman hangat.", care: "Teduh terang atau matahari pagi; tanah porous, siram saat atas media kering.", fact: "Nama lama Rhoeo discolor masih sering dipakai.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 10, name: "Palem umum", latin: "Arecaceae indet.", spec: "Famili palem sangat beragam; foto pelepah, batang dan buah dibutuhkan.", flower: "Bunga kecil bertandan; menghasilkan buah/biji setelah penyerbukan.", habitat: "Palem hidup dari hutan tropis sampai daerah kering.", care: "Jaga pucuk tumbuh, cocokkan cahaya dan air setelah identifikasi.", fact: "“Palem” adalah nama famili, bukan spesies tertentu.", location: "Depan labkim; Depan mulmed", ref: "Kew POWO|rujukan tambahan" },
            { id: 11, name: "Philodendron Burle Marx", latin: "Philodendron burle-marxii", spec: "Philodendron berdaun memanjang, dapat merambat/menjalar.", flower: "Bunga berupa tongkol dan seludang, jarang pada pot.", habitat: "Hutan tropis Amerika.", care: "Cahaya terang tersaring, media porous; beri rambatan dan pangkas sulur.", fact: "Nama spesies menghormati botanis lanskap Roberto Burle Marx.", location: "Depan labkim; Parkiran guru", ref: "Kew POWO|rujukan tambahan" },
            { id: 12, name: "Puring emas", latin: "Codiaeum variegatum", spec: "Perdu bergetah dengan daun tebal dan warna bercorak.", flower: "Bunga kecil tidak mencolok pada tandan.", habitat: "Asal Indo-Pasifik; taman tropis.", care: "Cahaya terang, media porous lembap; pakai sarung tangan saat memangkas.", fact: "“Emas” biasanya nama warna/kultivar, bukan spesies tersendiri.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 13, name: "Jambu biji", latin: "Psidium guajava", spec: "Pohon kecil berdaun berhadapan dan berbuah bulat/oval.", flower: "Bunga putih dengan benang sari banyak; serangga membantu penyerbukan.", habitat: "Asal Amerika tropis; kebun daerah hangat.", care: "Matahari penuh, tanah porous; siram teratur saat muda.", fact: "“Jambu” bisa merujuk beberapa jenis; cocokkan buah.", location: "Depan labkim; Bagian Kanan Masjid; Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 14, name: "Petai belalang", latin: "Leucaena leucocephala", spec: "Perdu/pohon kecil berdaun majemuk dan polong pipih.", flower: "Bunga putih krem berbentuk bonggol menarik serangga.", habitat: "Asal Meksiko-Amerika Tengah; tumbuh di kawasan tropis.", care: "Matahari penuh, tanah porous; kendalikan anakan.", fact: "Dapat cepat menyebar di sejumlah wilayah tropis.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 15, name: "Bunga kertas / bougenville", latin: "Bougainvillea spp.", spec: "Liana/perdu berduri; warna mencolok adalah braktea, bukan mahkota.", flower: "Braktea menarik serangga ke bunga sejati kecil di tengah.", habitat: "Asal Amerika Selatan; suka iklim panas dan cerah.", care: "Matahari penuh, media porous, beri rambatan dan pangkas selepas berbunga.", fact: "Dinamai dari penjelajah Louis Antoine de Bougainville.", location: "Depan labkim; Kebun; Ruang wakil (L); Depan labfis ; Depan perpus; Koperasi; Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 16, name: "Tapak dara", latin: "Catharanthus roseus", spec: "Perdu kecil berdaun mengilap dengan bunga lima mahkota.", flower: "Bunga menarik penyerbuk; putih/merah muda adalah variasi.", habitat: "Asal Madagaskar; taman hangat.", care: "Matahari penuh hingga teduh terang, tanah porous; jangan overwatering.", fact: "Senyawa alkaloidnya dipakai dalam obat farmasi.", location: "Depan labkim; Kebun; Parkiran guru; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 17, name: "Kamboja", latin: "Plumeria spp.", spec: "Pohon kecil bergetah dengan cabang tebal dan daun di ujung.", flower: "Bunga harum menarik ngengat malam.", habitat: "Asal Amerika tropis; iklim hangat dan cerah.", care: "Matahari penuh, media porous; kurangi air saat dorman.", fact: "Banyak ditanam sebagai tanaman hias dan memiliki makna budaya.", location: "Depan labkim; Dekat air mancur; Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 18, name: "Bungur kecil", latin: "Lagerstroemia indica", spec: "Perdu/pohon kecil berdaun sederhana; kulit batang bisa mengelupas.", flower: "Bunga berkelompok dengan mahkota berkerut menarik serangga.", habitat: "Asal Asia Timur; taman hangat.", care: "Matahari penuh, tanah porous; pangkas cabang lemah selepas berbunga.", fact: "Genus dinamai untuk kolektor botani Magnus von Lagerström.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 19, name: "Melati tempel", latin: "Wrightia antidysenterica", spec: "Perdu bercabang, daun berhadapan dan bunga putih kecil.", flower: "Bunga beraroma menarik serangga penyerbuk.", habitat: "Asia tropis; taman/pot besar.", care: "Cahaya terang, media porous lembap; pangkas ringan.", fact: "Universitas Nasional mencatat nama lokal “melati tempel”.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 20, name: "Lee Kwan Yew", latin: "Tarlmounia elliptica", spec: "Liana berkayu dengan sulur panjang dan daun kecil oval.", flower: "Bunga kecil putih seperti aster, dikunjungi serangga.", habitat: "Asia tropis; pagar/dinding di wilayah hangat.", care: "Cahaya terang, tanah porous; pangkas sulur secara berkala.", fact: "Nama lanskap mengacu pada bentuk tanaman yang menjuntai seperti tirai.", location: "Depan labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 21, name: "Sawo", latin: "Manilkara zapota", spec: "Pohon hijau bergetah putih, daun tebal mengilap, buah manis.", flower: "Bunga kecil pucat menjadi awal pembentukan buah.", habitat: "Asal Meksiko-Amerika Tengah; kebun tropis.", care: "Matahari penuh, tanah dalam berdrainase baik.", fact: "Getahnya dahulu digunakan untuk membuat permen karet alami.", location: "Belakang labkim; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 22, name: "Lidah buaya", latin: "Aloe vera", spec: "Sukulen roset dengan daun berdaging penyimpan air.", flower: "Bunga tabung pada tangkai menarik penyerbuk.", habitat: "Asal Semenanjung Arab; daerah hangat-kering.", care: "Cahaya terang, media kaktus porous; siram setelah kering.", fact: "Gel daun banyak digunakan dalam kosmetik.", location: "Belakang labkim; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 23, name: "Mahoni", latin: "Swietenia macrophylla", spec: "Pohon besar dengan daun majemuk dan buah kapsul kayu.", flower: "Bunga kecil; penyerbukan menghasilkan biji bersayap.", habitat: "Asal Amerika Tengah/Selatan; pohon peneduh tropis.", care: "Matahari penuh, tanah dalam; beri ruang luas.", fact: "Kayu bernilai tinggi sehingga asal dan pengelolaan lestari penting.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 24, name: "Jawer kotok", latin: "Coleus scutellarioides", spec: "Herba dengan batang bersudut dan daun berhadapan berwarna-warni.", flower: "Bunga kecil biru/putih pada malai; daun lebih mencolok.", habitat: "Asia tropis hingga Australia utara; taman hangat.", care: "Tanah gembur lembap, teduh parsial; cubit pucuk.", fact: "Stek batang mudah berakar.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 25, name: "Kalanchoe laetivirens", latin: "Kalanchoe laetivirens", spec: "Sukulen berdaun tebal bergerigi, kadang beranakan di tepi daun.", flower: "Bunga tabung kecil pada tangkai.", habitat: "Asal Madagaskar; tempat hangat dan cerah.", care: "Matahari pagi, media porous; siram setelah kering.", fact: "Anakan daun dapat menjadi cara perbanyakan vegetatif.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 26, name: "Epiphyllum umum", latin: "Epiphyllum spp.", spec: "Kaktus epifit dengan batang pipih dan tepi berlekuk.", flower: "Bunga besar sering mekar singkat dan menarik penyerbuk malam.", habitat: "Hutan tropis Amerika; menempel pada pohon/batuan.", care: "Teduh terang, media porous kaya organik; hindari terik siang.", fact: "Kaktus hutan memerlukan lebih banyak kelembapan daripada kaktus gurun.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 27, name: "Syngonium", latin: "Syngonium podophyllum", spec: "Liana dengan daun muda berbentuk panah; daun berubah saat dewasa.", flower: "Tongkol/seludang khas Araceae jarang terlihat di pot.", habitat: "Amerika Tengah/Selatan; merambat di hutan lembap.", care: "Cahaya tersaring, media porous; sediakan rambatan.", fact: "Daunnya dapat berubah dari bentuk panah menjadi berlekuk.", location: "Belakang labkim; Depan lemari piala (L); Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 28, name: "Sirsak", latin: "Annona muricata", spec: "Pohon kecil berdaun mengilap dan buah besar berduri lunak.", flower: "Bunga hijau kekuningan diserbuki serangga, termasuk kumbang.", habitat: "Karibia/Amerika tropis; kebun hangat.", care: "Matahari penuh, tanah subur porous; lindungi dari angin.", fact: "Daun/buah bukan pengganti terapi medis tanpa bukti klinis.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 29, name: "Oleander kuning", latin: "Cascabela thevetia", spec: "Perdu kecil berdaun panjang sempit dan bergetah putih.", flower: "Bunga corong kuning menarik serangga penyerbuk.", habitat: "Meksiko-Amerika Tengah; taman tropis cerah.", care: "Matahari penuh, tanah porous; seluruh tanaman beracun.", fact: "Thevetia peruviana adalah nama lama yang masih sering dipakai.", location: "Belakang labkim", ref: "Kew POWO|rujukan tambahan" },
            { id: 30, name: "Anggrek labang", latin: "Orchidaceae indet.", spec: "Inventaris hanya mencatat kelompok anggrek; perlu foto daun/akar/bunga.", flower: "Struktur bunga khusus untuk penyerbukan; rincian tergantung jenis.", habitat: "Anggrek hidup sebagai epifit, terestrial atau litofit tergantung spesies.", care: "Jangan tanam akar dalam tanah kebun; identifikasi dulu sebelum ubah perawatan.", fact: "Anggrek adalah kelompok besar, bukan spesies tunggal.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 31, name: "Sirih gading", latin: "Epipremnum aureum", spec: "Liana berdaun hati, berakar udara; corak warna bergantung kultivar.", flower: "Tongkol jarang muncul pada tanaman hias; stek batang umum untuk perbanyakan.", habitat: "Asal Pasifik barat; kini merambat luas di daerah tropis.", care: "Teduh terang, media porous; biarkan permukaan agak kering sebelum menyiram.", fact: "Daun dewasa pada sulur yang memanjat bisa jauh lebih besar.", location: "Bagian Kanan Masjid; Kebun; Ruang wakil (L); Depan Ruang wakil (D); Mulmed (L) ; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 32, name: "Paku sepat", latin: "Nephrolepis cordifolia", spec: "Paku berumpun dengan ental menyirip, rimpang dan umbi kecil.", flower: "Tidak berbunga; sori di bawah daun menghasilkan spora.", habitat: "Daerah tropis/subtropis; tanah atau tempat lembap.", care: "Teduh terang, media organik lembap tanpa genangan; batasi rimpang.", fact: "Nama lokal “paku sepat” dapat berubah antarwilayah.", location: "Bagian Kanan Masjid; Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 33, name: "Pakis hias", latin: "Paku-pakuan indet.", spec: "Jenis tidak dirinci; foto ental dan sori dibutuhkan.", flower: "Tidak berbunga; paku berkembang biak dengan spora.", habitat: "Umumnya tempat lembap dan teduh; kebutuhan tergantung jenis.", care: "Teduh terang, media porous agak lembap, hindari genangan.", fact: "Sori di balik daun bukan bunga atau biji.", location: "Bagian Kanan Masjid; Depan Ruang wakil (D)", ref: "Kew POWO|rujukan tambahan" },
            { id: 34, name: "Sri rezeki", latin: "Aglaonema spp.", spec: "Herba daun lebar dengan corak hijau, perak atau merah muda.", flower: "Bunga kecil pada tongkol berseludang; nilai hias utama ada di daun.", habitat: "Asia tropis; bawah naungan hutan lembap.", care: "Teduh terang, media organik porous; siram setelah permukaan agak kering.", fact: "“Beras tumpah” biasanya sebutan corak/kultivar.", location: "Bagian Kanan Masjid; Depan mulmed", ref: "Kew POWO|rujukan tambahan" },
            { id: 35, name: "Calathea ornata", latin: "Goeppertia ornata", spec: "Herba roset berdaun oval dengan garis merah muda saat muda.", flower: "Bunga kecil dekat pangkal, tidak mencolok.", habitat: "Kolombia/Venezuela; lantai hutan tropis lembap.", care: "Cahaya tidak langsung, media porous sedikit lembap.", fact: "Banyak Calathea dipindahkan ke genus Goeppertia.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 36, name: "Epiphyllum pumilum", latin: "Epiphyllum pumilum", spec: "Kaktus epifit berbatang pipih; identifikasi lokasi perlu foto.", flower: "Bunga Epiphyllum dapat besar/harum dan menarik penyerbuk malam.", habitat: "Hutan tropis Amerika; menempel pada pohon/batu.", care: "Teduh terang, media porous berserat; siram secukupnya.", fact: "Epifit menempel pada tumbuhan lain tanpa mengambil makanannya.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 37, name: "Peace lily", latin: "Spathiphyllum spp.", spec: "Herba berumpun dengan daun lanset hijau.", flower: "Seludang putih membingkai tongkol berisi bunga kecil.", habitat: "Amerika tropis; habitat hutan lembap.", care: "Teduh terang, media lembap merata dan berdrainase baik.", fact: "Bagian putih adalah seludang, bukan bunga sejati.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 38, name: "Lili Paris", latin: "Chlorophytum comosum", spec: "Herba roset berdaun pita melengkung dan stolon beranakan.", flower: "Bunga putih kecil pada tangkai dapat diikuti anakan.", habitat: "Afrika tropis; tanaman pot/gantung.", care: "Cahaya sedang/teduh terang, tanah porous agak lembap.", fact: "Anakan mudah diperbanyak tanpa biji.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 39, name: "Lacy tree philodendron", latin: "Thaumatophyllum bipinnatifidum", spec: "Batang kokoh dengan daun besar berlekuk dalam.", flower: "Tongkol dan seludang membantu reproduksi; jarang jadi daya hias utama.", habitat: "Amerika Selatan tropis; hangat dan lembap.", care: "Cahaya tersaring, tanah organik, beri ruang tajuk.", fact: "Nama lama Philodendron masih luas digunakan meski genusnya berubah.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 40, name: "Bakung putih", latin: "Crinum asiaticum", spec: "Herba berumbi dengan daun panjang seperti pita.", flower: "Bunga putih besar pada tangkai menarik penyerbuk.", habitat: "Asia tropis/Pasifik; taman hangat, kadang pesisir.", care: "Matahari sampai teduh terang, tanah porous; umbi jangan tergenang.", fact: "Nama bakung putih dapat menunjuk beberapa spesies; jangan konsumsi.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 41, name: "Bakung lele", latin: "Hymenocallis sp.", spec: "Tanaman berumbi berdaun pita; nama lokal tidak memastikan genus.", flower: "Sebagian Hymenocallis memiliki bunga putih seperti laba-laba.", habitat: "Amerika tropis/subtropis; taman hangat.", care: "Matahari pagi, media gembur; umbi jangan terendam.", fact: "Bakung lele juga kadang disebut untuk Crinum; foto diperlukan.", location: "Depan perpus; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 42, name: "Pandan Bali", latin: "Cordyline australis / Dracaena loureiri", spec: "Tanaman lanskap berdaun pita; pasangan nama lokal-takson berbeda.", flower: "Jika Cordyline/Dracaena, bunga kecil berkelompok pada malai.", habitat: "Keduanya tumbuh di iklim hangat, tetapi asalnya berbeda.", care: "Cahaya terang, tanah porous; jangan pangkas pucuk sebelum identifikasi.", fact: "Sumber Indonesia menyebut Cordyline australis maupun Dracaena loureiri.", location: "Bagian Kanan Masjid; Ruang wakil (L); Depan Ruang wakil (D); Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 43, name: "Terong", latin: "Solanum melongena", spec: "Herba/perdu berdaun lebar dengan buah beragam bentuk.", flower: "Bunga ungu berbentuk bintang; serangga membantu penyerbukan.", habitat: "Asal Asia Selatan; kebun sayur hangat.", care: "Matahari penuh, tanah subur porous, siram konsisten.", fact: "Kerabat tomat, kentang dan cabai dalam Solanaceae.", location: "Bagian Kanan Masjid; Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 44, name: "Bayam duri", latin: "Amaranthus spinosus", spec: "Herba tegak dengan daun oval dan sepasang duri di pangkal.", flower: "Bunga kehijauan rapat dalam bulir; angin/serangga membantu.", habitat: "Asal Amerika tropis; lahan terbuka tropis.", care: "Matahari penuh; cabut sebelum berbiji bila dianggap gulma.", fact: "Biji kecilnya banyak dan mudah tersebar.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 45, name: "Kaktus", latin: "Cactaceae indet.", spec: "Sukulen penyimpan air; bentuk batang/duri bervariasi.", flower: "Banyak kaktus berbunga besar dan menarik penyerbuk.", habitat: "Kebanyakan asal Amerika; habitat kering, kecuali kaktus hutan.", care: "Identifikasi dahulu; gurun perlu matahari, epifit lebih teduh.", fact: "Tidak semua tanaman berduri termasuk kaktus.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 46, name: "Patah tulang kriwil", latin: "Euphorbia tirucalli", spec: "Sukulen bergetah dengan ranting silindris tipis berpilin.", flower: "Bunga sangat kecil; tidak mencolok tetapi bereproduksi.", habitat: "Asal Afrika dan kawasan tropis sekitarnya.", care: "Matahari penuh, media porous; getah mengiritasi kulit/mata.", fact: "Nama merujuk batang rapuh; getah bukan obat rumahan aman.", location: "Bagian Kanan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 47, name: "Awar-awar", latin: "Ficus septica", spec: "Pohon kecil berdaun lebar, bergetah putih dan berbuah bulat.", flower: "Bunga tersembunyi di dalam sikonium; tawon ara membantu penyerbukan.", habitat: "Asia Tenggara/Pasifik barat; tepi hutan dan lahan lembap.", care: "Cahaya terang/parsial, tanah porous; beri ruang akar.", fact: "Bunga Ficus tidak tampak seperti bunga biasa.", location: "Bagian Kanan Masjid; Depan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 48, name: "Money tree", latin: "Pachira aquatica", spec: "Pohon berdaun majemuk menjari; identifikasi dari nama belum pasti.", flower: "Pohon matang dapat berbunga besar; pot jarang berbunga.", habitat: "Amerika Tengah/Selatan; habitat hangat dan lembap.", care: "Cahaya terang, media porous; siram setelah permukaan mengering.", fact: "Julukan money tree populer pada perdagangan tanaman hias.", location: "Depan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 49, name: "Srigading", latin: "Nyctanthes arbor-tristis", spec: "Perdu kecil dengan bunga putih berpusat jingga.", flower: "Bunga harum membuka malam/menjelang pagi dan menarik penyerbuk.", habitat: "Asia Selatan-Tenggara; taman tropis.", care: "Matahari/parsial, media porous; pangkas selepas berbunga.", fact: "Nama Inggrisnya night-flowering jasmine.", location: "Depan Masjid", ref: "Kew POWO|rujukan tambahan" },
            { id: 50, name: "Philodendron Lemon Lime", latin: "Philodendron hederaceum 'Lemon Lime'", spec: "Sulur berdaun hati hijau limau; warna dipengaruhi cahaya.", flower: "Tongkol/seludang jarang muncul di pot.", habitat: "Amerika tropis; merambat di hutan lembap.", care: "Cahaya terang tak langsung, media porous; stek dari ruas.", fact: "Jangan samakan dengan Dracaena kultivar Lemon Lime.", location: "Depan Masjid; Depan ruang piket lt 1; Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 51, name: "Artabotrys siamensis", latin: "Artabotrys siamensis", spec: "Liana berkayu berdaun sederhana dan cabang berkait.", flower: "Bunga kecil beraroma membantu penyerbukan serangga.", habitat: "Asia Tenggara; merambat di iklim tropis.", care: "Cahaya terang tersaring, tanah lembap porous, beri rambatan.", fact: "Termasuk keluarga Annonaceae, kerabat sirsak.", location: "Gang kantin", ref: "Kew POWO|rujukan tambahan" },
            { id: 52, name: "Pandan bertanda tanya", latin: "Pandanus sp.", spec: "Bila benar pandan, biasanya berumpun berdaun pita panjang.", flower: "Fungsi bunga/buah bergantung spesies.", habitat: "Genus Pandanus tumbuh di wilayah tropis.", care: "Tunggu identifikasi; sementara cahaya terang dan media lembap.", fact: "Tanda tanya pada inventaris dipertahankan sebagai ketidakpastian.", location: "Gang kantin", ref: "Kew POWO|rujukan tambahan" },
            { id: 53, name: "Labu / squash", latin: "Cucurbita spp.", spec: "Tanaman menjalar dengan sulur dan daun lebar menjari.", flower: "Bunga jantan/betina kuning; lebah membantu pembentukan buah.", habitat: "Asal genus dari Amerika; ditanam di kebun hangat.", care: "Matahari penuh, tanah subur lembap, beri ruang rambat.", fact: "Bunga betina memiliki bakal buah kecil di belakang mahkota.", location: "Belakang kantin", ref: "Kew POWO|rujukan tambahan" },
            { id: 54, name: "Parlor palm", latin: "Chamaedorea elegans", spec: "Palem kecil dengan daun menyirip dan batang ramping.", flower: "Bunga kecil kuning/jingga; jantan dan betina berbeda individu.", habitat: "Meksiko selatan-Amerika Tengah; bawah tajuk hutan.", care: "Teduh terang, tanah porous; biarkan agak kering.", fact: "Lebih toleran cahaya rendah daripada banyak palem.", location: "Belakang kantin", ref: "Kew POWO|rujukan tambahan" },
            { id: 55, name: "Sirih", latin: "Piper betle", spec: "Liana berdaun hati, batang beruas dan akar tambahan.", flower: "Bunga kecil pada bulir, lalu membentuk buah.", habitat: "Indo-Cina hingga Malesia; tropis lembap.", care: "Teduh terang, tanah organik lembap, beri ajir.", fact: "Bunga bulir adalah ciri keluarga Piperaceae.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 56, name: "Bamboo palm", latin: "Chamaedorea seifrizii", spec: "Palem berumpun dengan batang ramping beruas mirip bambu.", flower: "Bunga kecil pada tandan; menghasilkan buah.", habitat: "Asal Amerika Tengah; taman teduh hangat.", care: "Teduh terang, media porous; siram saat permukaan kering.", fact: "Namanya merujuk batang mirip bambu, bukan famili bambu.", location: "Kebun; Ruang wakil (L); Depan ruang musik; Mulmed (L) ; Dekat air mancur; Koperasi", ref: "Kew POWO|rujukan tambahan" },
            { id: 57, name: "Alpukat", latin: "Persea americana", spec: "Pohon dengan daun sederhana dan buah berdaging berbiji besar.", flower: "Bunga kecil kehijauan; fase jantan/betina berbeda waktu.", habitat: "Asal Meksiko-Amerika Tengah; daerah hangat.", care: "Matahari penuh, tanah dalam porous; hindari genangan.", fact: "Memiliki satu biji besar yang menempati banyak ruang buah.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 58, name: "Bunga telang", latin: "Clitoria ternatea", spec: "Liana berdaun majemuk dan bunga biru/ungu.", flower: "Bunga kupu-kupu menarik lebah dan membentuk polong.", habitat: "Asia tropis; kebun cerah hangat.", care: "Matahari penuh, tanah porous, sediakan rambatan.", fact: "Pigmen bunga berubah warna saat pH seduhan berubah.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 59, name: "Jeruk kasturi", latin: "Citrus × microcarpa", spec: "Perdu sitrus berduri berdaun harum dan berbuah kecil.", flower: "Bunga putih harum menarik lebah.", habitat: "Dibudidayakan di Asia Tenggara tropis.", care: "Matahari penuh, tanah porous, pangkas cabang kering.", fact: "Nama kasturi/calamansi dapat menunjuk jeruk berbeda.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 60, name: "Melon", latin: "Cucumis melo", spec: "Tanaman merambat berdaun lebar dan bersulur.", flower: "Bunga jantan/betina kuning; lebah membantu menghasilkan buah.", habitat: "Dibudidayakan luas di wilayah hangat.", care: "Matahari penuh, tanah subur porous, siram konsisten.", fact: "“Melon angar” mungkin ejaan/nama varietas lokal.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 61, name: "Jarak pagar", latin: "Jatropha curcas", spec: "Perdu berkayu dengan daun menjari dan buah kapsul.", flower: "Bunga kecil pada perbungaan menghasilkan buah/biji.", habitat: "Asal Amerika tropis; wilayah hangat agak kering.", care: "Matahari penuh, tanah porous; biji/getah jangan tertelan.", fact: "Minyak biji pernah diteliti sebagai bahan bakar.", location: "Kebun", ref: "Kew POWO|rujukan tambahan" },
            { id: 62, name: "Jeruk kingkit / cingkit", latin: "Triphasia trifolia", spec: "Perdu sitrus dengan daun tiga anak daun dan buah merah kecil.", flower: "Bunga putih harum menarik serangga.", habitat: "Asia Tenggara; semak/pagar tropis.", care: "Matahari terang, tanah porous; siram secukupnya.", fact: "Triphasia merujuk pada susunan tiga anak daun.", location: "Kebun; Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 63, name: "Suji / suji belut", latin: "Dracaena angustifolia", spec: "Perdu berdaun panjang sempit seperti pita.", flower: "Bunga kecil putih kehijauan pada malai.", habitat: "Asia Tenggara; kebun/hutan sekunder tropis.", care: "Teduh terang atau matahari pagi, tanah lembap porous.", fact: "Daun suji dikenal sebagai pewarna hijau makanan.", location: "Dekat air mancur; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 64, name: "Tecoma kuning", latin: "Tecoma stans", spec: "Perdu dengan daun majemuk dan bunga terompet kuning.", flower: "Bunga menarik lebah/kupu-kupu dan menghasilkan polong.", habitat: "Asal Amerika tropis/subtropis; tempat panas terbuka.", care: "Matahari penuh, pangkas dan kendalikan anakan.", fact: "Biji mudah menyebar di kawasan yang cocok.", location: "Depan lemari piala (L); Ruang wakil (L)", ref: "Kew POWO|rujukan tambahan" },
            { id: 65, name: "Tanjung", latin: "Mimusops elengi", spec: "Pohon hijau bertajuk rapat dengan daun tebal.", flower: "Bunga putih krem harum, terutama malam; menarik serangga.", habitat: "Asia Selatan-Tenggara; taman tropis.", care: "Matahari penuh/parsial, tanah dalam dan porous.", fact: "Bunga tanjung dikenal karena aroma dan rangkaian tradisional.", location: "Depan lemari piala (L)", ref: "Kew POWO|rujukan tambahan" },
            { id: 66, name: "Anggur", latin: "Vitis spp.", spec: "Liana berkayu dengan sulur, daun menjari dan tandan buah.", flower: "Bunga kecil dalam tandan; penyerbukan membentuk buah.", habitat: "Genus Vitis terutama belahan bumi utara.", care: "Matahari penuh, rambatan kuat, pangkas rutin.", fact: "Anggur telah dibudidayakan manusia selama ribuan tahun.", location: "Depan lemari piala (L)", ref: "Kew POWO|rujukan tambahan" },
            { id: 67, name: "Kembang sepatu", latin: "Hibiscus rosa-sinensis", spec: "Perdu berdaun mengilap dengan bunga besar berwarna-warni.", flower: "Bunga menarik penyerbuk dan sampel belajar struktur bunga.", habitat: "Asia tropis/hibrida budidaya; taman hangat.", care: "Matahari penuh, tanah subur lembap, pangkas selepas berbunga.", fact: "Sering dipakai sebagai contoh bunga lengkap dalam pelajaran.", location: "Ruang wakil (L); Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 68, name: "Mimba", latin: "Azadirachta indica", spec: "Pohon bertajuk lebar dengan daun majemuk bergerigi.", flower: "Bunga putih kecil harum menarik lebah, lalu membentuk buah.", habitat: "Asal anak benua India; tropis hangat.", care: "Matahari penuh, tanah porous; toleran kering setelah mapan.", fact: "Lama ditanam sebagai pohon peneduh di Asia Selatan.", location: "Ruang wakil (L)", ref: "Kew POWO|rujukan tambahan" },
            { id: 69, name: "Cemara Norfolk", latin: "Araucaria heterophylla", spec: "Konifer bertingkat simetris dengan cabang mendatar.", flower: "Tidak berbunga; membentuk kerucut reproduktif dan biji.", habitat: "Asal Pulau Norfolk di Pasifik; taman hangat.", care: "Cahaya terang, tanah porous; jangan potong pucuk utama.", fact: "Tajuk muda yang simetris membuatnya populer sebagai pohon hias.", location: "Ruang wakil (L); Mulmed (L) ; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 70, name: "Rombusa silver", latin: "Belum teridentifikasi", spec: "Nama dagang/lokal belum cukup untuk menetapkan genus/spesies.", flower: "Bentuk bunga belum dapat dinilai tanpa identifikasi.", habitat: "Habitat/sebaran belum dapat dipastikan.", care: "Foto daun, batang, bunga dan label diperlukan.", fact: "Nama jual tanaman tidak selalu konsisten dengan nama botani.", location: "Ruang wakil (L)", ref: "Kew POWO (identifikasi belum ada)|rujukan tambahan" },
            { id: 71, name: "Pucuk merah", latin: "Syzygium myrtifolium", spec: "Perdu dengan pucuk merah yang menghijau saat menua.", flower: "Bunga putih-krem kecil dikunjungi serangga.", habitat: "Asia Tenggara; taman tropis.", care: "Matahari cukup untuk warna; pangkas rutin.", fact: "Merahnya adalah daun muda, bukan bunga.", location: "Depan Ruang wakil (D); Depan labfis ; Depan mulmed; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 72, name: "Gelombang cinta", latin: "Anthurium plowmanii", spec: "Anthurium berdaun besar dengan tepi bergelombang.", flower: "Tongkol dan seludang menjalankan reproduksi.", habitat: "Amerika Selatan tropis; hutan lembap.", care: "Teduh terang, media kasar porous, jangan genangi pangkal.", fact: "Nama lokal merujuk bentuk daun.", location: "Depan Ruang wakil (D)", ref: "Kew POWO|rujukan tambahan" },
            { id: 73, name: "Karet kebo / bunga karet", latin: "Ficus elastica", spec: "Pohon berdaun tebal mengilap dan bergetah putih.", flower: "Bunga berada dalam sikonium; tawon ara menyerbuki.", habitat: "Asia Selatan-Tenggara; hutan/taman tropis.", care: "Cahaya terang tersaring, tanah porous; siram saat kering.", fact: "Getahnya pernah digunakan sebagai bahan karet.", location: "Depan Ruang wakil (D); Depan ruang piket lt 1; Parkiran guru; Koperasi; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 74, name: "Dracaena fragrans", latin: "Dracaena fragrans", spec: "Perdu tegak dengan daun pita; kultivar perlu dicocokkan.", flower: "Bunga putih kecil beraroma pada malai.", habitat: "Afrika tropis; taman teduh/ruang terang.", care: "Cahaya tersaring, media porous; hindari pot terus basah.", fact: "Catatan Janet Lind mungkin salah tulis Janet Craig.", location: "Depan labfis ", ref: "Kew POWO|rujukan tambahan" },
            { id: 75, name: "Kemoyang", latin: "Homalomena sp.", spec: "Kemungkinan Araceae dengan daun lebar berbentuk hati.", flower: "Tongkol/seludang kecil, kurang mencolok.", habitat: "Hutan tropis lembap Asia.", care: "Teduh terang, tanah organik porous dan lembap.", fact: "Kemoyang dipakai untuk beberapa spesies Homalomena.", location: "Dekat air mancur; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 76, name: "Sambang darah", latin: "Excoecaria cochinchinensis", spec: "Perdu dengan daun hijau di atas, merah-ungu di bawah.", flower: "Bunga kecil pada tandan, kurang mencolok.", habitat: "Asia Tenggara; taman tropis.", care: "Cahaya tersaring, tanah porous; hindari getah pada mata.", fact: "Sisi bawah daun merah adalah ciri hiasnya.", location: "Depan labfis ; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 77, name: "Anggur Brazil", latin: "Plinia cauliflora", spec: "Pohon kecil dengan buah ungu tumbuh langsung di batang.", flower: "Bunga putih mungil pada batang sebelum buah berkembang.", habitat: "Asal Bolivia timur/Brasil; kebun tropis.", care: "Tanah subur lembap porous; jangan biarkan akar kering.", fact: "Jabuticaba bukan anggur sejati dari genus Vitis.", location: "Depan labfis ; Depan ruang musik", ref: "Kew POWO|rujukan tambahan" },
            { id: 78, name: "Glodokan tiang", latin: "Monoon longifolium", spec: "Pohon ramping tinggi dengan cabang bertingkat dan daun sempit.", flower: "Bunga kecil kehijauan tidak mencolok.", habitat: "Asal Asia Selatan; jalur hijau tropis.", care: "Matahari penuh, sisakan jarak dari kabel/bangunan.", fact: "Nama lama Polyalthia longifolia masih sering digunakan.", location: "Depan labfis ; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 79, name: "Asoka / soka", latin: "Ixora coccinea", spec: "Perdu berdaun berhadapan dengan tandan bunga.", flower: "Bunga tabung menyediakan nektar bagi serangga.", habitat: "India hingga Asia Tenggara; taman tropis.", care: "Cahaya terang, tanah porous; pangkas selepas berbunga.", fact: "Asoka juga dapat berarti Saraca asoca, pohon berbeda.", location: "Depan perpus; Depan mulmed; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 80, name: "Ketapang biola", latin: "Ficus lyrata", spec: "Pohon/semak berdaun besar berbentuk biola.", flower: "Bunga tersembunyi dalam sikonium; tawon ara menyerbuki.", habitat: "Afrika barat tropis; ditanam di taman hangat.", care: "Cahaya terang, tanah porous, siram saat kering.", fact: "Nama fiddle-leaf fig merujuk bentuk daun.", location: "Depan ruang piket lt 1", ref: "Kew POWO|rujukan tambahan" },
            { id: 81, name: "Palem Jepang", latin: "Rhapis excelsa", spec: "Palem berumpun dengan daun kipas terbelah menjadi segmen.", flower: "Bunga kecil bertandan di antara pelepah.", habitat: "Tiongkok selatan; habitat teduh dan taman tropis.", care: "Teduh terang, tanah porous; buang pelepah tua.", fact: "Dikenal sebagai lady palm dan toleran cahaya rendah.", location: "Depan ruang piket lt 1", ref: "Kew POWO|rujukan tambahan" },
            { id: 82, name: "Paku tanduk rusa", latin: "Platycerium bifurcatum", spec: "Paku epifit dengan daun perisai dan daun fertil bercabang.", flower: "Tidak berbunga; sori menghasilkan spora.", habitat: "Australia timur/Papua; menempel pada pohon.", care: "Teduh terang, pasang pada papan/serat dan tiriskan.", fact: "Daun perisai menangkap serasah dan menahan air.", location: "Depan ruang piket lt 1", ref: "Kew POWO|rujukan tambahan" },
            { id: 83, name: "Pacar cina", latin: "Aglaia odorata", spec: "Perdu kecil dengan daun majemuk dan anak daun mengilap.", flower: "Bunga kuning kecil harum menarik serangga.", habitat: "Asia Tenggara tropis; taman/pekarangan.", care: "Matahari pagi atau terang, tanah porous.", fact: "Bunganya kecil namun aromanya kuat.", location: "Depan ruang piket lt 1", ref: "Kew POWO|rujukan tambahan" },
            { id: 84, name: "Daun katuk", latin: "Sauropus androgynus", spec: "Perdu berdaun kecil bertumpuk pada ranting.", flower: "Bunga kecil merah keunguan di ketiak daun.", habitat: "Asia Tenggara; kebun tropis lembap.", care: "Matahari atau teduh parsial, tanah subur; pangkas.", fact: "Dikenal sebagai sayuran daun.", location: "Depan mulmed", ref: "Kew POWO|rujukan tambahan" },
            { id: 85, name: "Wijaya kusuma", latin: "Epiphyllum oxypetalum", spec: "Kaktus epifit dengan batang pipih dan bunga besar.", flower: "Bunga putih harum mekar malam dan layu pagi.", habitat: "Amerika tropis; menempel pada pohon/batu di hutan.", care: "Teduh terang, media porous kaya organik.", fact: "Mekar semalam memunculkan kisah populer.", location: "Mulmed (L) ; Parkiran guru", ref: "Kew POWO|rujukan tambahan" },
            { id: 86, name: "Kiara payung", latin: "Filicium decipiens", spec: "Pohon bertajuk bulat dengan daun majemuk menyirip.", flower: "Bunga kecil kehijauan pada malai menarik serangga.", habitat: "Asia tropis; ditanam sebagai peneduh.", care: "Matahari penuh, tanah dalam; beri ruang tajuk.", fact: "Bentuk tajuk menyerupai payung.", location: "Mulmed (L) ; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 87, name: "Asparagus asparagoides", latin: "Asparagus asparagoides", spec: "Tanaman menjalar dengan batang lentur dan cladode pipih.", flower: "Bunga putih kecil menghasilkan buah beri.", habitat: "Asal Afrika timur hingga selatan.", care: "Cahaya terang, media porous; kendalikan buah/sulur.", fact: "Bagian pipih seperti daun sebenarnya batang termodifikasi.", location: "Mulmed (L) ", ref: "Kew POWO|rujukan tambahan" },
            { id: 88, name: "Ararea / aralia", latin: "Polyscias sp.", spec: "Mungkin salah tulis aralia; kelompok Polyscias punya daun majemuk.", flower: "Bunga kecil berkelompok.", habitat: "Banyak Polyscias berasal dari Asia tropis/Pasifik.", care: "Cahaya tersaring, tanah porous; siram saat mengering.", fact: "Aralia adalah nama umum untuk beberapa genus.", location: "Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 89, name: "Mengkudu", latin: "Morinda citrifolia", spec: "Pohon kecil berdaun besar dengan buah berbenjol.", flower: "Bunga kecil dalam kepala bunga berkembang jadi buah.", habitat: "Asia Tenggara-Pasifik; pesisir dan hutan sekunder.", care: "Matahari terang, tanah porous, siram saat muda.", fact: "Bau buah matang kuat dan menarik penyebar biji.", location: "Parkiran guru", ref: "Kew POWO|rujukan tambahan" },
            { id: 90, name: "Keladi katak", latin: "Drimiopsis maculata", spec: "Herba berumbi dengan daun hijau berbintik gelap.", flower: "Bunga kecil berbentuk bintang pada tangkai.", habitat: "Afrika timur/selatan; tanah agak kering.", care: "Teduh terang, media porous; kurangi air saat dorman.", fact: "Nama sinonim berbeda antarreferensi taksonomi.", location: "Parkiran guru", ref: "Kew POWO|rujukan tambahan" },
            { id: 91, name: "Kamboja Jepang", latin: "Adenium obesum", spec: "Sukulen berbatang pangkal membesar dan daun di ujung.", flower: "Bunga corong besar menarik penyerbuk.", habitat: "Afrika timur laut hingga Arabia; iklim hangat kering.", care: "Matahari penuh, media sangat porous; getah beracun.", fact: "Nama umum tidak berarti asal Jepang.", location: "Dekat air mancur; Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 92, name: "Ketapang", latin: "Terminalia catappa", spec: "Pohon besar bertingkat dengan daun lebar.", flower: "Bunga kecil kehijauan, serangga membantu penyerbukan.", habitat: "Asli Indo-Pasifik tropis; sering di pesisir/taman.", care: "Matahari penuh, tanah dalam, beri ruang tajuk.", fact: "Daunnya menunjukkan perubahan warna musiman.", location: "Depan ruang piket lt 1; Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 93, name: "Pandan suci", latin: "Pandanus amaryllifolius", spec: "Perdu berumpun berdaun pita; jika beraroma mungkin pandan wangi.", flower: "Bunga jarang terlihat pada budidaya.", habitat: "Dibudidayakan di pekarangan Asia Tenggara.", care: "Teduh parsial, tanah lembap porous; bagi anakan.", fact: "“Pandan suci” bukan nama ilmiah baku.", location: "Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 94, name: "Song of India", latin: "Dracaena reflexa", spec: "Perdu bercabang berdaun sempit rapat.", flower: "Bunga putih kehijauan kecil pada malai.", habitat: "Asal Madagaskar/pulau Samudra Hindia.", care: "Cahaya tersaring, media porous; pangkas.", fact: "Nama Song of India adalah nama dagang.", location: "Dekat air mancur", ref: "Kew POWO|rujukan tambahan" },
            { id: 95, name: "Mangga", latin: "Mangifera indica", spec: "Pohon buah dengan daun lanset dan buah berdaging.", flower: "Bunga kecil dalam malai; serangga membantu.", habitat: "Asal Asia Selatan; kini tersebar luas di tropis.", care: "Matahari penuh, tanah dalam porous; pangkas.", fact: "Dibudidayakan di Asia Selatan selama ribuan tahun.", location: "Dekat wall climbing; Ruang paskib; Lapangan bultang; Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 96, name: "Lengkuas", latin: "Alpinia galanga", spec: "Herba rimpang berbatang semu dan daun aromatik.", flower: "Bunga putih kemerahan bertandan menarik serangga.", habitat: "Asia tropis; kebun lembap dan subur.", care: "Teduh parsial, media organik lembap porous.", fact: "Rimpang menjadi bumbu penting Asia Tenggara.", location: "Koperasi", ref: "Kew POWO|rujukan tambahan" },
            { id: 97, name: "Temulawak", latin: "Curcuma zanthorrhiza", spec: "Herba berdaun lebar dengan rimpang khas.", flower: "Perbungaan berbraktea dari pangkal.", habitat: "Asli Jawa; kebun tropis lembap.", care: "Teduh parsial, tanah gembur organik.", fact: "Temulawak berasal dari Indonesia, khususnya Jawa.", location: "Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 98, name: "Hati ungu", latin: "Tradescantia pallida", spec: "Herba menjalar berdaun ungu dan batang berakar.", flower: "Bunga kecil merah muda tiga mahkota.", habitat: "Asal Meksiko; taman hangat cerah.", care: "Matahari pagi, media porous; pangkas sulur.", fact: "Stek ruas cepat tumbuh menjadi tanaman baru.", location: "Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 99, name: "Paku sarang burung", latin: "Asplenium nidus", spec: "Paku epifit berdaun utuh panjang membentuk roset.", flower: "Tidak berbunga; sori berupa garis spora di bawah daun.", habitat: "Asia tropis/Pasifik; menempel pada pohon/batu.", care: "Teduh terang, media berserat porous.", fact: "Roset dapat menangkap serasah dan kelembapan.", location: "Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 100, name: "Ciplukan", latin: "Physalis angulata", spec: "Herba kecil dengan buah beri tertutup kelopak lampion.", flower: "Bunga kuning kecil menarik penyerbuk.", habitat: "Asal Amerika tropis; lahan terbuka hangat.", care: "Matahari penuh, tanah porous.", fact: "Kelopak membungkus buah seperti lentera.", location: "Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 101, name: "Belimbing wuluh", latin: "Averrhoa bilimbi", spec: "Pohon kecil dengan daun majemuk dan buah asam.", flower: "Bunga merah muda kecil tumbuh pada batang.", habitat: "Asia Tenggara; kebun tropis lembap.", care: "Matahari penuh, tanah porous; pangkas cabang.", fact: "Lebih asam daripada belimbing manis.", location: "Lapangan bultang", ref: "Kew POWO|rujukan tambahan" },
            { id: 102, name: "Sacha inchi", latin: "Plukenetia volubilis", spec: "Liana berdaun hati dan kapsul bersayap.", flower: "Bunga jantan/betina kecil; penyerbukan membentuk biji.", habitat: "Asal Amerika Selatan tropis; perlu rambatan.", care: "Matahari penuh, media porous, beri penopang.", fact: "Dikenal sebagai Inca peanut.", location: "Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 103, name: "Bayam liar", latin: "Amaranthus spp.", spec: "Herba tegak; spesies liar sulit dibedakan tanpa foto.", flower: "Bunga kecil pada bulir; angin membantu penyerbukan.", habitat: "Banyak Amaranthus hidup di lahan terbuka hangat.", care: "Matahari penuh; identifikasi sebelum dikonsumsi.", fact: "“Bayam liar” bisa mencakup beberapa spesies.", location: "Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 104, name: "Teh Siam / teh-tehan", latin: "Acalypha siamensis", spec: "Perdu pagar berdaun kecil; perlu cocokkan foto.", flower: "Bunga kecil pada bulir ketiak daun.", habitat: "Indo-Cina hingga Sumatra; semak tropis.", care: "Matahari/parsial, tanah porous; pangkas.", fact: "Nama teh-tehan juga digunakan untuk tanaman pagar lain.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 105, name: "Kenanga Cina", latin: "Artabotrys hexapetalus", spec: "Liana berkayu dengan daun sederhana dan cabang berkait.", flower: "Bunga kuning kehijauan harum menarik serangga.", habitat: "Asia Selatan/Tenggara; merambat pada penopang.", care: "Cahaya terang, tanah lembap porous.", fact: "Disebut climbing ylang-ylang.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 106, name: "Jeruk nipis", latin: "Citrus × aurantiifolia", spec: "Pohon/perdu berduri dengan daun aromatik dan buah kecil.", flower: "Bunga putih harum dikunjungi lebah.", habitat: "Dibudidayakan di wilayah tropis.", care: "Matahari penuh, media porous, siram teratur.", fact: "Tanda × menandai asal hibrida.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 107, name: "Ceri Suriname", latin: "Eugenia uniflora", spec: "Perdu kecil berdaun mengilap beraroma dan buah berlekuk.", flower: "Bunga putih kecil menyediakan nektar.", habitat: "Asal Amerika Selatan tropis; pagar/kebun.", care: "Matahari terang, tanah porous, pangkas.", fact: "Buah matang bisa merah sampai ungu tua.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 108, name: "Melati kampung", latin: "Jasminum sambac", spec: "Perdu berdaun berhadapan dengan bunga putih.", flower: "Bunga harum menarik penyerbuk malam.", habitat: "Asia Selatan-Tenggara; taman tropis.", care: "Matahari pagi, tanah porous; pangkas.", fact: "Melati putih dikenal sebagai bunga nasional Indonesia.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 109, name: "Melinjo", latin: "Gnetum gnemon", spec: "Pohon kecil dengan daun berhadapan.", flower: "Tidak berbunga sejati; strobilus membentuk biji.", habitat: "Asia Tenggara; kebun dan hutan sekunder.", care: "Matahari/parsial, tanah subur porous.", fact: "Melinjo gymnospermae dengan daun mirip angiospermae.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 110, name: "Sereh", latin: "Cymbopogon citratus", spec: "Rumput berumpun dengan daun panjang beraroma lemon.", flower: "Bunga jarang pada budidaya.", habitat: "Asia Tenggara; kebun tropis terbuka.", care: "Matahari penuh, tanah porous; bagi rumpun.", fact: "Aroma lemon berasal dari minyak atsiri daun.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 111, name: "Insulin", latin: "Chamaecostus cuspidatus", spec: "Herba berumpun dengan daun lebar tersusun spiral.", flower: "Bunga jingga di ujung batang menarik penyerbuk.", habitat: "Dibudidayakan di daerah tropis hangat.", care: "Teduh terang/matahari pagi, tanah organik.", fact: "Julukan daun insulin bukan bukti mengganti obat.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" },
            { id: 112, name: "Beringin", latin: "Ficus benjamina", spec: "Pohon besar bertajuk lebar, cabang menjuntai.", flower: "Bunga tersembunyi dalam sikonium; tawon ara menyerbuki.", habitat: "Asia Selatan hingga Australia utara; hutan/taman.", care: "Matahari/parsial, tanah porous; jauhkan dari pondasi.", fact: "Ukuran dewasa jauh lebih besar daripada pohon pot.", location: "Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 113, name: "Pohon “lemon”", latin: "Belum teridentifikasi", spec: "Catatan bisa menunjuk jeruk lemon atau Dracaena.", flower: "Bunga belum dapat dijelaskan sebelum identifikasi.", habitat: "Habitat/sebaran tidak dapat dipastikan.", care: "Perlu foto tanaman, daun, batang, bunga.", fact: "Dicantumkan sebagai belum terverifikasi.", location: "Depan lemari piala (L)", ref: "Kew POWO (identifikasi belum ada)|rujukan tambahan" },
            { id: 114, name: "Areca palm", latin: "Dypsis lutescens", spec: "Palem berumpun dengan batang kuning-hijau.", flower: "Bunga kekuningan bertandan di bawah daun.", habitat: "Asal Madagaskar; taman tropis terang.", care: "Cahaya tersaring, media porous lembap.", fact: "Nama ilmiahnya pernah berpindah genus.", location: "Gerbang belakang", ref: "Kew POWO|rujukan tambahan" },
            { id: 115, name: "Philodendron umum", latin: "Philodendron sp.", spec: "Catatan hanya mencatat genus; bentuk daun perlu foto.", flower: "Bunga tongkol khas Araceae, jarang pada hiasan.", habitat: "Genus ini berasal dari hutan tropis Amerika.", care: "Cahaya terang tersaring, media porous.", fact: "Philodendron mencakup banyak jenis rambat/tegak.", location: "Depan lab Biologi & sekitaran", ref: "Kew POWO|rujukan tambahan" }
        ];

        // Placeholder Unsplash Stock Images
        const STOCK_IMAGES = [
            "https://images.unsplash.com/photo-1512428559087-560fa5ceab42?auto=format&fit=crop&q=80&w=600",
            "https://images.unsplash.com/photo-1545241047-6083a3684587?auto=format&fit=crop&q=80&w=600",
            "https://images.unsplash.com/photo-1463936575829-25148e1db1b8?auto=format&fit=crop&q=80&w=600",
            "https://images.unsplash.com/photo-1509316975850-ff9c5deb0cd9?auto=format&fit=crop&q=80&w=600",
            "https://images.unsplash.com/photo-1518531933037-91b2f5f229cc?auto=format&fit=crop&q=80&w=600"
        ];

        function App() {
            const [plants, setPlants] = useState([]);
            const [search, setSearch] = useState("");
            const [selectedLocation, setSelectedLocation] = useState("Semua");
            const [selectedPlant, setSelectedPlant] = useState(null);
            const [qrPlant, setQrPlant] = useState(null);
            const [customImages, setCustomImages] = useState({});

            // Initialize icons and local data
            useEffect(() => {
                const savedImages = localStorage.getItem("sman30_plant_images");
                if (savedImages) {
                    try {
                        setCustomImages(JSON.parse(savedImages));
                    } catch (e) {
                        console.error("Failed to parse custom images", e);
                    }
                }
                setPlants(INITIAL_PLANTS);
            }, []);

            useEffect(() => {
                if (window.lucide) {
                    window.lucide.createIcons();
                }
            });

            // Extract all unique locations
            const locations = useMemo(() => {
                const setLoc = new Set();
                INITIAL_PLANTS.forEach(p => {
                    const locs = p.location.split(";").map(s => s.trim());
                    locs.forEach(l => {
                        if (l) setLoc.add(l);
                    });
                });
                return ["Semua", ...Array.from(setLoc).sort()];
            }, []);

            // Filter plants by location & search
            const filteredPlants = useMemo(() => {
                return plants.filter(plant => {
                    const matchesSearch = plant.name.toLowerCase().includes(search.toLowerCase()) ||
                        plant.latin.toLowerCase().includes(search.toLowerCase()) ||
                        plant.spec.toLowerCase().includes(search.toLowerCase());

                    const matchesLocation = selectedLocation === "Semua" ||
                        plant.location.split(";").map(s => s.trim()).includes(selectedLocation);

                    return matchesSearch && matchesLocation;
                });
            }, [plants, search, selectedLocation]);

            // Handle custom image upload
            const handleImageUpload = (plantId, file) => {
                if (!file) return;
                const reader = new FileReader();
                reader.onloadend = () => {
                    const base64Image = reader.result;
                    const updated = { ...customImages, [plantId]: base64Image };
                    setCustomImages(updated);
                    localStorage.setItem("sman30_plant_images", JSON.stringify(updated));
                };
                reader.readAsDataURL(file);
            };

            const handleResetImage = (plantId) => {
                const updated = { ...customImages };
                delete updated[plantId];
                setCustomImages(updated);
                localStorage.setItem("sman30_plant_images", JSON.stringify(updated));
            };

            const getPlantImage = (id) => {
                if (customImages[id]) return customImages[id];
                return STOCK_IMAGES[id % STOCK_IMAGES.length];
            };

            // Keyboard shortcut Escape to close modals
            useEffect(() => {
                const handleKeyDown = (e) => {
                    if (e.key === "Escape") {
                        setSelectedPlant(null);
                        setQrPlant(null);
                    }
                };
                window.addEventListener("keydown", handleKeyDown);
                return () => window.removeEventListener("keydown", handleKeyDown);
            }, []);

            return (
                <div class="min-h-screen flex flex-col pb-16">
                    {/* Header Banner - Canva Style */}
                    <header class="bg-gradient-to-r from-emerald-800 via-teal-700 to-emerald-600 text-white pt-10 pb-16 px-4 relative overflow-hidden shadow-lg">
                        <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-emerald-400/20 rounded-full blur-3xl pointer-events-none"></div>
                        <div class="absolute left-10 top-0 w-40 h-40 bg-teal-300/10 rounded-full blur-2xl pointer-events-none"></div>

                        <div class="max-w-7xl mx-auto text-center relative z-10">
                            <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-emerald-500/30 backdrop-blur-md text-emerald-100 text-xs font-semibold tracking-wide uppercase mb-4 border border-emerald-400/30">
                                <i data-lucide="leaf" class="w-4 h-4 text-emerald-300"></i> SMAN 30 JAKARTA • PROGRAM ADIWIYATA
                            </div>
                            <h1 class="text-3xl md:text-5xl font-extrabold tracking-tight mb-3">
                                Katalog Inventaris Tanaman
                            </h1>
                            <p class="text-emerald-100/90 text-sm md:text-base max-w-2xl mx-auto font-normal leading-relaxed">
                                Jelajahi keanekaragaman hayati dan dokumentasi spesifikasi botani resmi lingkungan SMAN 30 Jakarta.
                            </p>

                            {/* Quick Stats Bar */}
                            <div class="mt-8 inline-flex flex-wrap justify-center gap-4 bg-white/10 backdrop-blur-md p-2 rounded-2xl border border-white/15 text-xs md:text-sm">
                                <div class="px-4 py-2 rounded-xl bg-white/10 flex items-center gap-2">
                                    <i data-lucide="sprout" class="w-4 h-4 text-emerald-300"></i>
                                    <span>Total Terdata: <strong>114 Jenis</strong></span>
                                </div>
                                <div class="px-4 py-2 rounded-xl bg-white/10 flex items-center gap-2">
                                    <i data-lucide="map-pin" class="w-4 h-4 text-teal-300"></i>
                                    <span>Lokasi: <strong>{locations.length - 1} Area</strong></span>
                                </div>
                                <div class="px-4 py-2 rounded-xl bg-white/10 flex items-center gap-2">
                                    <i data-lucide="qr-code" class="w-4 h-4 text-emerald-300"></i>
                                    <span>Sistem QR Code Integrasi</span>
                                </div>
                            </div>
                        </div>
                    </header>

                    {/* Filter & Search Bar Floating */}
                    <main class="max-w-7xl mx-auto px-4 -mt-8 w-full flex-grow relative z-20">
                        <div class="bg-white rounded-3xl p-4 md:p-6 canva-shadow border border-emerald-100/50 mb-10">
                            <div class="flex flex-col md:flex-row gap-4 items-center justify-between">
                                {/* Search Input */}
                                <div class="relative w-full md:w-1/2">
                                    <i data-lucide="search" class="w-5 h-5 absolute left-4 top-1/2 -translate-y-1/2 text-slate-400"></i>
                                    <input 
                                        type="text" 
                                        placeholder="Cari nama umum, ilmiah, atau spesifikasi..." 
                                        value={search}
                                        onChange={(e) => setSearch(e.target.value)}
                                        class="w-full pl-12 pr-4 py-3 bg-slate-50 rounded-2xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white text-sm transition-all"
                                    />
                                    {search && (
                                        <button onClick={() => setSearch("")} class="absolute right-4 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600">
                                            <i data-lucide="x-circle" class="w-4 h-4"></i>
                                        </button>
                                    )}
                                </div>

                                {/* Location Select Filter */}
                                <div class="relative w-full md:w-1/2 flex items-center gap-2">
                                    <i data-lucide="filter" class="w-5 h-5 text-emerald-600 hidden md:block"></i>
                                    <select 
                                        value={selectedLocation} 
                                        onChange={(e) => setSelectedLocation(e.target.value)}
                                        class="w-full py-3 px-4 bg-slate-50 rounded-2xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white text-sm font-medium text-slate-700 transition-all cursor-pointer"
                                    >
                                        <option value="Semua">🔍 Semua Area Sekolah ({INITIAL_PLANTS.length})</option>
                                        {locations.filter(l => l !== "Semua").map((loc, idx) => (
                                            <option key={idx} value={loc}>📍 {loc}</option>
                                        ))}
                                    </select>
                                </div>
                            </div>

                            {/* Active Filter Chips */}
                            <div class="mt-4 pt-3 border-t border-slate-100 flex flex-wrap items-center justify-between gap-2 text-xs text-slate-500">
                                <div>
                                    Menampilkan <strong class="text-emerald-700">{filteredPlants.length}</strong> dari {plants.length} jenis tanaman
                                </div>
                                {selectedLocation !== "Semua" && (
                                    <button 
                                        onClick={() => setSelectedLocation("Semua")} 
                                        class="text-emerald-600 font-semibold hover:underline flex items-center gap-1"
                                    >
                                        <i data-lucide="rotate-ccw" class="w-3 h-3"></i> Reset Filter Area
                                    </button>
                                )}
                            </div>
                        </div>

                        {/* Plant Grid Cards */}
                        {filteredPlants.length === 0 ? (
                            <div class="bg-white rounded-3xl p-12 text-center canva-shadow border border-dashed border-slate-300">
                                <div class="w-16 h-16 bg-emerald-50 rounded-full flex items-center justify-center mx-auto mb-4 text-emerald-600">
                                    <i data-lucide="search-x" class="w-8 h-8"></i>
                                </div>
                                <h3 class="text-lg font-bold text-slate-800 mb-1">Tanaman tidak ditemukan</h3>
                                <p class="text-slate-500 text-sm max-w-md mx-auto mb-6">
                                    Tidak ada hasil yang cocok dengan kata kunci "{search}" di lokasi "{selectedLocation}".
                                </p>
                                <button 
                                    onClick={() => { setSearch(""); setSelectedLocation("Semua"); }}
                                    class="px-5 py-2.5 bg-emerald-600 text-white rounded-xl font-medium text-sm hover:bg-emerald-700 transition-all shadow-md shadow-emerald-600/20"
                                >
                                    Tampilkan Semua Tanaman
                                </button>
                            </div>
                        ) : (
                            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                                {filteredPlants.map((plant) => (
                                    <PlantCard 
                                        key={plant.id} 
                                        plant={plant} 
                                        imageUrl={getPlantImage(plant.id)}
                                        hasCustomImage={!!customImages[plant.id]}
                                        onSelect={() => setSelectedPlant(plant)}
                                        onOpenQr={() => setQrPlant(plant)}
                                        onUploadImage={(file) => handleImageUpload(plant.id, file)}
                                    />
                                ))}
                            </div>
                        )}
                    </main>

                    {/* Footer */}
                    <footer class="mt-20 border-t border-slate-200 bg-white py-8 text-center text-xs text-slate-500">
                        <div class="max-w-7xl mx-auto px-4 flex flex-col md:flex-row items-center justify-between gap-4">
                            <div class="flex items-center gap-2 font-semibold text-slate-700">
                                <span class="w-6 h-6 rounded-lg bg-emerald-600 text-white flex items-center justify-center font-bold text-xs">30</span>
                                Tim Adiwiyata & KIR SMAN 30 Jakarta
                            </div>
                            <p>© 2026 Inventaris Digital Tanaman Sekolah. Hak Cipta Dilindungi.</p>
                        </div>
                    </footer>

                    {/* Modal Detail Infografis Canva Style */}
                    {selectedPlant && (
                        <PlantDetailModal 
                            plant={selectedPlant} 
                            imageUrl={getPlantImage(selectedPlant.id)}
                            hasCustomImage={!!customImages[selectedPlant.id]}
                            onClose={() => setSelectedPlant(null)}
                            onOpenQr={() => { const p = selectedPlant; setSelectedPlant(null); setQrPlant(p); }}
                            onUploadImage={(file) => handleImageUpload(selectedPlant.id, file)}
                            onResetImage={() => handleResetImage(selectedPlant.id)}
                        />
                    )}

                    {/* Modal Kode QR */}
                    {qrPlant && (
                        <QrCodeModal 
                            plant={qrPlant} 
                            onClose={() => setQrPlant(null)}
                        />
                    )}
                </div>
            );
        }

        // Single Plant Card Component
        function PlantCard({ plant, imageUrl, hasCustomImage, onSelect, onOpenQr, onUploadImage }) {
            const fileInputRef = useRef(null);

            const handleFileChange = (e) => {
                const file = e.target.files[0];
                if (file) {
                    onUploadImage(file);
                }
            };

            return (
                <div class="bg-white rounded-3xl overflow-hidden canva-shadow canva-shadow-hover transition-all duration-300 flex flex-col border border-slate-100 group">
                    {/* Image Area */}
                    <div class="relative h-56 bg-slate-100 overflow-hidden">
                        <img 
                            src={imageUrl} 
                            alt={plant.name} 
                            class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                            loading="lazy"
                        />
                        <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-black/10"></div>

                        {/* Location Tag Badge */}
                        <div class="absolute top-3 left-3 right-12 flex flex-wrap gap-1">
                            <span class="px-3 py-1 bg-white/90 backdrop-blur-md rounded-full text-[11px] font-bold text-emerald-800 shadow-sm truncate max-w-full">
                                📍 {plant.location.split(";")[0]}
                            </span>
                        </div>

                        {/* QR Code Quick Button */}
                        <button 
                            onClick={onOpenQr}
                            title="Tampilkan Kode QR"
                            class="absolute top-3 right-3 w-9 h-9 bg-white/90 backdrop-blur-md rounded-full flex items-center justify-center text-slate-700 hover:text-emerald-600 hover:bg-white shadow-sm transition-all"
                        >
                            <i data-lucide="qr-code" class="w-4 h-4"></i>
                        </button>

                        {/* CLEAR GANTI FOTO BUTTON ON CARD */}
                        <button 
                            onClick={(e) => {
                                e.stopPropagation();
                                fileInputRef.current?.click();
                            }}
                            class="absolute bottom-3 right-3 px-3 py-1.5 bg-white/95 backdrop-blur-md hover:bg-white text-slate-800 rounded-full text-xs font-semibold shadow-md flex items-center gap-1.5 hover:text-emerald-700 transition-all border border-emerald-100"
                        >
                            <i data-lucide="camera" class="w-3.5 h-3.5 text-emerald-600"></i>
                            <span>{hasCustomImage ? "Ubah Foto" : "Ganti Foto"}</span>
                        </button>
                        <input 
                            type="file" 
                            ref={fileInputRef} 
                            onChange={handleFileChange} 
                            accept="image/*" 
                            class="hidden" 
                        />

                        {/* Plant Names Over Image */}
                        <div class="absolute bottom-3 left-3 right-28 text-white">
                            <h3 class="font-extrabold text-base leading-tight drop-shadow-sm truncate">{plant.name}</h3>
                            <p class="text-xs text-emerald-200 italic font-light truncate">{plant.latin}</p>
                        </div>
                    </div>

                    {/* Card Body */}
                    <div class="p-5 flex-grow flex flex-col justify-between">
                        <p class="text-xs text-slate-600 line-clamp-3 leading-relaxed mb-4">
                            {plant.spec}
                        </p>

                        <div class="pt-3 border-t border-slate-100 flex items-center justify-between gap-2">
                            <span class="text-[11px] text-slate-400 font-medium">
                                SMAN30-PLANT-#{String(plant.id).padStart(3, '0')}
                            </span>
                            <button 
                                onClick={onSelect}
                                class="px-4 py-2 bg-emerald-50 hover:bg-emerald-100 text-emerald-700 rounded-xl font-bold text-xs transition-colors flex items-center gap-1"
                            >
                                Detail Infografis <i data-lucide="chevron-right" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                    </div>
                </div>
            );
        }

        // Modal Detail Infografis (Canva Style)
        function PlantDetailModal({ plant, imageUrl, hasCustomImage, onClose, onOpenQr, onUploadImage, onResetImage }) {
            const fileInputRef = useRef(null);

            const handleFileChange = (e) => {
                const file = e.target.files[0];
                if (file) {
                    onUploadImage(file);
                }
            };

            return (
                <div 
                    onClick={onClose} 
                    class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 overflow-y-auto animate-fadeIn"
                >
                    <div 
                        onClick={(e) => e.stopPropagation()} 
                        class="bg-white w-full max-w-3xl rounded-3xl shadow-2xl overflow-hidden my-8 relative flex flex-col max-h-[90vh]"
                    >
                        {/* Modal Header */}
                        <div class="relative h-64 md:h-80 bg-slate-800 flex-shrink-0">
                            <img src={imageUrl} alt={plant.name} class="w-full h-full object-cover" />
                            <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-slate-900/40 to-transparent"></div>

                            {/* Close Button 'X' */}
                            <button 
                                onClick={onClose}
                                class="absolute top-4 right-4 w-10 h-10 bg-black/40 hover:bg-black/70 text-white rounded-full flex items-center justify-center backdrop-blur-md transition-all z-10"
                            >
                                <i data-lucide="x" class="w-5 h-5"></i>
                            </button>

                            {/* Upload / Reset Photo Controls */}
                            <div class="absolute top-4 left-4 flex gap-2">
                                <button 
                                    onClick={() => fileInputRef.current?.click()}
                                    class="px-3.5 py-2 bg-white/90 hover:bg-white text-slate-800 rounded-full text-xs font-bold shadow-lg flex items-center gap-1.5 transition-all"
                                >
                                    <i data-lucide="camera" class="w-4 h-4 text-emerald-600"></i>
                                    <span>Ganti Foto Lapangan</span>
                                </button>
                                {hasCustomImage && (
                                    <button 
                                        onClick={onResetImage}
                                        title="Kembalikan ke foto bawaan"
                                        class="px-3 py-2 bg-red-500/80 hover:bg-red-600 text-white rounded-full text-xs font-bold shadow-lg transition-all"
                                    >
                                        <i data-lucide="rotate-ccw" class="w-3.5 h-3.5"></i>
                                    </button>
                                )}
                                <input 
                                    type="file" 
                                    ref={fileInputRef} 
                                    onChange={handleFileChange} 
                                    accept="image/*" 
                                    class="hidden" 
                                />
                            </div>

                            {/* Header Titles */}
                            <div class="absolute bottom-6 left-6 right-6 text-white">
                                <div class="inline-block px-3 py-1 bg-emerald-500 text-white rounded-full text-xs font-bold mb-2">
                                    SMAN30-PLANT-#{String(plant.id).padStart(3, '0')}
                                </div>
                                <h2 class="text-2xl md:text-4xl font-black">{plant.name}</h2>
                                <p class="text-emerald-300 italic text-sm md:text-base font-light">{plant.latin}</p>
                            </div>
                        </div>

                        {/* Modal Body Content */}
                        <div class="p-6 md:p-8 overflow-y-auto custom-scrollbar space-y-6 text-slate-700">
                            
                            {/* Infographic Grid */}
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <div class="bg-emerald-50/60 p-4 rounded-2xl border border-emerald-100">
                                    <div class="flex items-center gap-2 text-emerald-800 font-bold text-xs uppercase tracking-wider mb-1">
                                        <i data-lucide="info" class="w-4 h-4 text-emerald-600"></i> Spesifikasi & Ciri
                                    </div>
                                    <p class="text-sm text-slate-700 leading-relaxed">{plant.spec}</p>
                                </div>

                                <div class="bg-teal-50/60 p-4 rounded-2xl border border-teal-100">
                                    <div class="flex items-center gap-2 text-teal-800 font-bold text-xs uppercase tracking-wider mb-1">
                                        <i data-lucide="flower-2" class="w-4 h-4 text-teal-600"></i> Fungsi & Bunga
                                    </div>
                                    <p class="text-sm text-slate-700 leading-relaxed">{plant.flower}</p>
                                </div>

                                <div class="bg-amber-50/60 p-4 rounded-2xl border border-amber-100">
                                    <div class="flex items-center gap-2 text-amber-800 font-bold text-xs uppercase tracking-wider mb-1">
                                        <i data-lucide="sun" class="w-4 h-4 text-amber-600"></i> Cara Perawatan
                                    </div>
                                    <p class="text-sm text-slate-700 leading-relaxed">{plant.care}</p>
                                </div>

                                <div class="bg-blue-50/60 p-4 rounded-2xl border border-blue-100">
                                    <div class="flex items-center gap-2 text-blue-800 font-bold text-xs uppercase tracking-wider mb-1">
                                        <i data-lucide="globe" class="w-4 h-4 text-blue-600"></i> Habitat & Sebaran
                                    </div>
                                    <p class="text-sm text-slate-700 leading-relaxed">{plant.habitat}</p>
                                </div>
                            </div>

                            {/* Fact & History */}
                            <div class="bg-purple-50/60 p-5 rounded-2xl border border-purple-100">
                                <div class="flex items-center gap-2 text-purple-800 font-bold text-xs uppercase tracking-wider mb-1">
                                    <i data-lucide="sparkles" class="w-4 h-4 text-purple-600"></i> Fakta Unik & Sejarah
                                </div>
                                <p class="text-sm text-slate-700 leading-relaxed">{plant.fact}</p>
                            </div>

                            {/* Location List */}
                            <div>
                                <h4 class="font-bold text-slate-800 text-sm mb-2 flex items-center gap-1.5">
                                    <i data-lucide="map-pin" class="w-4 h-4 text-emerald-600"></i> Titik Lokasi Inventaris SMAN 30:
                                </h4>
                                <div class="flex flex-wrap gap-2">
                                    {plant.location.split(";").map((loc, i) => (
                                        <span key={i} class="px-3 py-1 bg-slate-100 text-slate-700 font-medium rounded-xl text-xs border border-slate-200">
                                            📍 {loc.trim()}
                                        </span>
                                    ))}
                                </div>
                            </div>

                            {/* References */}
                            <div class="pt-4 border-t border-slate-100 text-xs text-slate-400 flex justify-between items-center">
                                <span>Rujukan Data: {plant.ref}</span>
                            </div>
                        </div>

                        {/* Modal Footer */}
                        <div class="p-4 bg-slate-50 border-t border-slate-100 flex items-center justify-between gap-3 flex-shrink-0">
                            <button 
                                onClick={onOpenQr}
                                class="px-4 py-2.5 bg-emerald-100 hover:bg-emerald-200 text-emerald-800 rounded-xl font-bold text-xs transition-colors flex items-center gap-2"
                            >
                                <i data-lucide="qr-code" class="w-4 h-4"></i> Lihat Kode QR Cetak
                            </button>

                            <button 
                                onClick={onClose}
                                class="px-6 py-2.5 bg-slate-800 hover:bg-slate-900 text-white rounded-xl font-bold text-xs transition-colors"
                            >
                                Tutup
                            </button>
                        </div>
                    </div>
                </div>
            );
        }

        // Modal QR Code Generator
        function QrCodeModal({ plant, onClose }) {
            const qrRef = useRef(null);

            useEffect(() => {
                if (qrRef.current) {
                    qrRef.current.innerHTML = "";
                    const qrUrl = `${window.location.origin}${window.location.pathname}?id=${plant.id}`;
                    new QRCode(qrRef.current, {
                        text: qrUrl,
                        width: 180,
                        height: 180,
                        colorDark: "#065f46",
                        colorLight: "#ffffff",
                        correctLevel: QRCode.CorrectLevel.H
                    });
                }
            }, [plant]);

            return (
                <div 
                    onClick={onClose} 
                    class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 animate-fadeIn"
                >
                    <div 
                        onClick={(e) => e.stopPropagation()} 
                        class="bg-white w-full max-w-sm rounded-3xl p-6 shadow-2xl text-center relative border border-emerald-100"
                    >
                        <button 
                            onClick={onClose}
                            class="absolute top-4 right-4 w-8 h-8 bg-slate-100 hover:bg-slate-200 text-slate-600 rounded-full flex items-center justify-center transition-colors"
                        >
                            <i data-lucide="x" class="w-4 h-4"></i>
                        </button>

                        <div class="inline-flex p-3 rounded-2xl bg-emerald-50 text-emerald-600 mb-3">
                            <i data-lucide="qr-code" class="w-8 h-8"></i>
                        </div>

                        <h3 class="font-bold text-slate-800 text-lg">{plant.name}</h3>
                        <p class="text-xs text-slate-500 italic mb-4">{plant.latin}</p>

                        {/* QR Code Container */}
                        <div class="bg-emerald-50/50 p-4 rounded-2xl border border-emerald-100 inline-block mb-4">
                            <div ref={qrRef} class="flex justify-center"></div>
                        </div>

                        <p class="text-[11px] text-slate-400 mb-6">
                            Pindai kode ini dengan kamera HP untuk langsung membuka spesifikasi tanaman di lapangan SMAN 30.
                        </p>

                        <div class="flex gap-2">
                            <button 
                                onClick={() => window.print()} 
                                class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white rounded-xl font-bold text-xs transition-colors flex items-center justify-center gap-1.5 shadow-md shadow-emerald-600/20"
                            >
                                <i data-lucide="printer" class="w-4 h-4"></i> Cetak QR
                            </button>
                            <button 
                                onClick={onClose} 
                                class="w-full py-2.5 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl font-bold text-xs transition-colors"
                            >
                                Tutup
                            </button>
                        </div>
                    </div>
                </div>
            );
        }

        // Render App
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
