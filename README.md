<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LKS Online Sejarah - SMKN 1 Simpang Hulu</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        history: {
                            50: '#fdf8f6',
                            100: '#f2e8e5',
                            500: '#8c4327',
                            600: '#73331b',
                            700: '#5c2613',
                            800: '#471d0e',
                            900: '#301308',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        @media print {
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            body { background: white !important; color: black !important; }
            .card-box { border: 1px solid #ccc !important; box-shadow: none !important; }
        }
        .print-only { display: none; }
        .gradient-bg {
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 40%, #451a03 100%);
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col antialiased selection:bg-amber-200 selection:text-amber-900">

    <!-- Top Header / Banner -->
    <header class="gradient-bg text-white shadow-lg no-print sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
            <div class="flex items-center space-x-3">
                <div class="p-3 bg-amber-500/20 backdrop-blur-md rounded-2xl border border-amber-400/30 text-amber-300">
                    <i class="fa-solid fa-compass-drafting text-2xl"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <span class="bg-amber-500/20 text-amber-300 text-xs font-semibold px-2.5 py-0.5 rounded-full border border-amber-400/30">Kurikulum Merdeka</span>
                        <span class="bg-indigo-500/20 text-indigo-300 text-xs font-semibold px-2.5 py-0.5 rounded-full border border-indigo-400/30">SMKN 1 SIMPANG HULU</span>
                    </div>
                    <h1 class="text-xl md:text-2xl font-bold tracking-tight mt-0.5">LKS Online Sejarah Interaktif</h1>
                    <p class="text-xs text-slate-300">Pengantar Ilmu Sejarah, Penelitian, Praaksara & Jalur Rempah Nusantara</p>
                </div>
            </div>

            <div class="flex items-center space-x-2 text-xs md:text-sm">
                <div class="bg-white/10 backdrop-blur-md px-3 py-1.5 rounded-xl border border-white/10 flex items-center gap-2">
                    <i class="fa-solid fa-clock text-amber-400"></i>
                    <span id="timer-display">Waktu: 00:00</span>
                </div>
                <button onclick="showResetModal()" class="bg-rose-500/80 hover:bg-rose-600 text-white px-3 py-1.5 rounded-xl font-medium transition shadow flex items-center gap-1.5">
                    <i class="fa-solid fa-rotate-left"></i> Reset Data
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-6xl mx-auto px-4 py-6 flex-grow w-full">

        <!-- Student Identity Card -->
        <section class="bg-white rounded-2xl shadow-sm border border-slate-200 p-5 mb-6 no-print">
            <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                <div class="flex items-center gap-2 text-slate-800 font-bold text-lg">
                    <i class="fa-solid fa-id-card text-amber-600"></i>
                    <h2>Identitas Peserta Didik / Kelompok</h2>
                </div>
                <span class="text-xs bg-emerald-50 text-emerald-700 px-2.5 py-1 rounded-lg border border-emerald-200 font-medium flex items-center gap-1">
                    <i class="fa-solid fa-circle-check"></i> Terverifikasi SMKN 1 Simpang Hulu
                </span>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                <div class="md:col-span-2">
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nama Siswa / Anggota Kelompok <span class="text-rose-500">*</span></label>
                    <input type="text" id="student-name" oninput="saveIdentity()" placeholder="Nama Siswa..." class="w-full px-3 py-2 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-amber-500 text-sm font-medium">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Kelas <span class="text-rose-500">*</span></label>
                    <input type="text" id="student-class" oninput="saveIdentity()" placeholder="Contoh: XI" class="w-full px-3 py-2 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-amber-500 text-sm font-medium">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">No. Absen</label>
                    <input type="text" id="student-absent" oninput="saveIdentity()" placeholder="Contoh: 2, 1, 2, 3, 4, 5" class="w-full px-3 py-2 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-amber-500 text-sm font-medium">
                </div>
                <div class="md:col-span-4">
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Nama Sekolah</label>
                    <input type="text" id="student-school" oninput="saveIdentity()" placeholder="SMKN 1 SIMPANG HULU" class="w-full px-3 py-2 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-amber-500 text-sm font-medium bg-slate-50">
                </div>
            </div>
        </section>

        <!-- Tab Navigation -->
        <div class="flex overflow-x-auto gap-2 border-b border-slate-200 pb-2 mb-6 no-print scrollbar-none">
            <button onclick="switchTab('tab-materi')" id="btn-tab-materi" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-amber-600 text-white shadow-sm">
                <i class="fa-solid fa-book-open"></i> Rangkuman Materi
            </button>
            <button onclick="switchTab('tab-pg')" id="btn-tab-pg" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-slate-100 text-slate-600 hover:bg-slate-200">
                <i class="fa-solid fa-list-check"></i> Aktv 1: Pilihan Ganda
            </button>
            <button onclick="switchTab('tab-match')" id="btn-tab-match" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-slate-100 text-slate-600 hover:bg-slate-200">
                <i class="fa-solid fa-puzzle-piece"></i> Aktv 2: Menjodohkan
            </button>
            <button onclick="switchTab('tab-timeline')" id="btn-tab-timeline" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-slate-100 text-slate-600 hover:bg-slate-200">
                <i class="fa-solid fa-timeline"></i> Aktv 3: Kronologi
            </button>
            <button onclick="switchTab('tab-essay')" id="btn-tab-essay" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-slate-100 text-slate-600 hover:bg-slate-200">
                <i class="fa-solid fa-pen-nib"></i> Aktv 4: Analisis Sumber
            </button>
            <button onclick="switchTab('tab-report')" id="btn-tab-report" class="tab-btn px-4 py-2.5 rounded-xl font-semibold text-sm whitespace-nowrap transition flex items-center gap-2 bg-slate-100 text-slate-600 hover:bg-slate-200">
                <i class="fa-solid fa-square-poll-vertical"></i> Raport & Nilai
            </button>
        </div>

        <!-- TAB 1: RANGKUMAN MATERI -->
        <div id="tab-materi" class="tab-content block space-y-6">
            <div class="bg-gradient-to-r from-amber-50 to-orange-50 border border-amber-200 rounded-2xl p-5 text-amber-900">
                <div class="flex items-center gap-2 text-lg font-bold mb-2">
                    <i class="fa-solid fa-bullseye text-amber-700"></i>
                    <h3>Capaian Pembelajaran (CP) Sejarah Kurikulum Merdeka</h3>
                </div>
                <p class="text-sm leading-relaxed text-amber-800">
                    Peserta didik mampu memahami konsep dasar ilmu sejarah (manusia, ruang, waktu, diakronis, sinkronis), menganalisis 4 tahapan penelitian sejarah, memahami corak kehidupan manusia masa praaksara, serta merekonstruksi **Jalur Rempah Nusantara** sebagai poros maritim & perdagangan dunia.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Concept 1 -->
                <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 hover:border-amber-400 transition">
                    <div class="flex items-center gap-3 mb-3">
                        <div class="w-10 h-10 rounded-xl bg-amber-100 text-amber-700 flex items-center justify-center font-bold text-lg">1</div>
                        <h4 class="font-bold text-slate-800 text-base">Konsep Dasar Ilmu Sejarah</h4>
                    </div>
                    <ul class="text-xs text-slate-600 space-y-2 list-disc list-inside leading-relaxed">
                        <li><strong class="text-slate-800">Manusia:</strong> Subjek (pelaku) dan objek utama peristiwa sejarah.</li>
                        <li><strong class="text-slate-800">Ruang (Spasial):</strong> Tempat peristiwa sejarah berlangsung.</li>
                        <li><strong class="text-slate-800">Waktu (Temporal):</strong> Kapan peristiwa terjadi (kontinuitas, perubahan, pengulangan).</li>
                        <li><strong class="text-slate-800">Diakronis (Kronologis):</strong> Memanjang dalam waktu, menyempit dalam ruang (melihat urutan kronologi).</li>
                        <li><strong class="text-slate-800">Sinkronis:</strong> Meluas dalam ruang, menyempit dalam waktu (mengkaji struktur secara mendalam).</li>
                    </ul>
                </div>

                <!-- Concept 2 -->
                <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 hover:border-amber-400 transition">
                    <div class="flex items-center gap-3 mb-3">
                        <div class="w-10 h-10 rounded-xl bg-indigo-100 text-indigo-700 flex items-center justify-center font-bold text-lg">2</div>
                        <h4 class="font-bold text-slate-800 text-base">4 Langkah Penelitian Sejarah</h4>
                    </div>
                    <ol class="text-xs text-slate-600 space-y-2 list-decimal list-inside leading-relaxed">
                        <li><strong class="text-slate-800">Heuristik:</strong> Pengumpulan sumber sejarah (sumber primer & sekunder).</li>
                        <li><strong class="text-slate-800">Kritik / Verifikasi:</strong> Pengujian keabsahan (Kritik Eksternal = keaslian fisik; Kritik Internal = kredibilitas isi).</li>
                        <li><strong class="text-slate-800">Interpretasi:</strong> Penafsiran & perangkaian fakta sejarah menjadi satu kesatuan.</li>
                        <li><strong class="text-slate-800">Historiografi:</strong> Penulisan kisah sejarah secara ilmiah & sistematis.</li>
                    </ol>
                </div>

                <!-- Concept 3 -->
                <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 hover:border-amber-400 transition">
                    <div class="flex items-center gap-3 mb-3">
                        <div class="w-10 h-10 rounded-xl bg-emerald-100 text-emerald-700 flex items-center justify-center font-bold text-lg">3</div>
                        <h4 class="font-bold text-slate-800 text-base">Kehidupan Masa Praaksara</h4>
                    </div>
                    <ul class="text-xs text-slate-600 space-y-2 list-disc list-inside leading-relaxed">
                        <li><strong class="text-slate-800">Berburu & Mengumpulkan Makanan:</strong> Nomaden (berpindah), alat batu kasar (*Paleolitikum* & *Mesolitikum* - Kapak Perimbas).</li>
                        <li><strong class="text-slate-800">Bercocok Tanam (Neolitikum):</strong> Sedenter (menetap), *food producing*, alat batu halus (Kapak Persegi & Kapak Lonjong).</li>
                        <li><strong class="text-slate-800">Perundagian (Zaman Logam):</strong> Pembagian kerja ahli, teknik *a cire perdue* & *bivalve* (Nekara, Moko, Kapak Perunggu).</li>
                    </ul>
                </div>

                <!-- Concept 4: Jalur Rempah -->
                <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 hover:border-amber-400 transition">
                    <div class="flex items-center gap-3 mb-3">
                        <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-700 flex items-center justify-center font-bold text-lg"><i class="fa-solid fa-ship"></i></div>
                        <h4 class="font-bold text-slate-800 text-base">Jalur Rempah Nusantara</h4>
                    </div>
                    <ul class="text-xs text-slate-600 space-y-2 list-disc list-inside leading-relaxed">
                        <li><strong class="text-slate-800">Poros Maritim Dunia:</strong> Jaringan perdagangan laut kuno yang menghubungkan Maluku (kepulauan rempah: cengkeh & pala) dengan India, Tiongkok, Arab, hingga Eropa.</li>
                        <li><strong class="text-slate-800">Pertukaran Budaya & Komoditas:</strong> Tidak hanya perdagangan cengkeh & lada, namun melahirkan pertukaran agama, bahasa, dan teknologi pelayaran (Perahu Cadik).</li>
                        <li><strong class="text-slate-800">Pusat Pelabuhan Utama:</strong> Malaka, Barus, Tuban, Makassar, Ternate, dan Tidore.</li>
                    </ul>
                </div>
            </div>

            <div class="bg-slate-900 text-white p-5 rounded-2xl flex flex-col md:flex-row items-center justify-between gap-4">
                <div>
                    <h4 class="font-bold text-amber-400 text-base">Sudah mempelajari seluruh materi?</h4>
                    <p class="text-xs text-slate-300">Lanjutkan ke Lembar Kerja Aktivitas 1 untuk menguji pemahaman kelompokmu!</p>
                </div>
                <button onclick="switchTab('tab-pg')" class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-bold px-5 py-2.5 rounded-xl text-sm transition">
                    Mulai Aktivitas 1 <i class="fa-solid fa-arrow-right ml-1"></i>
                </button>
            </div>
        </div>

        <!-- TAB 2: PILIHAN GANDA -->
        <div id="tab-pg" class="tab-content hidden space-y-6">
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm flex justify-between items-center">
                <div>
                    <h3 class="font-bold text-lg text-slate-800">Aktivitas 1: Kuis Pilihan Ganda Interaktif</h3>
                    <p class="text-xs text-slate-500">Pilihlah salah satu jawaban yang paling tepat (10 Soal @10 Poin = Maks 100 Poin)</p>
                </div>
                <span id="pg-progress-badge" class="bg-amber-100 text-amber-800 text-xs font-bold px-3 py-1 rounded-full">0/10 Terjawab</span>
            </div>

            <div id="pg-container" class="space-y-6">
                <!-- Questions injected via JS -->
            </div>

            <div class="flex justify-end">
                <button onclick="gradePG()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-6 py-3 rounded-xl shadow-lg transition flex items-center gap-2">
                    <i class="fa-solid fa-check-double"></i> Periksa & Simpan Jawaban PG
                </button>
            </div>
        </div>

        <!-- TAB 3: MENJODOHKAN -->
        <div id="tab-match" class="tab-content hidden space-y-6">
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm">
                <h3 class="font-bold text-lg text-slate-800">Aktivitas 2: Menjodohkan Istilah Sejarah & Rempah</h3>
                <p class="text-xs text-slate-500 mt-1">Jodohkan istilah sejarah pada Kolom A dengan definisi atau keterangan yang sesuai pada Kolom B.</p>
            </div>

            <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
                <div id="matching-grid" class="space-y-4">
                    <!-- Dynamic matching rows -->
                </div>

                <div class="mt-6 flex justify-between items-center pt-4 border-t border-slate-100">
                    <span id="matching-score-badge" class="text-sm font-semibold text-slate-600">Skor Menjodohkan: -</span>
                    <button onclick="gradeMatching()" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold px-5 py-2.5 rounded-xl transition flex items-center gap-2 text-sm">
                        <i class="fa-solid fa-circle-check"></i> Periksa Jawaban Menjodohkan
                    </button>
                </div>
            </div>
        </div>

        <!-- TAB 4: KRONOLOGI / PENGURUTAN -->
        <div id="tab-timeline" class="tab-content hidden space-y-6">
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm">
                <h3 class="font-bold text-lg text-slate-800">Aktivitas 3: Pengurutan Kronologis Tahapan Penelitian Sejarah</h3>
                <p class="text-xs text-slate-500 mt-1">Gunakan tombol **Panah Atas / Bawah** untuk mengurutkan 4 tahapan penelitian sejarah dari tahap paling awal hingga akhir secara rinci.</p>
            </div>

            <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
                <p class="text-sm font-semibold text-slate-700 mb-4"><i class="fa-solid fa-arrow-down-short-wide text-amber-600 mr-2"></i>Urutkan Tahapan Penelitian Sejarah secara Tepat:</p>
                
                <div id="timeline-list" class="space-y-3">
                    <!-- Dynamic sortable items -->
                </div>

                <div class="mt-6 flex justify-between items-center pt-4 border-t border-slate-100">
                    <span id="timeline-score-badge" class="text-sm font-semibold text-slate-600">Status Urutan: Belum Diperiksa</span>
                    <button onclick="gradeTimeline()" class="bg-amber-600 hover:bg-amber-700 text-white font-bold px-5 py-2.5 rounded-xl transition flex items-center gap-2 text-sm">
                        <i class="fa-solid fa-sort"></i> Cek Urutan Kronologis
                    </button>
                </div>
            </div>
        </div>

        <!-- TAB 5: ANALISIS SUMBER & ESSAY -->
        <div id="tab-essay" class="tab-content hidden space-y-6">
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm">
                <h3 class="font-bold text-lg text-slate-800">Aktivitas 4: Analisis Sumber Sejarah & Studi Kasus Jalur Rempah</h3>
                <p class="text-xs text-slate-500 mt-1">Bacalah teks studi kasus di bawah ini, lalu jawablah pertanyaan analisis dengan rinci dan kritis.</p>
            </div>

            <!-- Case Study Box -->
            <div class="bg-amber-50/70 rounded-2xl p-5 border border-amber-200 space-y-3">
                <div class="flex items-center gap-2 text-amber-900 font-bold text-sm">
                    <i class="fa-solid fa-scroll text-amber-700"></i>
                    <h4>Studi Kasus: Barus, Prasasti Yupa, dan Perdagangan Kapur Barus & Cengkeh</h4>
                </div>
                <p class="text-xs text-slate-700 leading-relaxed italic">
                    "Sejak abad ke-1 Masehi, wilayah Nusantara telah terhubung dalam jaringan pelayaran dunia. Kota pelabuhan Kuno Barus di Sumatra Utara terkenal hingga ke Mesir kuno karena menghasilkan Kapur Barus. Sementara itu di Kalimantan Timur ditemukan Prasasti Yupa abad ke-4 M yang membuktikan adanya interaksi budaya dengan India. Kepulauan Maluku juga menjadi satu-satunya produsen Cengkeh dan Pala di dunia, menjadikan Nusantara pusat utama Jalur Rempah Maritim."
                </p>
            </div>

            <div class="space-y-6">
                <!-- Essay Question 1 -->
                <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm space-y-3">
                    <label class="block text-sm font-bold text-slate-800">
                        1. Mengapa keberadaan Jalur Rempah Nusantara dikatakan tidak hanya membawa dampak ekonomi, tetapi juga dampak budaya dan sosial bagi masyarakat Kepulauan Nusantara?
                    </label>
                    <textarea id="essay-q1" rows="3" oninput="saveEssay()" placeholder="Tuliskan jawaban analisis kelompokmu di sini..." class="w-full p-3 text-sm rounded-xl border border-slate-300 focus:ring-2 focus:ring-amber-500 focus:outline-none"></textarea>
                    <div id="essay-feedback-1" class="hidden text-xs p-3 rounded-xl bg-slate-100 border border-slate-200">
                        <strong class="text-slate-800">Indikator Kunci Jawaban:</strong>
                        <p class="text-slate-600 mt-0.5">Jalur Rempah menjadi sarana interaksi antar-bangsa (India, Tiongkok, Arab, Eropa) yang membawa pengaruh bahasa, agama (Hindu-Buddha & Islam), arsitektur, teknologi pelayaran, serta peradaban di Nusantara.</p>
                    </div>
                </div>

                <!-- Essay Question 2 -->
                <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm space-y-3">
                    <label class="block text-sm font-bold text-slate-800">
                        2. Berdasarkan sifatnya, Prasasti Yupa dan artefak sisa kapal dagang kuno termasuk dalam jenis sumber sejarah apa? Jelaskan alasannya!
                    </label>
                    <textarea id="essay-q2" rows="3" oninput="saveEssay()" placeholder="Tuliskan jawaban analisis kelompokmu di sini..." class="w-full p-3 text-sm rounded-xl border border-slate-300 focus:ring-2 focus:ring-amber-500 focus:outline-none"></textarea>
                    <div id="essay-feedback-2" class="hidden text-xs p-3 rounded-xl bg-slate-100 border border-slate-200">
                        <strong class="text-slate-800">Indikator Kunci Jawaban:</strong>
                        <p class="text-slate-600 mt-0.5">Termasuk **Sumber Sejarah Primer** (Benda/Tertulis), karena merupakan peninggalan asli yang berasal langsung dari zaman atau masa peristiwa sejarah tersebut terjadi.</p>
                    </div>
                </div>

                <div class="flex justify-between items-center">
                    <button onclick="toggleEssayFeedback()" class="text-xs text-amber-700 font-semibold hover:underline">
                        <i class="fa-solid fa-eye"></i> Tampilkan / Sembunyikan Pembahasan Kunci Jawaban
                    </button>
                    <button onclick="saveEssayComplete()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-5 py-2.5 rounded-xl transition text-sm">
                        <i class="fa-solid fa-floppy-disk"></i> Simpan Jawaban Analisis
                    </button>
                </div>
            </div>
        </div>

        <!-- TAB 6: REPORT / RAPORT -->
        <div id="tab-report" class="tab-content hidden space-y-6">
            <div id="printable-area" class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm space-y-6">
                <!-- Print Header -->
                <div class="border-b-2 border-slate-800 pb-4 flex justify-between items-center">
                    <div>
                        <h2 class="text-2xl font-black text-slate-900 tracking-tight uppercase">LEMBAR HASIL KERJA SISWA (LKS) DIGITAL</h2>
                        <p class="text-xs text-slate-600 font-bold">SMKN 1 SIMPANG HULU | MATA PELAJARAN SEJARAH</p>
                    </div>
                    <div class="text-right">
                        <span class="text-xs text-slate-500">Tanggal Pengerjaan:</span>
                        <p id="report-date" class="text-sm font-bold text-slate-800">-</p>
                    </div>
                </div>

                <!-- Student Info Table -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 bg-slate-50 p-4 rounded-xl border border-slate-200 text-sm">
                    <div class="col-span-2">
                        <span class="text-xs text-slate-500 block font-semibold">Nama Siswa / Kelompok:</span>
                        <strong id="rep-name" class="text-slate-800 font-bold">-</strong>
                    </div>
                    <div>
                        <span class="text-xs text-slate-500 block font-semibold">Kelas:</span>
                        <strong id="rep-class" class="text-slate-800 font-bold">-</strong>
                    </div>
                    <div>
                        <span class="text-xs text-slate-500 block font-semibold">No. Absen:</span>
                        <strong id="rep-absent" class="text-slate-800 font-bold">-</strong>
                    </div>
                    <div class="col-span-4 border-t border-slate-200 pt-2 mt-1">
                        <span class="text-xs text-slate-500 block font-semibold">Sekolah:</span>
                        <strong id="rep-school" class="text-slate-800 font-bold">-</strong>
                    </div>
                </div>

                <!-- Score Breakdown -->
                <div>
                    <h3 class="font-bold text-slate-800 mb-3 text-base">Rincian Perolehan Nilai Aktivitas</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-sm">
                            <thead>
                                <tr class="bg-slate-100 text-slate-700">
                                    <th class="p-3 border border-slate-200 rounded-tl-xl">Jenis Aktivitas</th>
                                    <th class="p-3 border border-slate-200">Bobot Maksimal</th>
                                    <th class="p-3 border border-slate-200">Skor Diperoleh</th>
                                    <th class="p-3 border border-slate-200 rounded-tr-xl">Status</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-200">
                                <tr>
                                    <td class="p-3 border border-slate-200 font-medium">Aktivitas 1: Kuis Pilihan Ganda</td>
                                    <td class="p-3 border border-slate-200">100 Poin</td>
                                    <td id="rep-score-pg" class="p-3 border border-slate-200 font-bold text-amber-700">0</td>
                                    <td id="rep-status-pg" class="p-3 border border-slate-200 text-xs">Belum dikerjakan</td>
                                </tr>
                                <tr>
                                    <td class="p-3 border border-slate-200 font-medium">Aktivitas 2: Menjodohkan Istilah</td>
                                    <td class="p-3 border border-slate-200">100 Poin</td>
                                    <td id="rep-score-match" class="p-3 border border-slate-200 font-bold text-indigo-700">0</td>
                                    <td id="rep-status-match" class="p-3 border border-slate-200 text-xs">Belum dikerjakan</td>
                                </tr>
                                <tr>
                                    <td class="p-3 border border-slate-200 font-medium">Aktivitas 3: Pengurutan Kronologis</td>
                                    <td class="p-3 border border-slate-200">100 Poin</td>
                                    <td id="rep-score-timeline" class="p-3 border border-slate-200 font-bold text-emerald-700">0</td>
                                    <td id="rep-status-timeline" class="p-3 border border-slate-200 text-xs">Belum dikerjakan</td>
                                </tr>
                                <tr>
                                    <td class="p-3 border border-slate-200 font-medium">Aktivitas 4: Analisis Sumber Sejarah</td>
                                    <td class="p-3 border border-slate-200">Kualitatif</td>
                                    <td id="rep-score-essay" class="p-3 border border-slate-200 font-bold text-slate-700">Tersimpan</td>
                                    <td id="rep-status-essay" class="p-3 border border-slate-200 text-xs">Menunggu penilaian guru</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Final Grade Summary -->
                <div class="bg-gradient-to-r from-amber-600 to-amber-800 text-white rounded-2xl p-6 flex flex-col md:flex-row justify-between items-center gap-4">
                    <div>
                        <span class="text-xs uppercase tracking-wider font-semibold opacity-90">Rata-Rata Nilai Objektif Siswa</span>
                        <h4 id="rep-final-score" class="text-4xl font-extrabold">0 / 100</h4>
                        <p id="rep-predicate" class="text-xs mt-1 text-amber-100">Predikat: Belum Selesai</p>
                    </div>
                    <div class="text-center md:text-right border-t md:border-t-0 md:border-l border-amber-400/40 pt-3 md:pt-0 md:pl-6">
                        <span class="text-xs opacity-90 block">Catatan Guru Mata Pelajaran:</span>
                        <p id="rep-teacher-note" class="text-xs italic mt-1 max-w-xs">"Selesaikan seluruh aktivitas LKS untuk memperoleh hasil akumulasi secara maksimal."</p>
                    </div>
                </div>

                <!-- Teacher Signature Placeholder for Printing -->
                <div class="pt-8 border-t border-slate-200 grid grid-cols-2 gap-8 text-center text-xs print-only">
                    <div>
                        <p>Mengetahui,</p>
                        <p class="font-bold mt-1">Orang Tua / Wali Siswa</p>
                        <div class="h-16"></div>
                        <p class="border-b border-slate-400 w-36 mx-auto"></p>
                    </div>
                    <div>
                        <p>Simpang Hulu, ..................... 2026</p>
                        <p class="font-bold mt-1">Guru Mata Pelajaran Sejarah</p>
                        <div class="h-16"></div>
                        <p class="border-b border-slate-400 w-36 mx-auto"></p>
                    </div>
                </div>
            </div>

            <!-- Print & Export Buttons -->
            <div class="flex flex-wrap justify-end gap-3 no-print">
                <button onclick="calculateFinalReport()" class="bg-slate-700 hover:bg-slate-800 text-white font-bold px-4 py-2.5 rounded-xl text-sm transition flex items-center gap-2">
                    <i class="fa-solid fa-arrows-rotate"></i> Perbarui Laporan
                </button>
                <button onclick="window.print()" class="bg-amber-600 hover:bg-amber-700 text-white font-bold px-5 py-2.5 rounded-xl text-sm transition shadow flex items-center gap-2">
                    <i class="fa-solid fa-print"></i> Cetak / Simpan PDF Raport LKS
                </button>
            </div>
        </div>

    </main>

    <!-- Custom Modal for Reset Confirmation -->
    <div id="reset-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm hidden flex items-center justify-center z-50 p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl border border-slate-200">
            <div class="flex items-center gap-3 text-rose-600 mb-3">
                <i class="fa-solid fa-triangle-exclamation text-2xl"></i>
                <h3 class="font-bold text-lg text-slate-800">Reset Data Pengerjaan?</h3>
            </div>
            <p class="text-xs text-slate-600 mb-6 leading-relaxed">
                Apakah Anda yakin ingin mengulang pengerjaan LKS ini dari awal? Semua nilai kuis, jawaban, dan identitas akan direset.
            </p>
            <div class="flex justify-end gap-3">
                <button onclick="hideResetModal()" class="px-4 py-2 text-xs font-semibold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-xl transition">Batal</button>
                <button onclick="confirmResetLKS()" class="px-4 py-2 text-xs font-semibold text-white bg-rose-600 hover:bg-rose-700 rounded-xl transition">Ya, Reset Sekarang</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-5 right-5 bg-slate-800 text-white px-4 py-3 rounded-2xl shadow-xl border border-slate-700 hidden flex items-center gap-3 z-50 transition-all duration-300">
        <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400 text-lg"></i>
        <span id="toast-msg" class="text-xs font-medium">Pesan pemberitahuan</span>
    </div>

    <script>
        // Default State initialized with requested user data
        let state = {
            student: { 
                name: 'F. SRI DEWI WULANDARI, IRWANSYAH, OBET EDOM, RINO', 
                class: 'XI', 
                absent: '2, 1, 2, 3, 4, 5', 
                school: 'SMKN 1 SIMPANG HULU' 
            },
            scores: { pg: 0, match: 0, timeline: 0 },
            completed: { pg: false, match: false, timeline: false, essay: false },
            startTime: Date.now(),
            pgAnswers: {}
        };

        // 10 Soal Pilihan Ganda Sejarah
        const pgQuestions = [
            {
                id: 1,
                question: "Istilah 'Sejarah' berasal dari bahasa Arab 'Syajaratun' yang secara harfiah memiliki arti...",
                options: ["A. Akar tumbuhan", "B. Pohon silsilah", "C. Kejadian masa lalu", "D. Bunga yang mekar", "E. Garis keturunan raja"],
                answer: 1,
                explanation: "Syajaratun berarti 'pohon', mengibaratkan silsilah keturunan sejarah yang bercabang-cabang."
            },
            {
                id: 2,
                question: "Aspek utama yang menjadi subjek sekaligus objek utama dalam kajian ilmu sejarah adalah...",
                options: ["A. Alam semesta", "B. Tumbuhan dan hewan", "C. Manusia", "D. Benda artefak", "E. Ruang dan iklim"],
                answer: 2,
                explanation: "Manusia adalah subjek (pelaku) dan objek utama yang dikaji dalam peristiwa sejarah."
            },
            {
                id: 3,
                question: "Pendekatan sejarah yang memanjang dalam waktu namun menyempit dalam ruang untuk melihat urutan kronologis dinamakan...",
                options: ["A. Sinkronis", "B. Diakronis (Kronologis)", "C. Akseleratif", "D. Periodisasi", "E. Kausalitas"],
                answer: 1,
                explanation: "Diakronis menekankan pada kronologi dan dinamika perubahan dalam rentang waktu."
            },
            {
                id: 4,
                question: "Komoditas rempah utama asal Kepulauan Maluku yang menjadi perburuan bangsa-bangsa dunia pada masa Jalur Rempah adalah...",
                options: ["A. Kopi dan Teh", "B. Cengkeh dan Pala", "C. Tembakau dan Padi", "D. Garam dan Gula", "E. Kapur dan Kayu Manis"],
                answer: 1,
                explanation: "Kepulauan Maluku terkenal sebagai 'Spice Islands' penghasil utama Cengkeh dan Pala."
            },
            {
                id: 5,
                question: "Langkah pertama dalam penelitian sejarah yang bertujuan mengumpulkan sumber-sumber sejarah dinamakan...",
                options: ["A. Verifikasi", "B. Historiografi", "C. Interpretasi", "D. Heuristik", "E. Ekskavasi"],
                answer: 3,
                explanation: "Heuristik (*heuriskein*) artinya menemukan atau mengumpulkan sumber-sumber sejarah."
            },
            {
                id: 6,
                question: "Pengujian terhadap keaslian fisik bahan sumber sejarah (kertas, batu, tinta) disebut sebagai...",
                options: ["A. Kritik Eksternal", "B. Kritik Internal", "C. Heuristik Khusus", "D. Historiografi Tradisional", "E. Sintesis Sejarah"],
                answer: 0,
                explanation: "Kritik eksternal bertujuan menguji keaslian fisik bahan dari sumber sejarah."
            },
            {
                id: 7,
                question: "Corak kehidupan manusia praaksara yang sudah menetap dan menghasilkan makanan sendiri (*food producing*) terjadi pada masa...",
                options: ["A. Paleolitikum", "B. Berburu tingkat awal", "C. Neolitikum (Bercocok Tanam)", "D. Mesolitikum", "E. Perundagian Awal"],
                answer: 2,
                explanation: "Masa Neolitikum menandai revolusi kehidupan manusia dari mencari makanan (*gathering*) menjadi menghasilkan makanan (*producing*)."
            },
            {
                id: 8,
                question: "Pelabuhan kuno di pesisir Sumatra Utara yang terkenal sebagai penghasil kapur Barus dan telah disinggahi pedagang Mesir & Yunani adalah...",
                options: ["A. Barus", "B. Malaka", "C. Sunda Kelapa", "D. Tuban", "E. Makassar"],
                answer: 0,
                explanation: "Barus adalah kota pelabuhan kuno penghasil Kapur Barus (*camphor*) yang tersohor hingga ke kawasan Mediterania."
            },
            {
                id: 9,
                question: "Hasil kebudayaan Megalitikum yang berupa tiang batu tunggal untuk pemujaan roh nenek moyang disebut...",
                options: ["A. Menhir", "B. Dolmen", "C. Sarkofagus", "D. Waruga", "E. Punden Berundak"],
                answer: 0,
                explanation: "Menhir adalah tiang atau tugu batu tunggal yang didirikan untuk menghormati dan memuja roh nenek moyang."
            },
            {
                id: 10,
                question: "Kajian sejarah yang meluas dalam ruang dan mengkaji struktur peristiwa pada satu masa tertentu dinamakan pendekatan...",
                options: ["A. Diakronis", "B. Sinkronis", "C. Ankronis", "D. Monokronis", "E. Teleologis"],
                answer: 1,
                explanation: "Pendekatan sinkronis meneliti berbagai aspek (sosial, ekonomi, politik) secara mendalam pada satu periode tertentu."
            }
        ];

        // Data Menjodohkan
        const matchingPairs = [
            { id: 1, term: "Jalur Rempah", matchId: "C", desc: "Jaringan perdagangan maritim kuno penghubung Nusantara dengan dunia." },
            { id: 2, term: "Kritik Internal", matchId: "B", desc: "Pengujian terhadap kredibilitas dan kebenaran isi dari sumber sejarah." },
            { id: 3, term: "Historiografi", matchId: "D", desc: "Tahapan penulisan karya ilmiah sejarah secara runtut dan sistematis." },
            { id: 4, term: "Kapur Barus", matchId: "A", desc: "Komoditas wewangian & pengobatan khas Sumatra Utara yang tersohor hingga Mesir." },
            { id: 5, term: "Neolitikum", matchId: "E", desc: "Zaman batu baru yang ditandai kehidupan menetap dan menghasilkan makanan." }
        ];

        // Data Timeline Kronologis
        let timelineItems = [
            { id: 3, title: "3. Interpretasi", desc: "Penafsiran keterkaitan antar fakta sejarah yang telah diverifikasi." },
            { id: 1, title: "1. Heuristik", desc: "Mengumpulkan sumber-sumber sejarah primer dan sekunder." },
            { id: 4, title: "4. Historiografi", desc: "Penulisan kisah sejarah menjadi bentuk karya tulis ilmiah." },
            { id: 2, title: "2. Kritik / Verifikasi", desc: "Menguji keaslian fisik dan kebenaran isi sumber sejarah." }
        ];

        window.onload = function() {
            loadLocalStorage();
            initStudentFields();
            renderPG();
            renderMatching();
            renderTimeline();
            startTimer();
            updateReportDate();
        };

        function initStudentFields() {
            document.getElementById('student-name').value = state.student.name;
            document.getElementById('student-class').value = state.student.class;
            document.getElementById('student-absent').value = state.student.absent;
            document.getElementById('student-school').value = state.student.school;
        }

        // Navigation Tab Switcher
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-amber-600', 'text-white', 'shadow-sm');
                btn.classList.add('bg-slate-100', 'text-slate-600');
            });

            document.getElementById(tabId).classList.remove('hidden');
            const activeBtn = document.getElementById('btn-' + tabId);
            if (activeBtn) {
                activeBtn.classList.remove('bg-slate-100', 'text-slate-600');
                activeBtn.classList.add('bg-amber-600', 'text-white', 'shadow-sm');
            }

            if(tabId === 'tab-report') {
                calculateFinalReport();
            }
        }

        // Render PG
        function renderPG() {
            const container = document.getElementById('pg-container');
            container.innerHTML = '';

            pgQuestions.forEach((q, idx) => {
                const qCard = document.createElement('div');
                qCard.className = "bg-white rounded-2xl p-5 border border-slate-200 shadow-sm space-y-4";
                
                let optionsHtml = '';
                q.options.forEach((opt, optIdx) => {
                    const isChecked = state.pgAnswers[q.id] === optIdx ? 'checked' : '';
                    optionsHtml += `
                        <label class="flex items-start gap-3 p-3 rounded-xl border border-slate-200 hover:bg-amber-50/50 cursor-pointer transition">
                            <input type="radio" name="pg-q-${q.id}" value="${optIdx}" ${isChecked} onchange="selectPG(${q.id}, ${optIdx})" class="mt-0.5 text-amber-600 focus:ring-amber-500">
                            <span class="text-sm text-slate-700 font-medium">${opt}</span>
                        </label>
                    `;
                });

                qCard.innerHTML = `
                    <div class="flex items-start gap-3">
                        <span class="w-7 h-7 rounded-lg bg-amber-100 text-amber-800 flex items-center justify-center font-bold text-xs flex-shrink-0">${idx+1}</span>
                        <p class="font-bold text-slate-800 text-sm md:text-base leading-snug">${q.question}</p>
                    </div>
                    <div class="space-y-2 pl-1 md:pl-10">
                        ${optionsHtml}
                    </div>
                    <div id="pg-feedback-${q.id}" class="hidden pl-1 md:pl-10 text-xs p-3 rounded-xl"></div>
                `;
                container.appendChild(qCard);
            });
            updatePGProgress();
        }

        function selectPG(qId, optIdx) {
            state.pgAnswers[qId] = optIdx;
            updatePGProgress();
            saveLocalStorage();
        }

        function updatePGProgress() {
            const answeredCount = Object.keys(state.pgAnswers).length;
            document.getElementById('pg-progress-badge').innerText = `${answeredCount}/10 Terjawab`;
        }

        function gradePG() {
            let correctCount = 0;

            pgQuestions.forEach(q => {
                const userAns = state.pgAnswers[q.id];
                const feedbackEl = document.getElementById(`pg-feedback-${q.id}`);
                feedbackEl.classList.remove('hidden', 'bg-emerald-50', 'bg-rose-50', 'text-emerald-800', 'text-rose-800');

                if (userAns !== undefined) {
                    if (userAns === q.answer) {
                        correctCount++;
                        feedbackEl.classList.add('bg-emerald-50', 'text-emerald-800', 'border', 'border-emerald-200');
                        feedbackEl.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-600 mr-1"></i> <strong>Benar!</strong> ${q.explanation}`;
                    } else {
                        feedbackEl.classList.add('bg-rose-50', 'text-rose-800', 'border', 'border-rose-200');
                        feedbackEl.innerHTML = `<i class="fa-solid fa-circle-xmark text-rose-600 mr-1"></i> <strong>Jawaban Kurang Tepat.</strong> Kunci: ${q.options[q.answer]}. ${q.explanation}`;
                    }
                } else {
                    feedbackEl.classList.add('bg-amber-50', 'text-amber-800', 'border', 'border-amber-200');
                    feedbackEl.innerHTML = `<i class="fa-solid fa-triangle-exclamation text-amber-600 mr-1"></i> Soal ini belum diisi.`;
                }
            });

            state.scores.pg = correctCount * 10;
            state.completed.pg = true;
            showToast(`Skor Kuis PG: ${state.scores.pg}/100`, "success");
            saveLocalStorage();
        }

        function renderMatching() {
            const container = document.getElementById('matching-grid');
            container.innerHTML = '';

            const shuffledDescs = [...matchingPairs].sort((a,b) => a.desc.localeCompare(b.desc));

            matchingPairs.forEach((pair, idx) => {
                const row = document.createElement('div');
                row.className = "grid grid-cols-1 md:grid-cols-2 gap-4 items-center bg-slate-50 p-4 rounded-xl border border-slate-200";

                let selectOptions = `<option value="">-- Pilih Pasangan yang Sesuai --</option>`;
                shuffledDescs.forEach((item) => {
                    selectOptions += `<option value="${item.matchId}">${item.desc}</option>`;
                });

                row.innerHTML = `
                    <div class="flex items-center gap-3">
                        <span class="w-6 h-6 rounded-md bg-indigo-100 text-indigo-700 flex items-center justify-center font-bold text-xs">${idx+1}</span>
                        <span class="font-bold text-slate-800 text-sm">${pair.term}</span>
                    </div>
                    <div>
                        <select id="match-select-${pair.id}" class="w-full text-xs p-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                            ${selectOptions}
                        </select>
                    </div>
                `;
                container.appendChild(row);
            });
        }

        function gradeMatching() {
            let correct = 0;
            matchingPairs.forEach(pair => {
                const selectEl = document.getElementById(`match-select-${pair.id}`);
                if (selectEl.value === pair.matchId) {
                    correct++;
                    selectEl.classList.add('border-emerald-500', 'bg-emerald-50');
                } else {
                    selectEl.classList.add('border-rose-500', 'bg-rose-50');
                }
            });

            state.scores.match = Math.round((correct / matchingPairs.length) * 100);
            state.completed.match = true;

            document.getElementById('matching-score-badge').innerText = `Skor Menjodohkan: ${state.scores.match}/100`;
            showToast(`Skor Menjodohkan: ${state.scores.match}/100`, "success");
            saveLocalStorage();
        }

        function renderTimeline() {
            const list = document.getElementById('timeline-list');
            list.innerHTML = '';

            timelineItems.forEach((item, index) => {
                const card = document.createElement('div');
                card.className = "flex items-center justify-between p-4 bg-slate-50 rounded-xl border border-slate-200 transition shadow-sm";
                card.innerHTML = `
                    <div class="flex items-center gap-3">
                        <span class="w-8 h-8 rounded-full bg-amber-600 text-white flex items-center justify-center font-bold text-sm">${index + 1}</span>
                        <div>
                            <h5 class="font-bold text-slate-800 text-sm">${item.title}</h5>
                            <p class="text-xs text-slate-500">${item.desc}</p>
                        </div>
                    </div>
                    <div class="flex flex-col gap-1">
                        <button onclick="moveTimeline(${index}, -1)" ${index === 0 ? 'disabled class="opacity-30 cursor-not-allowed"' : 'class="p-1 hover:bg-slate-200 rounded text-slate-600"'}>
                            <i class="fa-solid fa-chevron-up text-xs"></i>
                        </button>
                        <button onclick="moveTimeline(${index}, 1)" ${index === timelineItems.length - 1 ? 'disabled class="opacity-30 cursor-not-allowed"' : 'class="p-1 hover:bg-slate-200 rounded text-slate-600"'}>
                            <i class="fa-solid fa-chevron-down text-xs"></i>
                        </button>
                    </div>
                `;
                list.appendChild(card);
            });
        }

        function moveTimeline(index, direction) {
            const newIndex = index + direction;
            if (newIndex < 0 || newIndex >= timelineItems.length) return;
            
            const temp = timelineItems[index];
            timelineItems[index] = timelineItems[newIndex];
            timelineItems[newIndex] = temp;

            renderTimeline();
        }

        function gradeTimeline() {
            const correctOrder = [1, 2, 3, 4];
            let isCorrect = true;

            timelineItems.forEach((item, idx) => {
                if (item.id !== correctOrder[idx]) {
                    isCorrect = false;
                }
            });

            if (isCorrect) {
                state.scores.timeline = 100;
                document.getElementById('timeline-score-badge').innerHTML = `<span class="text-emerald-600 font-bold"><i class="fa-solid fa-circle-check"></i> Urutan Sempurna! (100 Poin)</span>`;
                showToast("Urutan Penelitian Sejarah Tepat!", "success");
                confetti({ particleCount: 70, spread: 60, origin: { y: 0.6 } });
            } else {
                state.scores.timeline = 0;
                document.getElementById('timeline-score-badge').innerHTML = `<span class="text-rose-600 font-bold"><i class="fa-solid fa-circle-xmark"></i> Urutan belum tepat. Coba susun kembali!</span>`;
                showToast("Urutan kronologis belum tepat.", "error");
            }
            state.completed.timeline = true;
            saveLocalStorage();
        }

        // Essay
        function saveEssay() {
            state.completed.essay = true;
            saveLocalStorage();
        }

        function toggleEssayFeedback() {
            document.getElementById('essay-feedback-1').classList.toggle('hidden');
            document.getElementById('essay-feedback-2').classList.toggle('hidden');
        }

        function saveEssayComplete() {
            state.completed.essay = true;
            showToast("Jawaban analisis tersimpan!", "success");
            saveLocalStorage();
        }

        // Identity
        function saveIdentity() {
            state.student.name = document.getElementById('student-name').value;
            state.student.class = document.getElementById('student-class').value;
            state.student.absent = document.getElementById('student-absent').value;
            state.student.school = document.getElementById('student-school').value;
            saveLocalStorage();
        }

        function calculateFinalReport() {
            document.getElementById('rep-name').innerText = state.student.name || "(Belum Diisi)";
            document.getElementById('rep-class').innerText = state.student.class || "-";
            document.getElementById('rep-absent').innerText = state.student.absent || "-";
            document.getElementById('rep-school').innerText = state.student.school || "SMKN 1 SIMPANG HULU";

            document.getElementById('rep-score-pg').innerText = state.scores.pg;
            document.getElementById('rep-status-pg').innerText = state.completed.pg ? "Selesai" : "Belum Dikerjakan";

            document.getElementById('rep-score-match').innerText = state.scores.match;
            document.getElementById('rep-status-match').innerText = state.completed.match ? "Selesai" : "Belum Dikerjakan";

            document.getElementById('rep-score-timeline').innerText = state.scores.timeline;
            document.getElementById('rep-status-timeline').innerText = state.completed.timeline ? "Selesai" : "Belum Dikerjakan";

            document.getElementById('rep-status-essay').innerText = state.completed.essay ? "Jawaban Tersimpan" : "Belum Diisi";

            const avgScore = Math.round((state.scores.pg + state.scores.match + state.scores.timeline) / 3);
            document.getElementById('rep-final-score').innerText = `${avgScore} / 100`;

            let predicate = "Perlu Bimbingan";
            if (avgScore >= 88) predicate = "Sangat Baik (A)";
            else if (avgScore >= 75) predicate = "Baik (B)";
            else if (avgScore >= 60) predicate = "Cukup (C)";

            document.getElementById('rep-predicate').innerText = `Predikat: ${predicate}`;
        }

        // Timer
        function startTimer() {
            setInterval(() => {
                const diff = Math.floor((Date.now() - state.startTime) / 1000);
                const mins = String(Math.floor(diff / 60)).padStart(2, '0');
                const secs = String(diff % 60).padStart(2, '0');
                document.getElementById('timer-display').innerText = `Waktu: ${mins}:${secs}`;
            }, 1000);
        }

        function updateReportDate() {
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            document.getElementById('report-date').innerText = new Date().toLocaleDateString('id-ID', options);
        }

        // Modal Controls
        function showResetModal() {
            document.getElementById('reset-modal').classList.remove('hidden');
        }

        function hideResetModal() {
            document.getElementById('reset-modal').classList.add('hidden');
        }

        function confirmResetLKS() {
            localStorage.removeItem('lks_sejarah_smkn1_simpanghulu');
            location.reload();
        }

        // Toast
        function showToast(message, type = "success") {
            const toast = document.getElementById('toast');
            const msgEl = document.getElementById('toast-msg');
            const iconEl = document.getElementById('toast-icon');

            msgEl.innerText = message;
            if (type === "success") {
                iconEl.className = "fa-solid fa-circle-check text-emerald-400 text-lg";
            } else {
                iconEl.className = "fa-solid fa-circle-exclamation text-rose-400 text-lg";
            }

            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3000);
        }

        // Local Storage
        function saveLocalStorage() {
            localStorage.setItem('lks_sejarah_smkn1_simpanghulu', JSON.stringify(state));
        }

        function loadLocalStorage() {
            const saved = localStorage.getItem('lks_sejarah_smkn1_simpanghulu');
            if (saved) {
                try {
                    const parsed = JSON.parse(saved);
                    state = { ...state, ...parsed };
                } catch(e) {
                    console.error("Gagal memuat penyimpanan lokal", e);
                }
            }
        }
    </script>
</body>
</html>
