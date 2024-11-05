<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.plyr.io/3.6.8/plyr.css" />
    <title>مشغل Plyr.io مع خيارات دقة</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            background-color: #222;
            color: #fff;
        }
        input, button, select {
            padding: 10px;
            margin: 10px;
            width: 300px;
            border-radius: 5px;
            border: none;
        }
        button {
            background-color: #3498db;
            color: #fff;
            cursor: pointer;
        }
        button:hover {
            background-color: #2980b9;
        }
        #playerContainer {
            width: 100%;
            max-width: 640px;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>مشغل Plyr.io مع خيارات دقة</h1>

    <input type="text" id="videoCode" placeholder="أدخل كود الفيديو (مثل 1026280260)" />
    <button onclick="loadVideo()">تحميل الفيديو</button>

    <label for="qualitySelect">اختر الدقة:</label>
    <select id="qualitySelect">
        <option value="360p">360p</option>
        <option value="720p">720p</option>
        <option value="1080p">1080p</option>
    </select>

    <div id="playerContainer">
        <video id="player" controls crossorigin playsinline></video>
    </div>

    <script src="https://cdn.plyr.io/3.6.8/plyr.polyfilled.js"></script>
    <script>
        const player = new Plyr('#player');

        function loadVideo() {
            const videoCode = document.getElementById('videoCode').value.trim();
            const quality = document.getElementById('qualitySelect').value;

            if (videoCode) {
                // تحويل كود الفيديو مع الدقة المحددة
                let videoUrl;
                switch (quality) {
                    case '360p':
                        videoUrl = `https://player.vimeo.com/video/${videoCode}?quality=360p`;
                        break;
                    case '720p':
                        videoUrl = `https://player.vimeo.com/video/${videoCode}?quality=720p`;
                        break;
                    case '1080p':
                        videoUrl = `https://player.vimeo.com/video/${videoCode}?quality=1080p`;
                        break;
                    default:
                        videoUrl = `https://player.vimeo.com/video/${videoCode}`;
                        break;
                }

                player.source = {
                    type: 'video',
                    sources: [{
                        src: videoUrl,
                        provider: 'vimeo'
                    }]
                };
            } else {
                alert("يرجى إدخال كود الفيديو.");
            }
        }
    </script>
</body>
</html>
