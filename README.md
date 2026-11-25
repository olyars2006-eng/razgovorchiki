# razgovorchiki
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Тест: Идеи Джона Локка</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'Georgia', serif;
    background: linear-gradient(135deg, #f5ecd7 0%, #e8d5b7 100%);
    color: #3a2e1f;
    min-height: 100vh;
    padding: 40px 20px;
    overflow-x: hidden;
  }
  .container {
    max-width: 820px;
    margin: 0 auto;
  }
  header {
    text-align: center;
    margin-bottom: 50px;
  }
  header h1 {
    font-size: 2.4em;
    color: #5a3e1b;
    margin-bottom: 10px;
    letter-spacing: 1px;
  }
  header p {
    font-style: italic;
    color: #7a5a3a;
    font-size: 1.1em;
  }
  .section-title {
    font-size: 1.6em;
    color: #5a3e1b;
    border-bottom: 2px solid #b8860b;
    padding-bottom: 8px;
    margin: 40px 0 25px;
  }
  .question {
    background: #fffaf0;
    border-left: 5px solid #b8860b;
    padding: 25px 30px;
    margin-bottom: 25px;
    border-radius: 8px;
    box-shadow: 0 3px 12px rgba(90,62,27,0.08);
    transition: transform 0.3s;
  }
  .question:hover { transform: translateY(-2px); }
  .question-text {
    font-size: 1.1em;
    margin-bottom: 18px;
    line-height: 1.5;
  }
  .options {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .option {
    background: #fdf6e3;
    border: 2px solid #d4b886;
    padding: 12px 18px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.25s;
    font-size: 1em;
    line-height: 1.4;
  }
  .option:hover:not(.disabled) {
    background: #f5e6c8;
    border-color: #b8860b;
    transform: translateX(4px);
  }
  .option.correct {
    background: #d4edda;
    border-color: #28a745;
    color: #155724;
    font-weight: 600;
    animation: pulse 0.6s;
  }
  .option.wrong {
    background: #f8d7da;
    border-color: #dc3545;
    color: #721c24;
    opacity: 0.75;
  }
  .option.disabled { cursor: default; }
  @keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.02); }
    100% { transform: scale(1); }
  }
  .comment {
    margin-top: 15px;
    padding: 12px 16px;
    background: #eef5ff;
    border-left: 3px solid #4a7ab8;
    border-radius: 4px;
    font-size: 0.95em;
    color: #2c4a6e;
    display: none;
    animation: fadeIn 0.5s;
  }
  .comment.show { display: block; }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(-5px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .open-question {
    background: #fffaf0;
    border-left: 5px solid #4a7ab8;
    padding: 25px 30px;
    margin-bottom: 25px;
    border-radius: 8px;
    box-shadow: 0 3px 12px rgba(90,62,27,0.08);
    position: relative;
  }
  .open-question textarea {
    width: 100%;
    min-height: 90px;
    padding: 12px;
    border: 2px solid #d4b886;
    border-radius: 6px;
    font-family: inherit;
    font-size: 1em;
    resize: vertical;
    background: #fdf6e3;
    color: #3a2e1f;
    margin-top: 12px;
  }
  .open-question textarea:focus {
    outline: none;
    border-color: #4a7ab8;
  }
  .scale {
    display: flex;
    gap: 8px;
    margin: 15px 0;
    flex-wrap: wrap;
  }
  .scale-btn {
    flex: 1;
    min-width: 50px;
    padding: 10px;
    border: 2px solid #d4b886;
    background: #fdf6e3;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1.1em;
    font-weight: bold;
    transition: all 0.2s;
  }
  .scale-btn:hover { background: #f5e6c8; }
  .scale-btn.selected {
    background: #4a7ab8;
    color: white;
    border-color: #2c5a8e;
  }
  .fly-btn {
    display: block;
    margin: 15px auto 0;
    padding: 10px 25px;
    background: #4a7ab8;
    color: white;
    border: none;
    border-radius: 25px;
    cursor: pointer;
    font-size: 1em;
    font-family: inherit;
    transition: all 0.3s;
  }
  .fly-btn:hover {
    background: #2c5a8e;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(74,122,184,0.3);
  }
  .fly-btn:disabled {
    background: #aaa;
    cursor: not-allowed;
    transform: none;
  }
  /* Небо для улетания */
  #sky {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 1000;
    overflow: hidden;
  }
  .cloud {
    position: absolute;
    background: white;
    border-radius: 50%;
    opacity: 0.85;
    filter: blur(2px);
  }
  .paper-plane {
    position: fixed;
    font-size: 2em;
    z-index: 1001;
    transition: none;
    pointer-events: none;
  }
  .scroll-card {
    position: fixed;
    background: #fffaf0;
    border: 2px solid #b8860b;
    padding: 15px;
    border-radius: 6px;
    max-width: 280px;
    font-size: 0.9em;
    box-shadow: 0 5px 20px rgba(0,0,0,0.2);
    z-index: 1001;
    transform-origin: center;
  }
  footer {
    text-align: center;
    margin-top: 60px;
    padding: 20px;
    color: #7a5a3a;
    font-style: italic;
  }
</style>
</head>
<body>

<div id="sky"></div>

<div class="container">
  <header>
    <h1>📜 Идеи Джона Локка</h1>
    <p>«Разум — это чистый лист, на котором опыт пишет свою историю»</p>
  </header>

  <h2 class="section-title">Часть А. Понимание идей Локка</h2>

  <div class="question" data-correct="1">
    <div class="question-text"><b>1.</b> Какой пример лучше всего иллюстрирует идею Локка о том, что человек — это <i>tabula rasa</i>?</div>
    <div class="options">
      <div class="option" data-idx="0">а) Ребёнок рождается с врождённым чувством справедливости, поэтому он интуитивно знает, что делиться — хорошо.</div>
      <div class="option" data-idx="1">б) Человек становится смелым, потому что много раз преодолевал страх в разных ситуациях.</div>
      <div class="option" data-idx="2">в) У некоторых людей от рождения есть «математический склад ума», а у других — нет.</div>
      <div class="option" data-idx="3">г) Характер и способности передаются по наследству, как цвет глаз.</div>
    </div>
    <div class="comment">💬 <b>Комментарий:</b> верный ответ — <b>б</b>. Остальные варианты предполагают врождённые идеи или качества.</div>
  </div>

  <div class="question" data-correct="2">
    <div class="question-text"><b>2.</b> Студент прочитал параграф и задумался: «Почему автор считает именно так? Может ли быть иначе?» Что из перечисленного соответствует рефлексии по Локку?</div>
    <div class="options">
      <div class="option" data-idx="0">а) Он просто запомнил текст, чтобы пересказать на экзамене.</div>
      <div class="option" data-idx="1">б) Он почувствовал, что текст скучный (ощущение).</div>
      <div class="option" data-idx="2">в) Он проанализировал свои мысли и сомнения по поводу прочитанного.</div>
      <div class="option" data-idx="3">г) Он отложил книгу, потому что устал.</div>
    </div>
    <div class="comment">💬 <b>Комментарий:</b> рефлексия — это «внутреннее восприятие деятельности нашего ума», то есть анализ собственных мыслей и действий (<b>в</b>).</div>
  </div>

  <div class="question" data-correct="1">
    <div class="question-text"><b>3.</b> Два студента готовятся к экзамену. Первый говорит: «У меня нет способностей к этому предмету, мне не дано». Второй: «Я пока не разобрался, но если разберу ошибки и потренируюсь, смогу». Чья позиция ближе к взглядам Локка?</div>
    <div class="options">
      <div class="option" data-idx="0">а) Первого, потому что способности врождённы.</div>
      <div class="option" data-idx="1">б) Второго, потому что опыт и упражнение формируют умение.</div>
      <div class="option" data-idx="2">в) Оба правы, так как всё зависит от наследственности.</div>
      <div class="option" data-idx="3">г) Ни один, потому что успех зависит только от удачи.</div>
    </div>
    <div class="comment">💬 <b>Комментарий:</b> Локк считал, что профессионализм — результат тренировок и обучения, а не врождённый дар (<b>б</b>).</div>
  </div>

  <div class="question" data-correct="1">
    <div class="question-text"><b>4.</b> Локк писал: «Счастье или несчастье людей есть большей частью дело их собственных рук». Как это связано с идеей «чистого листа»?</div>
    <div class="options">
      <div class="option" data-idx="0">а) Если лист чист, то всё, что на нём написано, — результат внешних обстоятельств, а не наших усилий.</div>
      <div class="option" data-idx="1">б) Если лист чист, то мы сами (и те, кто нас воспитывает) отвечаем за то, что на нём появится.</div>
      <div class="option" data-idx="2">в) Это не связано с идеей чистого листа.</div>
      <div class="option" data-idx="3">г) Локк имел в виду, что счастье зависит только от врождённых задатков.</div>
    </div>
    <div class="comment">💬 <b>Комментарий:</b> верный ответ — <b>б</b>. Ответственность за содержание «листа» лежит на нас и на воспитании.</div>
  </div>

  <h2 class="section-title">Часть Б. Рефлексия ✈️</h2>
  <p style="font-style:italic; color:#7a5a3a; margin-bottom:20px;">Ваши ответы — это мысли, которые отправятся в путешествие. Нажмите «Отправить в небо», и они улетят…</p>

  <div class="open-question" data-q="5">
    <div class="question-text"><b>5.</b> Вспомните случай из вашей жизни, когда анализ собственных ошибок (рефлексия) помог вам чему-то научиться. Что произошло, что вы поняли и что изменили?</div>
    <textarea placeholder="2–3 предложения..."></textarea>
    <button class="fly-btn">🕊️ Отправить в небо</button>
  </div>

  <div class="open-question" data-q="6">
    <div class="question-text"><b>6.</b> Согласны ли вы с утверждением Локка, что «девять из десяти человек становятся теми, кто они есть, благодаря своему воспитанию»?</div>
    <div class="scale">
      <button class="scale-btn" data-val="1">1</button>
      <button class="scale-btn" data-val="2">2</button>
      <button class="scale-btn" data-val="3">3</button>
      <button class="scale-btn" data-val="4">4</button>
      <button class="scale-btn" data-val="5">5</button>
    </div>
    <textarea placeholder="Потому что…"></textarea>
    <button class="fly-btn">🕊️ Отправить в небо</button>
  </div>

  <div class="open-question" data-q="7">
    <div class="question-text"><b>7.</b> Представьте, что вы — молодой специалист. Ошибка на работе — это провал или материал для роста? Как идея Локка помогает вам ответить?</div>
    <textarea placeholder="3–4 предложения..."></textarea>
    <button class="fly-btn">🕊️ Отправить в небо</button>
  </div>

  <div class="open-question" data-q="8">
    <div class="question-text"><b>8.</b> Что из сегодняшнего разговора вы забираете с собой? Что показалось лишним или непонятным?</div>
    <textarea placeholder="Свободный ответ..."></textarea>
    <button class="fly-btn">🕊️ Отправить в небо</button>
  </div>

  <footer>
    «Воспитание — это то, что формирует большой род людской» — Дж. Локк
  </footer>
