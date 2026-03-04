<!DOCTYPE html>
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>შექმენი ციფრული სიურპრიზი | 8 მარტი</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fira+Go:wght@300;400;700&display=swap');
        body { font-family: 'Fira Go', sans-serif; overflow-x: hidden; }
        .gradient-bg { background: linear-gradient(135deg, #1e1b4b 0%, #312e81 100%); }
        .card-preview { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .floating { animation: floating 3s ease-in-out infinite; }
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }
    </style>
</head>
<body class="gradient-bg text-white min-h-screen">

    <div id="generatorSection" class="container mx-auto px-4 py-12 max-w-2xl">
        <div class="text-center mb-10">
            <h1 class="text-3xl font-bold mb-4">🪄 შექმენი ციფრული სიურპრიზი</h1>
            <p class="text-slate-300">შეიყვანე ტექსტი და მიიღე პერსონალური ლინკი</p>
        </div>

        <div class="card-preview p-8 rounded-3xl shadow-2xl">
            <div class="space-y-6">
                <div>
                    <label class="block text-sm text-slate-400 mb-2">ვის ვულოცავთ?</label>
                    <input type="text" id="recipientName" placeholder="მაგ: ნინო" class="w-full bg-slate-800 border border-slate-700 p-4 rounded-xl outline-none focus:ring-2 focus:ring-pink-500">
                </div>
                <div>
                    <label class="block text-sm text-slate-400 mb-2">შენი სათქმელი (მილოცვა)</label>
                    <textarea id="messageBody" rows="4" placeholder="დაწერე შენი ემოციური ტექსტი..." class="w-full bg-slate-800 border border-slate-700 p-4 rounded-xl outline-none focus:ring-2 focus:ring-pink-500"></textarea>
                </div>
                <button onclick="generateSurprise()" class="w-full bg-pink-600 hover:bg-pink-700 p-4 rounded-xl font-bold text-lg transition-all shadow-lg shadow-pink-500/20">
                    ლინკის გენერაცია ✨
                </button>
            </div>
        </div>

        <div id="resultLink" class="hidden mt-8 p-6 bg-green-900/30 border border-green-500/50 rounded-2xl text-center">
            <p class="text-sm text-green-400 mb-2">ლინკი მზადაა! დააკოპირე და გაუგზავნე მას:</p>
            <input type="text" id="copyInput" readonly class="w-full bg-black/20 p-2 rounded text-center mb-4 text-xs italic">
            <button onclick="copyLink()" class="text-sm font-bold underline decoration-pink-500">ლინკის კოპირება</button>
        </div>
    </div>

    <div id="surprisePage" class="hidden fixed inset-0 flex items-center justify-center p-6 text-center">
        <div class="max-w-xl animate__animated animate__zoomIn">
            <div class="text-6xl mb-6 floating">🌸</div>
            <h1 class="text-5xl font-extrabold mb-4 text-pink-400" id="showName">ნინო</h1>
            <div class="bg-white/10 p-8 rounded-3xl border border-white/20 backdrop-blur-md shadow-2xl">
                <p class="text-xl italic leading-relaxed text-slate-100" id="showMessage">
                    შენი ტექსტი გამოჩნდება აქ...
                </p>
            </div>
            <p class="mt-8 text-slate-400 animate__animated animate__fadeInUp animate__delay-1s text-sm">
                გილოცავთ 8 მარტს! ✨
            </p>
            <button onclick="location.reload()" class="mt-12 text-xs text-slate-500 hover:text-white uppercase tracking-widest transition-colors">საკუთარი ბარათის შექმნა</button>
        </div>
        <div class="absolute inset-0 -z-10 pointer-events-none overflow-hidden" id="confetti"></div>
    </div>

    <script>
        // ფუნქცია: მონაცემების კოდირება URL-ში (Base64)
        function generateSurprise() {
            const name = document.getElementById('recipientName').value;
            const msg = document.getElementById('messageBody').value;

            if(!name || !msg) return alert("გთხოვთ შეავსოთ ველები");

            // ვაკეთებთ ტექსტის კოდირებას, რომ URL-ში გადაეცეს
            const data = btoa(unescape(encodeURIComponent(JSON.stringify({ n: name, m: msg }))));
            const shareUrl = window.location.origin + window.location.pathname + "?s=" + data;

            document.getElementById('copyInput').value = shareUrl;
            document.getElementById('resultLink').classList.remove('hidden');
        }

        function copyLink() {
            const copyText = document.getElementById("copyInput");
            copyText.select();
            document.execCommand("copy");
            alert("ლინკი დაკოპირებულია!");
        }

        // ფუნქცია: URL-დან მონაცემების ამოღება და ჩვენება
        function checkUrl() {
            const urlParams = new URLSearchParams(window.location.search);
            const surpriseData = urlParams.get('s');

            if(surpriseData) {
                try {
                    const decoded = JSON.parse(decodeURIComponent(escape(atob(surpriseData))));
                    document.getElementById('generatorSection').classList.add('hidden');
                    document.getElementById('surprisePage').classList.remove('hidden');
                    
                    document.getElementById('showName').innerText = decoded.n;
                    document.getElementById('showMessage').innerText = decoded.m;
                    document.title = "საჩუქარი " + decoded.n + "-სთვის";
                } catch(e) {
                    console.error("არასწორი ლინკი");
                }
            }
        }

        checkUrl();
    </script>
</body>
</html>
