<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Chúc mừng sinh nhật!</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-image: url('https://copilot.microsoft.com/th/id/BCO.63036954-13b1-4302-a39f-69c67342cf9e.png');
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      color: white;
    }

    .gift-box {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
    }

    .gift-box img {
      width: 200px;
      animation: bounce 1s infinite;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }

    .gift-box button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1.2em;
      background-color: #ff4081;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    .container {
      display: none;
      padding: 50px;
      background-color: rgba(0, 0, 0, 0.5);
      border-radius: 20px;
      margin: 50px auto;
      max-width: 600px;
    }

    h1 {
      font-size: 3em;
      color: #ffccff;
    }

    p {
      font-size: 1.5em;
      margin-bottom: 30px;
    }

    button.show-hearts {
      padding: 10px 20px;
      font-size: 1.2em;
      background-color: #ff4081;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
    }

    img.profile {
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 50%;
      border: 4px solid #fff;
      box-shadow: 0 0 10px rgba(255,255,255,0.5);
      margin-bottom: 20px;
    }

    audio {
      margin-top: 30px;
    }
  </style>
</head>
<body>

  <!-- Hộp quà -->
  <div class="gift-box" id="giftBox">
    
    <br>
    <button onclick="openGift()">Mở hộp quà 🎁</button>
  </div>

  <!-- Nội dung sinh nhật -->
  <div class="container" id="birthdayContent">
    <h1>🎂 Chúc mừng sinh nhật!</h1>
    <img src="c:\Users\ADMIN\Downloads\lan anh.jpg" alt="Người nhận" class="profile">
    <p>Chúc bạn một ngày thật vui vẻ, tràn đầy hạnh phúc và tiếng cười!</p>
    <button class="show-hearts" onclick="showHearts()">Bắn tim 💖</button>
    <audio controls autoplay loop>
      <source src="c:\Users\ADMIN\Downloads\SEB_3.8_WIN-20241008T014124Z-001\Khuc Hat Mung Sinh Nhat - Phan Dinh Tung - NhacHayVN.mp3" type="audio/mpeg">
      Trình duyệt của bạn không hỗ trợ phát nhạc.
    </audio>
    <canvas id="heartCanvas"></canvas>
  </div>

  <script>
    function openGift() {
      document.getElementById('giftBox').style.display = 'none';
      document.getElementById('birthdayContent').style.display = 'block';
    }

    function showHearts() {
      const canvas = document.getElementById('heartCanvas');
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      const ctx = canvas.getContext('2d');

      const hearts = [];
      for (let i = 0; i < 100; i++) {
        hearts.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          size: Math.random() * 20 + 10,
          speed: Math.random() * 2 + 1,
          color: `hsl(${Math.random() * 360}, 100%, 70%)`
        });
      }

      function drawHeart(x, y, size, color) {
        ctx.save();
        ctx.translate(x, y);
        ctx.scale(size / 100, size / 100);
        ctx.beginPath();
        ctx.moveTo(75, 40);
        ctx.bezierCurveTo(75, 37, 70, 25, 50, 25);
        ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5);
        ctx.bezierCurveTo(20, 80, 40, 102, 75, 120);
        ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5);
        ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25);
        ctx.bezierCurveTo(85, 25, 75, 37, 75, 40);
        ctx.closePath();
        ctx.fillStyle = color;
        ctx.fill();
        ctx.restore();
      }

      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        hearts.forEach(h => {
          drawHeart(h.x, h.y, h.size, h.color);
        });
        update();
      }

      function update() {
        hearts.forEach(h => {
          h.y += h.speed;
          if (h.y > canvas.height) {
            h.y = 0;
            h.x = Math.random() * canvas.width;
          }
        });
      }

      setInterval(draw, 30);
    }
  </script>
</body>
</html>
