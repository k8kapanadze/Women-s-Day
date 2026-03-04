
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ვარსკვლავების გზა | La La Land</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Playfair+Display:ital,wght@1,400;1,600&family=Fira+Go:wght@300;400;700&display=swap');

        :root { --gold: #f3cc4d; --bg: #05070a; --blue-accent: #1a233a; }

        body {
            background-color: var(--bg);
            color: white;
            font-family: 'Fira Go', sans-serif;
            margin: 0;
            overflow-x: hidden;
        }

        .serif-italic { font-family: 'Playfair Display', serif; font-style: italic; }
        .cinzel { font-family: 'Cinzel', serif; letter-spacing: 0.3em; }

        /* ვარსკვლავური ფონი */
        .stars-overlay {
            position: fixed;
            inset: 0;
            background-image: url('https://www.transparenttextures.com/patterns/stardust.png');
            opacity: 0.4;
            z-index: -1;
        }

        /* ვერტიკალური ოქროსფერი ხაზი */
        .path-line {
            position: absolute;
            left: 50%;
            top: 0;
            bottom: 0;
            width: 1px;
            background: linear-gradient(to bottom, transparent, var(--gold) 15%, var(--gold) 85%, transparent);
            transform: translateX(-50%);
            z-index: 1;
        }

        /* მოგონების ბლოკი */
        .memory-node {
            position: relative;
            margin-bottom: 120px;
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
        }

        .memory-node.active {
            opacity: 1;
            transform: translateY(0);
        }

        .star-point {
            width: 14px;
            height: 14px;
            background: var(--gold);
            border-radius: 50%;
            box-shadow: 0 0 20px var(--gold);
            z-index: 10;
        }

        .content-card {
            position: absolute;
            width: 85%;
            max-width: 320px;
            background: rgba(10, 14, 26, 0.9);
            border: 0.5px solid rgba(243, 204, 77, 0.2);
            padding: 25px;
            backdrop-filter: blur(10px);
            text-align: center;
        }

        /* მონაცვლეობითი განლაგება (მხოლოდ დესკტოპზე) */
        @media (min-width: 768px) {
            .memory-node:nth-child(even) .content-card { left: calc(50% + 40px); text-align: left; }
            .memory-node:nth-child(odd) .content-card { right: calc(50% + 40px); text-align: right; }
        }

        @media (max-width: 767px) {
            .content-card { top: 30px; position: relative; }
            .memory-node { flex-direction: column; margin-bottom: 80px; }
        }
    </style>
</head>
<body>

    <div class="stars-overlay"></div>

    <header class="h-screen flex flex-col items-center justify-center text-center px-6">
        <h1 class="cinzel text-3xl md:text-5xl text-amber-400 mb-6 animate__animated animate__fadeIn">The Map of Stars</h1>
        <p class="serif-italic text-lg md:text-xl text-slate-400 max-w-md animate__animated animate__fadeIn animate__delay-1s">
            "City of stars, are you shining just for me?"
        </p>
        <div class="mt-20 animate__animated animate__bounce animate__infinite">
            <span class="text-xs uppercase tracking-widest text-amber-500/50">ჩამოსქროლე</span>
        </div>
    </header>

    <section class="relative py-20">
        <div class="path-line"></div>

        <div class="memory-node">
            <div class="star-point"></div>
            <div class="content-card">
                <span class="cinzel text-[10px] text-amber-500 uppercase">The Lighthouse Cafe</span>
                <h3 class="serif-italic text-xl my-2">პირველი ნოტები</h3>
                <p class="text-sm text-slate-400 italic leading-relaxed">
                    "აქ, სადაც ჯაზი სუნთქავს... შენ მასწავლე, რომ ვნებას საზღვრები არ აქვს. ჩვენი ისტორია პირველივე აკორდიდან დაიწერა."
                </p>
            </div>
        </div>

        <div class="memory-node">
            <div class="star-point"></div>
            <div class="content-card">
                <span class="cinzel text-[10px] text-amber-500 uppercase">Griffith Observatory</span>
                <h3 class="serif-italic text-xl my-2">ცეკვა ვარსკვლავებს შორის</h3>
                <p class="text-sm text-slate-400 italic leading-relaxed">
                    "აქ ჩვენი ისტორია რეალობას გასცდა. პლანეტარიუმის ცაზე ავიჭერით და მივხვდით, რომ სამყარო მხოლოდ ჩვენ ორისთვის შეიქმნა."
                </p>
            </div>
        </div>

        <div class="memory-node">
            <div class="star-point"></div>
            <div class="content-card">
                <span class="cinzel text-[10px] text-amber-500 uppercase">Colorado Street Bridge</span>
                <h3 class="serif-italic text-xl my-2">ოცნებების ხიდი</h3>
                <p class="text-sm text-slate-400 italic leading-relaxed">
                    "მზის ჩასვლა და გულწრფელი დაპირებები. შენ დამინახე მაშინაც, როცა მე საკუთარ თავს ვერ ვხედავდი. მადლობა რწმენისთვის."
                </p>
            </div>
        </div>

        <div class="memory-node">
            <div class="star-point"></div>
            <div class="content-card">
                <span class="cinzel text-[10px] text-amber-500 uppercase">Seb's Club</span>
                <h3 class="serif-italic text-xl my-2">ჩემი სახლი შენ ხარ</h3>
                <p class="text-sm text-slate-400 italic leading-relaxed">
                    "სადაც არ უნდა ვიყოთ, ეს რუკა ყოველთვის შენთან მომიყვანს. შენ ხარ ჩემი მთავარი მელოდია და ჩემი სიმშვიდე."
                </p>
            </div>
        </div>
    </section>

    <footer class="h-screen flex flex-col items-center justify-center text-center px-6">
        <div class="text-4xl mb-8 animate__animated animate__pulse animate__infinite">🎹</div>
        <p class="serif-italic text-2xl text-amber-400 mb-4">"Here's to the fools who dream."</p>
        <p class="text-xs uppercase tracking-[0.4em] text-slate-500">გილოცავ 8 მარტს, ჩემო ვარსკვლავო!</p>
        <div class="w-px h-24 bg-gradient-to-b from-amber-500 to-transparent mt-12"></div>
    </footer>

    <script>
        // Scroll Reveal Logic
        const observerOptions = { threshold: 0.5 };
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.memory-node').forEach(node => {
            observer.observe(node);
        });
    </script>
</body>
</html>
