<!DOCTYPE html>
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>8 მარტის სიურპრიზის დამგეგმავი</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .glass-card {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        input[type="range"]::-webkit-slider-thumb {
            appearance: none;
            height: 20px;
            width: 20px;
            background: #f59e0b;
            border-radius: 50%;
            cursor: pointer;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen">

    <div class="container mx-auto px-4 py-12 max-w-5xl">
        <header class="text-center mb-16">
            <h1 class="text-5xl font-extrabold mb-4 bg-gradient-to-r from-amber-400 to-orange-500 bg-clip-text text-transparent">
                Surprise Maker
            </h1>
            <p class="text-slate-400 text-lg">შეუქმენი მას დაუვიწყარი 8 მარტი ჩვენი დახმარებით</p>
        </header>

        <div class="glass-card rounded-3xl p-8 mb-12 shadow-2xl">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                <div>
                    <label class="block text-xs uppercase tracking-widest text-amber-500 font-semibold mb-3">ვისთვის არის სიურპრიზი?</label>
                    <select id="recipient" onchange="updateOffers()" class="w-full bg-slate-800 border border-slate-700 p-4 rounded-xl outline-none focus:ring-2 focus:ring-amber-500 transition-all">
                        <option value="partner">მეუღლე / პარტნიორი</option>
                        <option value="mother">დედა</option>
                        <option value="colleague">კოლეგა / მეგობარი</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs uppercase tracking-widest text-amber-500 font-semibold mb-3">ბიუჯეტი: <span id="budgetText" class="text-white">300</span> ₾</label>
                    <input type="range" id="budget" min="50" max="1000" step="50" value="300" oninput="updateOffers()" class="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer mt-5">
                    <div class="flex justify-between text-xs text-slate-500 mt-2">
                        <span>50 ₾</span>
                        <span>1000 ₾</span>
                    </div>
                </div>
            </div>
        </div>

        <div id="offersGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            </div>

        <footer class="mt-20 text-center border-t border-slate-800 pt-8">
            <p class="text-slate-500 text-sm">© 2026 Surprise Planner - დამზადებულია ზრუნვით</p>
        </footer>
    </div>

    <script>
        const offers = [
            { id: 1, type: 'partner', min: 0, max: 150, title: "კინო-რომანტიკა", desc: "VIP ბილეთები, პრემიუმ შოკოლადის ნაკრები და ვარდების თაიგული სახლში.", icon: "🎬" },
            { id: 2, type: 'partner', min: 151, max: 500, title: "ვახშამი ტერასაზე", desc: "კერძო ვახშამი ქალაქის ხედით, პერსონალური მენიუ და ცოცხალი მუსიკა.", icon: "🍷" },
            { id: 3, type: 'partner', min: 501, max: 1000, title: "Premium Getaway", desc: "ორდღიანი დასვენება ხუთვარსკვლავიან სასტუმროში + სპა პროცედურები.", icon: "✨" },
            { id: 4, type: 'mother', min: 0, max: 200, title: "ყვავილების ოკეანე", desc: "გიგანტური თაიგული და პერსონალიზებული მილოცვის წერილი კალიგრაფისგან.", icon: "💐" },
            { id: 5, type: 'mother', min: 201, max: 1000, title: "ჯანმრთელობის ტური", desc: "სრული სარელაქსაციო კურსი საუკეთესო სპა ცენტრში + ტრანსპორტირება.", icon: "🧘‍♀️" },
            { id: 6, type: 'colleague', min: 0, max: 1000, title: "ოფისის ყუთი", desc: "პრემიუმ ყავა, დახვეწილი აქსესუარი და ბრენდირებული ტკბილეული.", icon: "🎁" }
        ];

        function updateOffers() {
            const recipient = document.getElementById('recipient').value;
            const budget = parseInt(document.getElementById('budget').value);
            document.getElementById('budgetText').innerText = budget;

            const grid = document.getElementById('offersGrid');
            grid.innerHTML = '';

            const filtered = offers.filter(o => o.type === recipient && budget >= o.min);

            filtered.forEach(offer => {
                const card = `
                    <div class="glass-card p-6 rounded-2xl hover:border-amber-500 transition-all duration-300 transform hover:-translate-y-2 group">
                        <div class="text-4xl mb-4">${offer.icon}</div>
                        <h3 class="text-xl font-bold mb-2 group-hover:text-amber-400 transition-colors">${offer.title}</h3>
                        <p class="text-slate-400 text-sm mb-6">${offer.desc}</p>
                        <div class="flex items-center justify-between">
                            <span class="text-amber-500 font-bold">${offer.max} ₾-მდე</span>
                            <button class="bg-amber-500 hover:bg-amber-600 text-slate-950 px-4 py-2 rounded-lg font-bold text-sm transition-all shadow-lg shadow-amber-500/20">
                                დაჯავშნა
                            </button>
                        </div>
                    </div>
                `;
                grid.innerHTML += card;
            });
        }

        // Initial call
        updateOffers();
    </script>
</body>
</html>
