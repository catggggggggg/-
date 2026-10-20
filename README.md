<html lang="ja">
<head>
  <meta charset="UTF-8">
  <!-- スマホの画面サイズに自動で合わせ、ズームを制御する必須設定 -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>LESSON 7 環境問題(1) - 5択クイズ</title>
  <style>
    /* 全体のモダンなデザイン設定 */
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      background-color: #f3f4f6;
      margin: 0;
      padding: 16px;
      color: #1f2937;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      background: #ffffff;
      padding: 24px 20px;
      border-radius: 16px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    }
    h1 {
      font-size: 1.25rem;
      text-align: center;
      color: #059669;
      margin-top: 0;
      margin-bottom: 24px;
      font-weight: 700;
    }
    .card {
      margin-bottom: 24px;
      padding: 16px;
      border: 1px solid #e5e7eb;
      border-radius: 12px;
      background: #f9fafb;
    }
    .jp {
      font-weight: 700;
      margin-bottom: 8px;
      font-size: 1rem;
      line-height: 1.5;
    }
    .en {
      margin-bottom: 16px;
      color: #4b5563;
      font-size: 0.95rem;
      line-height: 1.5;
    }
    .options-grid {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
    /* スマホでタップしやすいボタンデザイン */
    .btn {
      width: 100%;
      text-align: left;
      padding: 12px 16px;
      background: #ffffff;
      border: 1px solid #d1d5db;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      transition: all 0.2s;
      color: #374151;
    }
    .btn:hover {
      background: #f3f4f6;
    }
    .btn.selected {
      background: #d1fae5;
      border-color: #34d399;
      color: #065f46;
      font-weight: bold;
    }
    .btn.correct {
      background: #a7f3d0 !important;
      border-color: #10b981 !important;
      color: #065f46 !important;
      font-weight: bold;
    }
    .btn.wrong {
      background: #fecaca !important;
      border-color: #ef4444 !important;
      color: #991b1b !important;
      font-weight: bold;
    }
    .result-box {
      text-align: center;
      font-size: 1.5rem;
      font-weight: 700;
      margin-top: 24px;
      color: #059669;
      display: none;
    }
    .submit-btn {
      width: 100%;
      padding: 16px;
      background: #10b981;
      color: #ffffff;
      border: none;
      border-radius: 8px;
      font-size: 1.1rem;
      cursor: pointer;
      font-weight: bold;
      margin-top: 16px;
      box-shadow: 0 4px 6px -1px rgba(16, 185, 129, 0.2);
      transition: background 0.2s;
    }
    .submit-btn:hover {
      background: #059669;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>LESSON 7 環境問題(1) - 5択クイズ</h1>
    <div id="quiz-container"></div>
    <button class="submit-btn" onclick="checkAnswers()" id="submit-btn">採点する</button>
    <div id="result" class="result-box"></div>
  </div>

  <script>
    const quizData = [
      { jp: "① 我々は環境問題について、もっと考える必要がある。", en: "We need to think more about ( ____ ) problems.", ans: "environmental", opts: ["environmental", "environmentally", "environment", "unusual", "increasing"] },
      { jp: "② この袋は環境に優しい。", en: "This bag is ( ____ ) friendly.", ans: "environmentally", opts: ["environmentally", "environmental", "extreme", "rising", "serious"] },
      { jp: "③ 私たちは地球温暖化を止める必要がある。", en: "We need to stop global ( ____ ).", ans: "warming", opts: ["warming", "weather", "emissions", "change", "issues"] },
      { jp: "④ 地球温暖化が進んでいるのは本当だと思う。", en: "I think it is true that the earth is getting ( ____ ) and warmer.", ans: "warmer", opts: ["warmer", "rising", "higher", "more", "abnormal"] },
      { jp: "⑤ 地球の平均気温は上昇している。", en: "The average global temperature is ( ____ ).", ans: "rising", opts: ["rising", "increasing", "getting", "stopping", "causing"] },
      { jp: "⑥ 私たちは2030年までに二酸化炭素の排出量を3%削減するよう努めます。", en: "We will try to reduce carbon dioxide emissions by three ( ____ ) by 2030.", ans: "percent", opts: ["percent", "degree", "frequency", "issues", "levels"] },
      { jp: "⑦ 私たちは温室効果ガスの排出を減らすよう、努力する必要がある。", en: "We need to work hard to reduce ( ____ ) gas emissions.", ans: "greenhouse", opts: ["greenhouse", "environmental", "global", "abnormal", "sea"] },
      { jp: "⑧ 多くの国にとって、海面の上昇は深刻な問題だ。", en: "Rising ( ____ ) levels is a serious problem for a lot of countries.", ans: "sea", opts: ["sea", "ocean", "water", "air", "global"] },
      { jp: "⑨ 気候変動の原因は何？", en: "What is ( ____ ) change caused by?", ans: "climate", opts: ["climate", "weather", "temperature", "greenhouse", "environmental"] },
      { jp: "⑩ 異常気象が起こる頻度が増えてきている。", en: "The frequency of ( ____ ) weather has been increasing.", ans: "abnormal", opts: ["abnormal", "climate", "percent", "serious", "rising"] }
    ];

    const userAns = {};

    function renderQuiz() {
      const container = document.getElementById("quiz-container");
      container.innerHTML = quizData.map((q, idx) => `
        <div class="card">
          <div class="jp">${q.jp}</div>
          <div class="en">${q.en}</div>
          <div class="options-grid">
            ${q.opts.map(opt => `
              <button class="btn" name="q${idx}" value="${opt}" onclick="selectOpt(${idx}, '${opt}', this)">${opt}</button>
            `).join('')}
          </div>
        </div>
      `).join('');
    }

    function selectOpt(qIdx, opt, btn) {
      userAns[qIdx] = opt;
      const buttons = document.getElementsByName(`q${qIdx}`);
      buttons.forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
    }

    function checkAnswers() {
      let score = 0;
      quizData.forEach((q, idx) => {
        const buttons = document.getElementsByName(`q${idx}`);
        buttons.forEach(b => {
          b.disabled = true; // 採点後はボタンを押せなくする
          b.style.cursor = 'default';
          
          if (b.value === q.ans) {
            b.classList.add("correct"); // 正解の選択肢を緑色に
          }
          if (userAns[idx] === b.value && b.value !== q.ans) {
            b.classList.add("wrong"); // 間違って選んだ選択肢を赤色に
          }
        });
        if (userAns[idx] === q.ans) score++;
      });
      
      const resultBox = document.getElementById("result");
      resultBox.innerText = `スコア: ${score} / ${quizData.length} 点`;
      resultBox.style.display = "block";
      
      document.getElementById("submit-btn").style.display = "none";
      window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' }); // 結果まで自動スクロール
    }

    // 初回描画
    renderQuiz();
  </script>
</body>
</html>
