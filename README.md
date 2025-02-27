# Try
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تست تشخیص چهره</title>
    <script src="https://cdn.jsdelivr.net/npm/face-api.js"></script>
</head>
<body>
    <h1>تست تشخیص چهره</h1>
    <video id="video" autoplay playsinline></video>
    <p id="status">منتظر تشخیص چهره...</p>

    <script>
        async function startFaceDetection() {
            try {
                const video = document.getElementById('video');
                const stream = await navigator.mediaDevices.getUserMedia({ video: true });
                video.srcObject = stream;

                await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/face-api.js/weights/');

                setInterval(async () => {
                    const detections = await faceapi.detectAllFaces(video, new faceapi.TinyFaceDetectorOptions());
                    
                    if (detections.length > 0) {
                        document.getElementById('status').innerText = "✅ چهره شناسایی شد!";
                    } else {
                        document.getElementById('status').innerText = "❌ چهره‌ای شناسایی نشد!";
                    }
                }, 3000);
            } catch (error) {
                console.error("🚨 خطا در تشخیص چهره:", error);
                document.getElementById('status').innerText = "🚨 امکان تشخیص چهره وجود ندارد!";
            }
        }

        startFaceDetection();
    </script>
</body>
</html>
