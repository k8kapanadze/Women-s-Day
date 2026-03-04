
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ვარსკვლავების რუკა</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Playfair+Display:ital,wght@1,400&family=Fira+Go:wght@300;400&display=swap');

        :root { --gold: #f3cc4d; --bg: #05070a; }

        body {
            background-color: var(--bg);
            color: white;
            font-family: 'Fira Go', sans-serif;
            margin: 0;
            height: 100vh;
            overflow: hidden; /* რომ ეკრანი არ იძვროდეს */
        }

        .cinzel { font-family: 'Cinzel', serif; letter-spacing: 0.3em; color: var(--gold); }
        .serif-italic { font-family: 'Playfair Display', serif; font-style: italic; }

        /* ვარსკვლავური ცის ფონი */
        .sky {
            position: fixed;
            inset: 0;
            background-image: radial-gradient(circle at center, #111827 0%, #05070a 100%);
            z-index: -1;
        }

        /* პატარა მოციმციმე ვარსკვლავები დეკორისთვის */
        .decor-star {
            position: absolute;
            background: white;
            border-radius: 50%;
            opacity: 0.3;
            animation: twinkle 2s infinite alternate;
        }

        /* მთავარი მოგონებების ვარსკვლავები */
        .memory-star {
            position: absolute;
            width: 15px;
            height: 15px;
            background: var(--gold);
            border-radius: 50%;
            box-shadow: 0 0 15px var(--gold), 0 0 30px var(--gold);
            cursor: pointer;
            z-index: 20;
            transition: transform 0.3s;
        }

        .memory-star:hover { transform: scale(1.8); }

        /* მესიჯის ბარათი (Popup) */
        .message-card {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 90%;
            max-width: 350px;
            background: rgba(10, 14, 26, 0.95);
            border: 1px solid var(--gold);
            padding: 30px;
            text-align: center;
            backdrop-filter: blur(15px);
            display: none;
            z-index: 100;
            box-shadow: 0 0 50px rgba(0,0,0,0.8);
        }

        @keyframes twinkle {
            from { opacity: 0.2; }
            to { opacity: 0.7; }
        }

        /* ხაზები, რომლებიც აერთებს ვარსკვლავებს */
        .constellation-line {
            position: absolute;
            height: 1px;
            background: rgba(243, 204, 77, 0.15);
            transform-origin: left center;
            z-index: 5;
        }
    </style>
</head>
<body>

    <div class="sky" id="sky"></div>

    <header class="absolute top-10 w-full text-center z-50">
        <h1 class="cinzel text-2xl md:text-4xl animate__animated animate__fadeInDown">Our Map of Stars</h1>
        <p class="serif-italic text-slate-400 mt-2">დააჭირე ვარსკვლავებს...</p>
    </header>

    <div class="memory-star" style="top: 30%; left: 15%;" onclick="openMsg('Lighthouse Cafe', 'აქ პირველად გნახე პიანინოსთან... მუსიკა ჩვენს ისტორიას ყვებოდა.')"></div>
    <div class="memory-star" style="top: 25%; left: 75%;" onclick="openMsg('The Observatory', 'ცეკვა ვარსკვლავებს შორის. აქ რეალობა ოცნებად იქცა.')"></div>
    <div class="memory-star" style="top: 55%; left: 50%;" onclick="openMsg('Colorado Bridge', 'მზის ჩასვლა და შენი ღიმილი. აქ მივხვდი, რომ ჩემი სახლი შენ ხარ.')"></div>
    <div class="memory-star" style="top: 75%; left: 20%;" onclick="openMsg('Rialto Theatre', 'ჩვენი პირველი ფილმი. დრო გაჩერდა და მხოლოდ ჩვენი გულისცემა ისმოდა.')"></div>
    <div class="memory-star" style="top: 80%; left: 70%;" onclick="openMsg('Seb\'s Club', 'ჩემი ყველაზე დიდი საჩუქარი შენ ხარ. გილოცავ 8 მარტს! ✨')"></div>

    <div id="msgCard" class="message-card animate__animated">
        <h3 id="msgTitle" class="cinzel text-sm mb-4"></h3>
        <p id="msgText" class="serif-italic text-slate-200 text-lg"></p>
        <button onclick="closeMsg()" class="mt-8 text-[10px] uppercase tracking-widest text-amber-500 underline">დახურვა</button>
    </div>

    <script>
        // მესიჯის გახსნა
        function openMsg(title, text) {
            const card = document.getElementById('msgCard');
            document.getElementById('msgTitle').innerText = title;
            document.getElementById('msgText').innerText = text;
            card.style.display = 'block';
            card.classList.remove('animate__fadeOut');
            card.classList.add('animate__fadeIn');
        }

        // მესიჯის დახურვა
        function closeMsg() {
            const card = document.getElementById('msgCard');
            card.classList.replace('animate__fadeIn', 'animate__fadeOut');
            setTimeout(() => { card.style.display = 'none'; }, 500);
        }

        // დეკორატიული ვარსკვლავების გენერაცია
        function createDecorStars() {
            const sky = document.getElementById('sky');
            for(let i=0; i<50; i++) {
                const star = document.createElement('div');
                star.className = 'decor-star';
                const size = Math.random() * 3 + 'px';
                star.style.width = size;
                star.style.height = size;
                star.style.top = Math.random() * 100 + '%';
                star.style.left = Math.random() * 100 + '%';
                star.style.animationDelay = Math.random() * 2 + 's';
                sky.appendChild(star);
            }
        }

        createDecorStars();
    </script>
</body>
</html>
