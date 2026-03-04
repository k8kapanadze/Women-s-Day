
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ვარსკვლავების რუკა</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Playfair+Display:ital,wght@1,400;1,600&family=Fira+Go:wght@300;400&display=swap');

        :root {
            --gold: #f3cc4d;
            --deep-blue: #05070a;
        }

        body {
            margin: 0;
            background-color: var(--deep-blue);
            color: white;
            font-family: 'Fira Go', sans-serif;
            overflow: hidden;
        }

        /* პრემიუმ სათაურის სტილი */
        .main-title {
            font-family: 'Cinzel', serif;
            letter-spacing: 0.5em;
            text-transform: uppercase;
            color: var(--gold);
            text-shadow: 0 0 20px rgba(243, 204, 77, 0.4);
        }

        .sub-title {
            font-family: 'Playfair Display', serif;
            font-style: italic;
            color: #94a3b8;
        }

        /* რუკის სტილიზებული ფონი */
        .map-overlay {
            position: fixed;
            inset: 0;
            background-image: url('https://www.transparenttextures.com/patterns/stardust.png'), 
                              url('https://images.unsplash.com/photo-1526649661456-89c7ed4d00b8?q=80&w=2000&auto=format&fit=crop');
            background-size: repeat, cover;
            background-position: center;
            filter: grayscale(100%) brightness(15%) contrast(110%);
            z-index: -1;
            opacity: 0.6;
        }

        /* ვარსკვლავების (წერტილების) ანიმაცია */
        .star-point {
            position: absolute;
            width: 10px;
            height: 10px;
            background: var(--gold);
            border-radius: 50%;
            box-shadow: 0 0 15px var(--gold), 0 0 30px var(--gold);
            cursor: pointer;
            z-index: 20;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .star-point:hover {
            transform: scale(2.5);
            box-shadow: 0 0 25px var(--gold), 0 0 50px white;
        }

        /* დამაკავშირებელი ხაზები */
        .constellation-line {
            position: absolute;
            background: linear-gradient(90deg, transparent, rgba(243, 204, 77, 0.3), transparent);
            height: 1px;
            transform-origin: left center;
            z-index: 10;
            pointer-events: none;
            opacity: 0;
            animation: fadeInLine 2s forwards 1s;
        }

        @keyframes fadeInLine {
            to { opacity: 1; }
        }

        /* მინიმალისტური ბარათი */
        .memory-card {
            position: fixed;
            bottom: 60px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(10, 14, 26, 0.9);
            border: 0.5px solid rgba(243, 204, 77, 0.3);
            padding: 30px;
            border-radius: 2px;
            text-align: center;
            backdrop-filter: blur(15px);
            width: 350px;
            display: none;
            z-index: 100;
        }

        /* ოქროსფერი ჩარჩოს ეფექტი ბარათზე */
        .memory-card::before {
            content: '';
            position: absolute;
            inset: 5px;
            border: 0.5px solid rgba(243, 204, 77, 0.1);
            pointer-events: none;
        }
    </style>
</head>
<body>

    <div class="map-overlay"></div>

    <header class="pt-16 text-center relative z-50">
        <h1 class="main-title text-2xl md:text-4xl animate__animated animate__fadeIn">The Map of Stars</h1>
        <div class="w-24 h-px bg-amber-500/30 mx-auto my-4"></div>
        <p class="sub-title text-lg animate__animated animate__fadeIn animate__delay-1s">A Journey Through Our Memories</p>
    </header>

    <div id="constellation" class="relative w-full h-screen">
        <div class="star-point" style="top: 30%; left: 25%;" onclick="reveal('The First Waltz', 'ეს იყო ღამე, როდესაც ყველაფერი დაიწყო. შენი ღიმილი იმაზე კაშკაშა იყო, ვიდრე ეს ვარსკვლავები.')"></div>
        <div class="star-point" style="top: 55%; left: 40%;" onclick="reveal('Under the Jazz Lights', 'კაფე, სადაც მუსიკა ჩვენს ისტორიას ყვებოდა. ყოველი ნოტი შენს სახელს ჰგავდა.')"></div>
        <div class="star-point" style="top: 40%; left: 65%;" onclick="reveal('Observatory Dream', 'აქ ჩვენი სამყარო ვარსკვლავებს გასცდა. მადლობა, რომ ჩემს გვერდით ოცნებობ.')"></div>
        <div class="star-point" style="top: 70%; left: 75%;" onclick="reveal('The Final Toast', 'ჩემი სახლი იქ არის, სადაც შენ ხარ. გილოცავ 8 მარტს, ჩემო ვარსკვლავო.')"></div>
    </div>

    <div id="memoryCard" class="memory-card shadow-2xl">
        <h3 id="mTitle" class="text-amber-400 font-bold tracking-[0.2em] uppercase text-sm mb-3"></h3>
        <p id="mText" class="text-slate-300 italic text-sm leading-relaxed"></p>
        <button onclick="document.getElementById('memoryCard').style.display='none'" class="mt-6 text-[10px] uppercase tracking-widest text-slate-500 hover:text-amber-400 transition-colors">დახურვა</button>
    </div>

    <script>
        function reveal(title, text) {
            const card = document.getElementById('memoryCard');
            document.getElementById('mTitle').innerText = title;
            document.getElementById('mText').innerText = text;
            card.style.display = 'block';
            card.classList.remove('animate__fadeOutDown');
            card.classList.add('animate__animated', 'animate__fadeInUp');
        }

        function drawLines() {
            const points = document.querySelectorAll('.star-point');
            const container = document.getElementById('constellation');
            
            for (let i = 0; i < points.length - 1; i++) {
                const p1 = points[i].getBoundingClientRect();
                const p2 = points[i+1].getBoundingClientRect();
                
                const x1 = p1.left + 5;
                const y1 = p1.top + 5;
                const x2 = p2.left + 5;
                const y2 = p2.top + 5;
                
                const length = Math.sqrt(Math.pow(x2-x1, 2) + Math.pow(y2-y1, 2));
                const angle = Math.atan2(y2-y1, x2-x1) * 180 / Math.PI;
                
                const line = document.createElement('div');
                line.className = 'constellation-line';
                line.style.width = length + 'px';
                line.style.left = x1 + 'px';
                line.style.top = y1 + 'px';
                line.style.transform = `rotate(${angle}deg)`;
                
                container.appendChild(line);
            }
        }

        window.onload = drawLines;
        window.onresize = () => {
            document.querySelectorAll('.constellation-line').forEach(l => l.remove());
            drawLines();
        };
    </script>
</body>
</html>
