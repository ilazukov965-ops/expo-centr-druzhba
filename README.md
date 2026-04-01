<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Экспоцентр Дружба — Премиальное озеленение</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #0B120E;
            --emerald-deep: #1A2421;
            --sage: #8DA282;
            --white-soft: #F8F9FA;
            --glass: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
        }

        body { background-color: var(--bg-dark); color: var(--white-soft); font-family: 'Inter', sans-serif; overflow-x: hidden; scroll-behavior: smooth; }
        h1, h2, h3, .serif { font-family: 'Playfair Display', serif; }

        /* Navigation Transitions */
        .page-content { display: none; opacity: 0; transform: translateY(10px); transition: all 0.5s ease; }
        .page-content.active { display: block; opacity: 1; transform: translateY(0); }

        .glass-card {
            background: var(--glass);
            backdrop-filter: blur(15px);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            transition: all 0.4s ease;
        }

        .btn-cta {
            background-color: var(--sage); color: var(--bg-dark); padding: 12px 32px;
            border-radius: 4px; font-weight: 600; text-transform: uppercase; cursor: pointer;
            transition: 0.3s;
        }
        .btn-cta:hover { background-color: #a5bca3; transform: translateY(-2px); }

        .nav-link { position: relative; cursor: pointer; opacity: 0.7; transition: 0.3s; }
        .nav-link:hover, .nav-link.active { opacity: 1; color: var(--sage); }
        .nav-link.active::after { content: ''; position: absolute; bottom: -4px; left: 0; width: 100%; height: 1px; background: var(--sage); }

        /* Modals */
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 100; align-items: center; justify-content: center; backdrop-filter: blur(10px); }
        .modal.active { display: flex; }

        .loader { border: 2px solid rgba(255,255,255,0.1); border-top: 2px solid var(--sage); border-radius: 50%; width: 16px; height: 16px; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .hero-bg {
            background: linear-gradient(rgba(11, 18, 14, 0.6), rgba(11, 18, 14, 0.95)), 
                        url('https://images.unsplash.com/photo-1545241047-6083a3684587?auto=format&fit=crop&q=80&w=2000');
            background-size: cover; background-position: center;
        }
    </style>
</head>
<body>

    <!-- Header -->
    <nav class="fixed w-full z-50 top-0 px-8 py-6 flex justify-between items-center bg-black/40 backdrop-blur-md border-b border-white/5">
        <div class="flex items-center gap-4 cursor-pointer" onclick="showPage('home')">
            <svg class="w-12 h-12" viewBox="0 0 120 120">
                <path fill="none" stroke="white" stroke-width="1.2" d="M50 50 C45 50, 40 55, 40 70 C40 85, 45 95, 60 100 C75 95, 80 85, 80 70 C80 55, 75 50, 70 50" />
                <path fill="none" stroke="white" stroke-width="1.2" d="M40 55 C25 50, 15 45, 12 60 M40 55 C35 35, 40 25, 55 30" />
                <path fill="none" stroke="white" stroke-width="1.2" d="M80 55 C95 50, 105 45, 108 60 M80 55 C85 35, 80 25, 65 30" />
            </svg>
            <div class="hidden sm:block">
                <span class="block text-[10px] tracking-[0.4em] text-sage font-bold uppercase">Экспоцентр</span>
                <span class="text-lg serif tracking-wider">ДРУЖБА</span>
            </div>
        </div>
        
        <div class="hidden lg:flex gap-10">
            <span onclick="showPage('catalog')" class="nav-link text-xs uppercase tracking-widest" id="nav-catalog">Каталог</span>
            <span onclick="showPage('services')" class="nav-link text-xs uppercase tracking-widest" id="nav-services">Услуги</span>
            <span onclick="showPage('blog')" class="nav-link text-xs uppercase tracking-widest" id="nav-blog">Блог</span>
            <span onclick="showPage('ai')" class="nav-link text-xs uppercase tracking-widest text-sage font-bold" id="nav-ai">✨ ИИ-Хаб</span>
        </div>

        <div class="flex items-center gap-6">
            <button onclick="toggleModal('search-modal')" class="hover:text-sage transition">
                <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
            </button>
            <button onclick="toggleModal('cart-modal')" class="hover:text-sage transition relative">
                <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
                <span id="cart-count" class="absolute -top-2 -right-2 bg-sage text-bg-dark text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center">0</span>
            </button>
        </div>
    </nav>

    <!-- Page: HOME -->
    <main id="page-home" class="page-content active">
        <section class="hero-bg min-h-screen flex flex-col justify-center items-center text-center px-6">
            <span class="text-sage tracking-[0.5em] uppercase text-xs mb-6 block">Эксклюзивное озеленение</span>
            <h1 class="text-5xl md:text-8xl mb-10 leading-tight max-w-5xl italic serif font-light">Глубокий уют в каждом листке</h1>
            <div class="flex gap-4">
                <button onclick="showPage('catalog')" class="btn-cta">Исследовать коллекцию</button>
                <button onclick="showPage('ai')" class="px-8 py-3 border border-white/20 hover:border-sage transition rounded-sm uppercase text-[10px] tracking-widest">✨ Умный помощник</button>
            </div>
        </section>
    </main>

    <!-- Page: CATALOG -->
    <section id="page-catalog" class="page-content pt-32 px-6 pb-20">
        <div class="max-w-7xl mx-auto">
            <h2 class="text-5xl serif italic mb-16 text-center">Наша Коллекция</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-10" id="catalog-grid">
                <!-- Dynamic Items -->
            </div>
        </div>
    </section>

    <!-- Page: SERVICES -->
    <section id="page-services" class="page-content pt-32 px-6 pb-20">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-5xl serif italic mb-16 text-center">Профессиональный сервис</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                <div class="glass-card overflow-hidden">
                    <img src="https://images.unsplash.com/photo-1583847268964-b28dc2f51ac9?auto=format&fit=crop&w=800" class="w-full h-64 object-cover">
                    <div class="p-8">
                        <h3 class="text-2xl serif mb-4">Фитодизайн интерьера</h3>
                        <p class="text-gray-400 text-sm mb-6">Создаем уникальные зеленые экосистемы для квартир и загородных домов под ключ.</p>
                        <button class="text-xs font-bold text-sage uppercase border-b border-sage">Подробнее</button>
                    </div>
                </div>
                <div class="glass-card overflow-hidden">
                    <img src="https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=800" class="w-full h-64 object-cover">
                    <div class="p-8">
                        <h3 class="text-2xl serif mb-4">Озеленение офисов</h3>
                        <p class="text-gray-400 text-sm mb-6">Живые стены и зонирование растениями для повышения продуктивности вашей команды.</p>
                        <button class="text-xs font-bold text-sage uppercase border-b border-sage">Для бизнеса</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Page: BLOG -->
    <section id="page-blog" class="page-content pt-32 px-6 pb-20">
        <div class="max-w-4xl mx-auto">
            <h2 class="text-5xl serif italic mb-16 text-center">Блог о растениях</h2>
            <div class="space-y-12">
                <article class="glass-card p-8 flex flex-col md:flex-row gap-8 items-center">
                    <img src="https://images.unsplash.com/photo-1520412099561-64831ebaeeaf?w=400" class="w-full md:w-48 h-48 object-cover rounded-lg">
                    <div>
                        <span class="text-sage text-[10px] uppercase font-bold tracking-widest block mb-2">12 Апреля, 2024</span>
                        <h3 class="text-xl serif mb-4">Как правильно пересаживать тропические виды?</h3>
                        <p class="text-gray-400 text-sm mb-4">Разбираем тонкости выбора грунта и дренажа для монстер и фикусов.</p>
                        <button class="text-xs uppercase tracking-widest text-white/60 hover:text-white transition">Читать статью →</button>
                    </div>
                </article>
            </div>
        </div>
    </section>

    <!-- Page: AI HUB -->
    <section id="page-ai" class="page-content pt-32 px-6 pb-20">
        <div class="max-w-4xl mx-auto">
            <h2 class="text-5xl serif italic mb-8 text-center">ИИ-Помощник</h2>
            <div class="glass-card p-10 mb-10">
                <div class="flex items-center gap-4 mb-8">
                    <div class="w-10 h-10 bg-sage rounded-full flex items-center justify-center text-bg-dark font-bold">✨</div>
                    <h3 class="text-xl serif italic">Спросить Мудрого Лося</h3>
                </div>
                <div class="flex gap-4">
                    <input type="text" id="ai-question" placeholder="Почему желтеют листья у пальмы?" class="flex-grow bg-white/5 border border-white/10 rounded px-6 py-4 focus:outline-none focus:border-sage transition">
                    <button onclick="askAI()" class="btn-cta px-8">Спросить</button>
                </div>
                <div id="ai-response" class="mt-8 text-gray-300 text-sm italic leading-relaxed border-l border-sage/30 pl-6 hidden"></div>
            </div>

            <div class="glass-card p-10">
                <h3 class="text-xl serif italic mb-6">Фото-анализатор</h3>
                <div class="border-2 border-dashed border-white/10 rounded-2xl h-64 flex flex-col items-center justify-center cursor-pointer hover:border-sage/50 transition relative overflow-hidden" onclick="document.getElementById('ai-file').click()">
                    <img id="ai-preview" class="absolute inset-0 w-full h-full object-cover hidden">
                    <div id="ai-prompt" class="text-center">
                        <p class="text-xs uppercase tracking-widest text-gray-500">Загрузите фото растения</p>
                    </div>
                </div>
                <input type="file" id="ai-file" class="hidden" onchange="previewFile()">
                <button id="analyze-btn" onclick="analyzePhoto()" class="w-full btn-cta mt-6 hidden">Анализировать фото ✨</button>
                <div id="photo-result" class="mt-6 text-sm text-gray-400 hidden p-6 bg-black/20 rounded-lg"></div>
            </div>
        </div>
    </section>

    <!-- Modals -->
    <div id="search-modal" class="modal" onclick="toggleModal('search-modal')">
        <div class="w-full max-w-2xl px-6" onclick="event.stopPropagation()">
            <input type="text" placeholder="Искать в каталоге..." class="w-full bg-transparent border-b border-white/20 text-4xl serif italic p-4 focus:outline-none focus:border-sage transition text-center">
        </div>
    </div>

    <div id="cart-modal" class="modal" onclick="toggleModal('cart-modal')">
        <div class="w-full max-w-md bg-emerald-deep p-10 rounded-2xl border border-white/10" onclick="event.stopPropagation()">
            <h3 class="text-2xl serif italic mb-6">Ваша корзина</h3>
            <div id="cart-list" class="space-y-4 mb-8 text-sm text-gray-400 min-h-[100px]">
                Корзина пуста
            </div>
            <button onclick="toggleModal('cart-modal')" class="w-full btn-cta">Продолжить покупки</button>
        </div>
    </div>

    <!-- Footer -->
    <footer class="py-20 border-t border-white/5 mt-20">
        <div class="max-w-7xl mx-auto px-6 text-center">
            <p class="text-[10px] text-gray-600 uppercase tracking-widest mb-6 italic">© 2024 Expocentre Druzhba. Природа в гармонии с интеллектом.</p>
            <div class="flex justify-center gap-8 text-gray-500 text-xs font-light">
                <a href="#" class="hover:text-sage transition">Instagram</a>
                <a href="#" class="hover:text-sage transition">Telegram</a>
                <a href="#" class="hover:text-sage transition">Контакты</a>
            </div>
        </div>
    </footer>

    <script>
        const apiKey = ""; // API Key injected by environment
        let cart = [];

        const items = [
            { id: 1, name: "Aucuba Japonica", price: 20.99, img: "https://images.unsplash.com/photo-1592178036223-93666d92410a?w=400" },
            { id: 2, name: "Dracaena Marginata", price: 19.99, img: "https://images.unsplash.com/photo-1598512752271-33f913a5af13?w=400" },
            { id: 3, name: "Calathea Zebrina", price: 24.99, img: "https://images.unsplash.com/photo-1614594975525-e45190c55d0b?w=400" },
            { id: 4, name: "Monstera Deliciosa", price: 35.00, img: "https://images.unsplash.com/photo-1614594975525-e45190c55d0b?w=400" },
            { id: 5, name: "Ficus Lyrata", price: 45.99, img: "https://images.unsplash.com/photo-1597055181300-e3633a907519?w=400" },
            { id: 6, name: "Sansevieria", price: 15.50, img: "https://images.unsplash.com/photo-1593482892290-f54927ae1bf6?w=400" }
        ];

        // --- NAVIGATION LOGIC ---
        function showPage(pageId) {
            document.querySelectorAll('.page-content').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            
            const activePage = document.getElementById('page-' + pageId);
            const activeNav = document.getElementById('nav-' + pageId);
            
            if (activePage) activePage.classList.add('active');
            if (activeNav) activeNav.classList.add('active');
            
            window.scrollTo({ top: 0, behavior: 'smooth' });
            if (pageId === 'catalog') renderCatalog();
        }

        // --- CATALOG & CART ---
        function renderCatalog() {
            const grid = document.getElementById('catalog-grid');
            grid.innerHTML = items.map(item => `
                <div class="glass-card p-6 flex flex-col h-full">
                    <div class="h-64 rounded-xl overflow-hidden mb-6">
                        <img src="${item.img}" class="w-full h-full object-cover">
                    </div>
                    <h3 class="serif text-xl mb-1">${item.name}</h3>
                    <p class="text-sage font-bold mb-6">${item.price} $</p>
                    <button onclick="addToCart(${item.id})" class="mt-auto border border-white/10 py-3 text-[10px] uppercase tracking-widest hover:bg-sage hover:text-bg-dark transition">Добавить</button>
                </div>
            `).join('');
        }

        function addToCart(id) {
            const item = items.find(i => i.id === id);
            cart.push(item);
            updateCartUI();
            
            // Anim effect
            const btn = event.target;
            btn.innerText = "Добавлено ✓";
            setTimeout(() => btn.innerText = "Добавить", 1000);
        }

        function updateCartUI() {
            const count = document.getElementById('cart-count');
            const list = document.getElementById('cart-list');
            count.innerText = cart.length;
            
            if (cart.length === 0) {
                list.innerHTML = "Корзина пуста";
            } else {
                list.innerHTML = cart.map(item => `
                    <div class="flex justify-between items-center border-b border-white/5 pb-2">
                        <span>${item.name}</span>
                        <span class="text-sage">${item.price} $</span>
                    </div>
                `).join('');
                const total = cart.reduce((sum, i) => sum + i.price, 0).toFixed(2);
                list.innerHTML += `<div class="pt-4 flex justify-between font-bold text-white"><span>Итого:</span><span>${total} $</span></div>`;
            }
        }

        function toggleModal(id) {
            document.getElementById(id).classList.toggle('active');
        }

        // --- AI FEATURES ---
        async function askAI() {
            const q = document.getElementById('ai-question').value;
            const resBox = document.getElementById('ai-response');
            if (!q.trim()) return;

            resBox.classList.remove('hidden');
            resBox.innerHTML = '<span class="loader inline-block mr-2"></span> Хранитель леса думает...';

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: `Отвечай как старый мудрый лось-ботаник на вопрос: ${q}. Тон: спокойный, лесной, мудрый.` }] }]
                    })
                });
                const data = await response.json();
                resBox.innerText = data.candidates?.[0]?.content?.parts?.[0]?.text || "Лес хранит молчание.";
            } catch (e) {
                resBox.innerText = "Ошибка связи с лесом.";
            }
        }

        let base64Photo = "";
        function previewFile() {
            const file = document.getElementById('ai-file').files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    document.getElementById('ai-preview').src = e.target.result;
                    document.getElementById('ai-preview').classList.remove('hidden');
                    document.getElementById('ai-prompt').classList.add('hidden');
                    document.getElementById('analyze-btn').classList.remove('hidden');
                    base64Photo = e.target.result.split(',')[1];
                };
                reader.readAsDataURL(file);
            }
        }

        async function analyzePhoto() {
            const resultBox = document.getElementById('photo-result');
            const btn = document.getElementById('analyze-btn');
            
            btn.innerText = "⏳ Анализирую...";
            resultBox.classList.remove('hidden');
            resultBox.innerHTML = "Сканирую пиксели и структуру листа...";

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{
                            parts: [
                                { text: "Определи растение на фото. Назови вид и дай 3 кратких совета по уходу." },
                                { inlineData: { mimeType: "image/jpeg", data: base64Photo } }
                            ]
                        }]
                    })
                });
                const data = await response.json();
                resultBox.innerText = data.candidates?.[0]?.content?.parts?.[0]?.text || "Не удалось распознать.";
            } catch (e) {
                resultBox.innerText = "Ошибка анализа.";
            } finally {
                btn.innerText = "Анализ завершен ✨";
            }
        }

        // Init
        window.onload = () => showPage('home');
    </script>
</body>
</html>
