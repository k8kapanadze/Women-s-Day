<!DOCTYPE html>
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ჩვენი ვარსკვლავების რუკა | La La Land</title>
    
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=Fira+Go:wght@300;400;700&display=swap');

        body, html { margin: 0; padding: 0; height: 100%; font-family: 'Fira Go', sans-serif; background: #0a0e1a; }
        h1 { font-family: 'Playfair Display', serif; }

        /* რუკის სტილი - მუქი ფილტრი */
        #map { 
            width: 100%; 
            height: 100vh; 
            background: #0a0e1a;
            filter: invert(100%) hue-rotate(180deg) brightness(95%) contrast(90%);
        }

        /* ვარსკვლავის მარკერის სტილი */
        .custom-star {
            background: #f3cc4d;
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            box-shadow: 0 0 15px #f3cc4d;
            width: 30px !important;
            height: 30px !important;
            border: none;
        }

        /* მილოცვის ფანჯარა (Pop-up) */
        .leaflet-popup-content-wrapper {
            background: #161b2e;
            color: #f3cc4d;
            border: 1px solid #f3cc4d;
            border-radius: 15px;
            font-family: 'Fira Go', sans-serif;
        }
        .leaflet-popup-tip { background: #161b2e; border: 1px solid #f3cc4d; }

        .header-overlay {
            position: absolute;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            text-align: center;
            pointer-events: none;
            width: 100%;
        }
    </style>
</head>
<body>

    <div class="header-overlay">
        <h1 class="text-4xl md:text-5xl text-amber-400 drop-shadow-lg animate__animated animate__fadeInDown">Our Map of Stars</h1>
        <p class="text-slate-300 tracking-widest uppercase text-xs mt-2 bg-black/40 inline-block px-4 py-1 rounded-full">მოგზაურობა ჩვენს მოგონებებში</p>
    </div>

    <div id="map"></div>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // რუკის ინიციალიზაცია (კოორდინატები დაყენებულია თბილისზე, როგორც მაგალითი)
        var map = L.map('map', {
            zoomControl: false 
        }).setView([41.7151, 44.8271], 14); 

        // რუკის ვიზუალური შრე (CartoDB Dark Matter)
        L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
            attribution: '© OpenStreetMap'
        }).addTo(map);

        // მოგონებების მონაცემები
        const points = [
            {
                lat: 41.7100, lng: 44.8200,
                title: "პირველი შეხვედრა",
                text: "აქ ყველაფერი დაიწყო... შენი ღიმილი და პირველი 'გამარჯობა'.",
                icon: "✨"
            },
            {
                lat: 41.7200, lng: 44.8350,
                title: "ჩვენი საყვარელი კაფე",
                text: "ყველაზე გემრიელი ყავა და დაუსრულებელი საუბრები ჯაზზე.",
                icon: "☕"
            },
            {
                lat: 41.7050, lng: 44.8000,
                title: "ღამის გასეირნება",
                text: "ამ ხედიდან ქალაქი ისეთივე ლამაზი ჩანდა, როგორც შენ.",
                icon: "🌙"
            }
        ];

        // მარკერების დამატება
        points.forEach(point => {
            var starIcon = L.divIcon({
                className: 'custom-star animate__animated animate__pulse animate__infinite',
                iconSize: [30, 30]
            });

            L.marker([point.lat, point.lng], {icon: starIcon})
                .addTo(map)
                .bindPopup(`
                    <div style="text-align:center; padding:10px;">
                        <span style="font-size:24px;">${point.icon}</span>
                        <h3 style="margin:10px 0; font-weight:bold; font-size:18px;">${point.title}</h3>
                        <p style="font-size:14px; color:#cbd5e1; font-style:italic;">${point.text}</p>
                    </div>
                `);
        });

        // რუკის ცენტრის ავტომატური გასწორება მობილურზე
        map.on('click', function() {
            // ინტერაქციისთვის
        });
    </script>
</body>
</html>
