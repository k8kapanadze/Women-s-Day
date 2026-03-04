
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ადგილების რუკა</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital@1&family=Fira+Go:wght@300;400;700&display=swap');

        body {
            margin: 0;
            background-color: #05070a;
            color: #f3cc4d;
            font-family: 'Fira Go', sans-serif;
            overflow: hidden;
        }

        /* რუკის ფონი - აქ შეგიძლია ნებისმიერი ქალაქის მუქი რუკის სურათი ჩასვა */
        .map-bg {
            position: fixed;
            inset: 0;
            background-image: url('https://w0.peakpx.com/wallpaper/380/100/HD-wallpaper-dark-map-city-maps.jpg');
            background-size: cover;
            background-position: center;
            filter: grayscale(100%) brightness(20%) contrast(120%);
            z-index: -1;
        }

        .constellation-container {
            position: relative;
            width: 100vw;
            height: 100vh;
        }

        /* წერტილი (ვარსკვლავი) */
        .point {
            position: absolute;
            width: 12px;
            height: 12px;
            background: #f3cc4d;
            border-radius: 50%;
            box-shadow: 0 0 15px #f3cc4d, 0 0 30px #f3cc4d;
            cursor: pointer;
            transition: transform 0.3s;
            z-index: 10;
        }

        .point:hover {
            transform: scale(2);
        }

        /* ხაზები წერტილებს შორის */
        .line {
            position: absolute;
            background: linear-gradient(90deg, rgba(243,204,77,0.1), rgba(243,204,77,0.5), rgba(243,204,77,0.1));
            height: 1px;
            transform-origin: left center;
            z-index: 5;
            pointer-events: none;
        }

        /* ინფორმაციის ფანჯარა */
        .info-card {
            position: absolute;
            bottom: 50px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(10, 14, 26, 0.8);
            border: 1px solid #f3cc4d;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            backdrop-filter: blur(10px);
            max-width: 90%;
            width: 400px;
            display: none;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .header {
            position: absolute;
            top: 40px;
            width: 100%;
            text-align: center;
            font-family: 'Playfair Display', serif;
            font-style: italic;
        }
    </style>
</head>
<body>

    <div class="map-bg"></div>

    <div class="header">
        <h1 class="text-4xl md:text-5xl opacity-80">Our Universe in One City</h1>
        <p class="text-sm tracking-[0.3em] uppercase mt-2 text-slate-500">თბილისი, 2026</p>
    </div>

    <div class="constellation-container" id="container">
        <div class="point" style="top: 35%; left: 30%;" onclick="showInfo('პირველი პაემანი', 'აქ პირველად შეგამჩნიე და მივხვდი, რომ სამყარო შეიცვალა.')"></div>
        <div class="point" style="top: 45%; left: 55%;" onclick="showInfo('ჩვენი კაფე', 'საუკეთესო ყავა და ყველაზე გულწრფელი ღიმილი.')"></div>
        <div class="point" style="top: 25%; left: 70%;" onclick="showInfo('ხედი მთაწმინდიდან', 'ქალაქი ჩვენს ფეხქვეშ იყო, ვარსკვლავები კი - ჩვენს თავზე.')"></div>
        <div class="point" style="top: 65%; left: 45%;" onclick="showInfo('პირველი კოცნა', 'დრო გაჩერდა და მხოლოდ ჩვენი გულისცემა ისმოდა.')"></div>
    </div>

    <div id="infoCard" class="info-card">
        <h2 id="infoTitle" class="text-xl font-bold mb-2 uppercase tracking-widest"></h2>
        <p id="infoText" class="text-slate-300 italic"></p>
        <button onclick="this.parentElement.style.display='none'" class="mt-4 text-xs text-amber-500 underline">დახურვა</button>
    </div>

    <script>
        function showInfo(title, text) {
            const card = document.getElementById('infoCard');
            document.getElementById('infoTitle').innerText = title;
            document.getElementById('infoText').innerText = text;
            card.style.display = 'block';
            card.classList.add('animate__animated', 'animate__fadeInUp');
        }

        // ხაზების ავტომატური გაყვანა წერტილებს შორის (კონსტელაციის ეფექტი)
        function drawLines() {
            const points = document.querySelectorAll('.point');
            const container = document.getElementById('container');
            
            for (let i = 0; i < points.length - 1; i++) {
                const p1 = points[i].getBoundingClientRect();
                const p2 = points[i+1].getBoundingClientRect();
                
                const x1 = p1.left + p1.width/2;
                const y1 = p1.top + p1.height/2;
                const x2 = p2.left + p2.width/2;
                const y2 = p2.top + p2.height/2;
                
                const length = Math.sqrt(Math.pow(x2-x1, 2) + Math.pow(y2-y1, 2));
                const angle = Math.atan2(y2-y1, x2-x1) * 180 / Math.PI;
                
                const line = document.createElement('div');
                line.className = 'line';
                line.style.width = length + 'px';
                line.style.left = x1 + 'px';
                line.style.top = y1 + 'px';
                line.style.transform = `rotate(${angle}deg)`;
                
                container.appendChild(line);
            }
        }

        window.onload = drawLines;
        window.onresize = () => {
            document.querySelectorAll('.line').forEach(l => l.remove());
            drawLines();
        };
    </script>
</body>
</html>
