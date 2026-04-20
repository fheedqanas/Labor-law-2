<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>تحدي نظام العمل السعودي - النسخة النهائية</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(145deg, #f5f7fc 0%, #eef2f8 100%);
      font-family: 'Segoe UI', 'Tahoma', system-ui, -apple-system, 'Cairo', sans-serif;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 2rem 1.5rem;
    }

    .quiz-container {
      max-width: 880px;
      width: 100%;
      background: white;
      border-radius: 2.5rem;
      box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.25), 0 4px 12px rgba(0, 0, 0, 0.05);
      overflow: hidden;
    }

    .quiz-header {
      background: #0a2b3e;
      padding: 1.5rem 2rem;
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      flex-wrap: wrap;
      gap: 0.75rem;
    }

    .title-section {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      font-size: 1.8rem;
      font-weight: 700;
    }

    .title-section span {
      font-size: 2rem;
    }

    .score-badge {
      background: rgba(255,255,255,0.18);
      backdrop-filter: blur(2px);
      padding: 0.5rem 1rem;
      border-radius: 60px;
      font-weight: 600;
      font-size: 1rem;
    }

    .quiz-body {
      padding: 2rem 2rem 1.8rem;
    }

    .progress-area {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 1.8rem;
      font-weight: 600;
      color: #1e4663;
      border-bottom: 2px dashed #dce5ef;
      padding-bottom: 0.6rem;
    }

    .question-counter, .current-score {
      font-size: 1.1rem;
      background: #eef3fc;
      padding: 0.2rem 1rem;
      border-radius: 40px;
    }

    .question-text {
      font-size: 1.7rem;
      font-weight: 700;
      color: #0a2b3e;
      line-height: 1.4;
      margin: 1.2rem 0 1.8rem 0;
    }

    .options-list {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .option-btn {
      background: white;
      border: 2px solid #e2e8f0;
      border-radius: 1.5rem;
      padding: 1rem 1.5rem;
      font-size: 1rem;
      font-weight: 500;
      text-align: right;
      color: #1f3a4b;
      cursor: pointer;
      transition: all 0.2s;
      font-family: inherit;
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .option-btn:hover:not(:disabled) {
      background: #f8fafd;
      border-color: #9bb7d4;
      transform: scale(0.99);
    }

    .option-prefix {
      font-weight: 800;
      background: #eef2f8;
      width: 32px;
      height: 32px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      border-radius: 60px;
      color: #0f3b5c;
    }

    .option-correct {
      background: #e0f2e9 !important;
      border-color: #2b7a4b !important;
      color: #145c33;
    }

    .option-wrong {
      background: #ffe6e5 !important;
      border-color: #c23d3d !important;
      color: #9b2c2c;
    }

    .option-disabled {
      cursor: default;
      opacity: 0.9;
    }

    .action-buttons {
      display: flex;
      justify-content: space-between;
      gap: 1rem;
      margin-top: 1rem;
    }

    .next-btn, .restart-btn {
      border: none;
      padding: 0.9rem 1.6rem;
      border-radius: 2.5rem;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.2s;
      font-family: inherit;
    }

    .next-btn {
      background: #0a2b3e;
      color: white;
      flex: 2;
    }

    .next-btn:hover:not(:disabled) {
      background: #124c6e;
      transform: translateY(-2px);
    }

    .restart-btn {
      background: #edf2f7;
      color: #1e4663;
      border: 1px solid #cbdde9;
      flex: 1;
    }

    .restart-btn:hover {
      background: #e2eaf3;
    }

    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    .result-screen {
      text-align: center;
      padding: 2rem 1.5rem;
    }

    .final-score-box {
      background: #f0f6fe;
      border-radius: 2rem;
      padding: 1.8rem;
      margin: 1.5rem 0;
    }

    .final-score-number {
      font-size: 3.2rem;
      font-weight: 800;
      color: #0f3b5c;
    }

    .restart-full {
      background: #0a2b3e;
      color: white;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 3rem;
      font-weight: bold;
      font-size: 1rem;
      cursor: pointer;
    }

    hr {
      margin: 1rem 0;
      border: none;
      border-top: 2px dotted #cddfea;
    }

    @media (max-width: 600px) {
      body { padding: 1rem; }
      .quiz-body { padding: 1.5rem; }
      .question-text { font-size: 1.3rem; }
      .option-btn { padding: 0.7rem 1rem; }
    }
  </style>
</head>
<body>

<div class="quiz-container" id="quizApp">
  <div class="quiz-header">
    <div class="title-section">
      <span>⚖️</span> 
      <span>تحدي نظام العمل السعودي</span>
    </div>
    <div class="score-badge" id="headerScoreBadge">النتيجة: 0</div>
  </div>

  <div class="quiz-body" id="quizBody">
    <!-- المحتوى ديناميكي بواسطة js -->
  </div>
</div>

<script>
  // ==============================================================
  // الأسئلة مع الإجابات الصحيحة المحددة من قبل المستخدم
  // ==============================================================
  const QUESTIONS = [
    {
      text: "فترة التجربة هي إما 180 يوم أو 90 يوم فقط.",
      options: ["صحيح", "خطأ"],
      correct: 1   // خطأ
    },
    {
      text: "بشكل عام يتحول عقد العمل المحدد المدة إلى عقد غير محدد المدة بعد 3 تجديدات أو إذا بلغت مدة العقد الأصلي 4 سنوات.",
      options: ["صحيح", "خطأ"],
      correct: 1   // خطأ
    },
    {
      text: "فهيد باشر العمل في 1-1-2024 وترك العمل بنهاية عقده في 1-1-2025. راتب فهيد 5000. كم هي مستحقات نهاية الخدمة له؟",
      options: ["0 ريال", "2500 ريال", "5000 ريال", "7500 ريال"],
      correct: 1   // 2500 ريال
    },
    {
      text: "عامل دخل المملكة وأمضى أقل من سنة دون أن يتم إصدار رخصة عمل له. هل يستطيع نقل كفالته دون موافقة الكفيل؟",
      options: ["نعم", "لا", "بعد دفع غرامة", "فقط إذا كان العقد محدد المدة"],
      correct: 0   // نعم
    },
    {
      text: "خالد دخل سوق العمل لأول مرة بتاريخ 10-10-2025. ماهي نسبة الاستقطاع للتأمينات الاجتماعية؟",
      options: ["9%", "10%", "10.25%", "11%"],
      correct: 2   // 10.25%
    },
    {
      text: "عبد العزيز يملك مؤسسة فردية وهو مسجل كمالك للمنشأة. كم عدد العمال المعفيين من المقابل المادي عنده؟",
      options: ["لا يوجد إعفاء", "عامل واحد", "عاملان", "ثلاثة عمال"],
      correct: 2   // عاملان (المؤسسة الفردية: صاحب المنشأة + عاملان)
    },
    {
      text: "كم هو الحد الأقصى للإعفاء من المقابل المالي للمنشأة الصغيرة؟",
      options: ["عامل واحد", "3 عمال", "5 عمال", "4 عمال"],
      correct: 3   // 7 عمال (حسب التحديث: الحد الأعلى 4 عمال)
    },
    {
      text: "في التنظيم الجديد للاستقالة، لا يوجد فترة إشعار.",
      options: ["صحيح", "خطأ"],
      correct: 0   // صح (لا يوجد فترة إشعار في التنظيم الجديد)
    },
    {
      text: "الأصل في تسجيل الموظف الجديد هو تسجيله في التأمينات الاجتماعية أولاً.",
      options: ["صحيح", "خطأ"],
      correct: 1   // خطأ
    },
    {
      text: "عند نقل كفالة العامل، تظهر بياناته بشكل آلي في التأمينات الاجتماعية دون الحاجة لأي إضافة.",
      options: ["صحيح", "خطأ"],
      correct: 1   // خطأ
    }
  ];

  const TOTAL_QS = QUESTIONS.length;

  let currentIndex = 0;
  let userAnswers = new Array(TOTAL_QS).fill(null);
  let quizFinished = false;

  const quizBody = document.getElementById('quizBody');
  const headerScoreBadge = document.getElementById('headerScoreBadge');

  function computeCurrentScore() {
    let score = 0;
    for (let i = 0; i < TOTAL_QS; i++) {
      if (userAnswers[i] !== null && userAnswers[i] === QUESTIONS[i].correct) {
        score++;
      }
    }
    return score;
  }

  function updateHeaderScore() {
    const currentScore = computeCurrentScore();
    headerScoreBadge.innerText = `النتيجة: ${currentScore}`;
  }

  function renderFinalResult() {
    const finalScore = computeCurrentScore();
    const percentage = Math.round((finalScore / TOTAL_QS) * 100);
    quizBody.innerHTML = `
      <div class="result-screen">
        <div style="font-size: 3rem;">📋</div>
        <h2 style="color:#0a2b3e; margin: 0.5rem 0;">النتيجة النهائية</h2>
        <div class="final-score-box">
          <div class="final-score-number">${finalScore} / ${TOTAL_QS}</div>
          <div style="margin-top: 10px; font-weight:500;">نسبة الإجابات الصحيحة: ${percentage}%</div>
          <hr>
          <p style="color:#2c5a7a;">${finalScore === TOTAL_QS ? '🏆 ممتاز! إلمام كامل بنظام العمل' : (finalScore >= 7 ? '👍 جيد جداً، راجع بعض التفاصيل' : '📖 يُنصح بمراجعة التعديلات الجديدة لنظام العمل')}</p>
        </div>
        <button class="restart-full" id="finalRestartBtn">🔄 إعادة الاختبار</button>
      </div>
    `;
    const restartBtn = document.getElementById('finalRestartBtn');
    if (restartBtn) {
      restartBtn.addEventListener('click', () => resetAndRestart());
    }
    quizFinished = true;
  }

  function renderCurrentQuestion() {
    if (quizFinished) return;
    const qData = QUESTIONS[currentIndex];
    const selectedOpt = userAnswers[currentIndex];
    const isAnswered = (selectedOpt !== null);
    const currentScore = computeCurrentScore();

    let optionsHtml = '';
    const letters = ['أ', 'ب', 'ج', 'د'];
    for (let i = 0; i < qData.options.length; i++) {
      let additionalClass = '';
      if (isAnswered) {
        if (i === qData.correct) {
          additionalClass = 'option-correct';
        } else if (i === selectedOpt && i !== qData.correct) {
          additionalClass = 'option-wrong';
        }
      }
      const disabledAttr = isAnswered ? 'disabled' : '';
      let checkMark = '';
      if (isAnswered && i === qData.correct) checkMark = ' ✓';
      if (isAnswered && i === selectedOpt && i !== qData.correct) checkMark = ' ✗';
      
      optionsHtml += `
        <button class="option-btn ${additionalClass} ${isAnswered ? 'option-disabled' : ''}" data-opt-index="${i}" ${disabledAttr}>
          <span class="option-prefix">${letters[i]}</span>
          <span style="flex:1; text-align:right;">${qData.options[i]}${checkMark}</span>
        </button>
      `;
    }

    let nextButtonText = (currentIndex + 1 === TOTAL_QS) ? '🏁 إنهاء الاختبار' : 'السؤال التالي →';
    let nextDisabled = !isAnswered ? 'disabled' : '';

    const html = `
      <div class="progress-area">
        <div class="question-counter">السؤال ${currentIndex+1} / ${TOTAL_QS}</div>
        <div class="current-score">⭐ النتيجة: ${currentScore}</div>
      </div>
      <div class="question-text">${qData.text}</div>
      <div class="options-list" id="optionsList">
        ${optionsHtml}
      </div>
      <div class="action-buttons">
        <button class="next-btn" id="nextQuestionBtn" ${nextDisabled}>${nextButtonText}</button>
        <button class="restart-btn" id="restartQuizBtn">↺ إعادة الاختبار</button>
      </div>
    `;

    quizBody.innerHTML = html;

    const optButtons = document.querySelectorAll('.option-btn');
    optButtons.forEach(btn => {
      btn.addEventListener('click', (e) => {
        if (userAnswers[currentIndex] !== null) return;
        const selectedIdx = parseInt(btn.dataset.optIndex);
        userAnswers[currentIndex] = selectedIdx;
        renderCurrentQuestion();
        updateHeaderScore();
      });
    });

    const nextBtn = document.getElementById('nextQuestionBtn');
    if (nextBtn) {
      nextBtn.addEventListener('click', () => {
        if (userAnswers[currentIndex] === null) return;
        if (currentIndex + 1 < TOTAL_QS) {
          currentIndex++;
          renderCurrentQuestion();
          updateHeaderScore();
        } else {
          renderFinalResult();
          updateHeaderScore();
        }
      });
    }

    const restartBtn = document.getElementById('restartQuizBtn');
    if (restartBtn) {
      restartBtn.addEventListener('click', () => resetAndRestart());
    }
  }

  function resetAndRestart() {
    currentIndex = 0;
    userAnswers = new Array(TOTAL_QS).fill(null);
    quizFinished = false;
    renderCurrentQuestion();
    updateHeaderScore();
  }

  function init() {
    resetAndRestart();
  }

  init();
</script>
</body>
</html>