</div>

<script>
  // === Часть А: подсветка правильных ответов ===
  document.querySelectorAll('.question').forEach(q => {
    const correct = parseInt(q.dataset.correct);
    const options = q.querySelectorAll('.option');
    const comment = q.querySelector('.comment');

    options.forEach(opt => {
      opt.addEventListener('click', () => {
        if (opt.classList.contains('disabled')) return;
        const idx = parseInt(opt.dataset.idx);
        options.forEach(o => {
          o.classList.add('disabled');
          const i = parseInt(o.dataset.idx);
          if (i === correct) o.classList.add('correct');
          else if (i === idx) o.classList.add('wrong');
        });
        comment.classList.add('show');
      });
    });
  });

  // === Часть Б: шкала ===
  document.querySelectorAll('.scale').forEach(scale => {
    const btns = scale.querySelectorAll('.scale-btn');
    btns.forEach(btn => {
      btn.addEventListener('click', () => {
        btns.forEach(b => b.classList.remove('selected'));
        btn.classList.add('selected');
      });
    });
  });

  // === Небо с облаками ===
  const sky = document.getElementById('sky');
  function spawnCloud() {
    const cloud = document.createElement('div');
    cloud.className = 'cloud';
    const size = 60 + Math.random() * 100;
    cloud.style.width = size + 'px';
    cloud.style.height = size * 0.6 + 'px';
    cloud.style.top = '-150px';
    cloud.style.left = Math.random() * 100 + '%';
    cloud.style.opacity = 0.4 + Math.random() * 0.4;
    sky.appendChild(cloud);
    const duration = 8000 + Math.random() * 6000;
    cloud.animate([
      { transform: 'translateY(0)' },
      { transform: `translateY(${window.innerHeight + 200}px)` }
    ], { duration, easing: 'linear' });
    setTimeout(() => cloud.remove(), duration);
  }
  setInterval(spawnCloud, 2500);

  // === Улетание ответов ===
  document.querySelectorAll('.fly-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      const card = btn.closest('.open-question');
      const textarea = card.querySelector('textarea');
      const scale = card.querySelector('.scale');
      let text = textarea.value.trim();

      if (scale) {
        const selected = scale.querySelector('.scale-btn.selected');
        if (selected) text = `Оценка: ${selected.dataset.val}/5. ${text}`;
      }

      if (!text) {
        textarea.style.borderColor = '#dc3545';
        textarea.focus();
        setTimeout(() => textarea.style.borderColor = '#d4b886', 1500);
        return;
      }

      const rect = card.getBoundingClientRect();

      // Создаём свиток с текстом
      const scroll = document.createElement('div');
      scroll.className = 'scroll-card';
      scroll.textContent = text.length > 180 ? text.slice(0, 177) + '…' : text;
      scroll.style.left = (rect.left + 20) + 'px';
      scroll.style.top = rect.top + 'px';
      scroll.style.width = (rect.width - 40) + 'px';
      document.body.appendChild(scroll);

      // Бумажный самолётик
      const plane = document.createElement('div');
      plane.className = 'paper-plane';
      plane.textContent = '✈️';
      plane.style.left = (rect.left + rect.width / 2) + 'px';
      plane.style.top = (rect.top + rect.height / 2) + 'px';
      document.body.appendChild(plane);

      // Анимация свитка — сворачивается
      scroll.animate([
        { transform: 'scale(1) rotate(0deg)', opacity: 1 },
        { transform: 'scale(0.3) rotate(-15deg)', opacity: 0.8, offset: 0.4 },
        { transform: 'scale(0) rotate(-30deg)', opacity: 0 }
      ], { duration: 900, easing: 'ease-in', fill: 'forwards' });

      // Самолётик взлетает
      setTimeout(() => {
        const endX = window.innerWidth * (0.3 + Math.random() * 0.5);
        const endY = -100;
        plane.animate([
          { transform: 'translate(-50%, -50%) rotate(0deg) scale(1)', opacity: 1 },
          { transform: `translate(${endX - rect.left - rect.width/2}px, ${-100}px) rotate(-35deg) scale(0.6)`, opacity: 1, offset: 0.7 },
          { transform: `translate(${endX - rect.left - rect.width/2 + 100}px, -200px) rotate(-45deg) scale(0.3)`, opacity: 0 }
        ], { duration: 2200, easing: 'cubic-bezier(0.4, 0, 0.2, 1)', fill: 'forwards' });
      }, 600);

      // Очистка
      setTimeout(() => {
        scroll.remove();
        plane.remove();
      }, 3200);

      // Очистка поля
      textarea.value = '';
      if (scale) {
        scale.querySelectorAll('.scale-btn').forEach(b => b.classList.remove('selected'));
      }

      // Маленький эффект — искорки
      for (let i = 0; i < 6; i++) {
        const spark = document.createElement('div');
        spark.textContent = '✨';
        spark.style.position = 'fixed';
        spark.style.left = (rect.left + rect.width / 2) + 'px';
        spark.style.top = (rect.top + rect.height / 2) + 'px';
        spark.style.fontSize = '1.2em';
        spark.style.pointerEvents = 'none';
        spark.style.zIndex = '1002';
        document.body.appendChild(spark);
        const angle = (Math.PI * 2 * i) / 6;
        const dist = 60 + Math.random() * 40;
        spark.animate([
          { transform: 'translate(-50%, -50%) scale(1)', opacity: 1 },
          { transform: `translate(${Math.cos(angle)*dist}px, ${Math.sin(angle)*dist}px) scale(0)`, opacity: 0 }
        ], { duration: 800, easing: 'ease-out', fill: 'forwards' });
        setTimeout(() => spark.remove(), 900);
      }
    });
  });
</script>

</body>
</html>
