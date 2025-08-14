<!doctype html>
<html lang="th">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Happy Birthday</title>
<style>
  html, body {
    height:100%;
    margin:0;
    font-family: system-ui, -apple-system, 'Segoe UI', Roboto, 'Noto Sans Thai', sans-serif;
    overflow:hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #ffe7f1, #e6f7ff);
    position: relative;
    text-align: center;
  }
  .container {
    background: rgba(255,255,255,0.9);
    padding: 4vw;
    border-radius: 20px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.12);
    max-width: 90vw;
    transition: transform 0.5s;
  }
  input {
    padding: 8px;
    font-size: 16px;
    margin: 6px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
    width: 80%;
  }
  button {
    padding: 10px 20px;
    font-size: 18px;
    border:none;
    border-radius:8px;
    background:#ff79c6;
    color:white;
    cursor:pointer;
    margin-top:10px;
    transition: transform 0.2s;
  }
  button:hover {transform: scale(1.1);}
  .message {
    font-size: clamp(16px, 4vw, 28px);
    color:#d6336c;
    font-weight:bold;
    text-shadow: 1px 1px 3px #fff;
    max-width: 90%;
  }
  .confetti {
    position:absolute;
    width:100%;
    height:100%;
    pointer-events:none;
    top:0;
    left:0;
    overflow:hidden;
    z-index:9999;
  }
  .confetti-piece {
    position:absolute;
    width:10px;
    height:10px;
    background-color:red;
    opacity:0.8;
    animation:fall 3s linear infinite;
  }
  @keyframes fall {
    0% {transform: translateY(-10px) rotate(0deg);} 
    100% {transform: translateY(100vh) rotate(360deg);}
  }
</style>
</head>
<body>
<div class="container" id="formContainer">
  <h1>เธอเท่านั้น 🎉🎂</h1>
  <input type="text" id="name" placeholder="ชื่อเล่น" />
  <input type="date" id="birthday" placeholder="เลือกวันเกิด" />
  <br>
  <button onclick="showMessage()">กดสิจ๊ะ</button>
</div>
<div class="message" id="message"></div>
<div class="confetti" id="confetti"></div>

<script>
function showMessage() {
  const name = document.getElementById('name').value || 'คุณ';
  const birthday = document.getElementById('birthday').value;
  const messageDiv = document.getElementById('message');
  const formContainer = document.getElementById('formContainer');

  if(birthday !== '2000-08-15') {
    messageDiv.innerHTML = `❌ วันเกิดไม่ตรง! ลองใหม่อีกครั้ง.`;
    return;
  }

  const birthDate = new Date(birthday);
  const today = new Date();
  let age = today.getFullYear() - birthDate.getFullYear();
  const m = today.getMonth() - birthDate.getMonth();
  if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) { age--; }

  formContainer.remove();
  messageDiv.style.display = 'block';
  messageDiv.innerHTML = `🎂✨🎉<br>สุขสันต์วันเกิดค้าบบบบ❤️ เดะ<b>${name}</b>❤️!<br>ตอนนี้เดะ <b>${age} ปีแล้วนะ!</b><br>ขอให้ปีนี้เต็มไปด้วยความสุข ความรัก และความสำเร็จ<br>${birthDate.toLocaleDateString('th-TH')}<br>รักนะ ❤️`;

  createConfetti();
}

function createConfetti() {
  const confettiContainer = document.getElementById('confetti');
  const colors = ['#ff0a54','#ff477e','#ff7096','#ff85a1','#fbb1b9','#f9bec7','#f6c5c0'];
  for(let i=0;i<100;i++){
    const confetti = document.createElement('div');
    confetti.classList.add('confetti-piece');
    confetti.style.backgroundColor = colors[Math.floor(Math.random()*colors.length)];
    confetti.style.left = Math.random()*100 + 'vw';
    confetti.style.animationDuration = (2 + Math.random()*3) + 's';
    confetti.style.width = (5 + Math.random()*10) + 'px';
    confetti.style.height = (5 + Math.random()*10) + 'px';
    confettiContainer.appendChild(confetti);
  }
}
</script>
</body>
</html>
