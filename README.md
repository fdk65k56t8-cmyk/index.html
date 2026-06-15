<!DOCTYPE html>
<html lang="sr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kamera + Download</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      margin-top: 30px;
    }
    video {
      width: 320px;
      border-radius: 10px;
    }
    button {
      padding: 12px 18px;
      font-size: 18px;
      margin-top: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h2>Kamera aplikacija 📸</h2>

  <video id="video" autoplay playsinline></video>
  <br>

  <button id="snap">Klikni me</button>

  <canvas id="canvas" style="display:none;"></canvas>

  <script>
    const video = document.getElementById("video");
    const canvas = document.getElementById("canvas");
    const snap = document.getElementById("snap");

    // start kamera
    navigator.mediaDevices.getUserMedia({ video: true })
      .then(stream => {
        video.srcObject = stream;
      })
      .catch(err => {
        alert("Kamera nije dozvoljena: " + err);
      });

    snap.addEventListener("click", () => {
      const ctx = canvas.getContext("2d");

      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;

      ctx.drawImage(video, 0, 0);

      const imageData = canvas.toDataURL("image/png");

      // napravi download
      const link = document.createElement("a");
      link.href = imageData;
      link.download = "selfie.png";
      link.click();
    });
  </script>

</body>
</html>