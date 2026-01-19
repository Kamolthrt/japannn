# japannn
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<title>เกมจับคู่สัตว์ภาษาญี่ปุ่น</title>
<style>
body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
.game {
    background: white;
    padding: 20px;
    width: 300px;
    text-align: center;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}
button {
    width: 100%;
    margin: 5px 0;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
}
#result {
    margin-top: 10px;
    font-weight: bold;
}
</style>
</head>

<body>
<div class="game">
    <h3>เกมจับคู่สัตว์ภาษาญี่ปุ่น</h3>
    <h1 id="question">ねこ</h1>

    <div id="choices"></div>

    <p id="result"></p>
    <p>คะแนน: <span id="score">0</span> / 10</p>
</div>

<script>
const questions = [
  { jp: "ねこ", answer: "แมว", choices: ["แมว", "หมา", "ปลา"] },
  { jp: "いぬ", answer: "หมา", choices: ["นก", "หมา", "แมว"] },
  { jp: "さかな", answer: "ปลา", choices: ["ปลา", "วัว", "แมว"] },
  { jp: "とり", answer: "นก", choices: ["หมู", "นก", "ปลา"] },
  { jp: "うし", answer: "วัว", choices: ["วัว", "ม้า", "หมา"] },
  { jp: "ぶた", answer: "หมู", choices: ["หมู", "แมว", "ปลา"] },
  { jp: "うま", answer: "ม้า", choices: ["วัว", "ม้า", "หมา"] },
  { jp: "さる", answer: "ลิง", choices: ["ลิง", "หมู", "แมว"] },
  { jp: "ぞう", answer: "ช้าง", choices: ["ช้าง", "ม้า", "หมา"] },
  { jp: "とら", answer: "เสือ", choices: ["เสือ", "แมว", "หมา"] }
];

let current = 0;
let score = 0;

function loadQuestion() {
    if (current >= questions.length) {
        document.querySelector(".game").innerHTML =
        `<h2>จบเกม 🎉</h2>
         <p>คะแนนรวม: ${score} / 10</p>`;
        return;
    }

    document.getElementById("question").textContent = questions[current].jp;
    document.getElementById("result").textContent = "";
    document.getElementById("score").textContent = score;

    const choicesDiv = document.getElementById("choices");
    choicesDiv.innerHTML = "";

    questions[current].choices.forEach(choice => {
        const btn = document.createElement("button");
        btn.textContent = choice;
        btn.onclick = () => checkAnswer(choice);
        choicesDiv.appendChild(btn);
    });
}

function checkAnswer(choice) {
    if (choice === questions[current].answer) {
        score++;
        document.getElementById("result").textContent = "✅ ถูกต้อง!";
    } else {
        document.getElementById("result").textContent =
        "❌ ผิด! คำตอบคือ " + questions[current].answer;
    }
    current++;
    setTimeout(loadQuestion, 1000);
}

loadQuestion();
</script>
</body>
</html>
