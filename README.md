<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AYA WORLD ❤️</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&family=Dancing+Script:wght@700&display=swap');

        :root {
            --primary: #ff4d6d;
            --accent: #00d4ff;
            --dark-bg: #0d0118;
            --glass: rgba(255, 255, 255, 0.08);
            --glow: rgba(255, 77, 109, 0.4);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Tajawal', sans-serif;
            background-color: var(--dark-bg);
            color: white;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        #bg-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; }

        #login-screen {
            position: fixed; inset: 0; background: var(--dark-bg);
            display: flex; justify-content: center; align-items: center; z-index: 10000;
            transition: 1s ease-in-out;
        }

        .login-card {
            background: var(--glass); backdrop-filter: blur(25px);
            padding: 50px 30px; border-radius: 40px; text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.15); width: 90%; max-width: 400px;
        }

        input[type="text"], input[type="password"], textarea {
            width: 100%; padding: 15px; border-radius: 15px; 
            border: 2px solid rgba(255,255,255,0.1);
            background: rgba(255, 255, 255, 0.05); color: white; 
            text-align: center; font-size: 1.1rem;
            margin-bottom: 10px; outline: none; transition: 0.3s;
        }

        .btn-main {
            background: linear-gradient(45deg, var(--primary), #ff758c);
            color: white; border: none; padding: 15px 30px; border-radius: 15px;
            cursor: pointer; font-weight: bold; width: 100%; font-size: 1.1rem;
            transition: 0.3s; margin-top: 10px; box-shadow: 0 5px 15px rgba(255, 77, 109, 0.3);
        }

        #main-content { display: none; opacity: 0; transition: 1s opacity; }

        section { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 60px 20px; }

        .glass-box {
            background: var(--glass); backdrop-filter: blur(15px);
            border-radius: 25px; padding: 30px; border: 1px solid rgba(255,255,255,0.1);
            width: 100%; max-width: 700px; text-align: center; margin-bottom: 30px;
        }

        .timer-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-top: 25px; }
        .timer-unit { background: rgba(255, 255, 255, 0.03); border-radius: 18px; padding: 15px 5px; border: 1px solid rgba(255, 255, 255, 0.05); }
        .timer-val { font-size: 2.5rem; font-weight: 700; font-family: 'Dancing Script', cursive; color: var(--primary); text-shadow: 0 0 15px var(--glow); display: block; }
        .timer-label { font-size: 0.8rem; color: #ddd; opacity: 0.7; font-weight: bold; }

        .promise-container { width: 100%; max-width: 500px; margin: 25px auto 0; display: flex; flex-direction: column; gap: 12px; }
        .promise-row { background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1); padding: 12px 20px; border-radius: 18px; display: flex; justify-content: space-between; align-items: center; }

        .video-container { width: 100%; max-width: 600px; border-radius: 20px; margin: 25px auto; border: 2px solid var(--primary); overflow: hidden; }
        video { width: 100%; display: block; }

        .gallery { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; width: 100%; max-width: 1200px; }
        .photo-card-wrap { position: relative; }
        .photo-card { height: 400px; perspective: 1000px; }
        .photo-inner { width: 100%; height: 100%; transition: transform 0.7s; transform-style: preserve-3d; cursor: pointer; }
        .photo-card.flipped .photo-inner { transform: rotateY(180deg); }
        .face { position: absolute; width: 100%; height: 100%; backface-visibility: hidden; border-radius: 20px; overflow: hidden; border: 2px solid var(--primary); }
        .face img { width: 100%; height: 100%; object-fit: cover; }
        .face.back { background: linear-gradient(135deg, #1a022d, var(--primary)); transform: rotateY(180deg); display: flex; align-items: center; justify-content: center; padding: 20px; text-align: center; }

        .delete-btn { position: absolute; top: 10px; right: 10px; background: var(--primary); color: white; border: none; width: 35px; height: 35px; border-radius: 50%; cursor: pointer; z-index: 100; font-weight: bold; display: flex; justify-content: center; align-items: center; font-size: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }

        #love-msg-box { display: none; margin-top: 40px; border: 2px solid var(--accent); text-align: right; }
        
        #toast-container { position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%); z-index: 20000; }
        .toast { background: rgba(255, 255, 255, 0.1); backdrop-filter: blur(15px); border: 1px solid var(--primary); color: white; padding: 12px 25px; border-radius: 50px; margin-top: 10px; animation: slideUp 0.5s forwards; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .file-upload-label { display: block; background: rgba(255,255,255,0.1); padding: 15px; border-radius: 15px; border: 2px dashed var(--primary); cursor: pointer; margin-bottom: 10px; }

        .heart-particle { position: fixed; top: -20px; color: var(--primary); pointer-events: none; z-index: 9999; animation: fall linear forwards; }
        @keyframes fall { to { transform: translateY(105vh) rotate(360deg); opacity: 0; } }

        footer { padding: 40px; text-align: center; opacity: 0.5; font-family: 'Dancing Script', cursive; font-size: 1.5rem; }
    </style>
</head>
<body>

    <canvas id="bg-canvas"></canvas>
    <div id="toast-container"></div>

    <div id="login-screen">
        <div class="login-card">
            <h2 style="font-family:'Dancing Script'; font-size: 3rem; color: var(--primary);">Just for AYA ❤️</h2>
            <input type="text" id="pass" placeholder="اكتبي الباسورد">
            <button class="btn-main" onclick="unlock()">فتح الأبواب ❤️</button>
            <p id="error-msg" style="display:none; color: red; margin-top: 10px;">ركزي يا آية ❤️</p>
        </div>
    </div>

    <div id="main-content">
        <section>
            <div class="glass-box">
                <h3 style="margin-bottom: 15px;">حكايتنا مستمرة من... 🕰️</h3>
                <div class="timer-grid">
                    <div class="timer-unit"><span class="timer-val" id="days">00</span><span class="timer-label">يوم</span></div>
                    <div class="timer-unit"><span class="timer-val" id="hours">00</span><span class="timer-label">ساعة</span></div>
                    <div class="timer-unit"><span class="timer-val" id="minutes">00</span><span class="timer-label">دقيقة</span></div>
                    <div class="timer-unit"><span class="timer-val" id="seconds">00</span><span class="timer-label">ثانية</span></div>
                </div>
            </div>

            <div class="glass-box">
                <h1 style="font-family:'Dancing Script'; font-size: 3rem; color: var(--primary);">Together Forever</h1>
                <div class="video-container">
                    <video id="main-video" controls playsinline loop>
                        <source src=" https://www.image2url.com/r2/default/videos/1777854804288-d8be3b82-04f5-45ac-857d-fccb129fd8b8.mov" type="video/mp4">
                    </video>
                </div>
                <div class="promise-container">
                    <div class="promise-row"><span>هفضل سندك في كل وقت</span><span>🤝</span></div>
                    <div class="promise-row"><span>هكون دايماً أمانك وضحكتك</span><span>🛡️</span></div>
                    <div class="promise-row"><span>حبنا ملوش نهاية.. وعد</span><span>♾️</span></div>
                </div>
            </div>
        </section>

        <section>
            <h2 style="margin-bottom:40px; color:var(--accent); font-size: 2.2rem;"> وعودي ليكي (اضغطي عليهم) 📸</h2>
            <div class="gallery" id="main-gallery"></div>

            <button class="btn-main" style="max-width: 280px; margin-top: 50px;" onclick="revealLoveMsg()">المفاجأة الأخيرة 💌</button>
            <div id="love-msg-box" class="glass-box">
                <div id="typing-text" style="font-size:1.2rem; line-height:1.8; white-space: pre-wrap;"></div>
            </div>

            <div class="glass-box" style="margin-top:100px; width: 100%; max-width: 600px;">
                <h3 style="margin-bottom:20px; color:var(--accent);">إضافة ذكرى جديدة ✨</h3>
                <label for="new-img-file" class="file-upload-label" id="file-label">اضغطي هنا لرفع صورة 📸</label>
                <input type="file" id="new-img-file" accept="image/*" style="display:none;" onchange="updateFileName()">
                <textarea id="new-img-text" rows="2" placeholder="اكتبي كلمة حلوة لظهر الصورة..."></textarea>
                <button class="btn-main" onclick="addNewMemory()">إضافة وحفظ للأبد ❤️</button>
            </div>
            
            <footer>designed for aya</footer>
        </section>
    </div>

    <script>
        // تم تغيير التاريخ إلى 22 فبراير 2026
        const startDate = new Date("2026-02-22T00:00:00");
        const loveMsg = "يا آية.. يا أغلى إنسانة في حياتي..\n\nبمناسبة العيد، بكتب لك الكلام ده عشان يفضل شاهد على كل اللي جوايا ليكي. أنا النهاردة مش بس بحتفل بالعيد ، أنا بحتفل بوجودك اللي خلى لحياتي طعم ومعنى تانى خالص.\n\nأنا عاوزك تتأكدي إنك 'حبي الأخير'، إنتي النهاية السعيدة اللي كنت بتمناها، والمحطة اللي اكتفيت بيها عن العالم كله. من ساعة ما دخلتي حياتي وأنا بقيت حاسس إن ربنا راضي عني بجد، وخلاكي رزقي وسندي اللي ملوش مثيل.\n\nعاوز أوعدك النهاردة، زي ما وعدتك قبل كده، إني هفضل طول عمري سندك وضهرك اللي مش بيميل أبدًا. أنا الحيطة اللي تسندي عليها وإنتي مطمنة، وأنا الأمان اللي هترجعي له دايماً من أي تعب أو خوف. مستعد أضحي بكل غالي وعزيز، وأقف قدام أي ظرف في الدنيا دي، بس عشان نفضل سوا وعشان أشوف ضحكتك اللي بترد فيا الروح.\n\nإنتي مش بس حبيبتي، إنتي شريكة حلمي، والسبب اللي بيخليني عاوز أكون أحسن واحد في الدنيا عشانك. أوعدك إني مش هسيب إيدك أبدًا مهما حصل، وهفضل أتحمل المستحيل عشان خاطر عيونك. هكون جنبك في المُر قبل الحلو، وهشيل عنك تعبك قبل تعبي، وهفضل لآخر نَفَس في عمري أثبت لك إنك أغلى حاجة عندي في الكون.\n\nكل سنة وإنتي حبيبتي وست البنات وحبي الأخير والوحيد. ❤️🌹";

        const baseImages = [
            {img: "https://image2url.com/r2/default/images/1770415998189-80d9be10-a572-49b0-9940-ab14a3844ded.jpeg", txt: "وعدتِك وبوفّي.. هفضل دايماً سندِك في كل خطوة ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416046006-8d812174-6c13-4b91-9d66-fa6db04ca889.jpeg", txt: "وجودك في حياتي هو أكبر وأجمل نعمة ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416084353-646f426e-d927-467e-9caf-906fee2ffb8c.jpeg", txt: "إنتي العمر اللي بدأت أعيشه بجد ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416820462-f991316b-6630-4309-817e-1d10cc3c158f.jpeg", txt: "كل يوم بيعدي وإحنا سوا هو عيد ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416847490-e8f9cd3c-7ce0-4434-b1a5-aff2eedf2b5a.jpeg", txt: "ضحكتك هي اللي بتنور لي الدنيا ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416870899-a7017a5d-f299-4e51-b78e-afd3a1ab756d.jpeg", txt: "مفيش كلام يوصف حبي ليكي ❤️"},
            {img: "https://image2url.com/r2/default/images/1770416892614-77dc752c-50de-46e8-b4c5-1da06fa06419.jpeg", txt: "إنتي ملكة قلبي وحبيبتي الوحيدة ❤️"}
        ];

        function showToast(message) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = 'toast'; toast.innerHTML = `✨ ${message}`;
            container.appendChild(toast);
            setTimeout(() => toast.remove(), 3000);
        }

        function unlock() {
            if(document.getElementById('pass').value === '22/2') {
                document.getElementById('main-video').play().catch(() => {});
                updateTimeline(); 
                document.getElementById('login-screen').style.transform = 'translateY(-100%)';
                setTimeout(() => {
                    document.getElementById('login-screen').style.display = 'none';
                    document.getElementById('main-content').style.display = 'block';
                    setTimeout(() => document.getElementById('main-content').style.opacity = '1', 50);
                    initGallery();
                    startHeartsRain();
                    setInterval(updateTimeline, 1000);
                }, 1000);
            } else { document.getElementById('error-msg').style.display = 'block'; }
        }

        function updateTimeline() {
            const diff = new Date() - startDate;
            const absoluteDiff = Math.abs(diff);
            const d = Math.floor(absoluteDiff / 86400000);
            const h = Math.floor((absoluteDiff / 3600000) % 24);
            const m = Math.floor((absoluteDiff / 60000) % 60);
            const s = Math.floor((absoluteDiff / 1000) % 60);
            
            document.getElementById('days').innerText = d.toString().padStart(2, '0');
            document.getElementById('hours').innerText = h.toString().padStart(2, '0');
            document.getElementById('minutes').innerText = m.toString().padStart(2, '0');
            document.getElementById('seconds').innerText = s.toString().padStart(2, '0');
        }

        function initGallery() {
            const gallery = document.getElementById('main-gallery');
            gallery.innerHTML = '';
            baseImages.forEach(data => renderCard(data, false));
            JSON.parse(localStorage.getItem('aya_memories') || '[]').forEach(data => renderCard(data, true));
        }

        function renderCard(data, isDeletable) {
            const wrap = document.createElement('div');
            wrap.className = 'photo-card-wrap';
            if(data.id) wrap.id = "wrap-" + data.id;
            wrap.innerHTML = `
                ${isDeletable ? `<button class="delete-btn" onclick="deleteMemory(${data.id})">×</button>` : ''}
                <div class="photo-card" onclick="this.classList.toggle('flipped')">
                    <div class="photo-inner">
                        <div class="face front"><img src="${data.image || data.img}"></div>
                        <div class="face back"><h3>${data.text || data.txt} ❤️</h3></div>
                    </div>
                </div>
            `;
            document.getElementById('main-gallery').appendChild(wrap);
        }

        function addNewMemory() {
            const fileInput = document.getElementById('new-img-file');
            const textInput = document.getElementById('new-img-text');
            if (!fileInput.files[0] || !textInput.value.trim()) { showToast("اختاري صورة وكلمة حلوة ❤️"); return; }
            
            const reader = new FileReader();
            reader.onload = (e) => {
                const img = new Image(); img.src = e.target.result;
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    const maxW = 800; const scale = maxW / img.width;
                    canvas.width = maxW; canvas.height = img.height * scale;
                    canvas.getContext('2d').drawImage(img, 0, 0, canvas.width, canvas.height);
                    const newMem = { id: Date.now(), image: canvas.toDataURL('image/jpeg', 0.7), text: textInput.value };
                    let memories = JSON.parse(localStorage.getItem('aya_memories') || '[]');
                    memories.push(newMem);
                    localStorage.setItem('aya_memories', JSON.stringify(memories));
                    renderCard(newMem, true); showToast("تم الحفظ بنجاح! ❤️");
                    fileInput.value = ''; textInput.value = '';
                    document.getElementById('file-label').innerText = "اضغطي هنا لرفع صورة 📸";
                };
            };
            reader.readAsDataURL(fileInput.files[0]);
        }

        function deleteMemory(id) {
            if(confirm("حذف الذكرى؟ ❤️")) {
                let memories = JSON.parse(localStorage.getItem('aya_memories') || '[]');
                localStorage.setItem('aya_memories', JSON.stringify(memories.filter(m => m.id !== id)));
                document.getElementById("wrap-" + id).remove();
                showToast("تم الحذف! 🗑️");
            }
        }

        let charIdx = 0;
        function revealLoveMsg() {
            const box = document.getElementById('love-msg-box');
            box.style.display = 'block';
            if(charIdx === 0) typeEffect();
            box.scrollIntoView({ behavior: 'smooth' });
        }

        function typeEffect() {
            if(charIdx < loveMsg.length) {
                let char = loveMsg.charAt(charIdx);
                document.getElementById('typing-text').innerHTML += char === "\n" ? "<br>" : char;
                charIdx++;
                setTimeout(typeEffect, 40);
            }
        }

        function updateFileName() {
            const file = document.getElementById('new-img-file').files[0];
            if(file) document.getElementById('file-label').innerText = "تم اختيار: " + file.name;
        }

        function startHeartsRain() {
            setInterval(() => {
                const heart = document.createElement('div'); heart.innerHTML = '❤️';
                heart.className = 'heart-particle'; heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDuration = Math.random() * 3 + 2 + 's';
                document.body.appendChild(heart); setTimeout(() => heart.remove(), 5000);
            }, 300);
        }

        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let pts = [];
        function resize() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        window.onresize = resize; resize();
        for(let i=0; i<50; i++) pts.push({x: Math.random()*canvas.width, y: Math.random()*canvas.height, vx: Math.random()*0.5-0.25, vy: Math.random()*0.5-0.25});
        function anim() {
            ctx.clearRect(0,0,canvas.width, canvas.height); ctx.fillStyle = "rgba(255, 77, 109, 0.2)";
            pts.forEach(p => {
                p.x += p.vx; p.y += p.vy;
                if(p.x<0 || p.x>canvas.width) p.vx*=-1; if(p.y<0 || p.y>canvas.height) p.vy*=-1;
                ctx.beginPath(); ctx.arc(p.x, p.y, 2, 0, Math.PI*2); ctx.fill();
            });
            requestAnimationFrame(anim);
        }
        anim();
    </script>
</body>
</html>
