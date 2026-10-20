<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LESSON 7 - 単語並び替えクイズ</title>
  <style>
    body { font-family: sans-serif; background: #f4f6f8; margin: 0; padding: 20px; color: #333; }
    .container { max-width: 600px; margin: 0 auto; background: #fff; padding: 20px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
    h1 { font-size: 1.2rem; text-align: center; color: #1565c0; margin-top: 0; }
    .card { margin-bottom: 20px; padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px; background: #fafafa; }
    .jp { font-weight: bold; margin-bottom: 10px; }
    .word-pool, .ans-pool { display: flex; flex-wrap: wrap; gap: 6px; min-height: 40px; padding: 8px; border-radius: 6px; margin-bottom: 8px; }
    .word-pool { background: #eef2f5; }
    .ans-pool { background: #fff; border: 2px dashed #90caf9; }
    .word-btn { padding: 6px 10px; background: #fff; border: 1px solid #90caf9; border-radius: 4px; cursor: pointer; font-size: 0.9rem; }
    .submit-btn { width: 100%; padding: 12px; background: #1565c0; color: #fff; border: none; border-radius: 6px; font-size: 1rem; cursor: pointer; font-weight: bold; margin-top: 15px; }
    .result-box { text-align: center; font-size: 1.3rem; font-weight: bold; margin-top: 20px; color: #1565c0; }
  </style>
</head>
<body>
  <div class="container">
    <h1>LESSON 7 - 単語並び替えクイズ</h1>
    <div id="quiz-container"></div>
    <button class="submit-btn" onclick="checkAnswers()">採点する</button>
    <div id="result" class="result-box"></div>
  </div>

  <script>
    const quizData = [
      { jp: "① 我々は環境問題について、もっと考える必要がある。", words: ["We", "need", "to", "think", "more", "about", "environmental", "problems."] },
      { jp: "② この袋は環境に優しい。", words: ["This", "bag", "is", "environmentally", "friendly."] },
      { jp: "③ 私たちは地球温暖化を止める必要がある。", words: ["We", "need", "to", "stop", "global", "warming."] },
      { jp: "④ 地球温暖化が進んでいるのは本当だと思う。", words: ["I", "think", "it", "is", "true", "that", "the", "earth", "is", "getting", "warmer", "and", "warmer."] },
      { jp: "⑤ 地球の平均気温は上昇している。", words: ["The", "average", "global", "temperature", "is", "rising."] },
      { jp: "⑥ 私たちは2030年までに二酸化炭素の排出量を3%削減するよう努めます。", words: ["We", "will", "try", "to", "reduce", "carbon", "dioxide", "emissions", "by", "three", "percent", "by", "2030."] },
      { jp: "⑦ 私たちは温室効果ガスの排出を減らすよう、努力する必要がある。", words: ["We", "need", "to", "work", "hard", "to", "reduce", "greenhouse", "gas", "emissions."] },
      { jp: "⑧ 多くの国にとって、海面の上昇は深刻な問題だ。", words: ["Rising", "sea", "levels", "is", "a", "serious", "problem", "for", "a", "lot", "of", "countries."] },
      { jp: "⑨ 気候変動の原因は何？", words: ["What", "is", "climate", "change", "caused", "by?"] },
      { jp: "⑩ 異常気象が起こる頻度が増えてきている。", words: ["The", "frequency", "of", "abnormal", "weather", "has", "been", "increasing."] }
    ];

    const state = quizData.map(q => ({
      words: [...q.words].sort(() => Math.random() - 0.5),
      userAns: []
    }));

    function render() {
      const container = document.getElementById("quiz-container");
      container.innerHTML = quizData.map((q, idx) => `
        <div class="card">
          <div class="jp">${q.jp}</div>
          <div class="ans-pool" id="ans-${idx}">
            ${state[idx].userAns.map((w, wIdx) => `<button class="word-btn" onclick="removeWord(${idx}, ${wIdx})">${w}</button>`).join('')}
          </div>
          <div class="word-pool">
            ${state[idx].words.map((w, wIdx) => `<button class="word-btn" onclick="addWord(${idx}, ${wIdx})">${w}</button>`).join('')}
          </div>
        </div>
      `).join('');
    }

    function addWord(qIdx, wIdx) {
      const word = state[qIdx].words.splice(wIdx, 1)[0];
      state[qIdx].userAns.push(word);
      render();
    }

    function removeWord(qIdx, wIdx) {
      const word = state[qIdx].userAns.splice(wIdx, 1)[0];
      state[qIdx].words.push(word);
      render();
    }

    function checkAnswers() {
      let score = 0;
      quizData.forEach((q, idx) => {
        if (state[idx].userAns.join(' ') === q.words.join(' ')) {
          score++;
          document.getElementById(`ans-${idx}`).style.borderColor = "#4caf50";
        } else {
          document.getElementById(`ans-${idx}`).style.borderColor = "#f44336";
        }
      });
      document.getElementById("result").innerText = `スコア: ${score} / ${quizData.length} 点`;
    }

    render();
  </script>
</body>
</html>
