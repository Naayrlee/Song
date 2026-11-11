<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>รักให้เธอได้รู้</title>
    <style>
        /* ตกแต่งหน้าเว็บไซต์ */
        body {
            background-color: #101010;
            color: white;
            font-family: monospace;
            padding: 40px;
        }
        h1 {
            color: #d8a4ff;
        }
        #lyrics {
            margin-top: 40px;
            font-size: 20px;
            line-height: 2.5;
        }
        .line {
            opacity: 0;
            animation: fadeIn 1s forwards;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        button {
            padding: 12px 25px;
            background: #d8a4ff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <h1>Song For You ♡</h1>
    <p>เพลงนี้อยากให้เธอลองฟัง...</p>

    <button id="playButton">เริ่มฟังเพลง</button>
    <audio id="song">
        <source src="https://naayrlee.github.io/Song/%E0%B8%A3%E0%B8%B1%E0%B8%81%E0%B9%83%E0%B8%AB%E0%B9%89%E0%B9%80%E0%B8%98%E0%B8%AD%E0%B9%84%E0%B8%94%E0%B9%89%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B9%80%E0%B8%99%E0%B8%B7%E0%B9%89%E0%B8%AD%E0%B9%80%E0%B8%9E%E0%B8%A5%E0%B8%87.mp4">
    </audio>
    <div id="lyrics"></div>
    <script>

        // 1. เรียกใช้งาน Element
        const song = document.getElementById("song");
        const lyricsBox = document.getElementById("lyrics");
        const playButton = document.getElementById("playButton");

        // 2. กำหนดเนื้อเพลงและเวลาที่ต้องการให้ปรากฏ
        const lyrics = [
            { time: 0.5, text: "แค่อยากให้เธอรู้" },
            { time: 2.5, text: "ความรักมันเป็นอย่างไร" },
            { time: 4.5, text: "ให้เธอมองทางนี้" },
            { time: 6, text: "baby look into my eyes" },
            { time: 8.5, text: "Baby come get your love" },
            { time: 10.5, text: "ให้ฉัน get you the world" },
            { time: 12.5, text: "โลกที่เหมือนฝันละเมอ" },
            { time: 14.5, text: "โลกที่เธอไม่คิดว่าจะได้เจอ..." },
            { time: 18, text: "ถ้าเธอยังสงสัยว่า" },
            { time: 20, text: "ความรักหน้าตาเป็นไง" },
            { time: 22.5, text: "ก่อนที่เธอจะไป" },
            { time: 24.5, text: "ขอให้มันเป็นฉันได้ไหม" },
            { time: 26.5, text: "คนที่รักเธอและ" },
            { time: 28, text: "คนที่เธอเปิด" },
            { time: 30.5, text: "ให้ฉันรักให้เธอได้รู้..." },
             { time: 32.5, text: "===== ♡ =====" }
        ];

        // 3. เก็บจำนวนบรรทัดที่แสดงแล้ว
        let currentLine = 0;

        // 4. เริ่มเล่นเพลง
        playButton.addEventListener("click", async () => {
            try {
                await song.play();
                playButton.textContent = "กำลังฟัง ♫";
            } catch (error) {
                console.log("ไม่สามารถเล่นเพลงได้", error);
            }
        });
        // 5. ตรวจสอบเวลาเพลง
        song.addEventListener("timeupdate", () => {
            while (
                currentLine < lyrics.length &&
                song.currentTime >= lyrics[currentLine].time
            ) {
                // สร้าง Element สำหรับเนื้อเพลง
                const line = document.createElement("div");
                line.className = "line";
                line.textContent = lyrics[currentLine].text;
                // เพิ่มเนื้อเพลงลงในหน้าเว็บ
                lyricsBox.appendChild(line);
                // ไปยังเนื้อเพลงบรรทัดถัดไป
                currentLine++;
            }
        });
        // 6. เมื่อเพลงจบ
        song.addEventListener("ended", () => {
            playButton.textContent = "ทำเพลงจีบแล้วนะ♡";
        });

    </script>

</body>
</html>
