# love-glitch
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>(r)ii - [mn]</title>
  <style>
    body {
      background-color: #000;
      color: #fff;
      font-family: 'Fira Code', monospace;
      overflow-x: hidden;
      padding: 40px;
    }
    .line {
      position: absolute;
      opacity: 0;
      transition: all 1.5s ease;
    }
    .active .line {
      opacity: 1;
    }
    .line.ordered {
      position: relative !important;
      top: auto !important;
      left: auto !important;
      transform: none !important;
      margin-bottom: 12px;
    }
    .glitch-r {
      color: #ff4444;
      animation: bounce 1s infinite alternate;
    }
    .glitch-m {
      color: #44ffff;
      animation: bounce 1.3s infinite alternate;
    }
    .glitch-n {
      color: #66ff66;
      animation: bounce 1.1s infinite alternate;
    }
    @keyframes bounce {
      0% { transform: translateY(0); }
      100% { transform: translateY(-5px); }
    }
    .numbers {
      animation: blink 0.4s 5 alternate;
      color: #ccc;
    }
    @keyframes blink {
      0% { opacity: 0.2; }
      100% { opacity: 1; }
    }
    .flash {
      animation: flash 2s infinite;
    }
    @keyframes flash {
      0%, 100% { color: #fff; }
      50% { color: #ff0; }
    }
    .container {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0.2);
      transition: all 2s ease;
    }
    .container.reveal {
      transform: translate(0, 0) scale(1);
      position: relative;
      top: auto;
      left: auto;
    }
    #unlock-section {
      text-align: center;
      margin-bottom: 40px;
    }
    #reveal-btn {
      background: none;
      color: #fff;
      border: 1px solid #fff;
      padding: 10px 20px;
      cursor: pointer;
      font-family: inherit;
      font-size: 1rem;
    }
    input[type="password"] {
      padding: 5px;
      font-size: 1rem;
      font-family: inherit;
      background: #111;
      border: 1px solid #555;
      color: #fff;
    }
    .hidden { display: none; }
  </style>
</head>
<body>
  <div id="unlock-section">
    <p>nhập mật mã để giải mã hỗn độn:</p>
    <input type="password" id="password" placeholder="*********">
    <button id="reveal-btn">giải mã hỗn độn</button>
  </div>
  <div class="container hidden" id="poem"></div>
  <script>
    const btn = document.getElementById('reveal-btn');
    const poem = document.getElementById('poem');
    const passwordInput = document.getElementById('password');
    const unlockSection = document.getElementById('unlock-section');

    const lines = [
      "bản sắc hợp nhân tính, <span class='glitch-r'>(r)</span> đinh ninh <span class='glitch-n'>[n]</span> và <span class='glitch-m'>[m]</span> là hai cá thể",
      "chung dải cộng hưởng nhưng phân lớp theo nhịp thở,",
      "một lồi ra theo đồ thị tuyến tính,",
      "một lõm vào như sóng âm đập vỡ đầu cơn mưa.",
      "<span class='numbers' id='seq'>0101—delta—0001—gamma—</span>",
      "chúng trôi theo luồng tín hiệu như gió trong miền băng giá,",
      "cái gọi là khác biệt bị render lại bằng hệ tọa âm rối rắm đa pha.",
      "<span class='glitch-n'>[n]</span>: kết quả của một phép chập tuyến thời,",
      "dễ hiểu như đường tích lũy không có nhiễu.",
      "<span class='glitch-m'>[m]</span> thì ẩn: một dạng sóng đứng trong vùng phiểu",
      "biểu hiện trễ 0.3 giây khi não người cố nghe hiểu,",
      "tần số vượt 12.5Hz,",
      "<span class='glitch-r'>[r]</span> co lại như bề mặt lưới xếp trong không-thời gian lỗi,",
      "mỗi lần rung là một lần dữ liệu bóp méo lịch sử-",
      "<span class='flash'>ver. 5.23.011-bản vá phụ âm môi mới nổi:</span>",
      "bổ sung giao diện xúc cảm cho phần tử labial,",
      "nơi từng cú phát âm nay rát bỏng, mềm như ngón tay thổi lửa vào đầu.",
      "minimo, hoặc <span class='glitch-r'>(r)</span>nimo, hoặc cả hai:",
      "<span class='flash'>là một superposition dạng schrödinger,</span>",
      "vừa <span class='glitch-n'>[n]</span>, vừa <span class='glitch-m'>[m]</span>, vừa đang loading giữa hai tầng meaning.",
      "collapse chỉ xảy ra khi waveform dội vào tai người,",
      "và ngay khi nó chạm, entropy bảo toàn,",
      "song định nghĩa, lại tự gãy răng trong vùng ý thức chưa khởi."
    ];

    btn.addEventListener('click', () => {
      if (passwordInput.value === '12345') {
        unlockSection.classList.add('hidden');
        poem.classList.remove('hidden');
        poem.classList.add('reveal');

        lines.forEach((text, i) => {
          const div = document.createElement('div');
          div.className = 'line';
          div.style.top = `${Math.random() * 80}vh`;
          div.style.left = `${Math.random() * 80}vw`;
          div.innerHTML = text;
          poem.appendChild(div);
        });

        setTimeout(() => {
          poem.classList.add('active');
        }, 300);

        setTimeout(() => {
          const seq = document.getElementById('seq');
          if (seq) seq.remove();
        }, 3000);

        let binary = document.createElement('div');
        binary.className = 'line numbers';
        binary.style.position = 'fixed';
        binary.style.bottom = '10px';
        binary.style.left = '50%';
        binary.style.transform = 'translateX(-50%)';
        poem.appendChild(binary);

        let val = '0100';
        setInterval(() => {
          binary.textContent = val;
          val = val === '0100' ? '1001' : '0100';
        }, 400);

        document.body.addEventListener('click', () => {
          const lines = document.querySelectorAll('.line');
          lines.forEach((line, i) => {
            line.classList.add('ordered');
          });
        });
      } else {
        alert('sai mật mã!');
      }
    });
  </script>
</body>
</html>
