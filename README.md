<!DOCTYPE html>
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ვარსკვლავების რუკა | La La Land Style</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=Fira+Go:wght@300;400;700&display=swap');

        :root {
            --la-blue: #0a0e1a;
            --la-gold: #f3cc4d;
            --la-purple: #2d1b4e;
        }

        body {
            font-family: 'Fira Go', sans-serif;
            background-color: var(--la-blue);
            color: white;
            overflow: hidden;
        }

        h1, .serif { font-family: 'Playfair Display', serif; }

        /* რუკის ფონი - ვინტაჟური ეფექტი */
        .map-container {
            position: relative;
            width: 100vw;
            height: 100vh;
            background: radial-gradient(circle, #1a233a 0%, #0a0e1a 100%);
            background-image: url('https://www.transparenttextures.com/patterns/stardust.png');
            overflow: hidden;
        }

        /* ვარსკვლავი (Marker) */
        .star-marker {
            position: absolute;
            cursor: pointer;
            width: 30px;
            height: 30px;
            background: var(--la-gold);
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            filter: drop-shadow(0 0 10px #f3cc4d);
            transition: transform 0.3s ease;
            z-index: 10;
        }

        .star-marker:hover {
            transform: scale(1.5) rotate(20deg);
        }

        /* Pop-up ფანჯარა */
        .modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            z-index: 50;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .modal-content {
            background: linear-gradient(135deg, #161b2e 0%, #0a0e1a 100%);
            border: 2px solid var(--la-gold);
            max-width: 500px;
            width: 100%;
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            box-shadow: 0 0 30px rgba(243, 204, 77, 0.2);
        }

        /* ანიმაციური ხაზები რუკაზე */
        .constellation-line {
            position: absolute;
            height: 1px;
            background: rgba(243, 204, 77, 0.2);
            transform-origin: left center;
            z-index: 1;
        }
    </style>
</head>
<body>

    <div class="map-container" id="map">
        <div class="absolute top-10 left-0 w-full text-center z-20 pointer-events-none">
            <h1 class="text-4xl md:text-6xl text-amber-400 mb-2 animate__animated animate__fadeInDown">Our Map of Stars</h1>
            <p class="text-slate-400 tracking-widest uppercase text-sm">Sebastian & Mia • Los Angeles Memory</p>
        </div>

        <div class="star-marker" style="top: 30%; left: 20%;" onclick="openBox(1)"></div>
        <div class="star-marker" style="top: 50%; left: 45%;" onclick="openBox(2)"></div>
        <div class="star-marker" style="top: 25%; left: 70%;" onclick="openBox(3)"></div>
        <div class="star-marker" style="top: 70%; left: 25%;" onclick="openBox(4)"></div>
        <div class="star-marker" style="top: 75%; left: 75%;" onclick="openBox(5)"></div>

        <div class="absolute bottom-10 right-10 flex items-center space-x-3">
            <span class="text-xs uppercase tracking-tighter text-amber-500">City of Stars is playing...</span>
            <div class="w-10 h-10 border border-amber-500 rounded-full flex items-center justify-center animate-spin-slow">
                🎵
            </div>
        </div>
    </div>

    <div id="modal" class="modal animate__animated animate__fadeIn">
        <div class="modal-content animate__animated animate__zoomIn">
            <div id="modal-icon" class="text-5xl mb-4">✨</div>
            <h2 id="modal-title" class="serif text-3xl text-amber-400 mb-4">ადგილის სახელი</h2>
            <p id="modal-text" class="text-slate-300 leading-relaxed italic mb-6">მოგონების ტექსტი აქ დაიწერება...</p>
            <button onclick="closeBox()" class="border border-amber-500 text-amber-500 px-8 py-2 rounded-full hover:bg-amber-500 hover:text-black transition-all">დახურვა</button>
        </div>
    </div>

    <script>
        const memories = {
            1: {
                title: "Lighthouse Cafe",
                text: "აქ, სადაც ჯაზი სუნთქავს... შენ მასწავლე, რომ ვნებას საზღვრები არ აქვს. ჩვენი პირველი ნამდვილი საუბარი.",
                icon: "🎷"
            },
            2: {
                title: "Griffith Observatory",
                text: "ცეკვა ვარსკვლავებს შორის. აქ ჩვენი ისტორია რეალობას გასცდა და პლანეტარიუმის ცაზე ავიჭერით.",
                icon: "🔭"
            },
            3: {
                title: "Colorado Street Bridge",
                text: "მზის ჩასვლა და გულწრფელი დაპირებები. შენ დამინახე მაშინაც, როცა მე საკუთარ თავს ვერ ვხედავდი.",
                icon: "🌉"
            },
            4: {
                title: "Rialto Theatre",
                text: "პირველი ფილმი და პირველი შეხება. 'Rebel Without a Cause' ფონზე და ჩვენი სამყაროს დასაწყისი.",
                icon: "🎬"
            },
            5: {
                title: "Sebastian's Club",
                text: "სადაც არ უნდა ვიყოთ, ეს რუკა ყოველთვის შენთან მომიყვანს. ჩემი სახლი შენ ხარ. გილოცავ 8 მარტს!",
                icon: "🎹"
            }
        };

        function openBox(id) {
            const data = memories[id];
            document.getElementById('modal-title').innerText = data.title;
            document.getElementById('modal-text').innerText = data.text;
            document.getElementById('modal-icon').innerText = data.icon;
            document.getElementById('modal').style.display = 'flex';
        }

        function closeBox() {
            document.getElementById('modal').style.display = 'none';
        }

        // დახურვა ESC-ით
        window.onkeydown = function(event) {
            if (event.keyCode == 27) closeBox();
        };
    </script>

    <style>
        @keyframes spin-slow {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .animate-spin-slow {
            animation: spin-slow 8s linear infinite;
        }
    </style>
</body>
</html>
