[gemini-code-1792072637952.html](https://github.com/user-attachments/files/33498078/gemini-code-1792072637952.html)
<!DOCTYPE html>
<html lang="ru" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="Система Режима" />
  <meta name="theme-color" content="#090d16" />
  <title>Система Режима • AI Наставник (AQ Ready)</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            bgMain: '#090d16',
            bgCard: '#111827',
            bgElevated: '#1e293b',
            accent: '#10b981',
            accentBlue: '#3b82f6'
          }
        }
      }
    };
  </script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap');

    * {
      -webkit-tap-highlight-color: transparent;
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      background-color: #090d16;
      color: #f8fafc;
      padding-bottom: calc(5.5rem + env(safe-area-inset-bottom));
      overflow-x: hidden;
    }

    .mono {
      font-family: 'JetBrains Mono', monospace;
    }

    .glass-card {
      background: rgba(17, 24, 39, 0.88);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .habit-done .habit-title {
      text-decoration: line-through;
      color: #64748b;
    }

    .habit-done {
      background: rgba(16, 185, 129, 0.05);
      border-color: rgba(16, 185, 129, 0.22);
    }

    .tab-btn-active {
      color: #10b981 !important;
      background: rgba(16, 185, 129, 0.14);
      border-color: rgba(16, 185, 129, 0.35);
    }

    .posture-step-active {
      border-color: rgba(16, 185, 129, 0.7) !important;
      background: rgba(16, 185, 129, 0.1) !important;
      box-shadow: 0 0 20px -5px rgba(16, 185, 129, 0.28);
    }

    .posture-step-done {
      border-color: rgba(16, 185, 129, 0.3) !important;
      background: rgba(15, 23, 42, 0.65) !important;
      opacity: 0.8;
    }

    .ai-box {
      background: linear-gradient(135deg, rgba(16, 185, 129, 0.08), rgba(59, 130, 246, 0.08));
      border: 1px solid rgba(56, 189, 248, 0.28);
    }

    @keyframes pulseGlow {
      0%, 100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.35); }
      50% { box-shadow: 0 0 0 8px rgba(16, 185, 129, 0); }
    }

    .pulse-badge {
      animation: pulseGlow 2.2s infinite;
    }

    ::-webkit-scrollbar {
      width: 4px;
      height: 4px;
    }
    ::-webkit-scrollbar-thumb {
      background: #1e293b;
      border-radius: 9999px;
    }
  </style>
</head>
<body class="min-h-screen selection:bg-emerald-500 selection:text-slate-950">

  <!-- ШАПКА -->
  <header class="sticky top-0 z-30 bg-[#090d16]/92 backdrop-blur-xl border-b border-slate-800/80">
    <div class="max-w-3xl mx-auto px-4 py-2.5 flex items-center justify-between gap-2">
      <div>
        <div class="flex items-center gap-2">
          <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 pulse-badge"></span>
          <h1 class="text-base font-extrabold tracking-tight text-white">СИСТЕМА РЕЖИМА</h1>
          <span id="headerRankBadge" class="text-[10px] font-bold px-2 py-0.5 rounded-full bg-amber-500/15 text-amber-300 border border-amber-500/30">
            Ур. 1 • Старт
          </span>
          <span id="aiHeaderIndicator" onclick="switchTab('settings')" class="cursor-pointer text-[10px] font-bold px-2 py-0.5 rounded-full bg-sky-500/15 text-sky-300 border border-sky-500/30">
            ✨ AI
          </span>
        </div>
        <p id="currentDateLabel" class="text-[11px] text-slate-400 mt-0.5">Загрузка даты...</p>
      </div>

      <div class="flex items-center gap-2">
        <button onclick="openEmergencyMode()" title="Экстренная перезагрузка"
          class="px-2.5 py-1 rounded-xl bg-rose-500/15 hover:bg-rose-500/25 border border-rose-500/30 text-rose-300 text-xs font-semibold flex items-center gap-1 transition">
          <span>🚨</span><span class="hidden sm:inline">Срыв</span>
        </button>

        <button onclick="manualEditStreak()" title="Нажми для корректировки серии"
          class="px-2.5 py-1 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-500/30 flex items-center gap-1.5 transition">
          <span class="text-sm">🔥</span>
          <span class="text-xs font-extrabold text-amber-300 mono leading-none"><span id="streakCount">0</span> дн.</span>
        </button>
      </div>
    </div>

    <!-- ВЕРХНИЕ ВКЛАДКИ НА ПК -->
    <div class="hidden sm:block max-w-3xl mx-auto px-4 pb-2">
      <nav class="grid grid-cols-6 gap-1 bg-slate-900/90 p-1 rounded-xl border border-slate-800">
        <button onclick="switchTab('checklist')" data-tab="checklist" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>✅</span><span>Чек-лист</span>
          <span id="badgeTabChecklistTop" class="ml-0.5 px-1.5 py-0.2 rounded-full text-[10px] bg-emerald-500/20 text-emerald-300 mono">0</span>
        </button>
        <button onclick="switchTab('english')" data-tab="english" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>🇬🇧</span><span>Английский</span>
        </button>
        <button onclick="switchTab('workouts')" data-tab="workouts" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>🧘</span><span>Осанка и Сила</span>
        </button>
        <button onclick="switchTab('coach')" data-tab="coach" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>⚡</span><span>Тренер</span>
        </button>
        <button onclick="switchTab('finance')" data-tab="finance" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>🛡️</span><span>Финансы</span>
        </button>
        <button onclick="switchTab('settings')" data-tab="settings" class="tab-nav-btn py-1.5 px-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition flex items-center justify-center gap-1">
          <span>⚙️</span><span>Настройки</span>
        </button>
      </nav>
    </div>
  </header>

  <main class="max-w-3xl mx-auto px-3.5 pt-3 space-y-3.5">

    <!-- ==========================================
         ВКЛАДКА 1: ЧЕК-ЛИСТ + УМНАЯ ВЕЧЕРНЯЯ РАЗГРУЗКА (AI BRAIN DUMP)
         ========================================== -->
    <section id="tab-checklist" class="tab-panel space-y-3">
      <!-- Компактная плашка прогресса -->
      <div class="glass-card rounded-2xl p-3 sm:p-4">
        <div class="flex items-center justify-between gap-2 mb-2">
          <h2 class="text-sm sm:text-base font-bold text-white">
            Прогресс дня: <span id="progressText" class="mono text-emerald-400">0/7 (0%)</span>
          </h2>
          <div class="flex items-center gap-1.5">
            <button onclick="openHabitModal()"
              class="px-2.5 py-1 rounded-lg bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-bold text-xs transition">
              ＋ Привычка
            </button>
            <button onclick="resetTodayChecklist()"
              class="px-2 py-1 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-300 text-xs transition">
              Сброс
            </button>
          </div>
        </div>

        <div class="w-full h-2 bg-slate-800 rounded-full overflow-hidden p-0.5 border border-slate-700/60">
          <div id="progressBar" class="h-full bg-gradient-to-r from-emerald-500 to-cyan-400 rounded-full transition-all duration-300" style="width: 0%"></div>
        </div>
      </div>

      <!-- Компактный список привычек -->
      <div id="habitsList" class="space-y-2"></div>

      <!-- Умная вечерняя разгрузка (De-stress Brain Dump 22:30 с Gemini API) -->
      <div class="glass-card rounded-2xl p-3.5 border border-indigo-500/30 space-y-2.5">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <div class="flex items-center gap-1.5 text-xs font-bold text-white">
            <span>🧠</span><span>Вечерняя выгрузка мыслей (22:30 De-stress)</span>
          </div>
          <div class="flex items-center gap-1.5">
            <button onclick="aiDeStressBrainDump()" id="btnAiBrainDump"
              class="px-2.5 py-1 rounded-lg bg-sky-500 hover:bg-sky-400 text-slate-950 font-extrabold text-[11px] transition flex items-center gap-1">
              <span>✨</span><span>ИИ-переоценка и закрыть гештальт</span>
            </button>
            <button onclick="clearBrainDump()"
              class="px-2.5 py-1 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-300 font-semibold text-[11px] transition">
              Просто очистить
            </button>
          </div>
        </div>

        <textarea id="brainDumpInput" rows="2"
          placeholder="Крутятся ошибки прошлого или тревоги о завтрашнем дне? Выпиши сюда перед сном..."
          oninput="saveBrainDumpDraft()"
          class="w-full rounded-xl bg-slate-900/90 border border-slate-700/80 focus:border-indigo-400 focus:outline-none p-2.5 text-xs text-slate-100 placeholder-slate-500 resize-none"></textarea>

        <!-- Ответ ИИ для спокойного сна -->
        <div id="aiBrainDumpResult" class="hidden ai-box rounded-xl p-3 text-xs text-slate-100 leading-relaxed whitespace-pre-line"></div>
      </div>
    </section>

    <!-- ==========================================
         ВКЛАДКА 2: АНГЛИЙСКИЙ (ПРОВЕРКА ФРАЗ В 1 КЛИК + AI ANKI + КВАНТОВАНИЕ)
         ========================================== -->
    <section id="tab-english" class="tab-panel space-y-3 hidden">
      <!-- Квантование 30-минутного урока на 2 дня -->
      <div class="glass-card rounded-2xl p-4 border border-sky-500/35 space-y-3">
        <div class="flex items-start justify-between gap-2">
          <div>
            <span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-sky-500/20 text-sky-300 border border-sky-500/30">
              🇬🇧 High A0 – Entry A1 • 10–15 мин/день
            </span>
            <h2 class="text-base font-extrabold text-white mt-1">Квантование урока (2 дня по 15 мин)</h2>
          </div>
          <span id="engFullStatusBadge" class="px-2.5 py-0.5 rounded-lg text-xs font-bold bg-slate-900 text-slate-300">
            0/2 блока
          </span>
        </div>

        <div class="grid grid-cols-2 gap-1.5 bg-slate-900 p-1 rounded-xl border border-slate-800 text-xs">
          <button id="btnEngModeDay1" onclick="setEnglishCycleDay(1)" class="py-2 rounded-lg font-bold transition text-center">
            📘 День 1: Теория + вслух (15м)
          </button>
          <button id="btnEngModeDay2" onclick="setEnglishCycleDay(2)" class="py-2 rounded-lg font-bold transition text-center">
            🗣️ День 2: Практика + Anki (15м)
          </button>
        </div>
        <div id="engCycleHintBox" class="p-2.5 rounded-xl bg-sky-500/10 border border-sky-500/20 text-xs text-sky-200"></div>
      </div>

      <!-- Дневной и вечерний блоки с таймерами -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
        <div class="glass-card rounded-2xl p-3.5 border border-slate-800 space-y-2.5">
          <div class="flex items-center justify-between">
            <span class="text-xs font-bold text-amber-300">☀️ Дневной фокус (до 19:00)</span>
            <span class="text-[11px] mono text-emerald-400 font-bold">+15 XP</span>
          </div>
          <label class="flex items-start gap-2 cursor-pointer select-none">
            <input id="chkEngDaytime" type="checkbox" onchange="toggleEnglishBlock('daytime')" class="mt-0.5 w-4 h-4 rounded accent-emerald-500" />
            <span class="text-xs text-slate-200">12–15 мин видео (ставь паузу и говори вслух!)</span>
          </label>
          <div class="flex items-center justify-between pt-1 border-t border-slate-800">
            <div id="engTimerDayDisplay" class="mono text-base font-bold text-sky-300">15:00</div>
            <div class="flex gap-1">
              <button id="btnEngTimerDayToggle" onclick="toggleEnglishTimer('daytime')" class="px-3 py-1 rounded-lg bg-sky-500 text-slate-950 font-bold text-xs">▶ Старт</button>
              <button onclick="resetEnglishTimer('daytime')" class="px-2 py-1 rounded-lg bg-slate-800 text-xs text-slate-300">↺</button>
            </div>
          </div>
        </div>

        <div class="glass-card rounded-2xl p-3.5 border border-slate-800 space-y-2.5">
          <div class="flex items-center justify-between">
            <span class="text-xs font-bold text-indigo-300">🌙 Вечерний фокус (после 21:00)</span>
            <span class="text-[11px] mono text-emerald-400 font-bold">+10 XP</span>
          </div>
          <label class="flex items-start gap-2 cursor-pointer select-none">
            <input id="chkEngEvening" type="checkbox" onchange="toggleEnglishBlock('evening')" class="mt-0.5 w-4 h-4 rounded accent-emerald-500" />
            <span class="text-xs text-slate-200">5 мин карточек Anki вслух перед сном</span>
          </label>
          <div class="flex items-center justify-between pt-1 border-t border-slate-800">
            <div id="engTimerEveDisplay" class="mono text-base font-bold text-indigo-300">05:00</div>
            <div class="flex gap-1">
              <button id="btnEngTimerEveToggle" onclick="toggleEnglishTimer('evening')" class="px-3 py-1 rounded-lg bg-indigo-500 text-slate-950 font-bold text-xs">▶ Старт</button>
              <button onclick="resetEnglishTimer('evening')" class="px-2 py-1 rounded-lg bg-slate-800 text-xs text-slate-300">↺</button>
            </div>
          </div>
        </div>
      </div>

      <!-- AI БЛОК 1: ПРОВЕРКА ФРАЗЫ ЗА 1 КЛИК -->
      <div class="glass-card rounded-2xl p-4 border border-sky-500/40 space-y-2.5">
        <div class="flex items-center justify-between gap-2">
          <div>
            <span class="text-[10px] font-extrabold uppercase tracking-wider text-sky-400">✨ Gemini Репетитор (Fast-модель)</span>
            <h3 class="text-sm font-bold text-white">Проверка твоей фразы за 1 клик</h3>
          </div>
          <span class="text-[11px] text-slate-400">Окончания -s/-es, have/has, связка to</span>
        </div>

        <div class="flex gap-2">
          <input id="engUserSentenceInput" type="text"
            placeholder="Напиши фразу о своем дне (напр: He want buy car / I goes to college)..."
            onkeydown="if(event.key==='Enter') aiCheckEnglishSentence()"
            class="flex-1 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-xs text-white focus:border-sky-400 focus:outline-none" />
          <button onclick="aiCheckEnglishSentence()" id="btnAiCheckEng"
            class="px-3.5 py-2 rounded-xl bg-sky-500 hover:bg-sky-400 text-slate-950 font-extrabold text-xs shrink-0 transition">
            ✨ Проверить
          </button>
        </div>

        <div id="aiEngCheckResult" class="hidden ai-box rounded-xl p-3 text-xs text-slate-100 leading-relaxed whitespace-pre-line"></div>
      </div>

      <!-- AI БЛОК 2: ГЕНЕРАТОР 3 КОНТЕКСТНЫХ ШАБЛОНОВ ДЛЯ ANKI -->
      <div class="glass-card rounded-2xl p-3.5 border border-emerald-500/30 space-y-2.5">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <span class="text-xs font-bold text-emerald-400">🗣️ Шаблоны для речи и Anki</span>
          <div class="flex items-center gap-1.5">
            <button onclick="aiGenerateAnkiTemplates()" id="btnAiGenAnki"
              class="px-3 py-1 rounded-lg bg-sky-500/20 hover:bg-sky-500/30 border border-sky-500/40 text-sky-300 font-bold text-xs transition">
              ✨ Сгенерировать 3 фразы для Anki (AI)
            </button>
            <button onclick="rollEnglishPattern()" class="px-2.5 py-1 rounded-lg bg-emerald-500 text-slate-950 font-bold text-xs">
              🎲 Базовый шаблон
            </button>
          </div>
        </div>

        <div class="p-3 rounded-xl bg-slate-900 border border-slate-800 space-y-1">
          <div id="engPatternRuleBadge" class="text-[10px] font-bold text-emerald-300"></div>
          <div id="engPatternMainText" class="text-base font-bold text-white mono"></div>
          <div id="engPatternDrillText" class="text-xs text-slate-300"></div>
        </div>

        <div id="aiAnkiCardsResult" class="hidden ai-box rounded-xl p-3 text-xs text-slate-100 leading-relaxed whitespace-pre-line mono"></div>
      </div>
    </section>

    <!-- ==========================================
         ВКЛАДКА 3: ОСАНКА И СИЛА + АДАПТАЦИЯ ПОД САМОЧУВСТВИЕ (AI)
         ========================================== -->
    <section id="tab-workouts" class="tab-panel space-y-3 hidden">

      <!-- АДАПТИВНЫЙ ТРЕНЕР И УПРАВЛЕНИЕ НАГРУЗКОЙ ПО САМОЧУВСТВИЕ -->
      <div class="glass-card rounded-2xl p-4 border border-sky-500/35 space-y-2.5">
        <div class="flex items-center justify-between">
          <div>
            <span class="text-[10px] font-extrabold uppercase tracking-wider text-sky-400">✨ Умная дозировка нагрузки</span>
            <h3 class="text-sm font-bold text-white">Как самочувствие перед тренировкой?</h3>
          </div>
          <span id="currentMoodLabel" class="text-xs font-bold text-emerald-400">Выбери состояние</span>
        </div>

        <div class="grid grid-cols-3 gap-2 text-xs">
          <button onclick="aiAdaptWorkoutByMood('Полон сил 🔥')"
            class="py-2 px-2 rounded-xl bg-emerald-500/15 hover:bg-emerald-500/25 border border-emerald-500/30 text-emerald-300 font-bold transition">
            🔥 Полон сил
          </button>
          <button onclick="aiAdaptWorkoutByMood('Устал после пар 😮‍💨')"
            class="py-2 px-2 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-500/30 text-amber-300 font-bold transition">
            😮‍💨 Устал после пар
          </button>
          <button onclick="aiAdaptWorkoutByMood('Сорвались планы 🚨')"
            class="py-2 px-2 rounded-xl bg-rose-500/15 hover:bg-rose-500/25 border border-rose-500/30 text-rose-300 font-bold transition">
            🚨 Сорвались планы
          </button>
        </div>

        <div id="aiWorkoutMoodResult" class="hidden ai-box rounded-xl p-3 text-xs text-slate-100 leading-relaxed whitespace-pre-line"></div>
      </div>

      <!-- Пошаговый комплекс осанки -->
      <div class="glass-card rounded-2xl p-4 border border-emerald-500/40 space-y-3">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <div>
            <span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">
              🧘 Пошаговый комплекс 7–10 мин
            </span>
            <h2 class="text-base font-extrabold text-white mt-1">Разминка для осанки и спины</h2>
          </div>
          <div class="flex items-center gap-1.5">
            <button onclick="startOrTogglePostureComplex()"
              class="btn-posture-start px-3.5 py-1.5 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-extrabold text-xs transition">
              ▶ Запустить по очереди
            </button>
            <button onclick="finishPostureComplexEarly()"
              class="px-2.5 py-1.5 rounded-xl bg-slate-800 text-slate-300 text-xs">
              ⚡ Досрочно
            </button>
          </div>
        </div>

        <div id="postureStepsContainerTab" class="grid grid-cols-1 md:grid-cols-3 gap-2.5"></div>
      </div>

      <!-- Силовой блок -->
      <div class="glass-card rounded-2xl p-4 space-y-3">
        <div class="flex items-center justify-between">
          <h3 class="text-sm font-bold text-white">💪 Домашний силовой блок</h3>
          <button onclick="resetTodayWorkouts()" class="text-xs text-slate-400 hover:text-white">Сброс объема</button>
        </div>

        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2">
          <div class="bg-slate-900 p-2.5 rounded-xl border border-slate-800">
            <div class="text-[10px] text-slate-400">Турник / Вис</div>
            <div class="text-sm font-bold text-white mono mt-0.5"><span id="sumPullups">0</span> повт • <span id="sumHangSec">0</span>с</div>
          </div>
          <div class="bg-slate-900 p-2.5 rounded-xl border border-slate-800">
            <div class="text-[10px] text-slate-400">Отжимания</div>
            <div class="text-sm font-bold text-white mono mt-0.5"><span id="sumPushups">0</span> повт</div>
          </div>
          <div class="bg-slate-900 p-2.5 rounded-xl border border-slate-800">
            <div class="text-[10px] text-slate-400">Приседания</div>
            <div class="text-sm font-bold text-white mono mt-0.5"><span id="sumSquats">0</span> повт</div>
          </div>
          <div class="bg-slate-900 p-2.5 rounded-xl border border-slate-800">
            <div class="text-[10px] text-slate-400">Планка</div>
            <div class="text-sm font-bold text-white mono mt-0.5"><span id="sumPlankSec">0</span> сек</div>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 text-xs">
          <div class="p-3 rounded-xl bg-slate-900 border border-slate-800 space-y-2">
            <div class="font-bold text-white flex justify-between">
              <span>Турник и Вис</span><span class="text-emerald-400">+5 XP</span>
            </div>
            <div class="flex gap-2">
              <input id="inputPullups" type="number" value="8" class="w-16 px-2 py-1 rounded bg-slate-950 border border-slate-700 text-center text-white" />
              <button onclick="addWorkoutSet('pullups')" class="flex-1 py-1 rounded bg-emerald-500/20 text-emerald-300 font-bold border border-emerald-500/30">＋ подход</button>
            </div>
            <div class="flex justify-between items-center pt-1 border-t border-slate-800">
              <span id="hangStopwatchDisplay" class="mono font-bold text-amber-300">Вис: 00:00</span>
              <div class="flex gap-1">
                <button onclick="toggleStopwatch('hang')" id="btnHangToggle" class="px-2 py-0.5 rounded bg-amber-500/20 text-amber-300">Старт</button>
                <button onclick="saveStopwatchToVolume('hang')" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Записать</button>
              </div>
            </div>
          </div>

          <div class="p-3 rounded-xl bg-slate-900 border border-slate-800 space-y-2">
            <div class="font-bold text-white flex justify-between">
              <span>Отжимания</span><span class="text-emerald-400">+5 XP</span>
            </div>
            <div class="flex gap-2">
              <input id="inputPushups" type="number" value="15" class="w-16 px-2 py-1 rounded bg-slate-950 border border-slate-700 text-center text-white" />
              <button onclick="addWorkoutSet('pushups')" class="flex-1 py-1 rounded bg-emerald-500/20 text-emerald-300 font-bold border border-emerald-500/30">＋ подход</button>
            </div>
          </div>

          <div class="p-3 rounded-xl bg-slate-900 border border-slate-800 space-y-2">
            <div class="font-bold text-white flex justify-between">
              <span>Приседания</span><span class="text-emerald-400">+5 XP</span>
            </div>
            <div class="flex gap-2">
              <input id="inputSquats" type="number" value="20" class="w-16 px-2 py-1 rounded bg-slate-950 border border-slate-700 text-center text-white" />
              <button onclick="addWorkoutSet('squats')" class="flex-1 py-1 rounded bg-emerald-500/20 text-emerald-300 font-bold border border-emerald-500/30">＋ подход</button>
            </div>
          </div>

          <div class="p-3 rounded-xl bg-slate-900 border border-slate-800 space-y-2">
            <div class="font-bold text-white flex justify-between">
              <span>Планка</span><span class="text-emerald-400">+5 XP</span>
            </div>
            <div class="flex justify-between items-center pt-1">
              <span id="plankStopwatchDisplay" class="mono font-bold text-cyan-300 text-sm">00:00</span>
              <div class="flex gap-1">
                <button onclick="toggleStopwatch('plank')" id="btnPlankToggle" class="px-2 py-1 rounded bg-cyan-500/20 text-cyan-300 font-bold">Старт</button>
                <button onclick="saveStopwatchToVolume('plank')" class="px-2 py-1 rounded bg-emerald-500 text-slate-950 font-bold">Записать</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ==========================================
         ВКЛАДКА 4: ТРЕНЕР (С ИИ-ГЕНЕРАЦИЕЙ МИКРО-ЧЕЛЛЕНДЖА)
         ========================================== -->
    <section id="tab-coach" class="tab-panel space-y-3 hidden">
      <div class="glass-card rounded-2xl p-4 border border-amber-500/30 space-y-2">
        <div class="flex items-center justify-between">
          <span id="coachRankTitle" class="text-base font-bold text-white">Уровень 1: Старт 🌱</span>
          <span class="text-sm font-extrabold text-amber-400 mono"><span id="coachTotalXP">0</span> XP</span>
        </div>
        <div class="w-full h-2.5 bg-slate-900 rounded-full overflow-hidden border border-slate-700">
          <div id="coachXpBar" class="h-full bg-gradient-to-r from-amber-500 to-yellow-300 rounded-full" style="width: 0%"></div>
        </div>
      </div>

      <div class="glass-card rounded-2xl p-4 border border-emerald-500/30 space-y-2.5">
        <div class="flex justify-between items-center text-xs text-slate-400">
          <span class="font-bold text-emerald-400">⚡ Челлендж дня (+50 XP)</span>
          <button onclick="aiGeneratePersonalChallenge()" id="btnAiCoachChallenge"
            class="px-2.5 py-1 rounded-lg bg-sky-500/20 hover:bg-sky-500/30 border border-sky-500/30 text-sky-300 font-bold text-[11px] transition">
            ✨ Сгенерировать персональный (AI)
          </button>
        </div>
        <p id="dailyChallengeText" class="text-sm font-bold text-white bg-slate-900 p-3 rounded-xl border border-slate-800"></p>
        <div class="flex gap-2">
          <button id="btnCompleteChallenge" onclick="completeDailyChallenge()" class="flex-1 py-2 rounded-xl bg-emerald-500 text-slate-950 font-bold text-xs">
            🏆 Выполнено (+50 XP)
          </button>
          <button onclick="swapDailyChallenge()" class="px-3 py-2 rounded-xl bg-slate-800 text-slate-300 text-xs" title="Сменить из базы">
            🔄
          </button>
        </div>
      </div>

      <div class="glass-card rounded-2xl p-3">
        <h4 class="text-xs font-bold text-slate-400 mb-2">Журнал XP</h4>
        <div id="xpHistoryList" class="space-y-1 text-xs text-slate-300 max-h-40 overflow-y-auto"></div>
      </div>
    </section>

    <!-- ==========================================
         ВКЛАДКА 5: ФИНАНСЫ (ПРАВИЛО 48 ЧАСОВ + AI РАЗБОР ЦЕЛЕСООБРАЗНОСТИ)
         ========================================== -->
    <section id="tab-finance" class="tab-panel space-y-3 hidden">
      <div class="glass-card rounded-2xl p-4 space-y-3">
        <div class="flex justify-between items-center">
          <div>
            <h3 class="text-sm font-bold text-white">Правило 48 часов + AI Фильтр</h3>
            <p class="text-xs text-slate-400">Защита от импульсивных трат с расчетом стоимости владения</p>
          </div>
          <div class="text-right">
            <span class="text-xs text-slate-400">Сэкономлено:</span>
            <div class="text-sm font-extrabold text-emerald-400 mono"><span id="savedMoneyTotal">0</span> ₽</div>
          </div>
        </div>

        <div class="flex flex-wrap sm:flex-nowrap gap-2">
          <input id="wishItemName" type="text" placeholder="Название вещи (напр. кроссовки, гаджет)" class="flex-1 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-xs text-white" />
          <input id="wishItemPrice" type="number" placeholder="Цена ₽" class="w-24 px-2.5 py-2 rounded-xl bg-slate-900 border border-slate-700 text-xs text-white mono" />
          <button onclick="aiAnalyzeFinancePurchase()" id="btnAiFinanceCheck"
            class="px-3 py-2 rounded-xl bg-sky-500/20 hover:bg-sky-500/30 border border-sky-500/40 text-sky-300 font-bold text-xs transition">
            ✨ AI-разбор
          </button>
          <button onclick="addFinanceItem()" class="px-3.5 py-2 rounded-xl bg-emerald-500 text-slate-950 font-extrabold text-xs">
            ⏳ Отложить
          </button>
        </div>

        <div id="aiFinancePreCheckResult" class="hidden ai-box rounded-xl p-3 text-xs text-slate-100 leading-relaxed whitespace-pre-line"></div>

        <div id="financeItemsList" class="space-y-2"></div>
      </div>
    </section>

    <!-- ==========================================
         ВКЛАДКА 6: НАСТРОЙКИ (AQ. KEY SUPPORT + AUTO-DISCOVERY + SMART ROUTER)
         ========================================== -->
    <section id="tab-settings" class="tab-panel space-y-3 hidden">
      <!-- БЛОК НАСТРОЙКИ GEMINI API KEY (ПОДДЕРЖКА AQ. И УМНЫЙ ВЫБОР МОДЕЛИ) -->
      <div class="glass-card rounded-2xl p-4 space-y-3 border border-emerald-500/40 text-xs">
        <div class="flex flex-wrap justify-between items-center gap-2">
          <div>
            <span class="text-[10px] font-extrabold uppercase tracking-wider text-emerald-400">✨ ИИ-Ядро Наставника (AQ. & AIza Ready)</span>
            <h3 class="text-sm font-bold text-white">Настройка Google Gemini API Key</h3>
          </div>
          <a href="https://aistudio.google.com/app/apikey" target="_blank" rel="noopener"
            class="px-2.5 py-1 rounded-lg bg-emerald-500/15 text-emerald-300 border border-emerald-500/30 font-semibold">
            Получить ключ в AI Studio ↗
          </a>
        </div>

        <p class="text-slate-400 text-[11px] leading-relaxed">
          Полная поддержка ключей нового стандарта <b>AQ.Ab8...</b> и классических <b>AIzaSy...</b> через заголовок <code class="text-emerald-300">x-goog-api-key</code>. Скрипт сам опрашивает доступные твоему проекту модели и автоматически выбирает быструю или глубокую модель под задачу.
        </p>

        <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
          <input id="geminiApiKeyInput" type="password" placeholder="Вставь ключ AQ.... или AIzaSy..."
            oninput="saveGeminiConfig()"
            class="sm:col-span-2 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-white mono text-xs focus:border-emerald-400 focus:outline-none" />

          <select id="geminiModelSelect" onchange="saveGeminiConfig()"
            class="px-2.5 py-2 rounded-xl bg-slate-900 border border-slate-700 text-white text-xs mono">
            <option value="auto">🤖 Авто-выбор под задачу (Smart Router)</option>
          </select>
        </div>

        <!-- Инфо-панель обнаруженных моделей для роутера -->
        <div id="routerModelsInfo" class="hidden p-2.5 rounded-xl bg-slate-900/90 border border-slate-800 text-[11px] text-slate-300 space-y-1">
          <div class="flex items-center justify-between">
            <span>⚡ <b>Быстрые задачи</b> (Английский, Anki, Самочувствие):</span>
            <span id="fastModelBadge" class="mono text-emerald-400 font-bold">авто</span>
          </div>
          <div class="flex items-center justify-between">
            <span>🧠 <b>Глубокий разбор</b> (Вечерний КПТ, Финансы 48ч, Отчет):</span>
            <span id="deepModelBadge" class="mono text-sky-400 font-bold">авто</span>
          </div>
        </div>

        <div class="flex flex-wrap items-center justify-between gap-2 pt-1">
          <button onclick="testGeminiConnection()" id="btnTestGemini"
            class="px-3.5 py-2 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-extrabold text-xs transition">
            ✨ Проверить ключ и найти доступные модели
          </button>
          <span id="geminiStatusLabel" class="text-[11px] font-semibold text-slate-400">Ожидание проверки</span>
        </div>

        <!-- Лог точной диагностики ошибок API -->
        <div id="geminiErrorDiagBox" class="hidden p-2.5 rounded-xl bg-rose-950/50 border border-rose-500/40 text-[11px] text-rose-200 mono whitespace-pre-wrap"></div>
      </div>

      <!-- Расписание уведомлений -->
      <div class="glass-card rounded-2xl p-4 space-y-3">
        <div class="flex items-center justify-between">
          <h3 class="text-sm font-bold text-white">Расписание уведомлений</h3>
          <button onclick="requestPushPermissions()" class="px-2.5 py-1 rounded-lg bg-emerald-500 text-slate-950 font-bold text-xs">🔔 Push</button>
        </div>

        <div class="space-y-1.5 text-xs">
          <div class="p-2 rounded-xl bg-slate-900 flex justify-between items-center">
            <span>08:00 • Утренний чек</span>
            <button onclick="triggerContextualAlert('morning', true)" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Тест</button>
          </div>
          <div class="p-2 rounded-xl bg-slate-900 flex justify-between items-center">
            <span>18:00 • Дневной английский</span>
            <button onclick="triggerContextualAlert('english', true)" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Тест</button>
          </div>
          <div class="p-2 rounded-xl bg-slate-900 flex justify-between items-center">
            <span>21:00 • Вечерний фокус</span>
            <button onclick="triggerContextualAlert('evening', true)" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Тест</button>
          </div>
          <div class="p-2 rounded-xl bg-slate-900 flex justify-between items-center">
            <span>21:45 • Угроза срыва (&lt;50%)</span>
            <button onclick="triggerContextualAlert('danger', true)" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Тест</button>
          </div>
          <div class="p-2 rounded-xl bg-slate-900 flex justify-between items-center">
            <span>22:30 • Стоп-экран</span>
            <button onclick="triggerContextualAlert('sleep', true)" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300">Тест</button>
          </div>
        </div>
      </div>

      <!-- Telegram Bot API -->
      <div class="glass-card rounded-2xl p-4 space-y-2.5 border border-sky-500/30 text-xs">
        <div class="flex justify-between items-center">
          <span class="font-bold text-white">Telegram (@moyadisciplinabot)</span>
          <a href="https://t.me/moyadisciplinabot" target="_blank" class="text-sky-400">Открыть бота ↗</a>
        </div>
        <input id="tgBotToken" type="password" placeholder="Bot Token" oninput="saveTelegramConfig()" class="w-full px-2.5 py-1.5 rounded-lg bg-slate-900 border border-slate-700 text-white mono" />
        <input id="tgChatId" type="text" placeholder="Chat ID" oninput="saveTelegramConfig()" class="w-full px-2.5 py-1.5 rounded-lg bg-slate-900 border border-slate-700 text-white mono" />
        <div class="flex flex-wrap gap-2 pt-1">
          <button onclick="testTelegramConnection()" class="px-3 py-1.5 rounded-lg bg-sky-500 text-slate-950 font-bold">Проверить связь</button>
          <button onclick="sendDailyReportToTelegram()" class="px-3 py-1.5 rounded-lg bg-slate-800 text-slate-200 font-semibold">📊 Отчет дня + ИИ-анализ</button>
        </div>
      </div>
    </section>

  </main>

  <!-- НИЖНИЕ МОБИЛЬНЫЕ ВКЛАДКИ -->
  <nav class="sm:hidden fixed bottom-0 left-0 right-0 z-40 bg-[#090d16]/95 backdrop-blur-xl border-t border-slate-800 px-1 pt-1 pb-[calc(0.4rem+env(safe-area-inset-bottom))]">
    <div class="grid grid-cols-6 gap-0.5 text-center">
      <button onclick="switchTab('checklist')" data-tab="checklist" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400 relative">
        <span class="text-sm">✅</span><span>Чек</span>
        <span id="badgeTabChecklistMob" class="absolute top-0 right-1 px-1 rounded-full text-[9px] bg-emerald-500 text-slate-950 font-bold mono">0</span>
      </button>
      <button onclick="switchTab('english')" data-tab="english" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400">
        <span class="text-sm">🇬🇧</span><span>Англ</span>
      </button>
      <button onclick="switchTab('workouts')" data-tab="workouts" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400">
        <span class="text-sm">🧘</span><span>Осанка</span>
      </button>
      <button onclick="switchTab('coach')" data-tab="coach" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400">
        <span class="text-sm">⚡</span><span>Тренер</span>
      </button>
      <button onclick="switchTab('finance')" data-tab="finance" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400">
        <span class="text-sm">🛡️</span><span>Финансы</span>
      </button>
      <button onclick="switchTab('settings')" data-tab="settings" class="tab-nav-btn py-1 rounded-xl flex flex-col items-center text-[10px] text-slate-400">
        <span class="text-sm">⚙️</span><span>Настр</span>
      </button>
    </div>
  </nav>

  <!-- МОДАЛЬНОЕ ОКНО ПРИВЫЧКИ -->
  <div id="habitModal" class="fixed inset-0 z-50 bg-black/75 backdrop-blur-sm hidden items-center justify-center p-4">
    <div class="glass-card rounded-2xl max-w-sm w-full p-4 border border-slate-700 space-y-3">
      <div class="flex justify-between items-center">
        <h3 id="habitModalTitle" class="text-sm font-bold text-white">Привычка</h3>
        <button onclick="closeHabitModal()" class="text-slate-400 text-sm">✕</button>
      </div>
      <input type="hidden" id="editHabitId" />
      <input id="habitTitleInput" type="text" placeholder="Название" class="w-full px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-700 text-xs text-white" />
      <input id="habitDescInput" type="text" placeholder="Описание" class="w-full px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-700 text-xs text-white" />
      <div class="flex items-center justify-between text-xs">
        <label class="text-slate-400">Таймер (мин):</label>
        <input id="habitTimerInput" type="number" min="0" value="0" class="w-16 px-2 py-1 rounded bg-slate-900 border border-slate-700 text-center text-white" />
      </div>
      <label class="flex items-center gap-2 text-xs text-slate-300">
        <input id="habitDictionCheck" type="checkbox" class="rounded bg-slate-900 accent-emerald-500" />
        <span>Генератор слов для речи</span>
      </label>
      <div class="flex justify-end gap-2 pt-1">
        <button onclick="closeHabitModal()" class="px-3 py-1 rounded bg-slate-800 text-xs text-slate-300">Отмена</button>
        <button onclick="saveHabitFromModal()" class="px-3 py-1 rounded bg-emerald-500 text-slate-950 font-bold text-xs">Сохранить</button>
      </div>
    </div>
  </div>

  <!-- ЭКСТРЕННАЯ ПЕРЕЗАГРУЗКА -->
  <div id="emergencyOverlay" class="fixed inset-0 z-50 bg-[#090d16]/95 backdrop-blur-xl hidden items-center justify-center p-4">
    <div class="max-w-md w-full glass-card rounded-2xl p-5 border border-rose-500/40 space-y-4">
      <div class="flex justify-between items-center">
        <span class="text-xs font-bold text-rose-300">🚨 ВЫХОД ИЗ АПАТИИ</span>
        <button onclick="closeEmergencyMode()" class="text-slate-400 text-xs">✕</button>
      </div>
      <div class="space-y-2 text-xs text-slate-200">
        <div class="p-2 rounded bg-slate-900">1. Умойся холодной водой и выпей стакан воды</div>
        <div class="p-2 rounded bg-slate-900">2. Выйди на улицу на 15 минут спокойным шагом</div>
        <div class="p-2 rounded bg-slate-900">3. Сделай одно микро-действие на 2 минуты</div>
      </div>
      <button onclick="closeEmergencyMode()" class="w-full py-2 rounded-xl bg-emerald-500 text-slate-950 font-bold text-xs">
        ⚡ Я вернулся в строй
      </button>
    </div>
  </div>

  <div id="toastContainer" class="fixed top-14 right-4 z-50 space-y-1.5 pointer-events-none"></div>

  <script>
    const STORAGE_KEY = 'personal_discipline_system_v9_aq';

    const DEFAULT_HABITS = [
      { id: 'h1', title: 'Подъем в 07:00', desc: 'Без переноса будильника, стакан воды сразу после пробуждения', timerMin: 0, isDiction: false, isPosture: false, isEnglish: false, done: false },
      { id: 'h2', title: 'Разминка для осанки (7–10 мин)', desc: 'Ангелы у стены, ягодичный мостик, поза сфинкса', timerMin: 8, isDiction: false, isPosture: true, isEnglish: false, done: false },
      { id: 'h3', title: 'Чтение книги вслух (5 мин / 2 стр)', desc: 'Четкая артикуляция, контроль темпа и дикции', timerMin: 5, isDiction: false, isPosture: false, isEnglish: false, done: false },
      { id: 'h4', title: 'Английский язык (15 мин днем + 5 мин вечером)', desc: 'Квантование урока + шаблоны и карточки Anki', timerMin: 15, isDiction: false, isPosture: false, isEnglish: true, done: false },
      { id: 'h5', title: 'Дикция и речь (2 мин)', desc: 'Описание предмета без пауз-паразитов по схеме', timerMin: 2, isDiction: true, isPosture: false, isEnglish: false, done: false },
      { id: 'h6', title: 'Лимит на YouTube (до 45 мин)', desc: 'Экранное время под паролем, без фоновых залипаний', timerMin: 0, isDiction: false, isPosture: false, isEnglish: false, done: false },
      { id: 'h7', title: 'Отбой в 23:00', desc: 'Экран выключен за 30 мин до сна, телефон на столе', timerMin: 0, isDiction: false, isPosture: false, isEnglish: false, done: false }
    ];

    const POSTURE_EXERCISES = [
      {
        id: 'step1', num: 1,
        title: '1. «Ангелы у стены»',
        normLabel: '12 повторений (или 60 сек)',
        durationSec: 60, targetReps: 12,
        tip: 'Прижми затылок, лопатки и крестец к стене. Скользи предплечьями вверх-вниз без отрыва поясницы.'
      },
      {
        id: 'step2', num: 2,
        title: '2. Ягодичный мостик',
        normLabel: '15 повторений (фиксация 2 сек вверху)',
        durationSec: 60, targetReps: 15,
        tip: 'Подъем таза на выдохе, зажимай ягодицы в верхней точке, снимая спазм с поясницы.'
      },
      {
        id: 'step3', num: 3,
        title: '3. Поза «Сфинкса»',
        normLabel: '45 секунд статики',
        durationSec: 45, targetReps: 0,
        tip: 'Опора на предплечья, плечи вниз от ушей, макушка тянется вверх, подбородок слегка назад.'
      }
    ];

    const ENGLISH_PATTERNS = [
      { rule: 'Отработка окончания -s / -es (He / She / It)', template: 'He works here / She reads books', drill: '🗣️ He works here. She reads books every evening. He understands.' },
      { rule: 'Отработка have → has', template: 'He has an offer / She has time', drill: '🗣️ I have a plan → He has an offer. She has free time today.' },
      { rule: 'Конструкция с It + -s', template: 'It looks interesting / It seems easy', drill: '🗣️ It looks interesting. It seems easy now. It works well.' },
      { rule: 'Связка двух глаголов через to', template: 'He wants to buy a car / She tries to learn', drill: '🗣️ He wants to buy a car. She tries to learn. He needs to finish.' }
    ];

    const DICTION_WORDS = ['Металлическая ложка', 'Кроссовок', 'Наручные часы', 'Ключи', 'Окно', 'Кружка', 'Лампа', 'Ручка двери', 'Фонарик', 'Рюкзак'];
    const COACH_CHALLENGES = ['Провисеть на турнике 90 секунд за 2–3 подхода', '3 подхода отжиманий с ровной спиной', 'Описать 2 предмета подряд без единой паузы', '3 минуты растяжки шеи и плеч', 'Дорога домой полностью без телефона'];
    const RANKS = [
      { level: 1, title: 'Старт 🌱', minXP: 0, nextXP: 100 },
      { level: 2, title: 'В фокусе 🎯', minXP: 100, nextXP: 250 },
      { level: 3, title: 'Кремень 🪨', minXP: 250, nextXP: 450 },
      { level: 4, title: 'Дисциплина ⚡', minXP: 450, nextXP: 700 },
      { level: 5, title: 'Титан 🛡️', minXP: 700, nextXP: 1000 },
      { level: 6, title: 'Абсолют 👑', minXP: 1000, nextXP: 2500 }
    ];

    let state = {
      activeTab: 'checklist',
      lastDate: getTodayISO(),
      streak: 0,
      streakIncrementedToday: false,
      victorySentToday: false,
      habits: JSON.parse(JSON.stringify(DEFAULT_HABITS)),
      brainDumpDraft: '',
      english: { cycleDay: 1, daytimeDone: false, eveningDone: false, patternIndex: 0 },
      coach: { xp: 0, challengeIndex: 0, customChallengeText: '', challengeDone: false, swappedToday: false, history: [] },
      workouts: { pullupsReps: 0, pullupsSets: 0, hangSec: 0, pushupsReps: 0, pushupsSets: 0, squatsReps: 0, squatsSets: 0, plankSec: 0, plankSets: 0, postureCompletedToday: false, moodToday: '' },
      finance: { savedTotal: 0, items: [] },
      notifications: { sched_morning: '08:00', sched_english: '18:00', sched_evening: '21:00', sched_danger: '21:45', sched_sleep: '22:30', sentLog: {} },
      telegram: { botToken: '', chatId: '' },
      gemini: {
        apiKey: '',
        selectedMode: 'auto', // 'auto' или конкретное имя модели
        availableModels: [],
        fastModel: '',
        deepModel: ''
      }
    };

    const activeHabitTimers = {};
    const stopwatches = { hang: { sec: 0, interval: null }, plank: { sec: 0, interval: null } };
    const englishTimers = { daytime: { remainingSec: 15 * 60, running: false, interval: null }, evening: { remainingSec: 5 * 60, running: false, interval: null } };
    const postureState = { activeStepIndex: 0, running: false, interval: null, remainingSec: POSTURE_EXERCISES[0].durationSec, doneSteps: [false, false, false], repsCount: [0, 0, 0] };

    function getTodayISO() {
      const d = new Date();
      return new Date(d.getTime() - d.getTimezoneOffset() * 60000).toISOString().slice(0, 10);
    }

    function formatSecondsMMSS(sec) {
      const s = Math.max(0, sec);
      return `${String(Math.floor(s / 60)).padStart(2, '0')}:${String(s % 60).padStart(2, '0')}`;
    }

    // =========================================================================
    // ЯДРО GEMINI API (AQ. STANDARD + AUTO-DISCOVERY + SMART TASK ROUTER)
    // =========================================================================
    function saveGeminiConfig() {
      // Никаких блокировок по префиксу AIza — принимаем и AQ., и AIzaSy
      const rawKey = document.getElementById('geminiApiKeyInput').value.trim();
      const selectedMode = document.getElementById('geminiModelSelect').value || 'auto';
      state.gemini.apiKey = rawKey;
      state.gemini.selectedMode = selectedMode;
      saveState();
      updateAiHeaderBadge();
    }

    function updateAiHeaderBadge() {
      const badge = document.getElementById('aiHeaderIndicator');
      if (!badge) return;
      if (state.gemini && state.gemini.apiKey) {
        const fastLabel = state.gemini.fastModel ? ` • ${state.gemini.fastModel.replace('gemini-', '')}` : '';
        badge.textContent = `✨ AI Активен${fastLabel}`;
        badge.className = 'cursor-pointer text-[10px] font-bold px-2 py-0.5 rounded-full bg-emerald-500/20 text-emerald-300 border border-emerald-500/40';
      } else {
        badge.textContent = '✨ Ввести AI Key';
        badge.className = 'cursor-pointer text-[10px] font-bold px-2 py-0.5 rounded-full bg-sky-500/15 text-sky-300 border border-sky-500/30';
      }
    }

    // Динамическое обнаружение доступных моделей для ключа AQ. / AIza
    async function detectAvailableModels(apiKey) {
      const cleanKey = (apiKey || '').trim();
      if (!cleanKey) return { ok: false, error: 'Ключ пуст' };

      try {
        // Строго чистый URL без ?key= и передача ключа только в заголовке x-goog-api-key
        const res = await fetch('https://generativelanguage.googleapis.com/v1beta/models', {
          method: 'GET',
          headers: {
            'x-goog-api-key': cleanKey
          }
        });

        const data = await res.json();
        if (!res.ok) {
          const msg = data?.error?.message || `HTTP ${res.status}`;
          return { ok: false, status: res.status, error: msg };
        }

        const rawModels = data.models || [];
        // Оставляем только модели с поддержкой generateContent и исключаем устаревшие 1.0 / 1.5 / vision
        const validModels = rawModels
          .filter(m => Array.isArray(m.supportedGenerationMethods) && m.supportedGenerationMethods.includes('generateContent'))
          .map(m => m.name.replace(/^models\//, ''))
          .filter(name => {
            const low = name.toLowerCase();
            return low.startsWith('gemini-')
              && !low.includes('1.0')
              && !low.includes('1.5')
              && !low.includes('embedding')
              && !low.includes('aqa')
              && !low.includes('imagen')
              && !low.includes('tts');
          });

        if (validModels.length === 0) {
          return { ok: false, error: 'Для данного ключа не найдено актуальных текстовых моделей Gemini 2.x+' };
        }

        // Приоритет для быстрой модели (fast): gemini-2.5-flash -> gemini-2.0-flash -> любая flash
        const pickPriority = (list, preferences) => {
          for (const pref of preferences) {
            const exact = list.find(m => m === pref);
            if (exact) return exact;
            const partial = list.find(m => m.includes(pref));
            if (partial) return partial;
          }
          return list[0];
        };

        const fastModel = pickPriority(validModels, [
          'gemini-2.5-flash',
          'gemini-2.0-flash',
          'flash'
        ]);

        // Приоритет для глубокой модели (deep): gemini-2.5-pro -> gemini-2.5-flash -> pro
        const deepModel = pickPriority(validModels, [
          'gemini-2.5-pro',
          'gemini-2.5-flash',
          'pro',
          'gemini-2.0-flash'
        ]);

        state.gemini.availableModels = validModels;
        state.gemini.fastModel = fastModel;
        state.gemini.deepModel = deepModel;
        saveState();
        populateModelSelectDropdown();

        return { ok: true, models: validModels, fastModel, deepModel };
      } catch (err) {
        return { ok: false, error: `Сетевая ошибка: ${err.message}` };
      }
    }

    function populateModelSelectDropdown() {
      const sel = document.getElementById('geminiModelSelect');
      const infoBox = document.getElementById('routerModelsInfo');
      if (!sel) return;

      const currentVal = state.gemini.selectedMode || 'auto';
      const models = state.gemini.availableModels || [];

      sel.innerHTML = `<option value="auto">🤖 Авто-выбор под задачу (Smart Router)</option>`;
      models.forEach(m => {
        const opt = document.createElement('option');
        opt.value = m;
        opt.textContent = m;
        sel.appendChild(opt);
      });

      if (models.includes(currentVal) || currentVal === 'auto') {
        sel.value = currentVal;
      } else {
        sel.value = 'auto';
      }

      if (state.gemini.fastModel || state.gemini.deepModel) {
        infoBox.classList.remove('hidden');
        document.getElementById('fastModelBadge').textContent = state.gemini.fastModel || 'авто';
        document.getElementById('deepModelBadge').textContent = state.gemini.deepModel || 'авто';
      }
      updateAiHeaderBadge();
    }

    // Выбор оптимальной модели под конкретную задачу ('fast' или 'deep')
    function pickModelForTask(taskComplexity = 'fast') {
      if (state.gemini.selectedMode && state.gemini.selectedMode !== 'auto') {
        return state.gemini.selectedMode;
      }
      if (taskComplexity === 'deep' && state.gemini.deepModel) {
        return state.gemini.deepModel;
      }
      if (state.gemini.fastModel) {
        return state.gemini.fastModel;
      }
      return 'gemini-2.5-flash';
    }

    // Вызов генерации контента (строго через заголовок x-goog-api-key без ?key= в URL)
    async function callGeminiAPI(systemPrompt, userPrompt, options = {}) {
      const taskComplexity = options.complexity || 'fast'; // 'fast' | 'deep'
      const maxTokens = options.maxTokens || 200;

      const apiKey = state.gemini && state.gemini.apiKey ? state.gemini.apiKey.trim() : '';
      if (!apiKey) {
        switchTab('settings');
        showToast('Введи ключ AQ.... или AIzaSy... во вкладке Настройки', 'warn');
        return null;
      }

      const diagBox = document.getElementById('geminiErrorDiagBox');
      if (diagBox) diagBox.classList.add('hidden');

      // Если список моделей еще ни разу не запрашивался для этого ключа — делаем Auto-Discovery
      if (!state.gemini.availableModels || state.gemini.availableModels.length === 0) {
        const disc = await detectAvailableModels(apiKey);
        if (!disc.ok) {
          showApiErrorDiagnostics(`Ошибка обнаружения моделей: ${disc.error}`);
          return null;
        }
      }

      const targetModel = pickModelForTask(taskComplexity);
      const fallbackModels = [
        targetModel,
        state.gemini.fastModel,
        state.gemini.deepModel,
        ...(state.gemini.availableModels || [])
      ].filter((v, i, a) => v && a.indexOf(v) === i);

      const doneCount = state.habits.filter(h => h.done).length;
      const contextHeader = `[Контекст пользователя: закрыто ${doneCount}/${state.habits.length} задач дня, серия ${state.streak} дн., уровень XP: ${state.coach.xp}. Отвечай строго в 2-3 строки без приветствий и воды.]`;

      let lastErrorText = '';

      for (const modelName of fallbackModels) {
        try {
          const cleanEndpoint = `https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent`;
          const response = await fetch(cleanEndpoint, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
              'x-goog-api-key': apiKey
            },
            body: JSON.stringify({
              systemInstruction: {
                parts: [{ text: `${systemPrompt} ${contextHeader}` }]
              },
              contents: [
                { role: 'user', parts: [{ text: userPrompt }] }
              ],
              generationConfig: {
                temperature: taskComplexity === 'deep' ? 0.5 : 0.35,
                maxOutputTokens: maxTokens
              }
            })
          });

          const data = await response.json();
          if (response.ok && data.candidates && data.candidates[0]?.content?.parts?.[0]?.text) {
            const text = data.candidates[0].content.parts[0].text.trim();
            return { text, modelUsed: modelName };
          } else {
            const errMsg = data?.error?.message || `HTTP ${response.status}`;
            lastErrorText = `[${modelName}] HTTP ${response.status}: ${errMsg}`;
            // Если модель вернула 404 или перегружена — пробуем следующую из обнаруженных
          }
        } catch (err) {
          lastErrorText = `Сетевая ошибка (${modelName}): ${err.message}`;
        }
      }

      showApiErrorDiagnostics(lastErrorText || 'Неизвестная ошибка запроса к Gemini API');
      return null;
    }

    function showApiErrorDiagnostics(errorDetails) {
      const diagBox = document.getElementById('geminiErrorDiagBox');
      if (diagBox) {
        diagBox.textContent = `⚠️ Диагностика API:\n${errorDetails}`;
        diagBox.classList.remove('hidden');
      }
      showToast(`⚠️ Ошибка API: ${errorDetails.slice(0, 90)}`, 'warn');
    }

    async function testGeminiConnection() {
      const statusEl = document.getElementById('geminiStatusLabel');
      const btn = document.getElementById('btnTestGemini');
      const apiKey = document.getElementById('geminiApiKeyInput').value.trim();

      if (!apiKey) {
        showToast('Вставь свой ключ в поле ввода', 'warn');
        return;
      }

      saveGeminiConfig();
      btn.textContent = '⏳ Опрос доступных моделей...';
      if (statusEl) statusEl.textContent = 'Поиск моделей...';

      const disc = await detectAvailableModels(apiKey);
      if (!disc.ok) {
        btn.textContent = '✨ Проверить ключ и найти доступные модели';
        if (statusEl) {
          statusEl.textContent = '❌ Ошибка авторизации';
          statusEl.className = 'text-[11px] font-bold text-rose-400';
        }
        showApiErrorDiagnostics(`Статус ${disc.status || ''}: ${disc.error}`);
        return;
      }

      // Тестовый запрос к выбранной быстрой модели
      const res = await callGeminiAPI(
        'Ты лаконичный наставник дисциплины.',
        'Напиши 1 короткую фразу (до 8 слов) на русском: связь и авто-выбор моделей работают.',
        { complexity: 'fast', maxTokens: 60 }
      );

      btn.textContent = '✨ Проверить ключ и найти доступные модели';
      if (res && res.text) {
        if (statusEl) {
          statusEl.textContent = `✅ Активно (${disc.models.length} мод. доступно)`;
          statusEl.className = 'text-[11px] font-bold text-emerald-400';
        }
        showToast(`✅ [${res.modelUsed}]: ${res.text}`);
      } else {
        if (statusEl) {
          statusEl.textContent = '❌ Ошибка генерации';
          statusEl.className = 'text-[11px] font-bold text-rose-400';
        }
      }
    }

    // 1. ИИ-ФУНКЦИЯ: ПРОВЕРКА ФРАЗЫ НА АНГЛИЙСКОМ ЗА 1 КЛИК (Complexity: FAST)
    async function aiCheckEnglishSentence() {
      const inputEl = document.getElementById('engUserSentenceInput');
      const resEl = document.getElementById('aiEngCheckResult');
      const btn = document.getElementById('btnAiCheckEng');
      const phrase = inputEl.value.trim();

      if (!phrase) {
        showToast('Сначала введи фразу на английском', 'warn');
        return;
      }

      btn.textContent = '⏳...';
      resEl.classList.remove('hidden');
      resEl.textContent = 'Анализирую грамматику...';

      const sysPrompt = 'Ты практический репетитор английского для уровня High A0 – Entry A1. Проверь фразу пользователя. Выдай ответ СТРОГО в 2 строки без приветствий: 1 строка: "✅ Правильно: [исправленный естественный вариант на английском]". 2 строка: "💡 Правило: [объяснение простыми словами на русском в 1 предложении: окончания -s/-es, have/has, связка через to или артикли]".';
      const res = await callGeminiAPI(sysPrompt, `Моя фраза: "${phrase}"`, { complexity: 'fast' });

      btn.textContent = '✨ Проверить';
      if (res && res.text) {
        resEl.textContent = `${res.text}\n\n🤖 Модель: ${res.modelUsed}`;
        addCoachXP(5, 'AI-разбор английской фразы');
      } else {
        resEl.classList.add('hidden');
      }
    }

    // 2. ИИ-ФУНКЦИЯ: ГЕНЕРАЦИЯ 3 КОНТЕКСТНЫХ ШАБЛОНОВ ДЛЯ ANKI (Complexity: FAST)
    async function aiGenerateAnkiTemplates() {
      const resEl = document.getElementById('aiAnkiCardsResult');
      const btn = document.getElementById('btnAiGenAnki');
      btn.textContent = '⏳ Генерация...';
      resEl.classList.remove('hidden');
      resEl.textContent = 'Составляю 3 жизненных шаблона для Anki...';

      const currentRule = ENGLISH_PATTERNS[state.english.patternIndex || 0].rule;
      const sysPrompt = 'Ты методист английского (уровень High A0 - Entry A1). Составь ровно 3 короткие жизненные фразы для карточек Anki (темы: учеба, тренировка, работа, режим дня) под правило пользователя. Выдай только 3 строки в формате: "1. [Фраза на английском] — [Перевод на русский]". Никаких вступлений.';
      const res = await callGeminiAPI(sysPrompt, `Правило фокуса: ${currentRule}`, { complexity: 'fast' });

      btn.textContent = '✨ Сгенерировать 3 фразы для Anki (AI)';
      if (res && res.text) {
        resEl.textContent = `${res.text}\n[Модель: ${res.modelUsed}]`;
        addCoachXP(5, 'Сгенерированы 3 контекстные карточки Anki');
      } else {
        resEl.classList.add('hidden');
      }
    }

    // 3. ИИ-ФУНКЦИЯ: АДАПТАЦИЯ ТРЕНИРОВКИ ПО САМОЧУВСТВИЮ (Complexity: FAST)
    async function aiAdaptWorkoutByMood(moodText) {
      state.workouts.moodToday = moodText;
      document.getElementById('currentMoodLabel').textContent = moodText;
      saveState();

      const resEl = document.getElementById('aiWorkoutMoodResult');
      resEl.classList.remove('hidden');
      resEl.textContent = 'Подбираю оптимальную нагрузку под твое состояние...';

      const w = state.workouts;
      const sysPrompt = 'Ты адаптивный тренер ЛФК и калистеники. Пользователь выбрал самочувствие перед домашней тренировкой. Выдай конкретный план в 2 коротких строках без воды: если "Устал после пар" или "Сорвались планы" — отмени отказные подходы и дай мягкую разгрузку позвоночника (ангелы у стены, сфинкс, вис 30 сек); если "Полон сил" — дай четкую связку на турник, отжимания и планку.';
      const userPrompt = `Самочувствие: ${moodText}. Уже сделано сегодня: подтягивания ${w.pullupsReps}, отжимания ${w.pushupsReps}, приседания ${w.squatsReps}, планка ${w.plankSec} сек.`;

      const res = await callGeminiAPI(sysPrompt, userPrompt, { complexity: 'fast' });
      if (res && res.text) {
        resEl.textContent = `${res.text}\n[Модель: ${res.modelUsed}]`;
      } else {
        if (moodText.includes('Полон сил')) {
          resEl.textContent = '🔥 Боевой режим: сделай 3 круга: 8 подтягиваний + 15 отжиманий с идеальной техникой + 45 сек планки.\n💡 Заверши 45 секундами виса для декомпрессии спины.';
        } else {
          resEl.textContent = '🧘 Режим сохранения серии: убери тяжелые подходы. Сделай спокойный вис на турнике 30 сек и запусти пошаговый комплекс осанки ниже.\n💡 Это снимет зажимы после дня и сохранит дисциплину без выгорания.';
        }
      }
    }

    // 4. ИИ-ФУНКЦИЯ: ВЕЧЕРНЯЯ РАЗГРУЗКА МЫСЛЕЙ (Complexity: DEEP)
    async function aiDeStressBrainDump() {
      const inputEl = document.getElementById('brainDumpInput');
      const resEl = document.getElementById('aiBrainDumpResult');
      const btn = document.getElementById('btnAiBrainDump');
      const thoughts = inputEl.value.trim();

      if (!thoughts) {
        showToast('Напиши, что тревожит или крутится в голове перед сном', 'warn');
        return;
      }

      btn.textContent = '⏳ Разгрузка...';
      resEl.classList.remove('hidden');
      resEl.textContent = 'Закрываю гештальт дня...';

      const sysPrompt = 'Ты спокойный вечерний психолог-практик (КПТ). Пользователь в 22:30 перед сном выписал тревожные мысли или ошибки прошлого. Напиши СТРОГО 2 спокойных предложения когнитивной переоценки: отдели то, что уже нельзя изменить сегодня, зафиксируй 1 простой шаг на утро и разреши мозгу спокойно спать.';
      const res = await callGeminiAPI(sysPrompt, `Мысли перед сном: "${thoughts}"`, { complexity: 'deep', maxTokens: 220 });

      btn.innerHTML = '<span>✨</span><span>ИИ-переоценка и закрыть гештальт</span>';
      if (res && res.text) {
        resEl.textContent = `🌙 Когнитивная разгрузка на ночь (${res.modelUsed}):\n${res.text}`;
        state.brainDumpDraft = '';
        inputEl.value = '';
        addCoachXP(10, 'Вечерняя ИИ-разгрузка головы перед сном');
        saveState();
      } else {
        resEl.classList.add('hidden');
      }
    }

    // 5. ИИ-ФУНКЦИЯ: ФИНАНСОВЫЙ ФИЛЬТР «ПРАВИЛО 48 ЧАСОВ» (Complexity: DEEP)
    async function aiAnalyzeFinancePurchase() {
      const name = document.getElementById('wishItemName').value.trim();
      const price = parseInt(document.getElementById('wishItemPrice').value || '0', 10);
      const resEl = document.getElementById('aiFinancePreCheckResult');
      const btn = document.getElementById('btnAiFinanceCheck');

      if (!name || price <= 0) {
        showToast('Введи название вещи и цену для AI-разбора', 'warn');
        return;
      }

      btn.textContent = '⏳...';
      resEl.classList.remove('hidden');
      resEl.textContent = 'Оцениваю целесообразность траты...';

      const sysPrompt = 'Ты трезвый финансовый советник. Пользователь хочет совершить покупку. Выдай строго 3 короткие строки без вступлений: 1) Неудобный вопрос №1 о реальной необходимости против минутного импульса. 2) Неудобный вопрос №2 о частоте использования через 2 недели. 3) Расчет стоимости владения и сколько часов труда это стоит.';
      const res = await callGeminiAPI(sysPrompt, `Хочу купить: "${name}" за ${price} рублей.`, { complexity: 'deep', maxTokens: 220 });

      btn.textContent = '✨ AI-разбор';
      if (res && res.text) {
        resEl.textContent = `${res.text}\n[Модель: ${res.modelUsed}]`;
      } else {
        resEl.classList.add('hidden');
      }
    }

    // 6. ИИ-ФУНКЦИЯ: ПЕРСОНАЛЬНЫЙ ЧЕЛЛЕНДЖ ДНЯ ОТ ТРЕНЕРА (Complexity: FAST)
    async function aiGeneratePersonalChallenge() {
      const btn = document.getElementById('btnAiCoachChallenge');
      btn.textContent = '⏳ Генерация...';

      const sysPrompt = 'Придумай 1 конкретный выполнимый за 3–5 минут микро-челлендж на сегодня (осанка, турник, дикция без пауз или цифровой детокс по дороге домой). Строго 1 предложение без кавычек и вступлений.';
      const res = await callGeminiAPI(sysPrompt, 'Дай свежее задание дня.', { complexity: 'fast' });

      btn.textContent = '✨ Сгенерировать персональный (AI)';
      if (res && res.text) {
        state.coach.customChallengeText = res.text.replace(/^["«]|["»]$/g, '');
        state.coach.challengeDone = false;
        saveState();
        renderCoach();
        showToast(`⚡ Челлендж от ${res.modelUsed} готов!`);
      }
    }

    // =========================================================================
    // АВТОНОМНЫЕ ЗВУКИ (WEB AUDIO API)
    // =========================================================================
    let audioCtx = null;
    function getAudioCtx() {
      if (!audioCtx) {
        const C = window.AudioContext || window.webkitAudioContext;
        if (C) audioCtx = new C();
      }
      if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume();
      return audioCtx;
    }

    function playClickSound(checked = true) {
      try {
        const ctx = getAudioCtx(); if (!ctx) return;
        const o = ctx.createOscillator(), g = ctx.createGain();
        o.type = 'triangle';
        o.frequency.setValueAtTime(checked ? 600 : 300, ctx.currentTime);
        o.frequency.exponentialRampToValueAtTime(checked ? 900 : 200, ctx.currentTime + 0.05);
        g.gain.setValueAtTime(0.12, ctx.currentTime);
        g.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.05);
        o.connect(g); g.connect(ctx.destination);
        o.start(); o.stop(ctx.currentTime + 0.06);
      } catch (e) {}
    }

    function playTimerFinishBeep() {
      try {
        const ctx = getAudioCtx(); if (!ctx) return;
        [587, 880].forEach((f, i) => {
          const o = ctx.createOscillator(), g = ctx.createGain();
          o.frequency.setValueAtTime(f, ctx.currentTime + i * 0.16);
          g.gain.setValueAtTime(0.2, ctx.currentTime + i * 0.16);
          g.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + i * 0.16 + 0.14);
          o.connect(g); g.connect(ctx.destination);
          o.start(ctx.currentTime + i * 0.16); o.stop(ctx.currentTime + i * 0.16 + 0.15);
        });
      } catch (e) {}
    }

    // =========================================================================
    // ХРАНИЛИЩЕ И ПРОВЕРКА НОВОГО ДНЯ
    // =========================================================================
    function loadState() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY)
          || localStorage.getItem('personal_discipline_system_v8_ai')
          || localStorage.getItem('personal_discipline_system_v7');
        if (raw) {
          const p = JSON.parse(raw);
          state = Object.assign({}, state, p);
          state.english = Object.assign({ cycleDay: 1, daytimeDone: false, eveningDone: false, patternIndex: 0 }, p.english || {});
          state.coach = Object.assign({ xp: 0, challengeIndex: 0, customChallengeText: '', challengeDone: false, swappedToday: false, history: [] }, p.coach || {});
          state.workouts = Object.assign({ pullupsReps: 0, pullupsSets: 0, hangSec: 0, pushupsReps: 0, pushupsSets: 0, squatsReps: 0, squatsSets: 0, plankSec: 0, plankSets: 0, postureCompletedToday: false, moodToday: '' }, p.workouts || {});
          state.finance = Object.assign({ savedTotal: 0, items: [] }, p.finance || {});
          state.telegram = Object.assign({ botToken: '', chatId: '' }, p.telegram || {});
          state.gemini = Object.assign({ apiKey: '', selectedMode: 'auto', availableModels: [], fastModel: '', deepModel: '' }, p.gemini || {});
        }
      } catch (e) {}
      checkDayRollover();
    }

    function saveState() {
      try { localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); } catch (e) {}
    }

    function checkDayRollover() {
      const today = getTodayISO();
      if (state.lastDate !== today) {
        const total = state.habits.length;
        const done = state.habits.filter(h => h.done).length;
        if (!(total > 0 && done === total)) state.streak = 0;
        if (state.english && state.english.daytimeDone) state.english.cycleDay = state.english.cycleDay === 1 ? 2 : 1;
        state.english.daytimeDone = false;
        state.english.eveningDone = false;
        state.habits.forEach(h => h.done = false);
        state.streakIncrementedToday = false;
        state.victorySentToday = false;
        state.coach.customChallengeText = '';
        state.coach.challengeDone = false;
        state.coach.swappedToday = false;
        state.workouts = { pullupsReps: 0, pullupsSets: 0, hangSec: 0, pushupsReps: 0, pushupsSets: 0, squatsReps: 0, squatsSets: 0, plankSec: 0, plankSets: 0, postureCompletedToday: false, moodToday: '' };
        resetPostureComplex(false);
        state.lastDate = today;
        saveState();
      }
    }

    function switchTab(t) {
      state.activeTab = t;
      saveState();
      document.querySelectorAll('.tab-panel').forEach(p => p.classList.toggle('hidden', p.id !== `tab-${t}`));
      document.querySelectorAll('.tab-nav-btn').forEach(b => b.classList.toggle('tab-btn-active', b.getAttribute('data-tab') === t));
    }

    // =========================================================================
    // ПОШАГОВЫЙ КОМПЛЕКС ОСАНКИ
    // =========================================================================
    function renderPostureComplex() {
      const tabContainer = document.getElementById('postureStepsContainerTab');
      if (!tabContainer) return;
      const allDone = postureState.doneSteps.every(Boolean) || state.workouts.postureCompletedToday;

      tabContainer.innerHTML = POSTURE_EXERCISES.map((ex, idx) => {
        const isCurrent = idx === postureState.activeStepIndex && !allDone;
        const isDone = postureState.doneSteps[idx] || state.workouts.postureCompletedToday;
        const stepSec = isCurrent ? postureState.remainingSec : (isDone ? 0 : ex.durationSec);

        return `
          <div class="p-3.5 rounded-xl bg-slate-900/90 border border-slate-800 flex flex-col justify-between gap-2.5 transition-all ${isCurrent ? 'posture-step-active' : ''} ${isDone ? 'posture-step-done' : ''}">
            <div class="space-y-1.5">
              <div class="flex items-center justify-between">
                <span class="text-[11px] font-bold ${isDone ? 'text-emerald-400' : isCurrent ? 'text-emerald-300' : 'text-slate-400'}">
                  ${isDone ? '✅ Готово' : 'Шаг ' + ex.num + ' / 3'}
                </span>
                <span class="mono text-xs font-bold text-slate-300">⏱ ${formatSecondsMMSS(stepSec)}</span>
              </div>
              <div class="text-sm font-bold text-white">${ex.title}</div>
              <div class="text-xs font-semibold text-emerald-400">${ex.normLabel}</div>
              <div class="text-xs text-slate-300 bg-slate-950 p-2.5 rounded-lg border border-slate-800">
                💡 ${ex.tip}
              </div>
            </div>
            <div class="pt-2 border-t border-slate-800 flex justify-between items-center">
              ${ex.targetReps > 0 ? `
                <div class="flex items-center gap-1.5">
                  <button onclick="incrementPostureRep(${idx})" class="px-2 py-0.5 rounded bg-slate-800 text-xs font-bold text-emerald-300">＋1</button>
                  <span class="mono text-xs text-slate-300">${postureState.repsCount[idx]}/${ex.targetReps}</span>
                </div>
              ` : '<span class="text-[11px] text-slate-400">Статика</span>'}
              <button onclick="selectAndRunPostureStep(${idx})" class="px-3 py-1 rounded-lg text-xs font-bold ${isCurrent && postureState.running ? 'bg-amber-500 text-slate-950' : 'bg-emerald-500/20 text-emerald-300'}">
                ${isDone ? 'Повторить' : isCurrent && postureState.running ? '⏸' : '▶'}
              </button>
            </div>
          </div>
        `;
      }).join('');

      document.querySelectorAll('.btn-posture-start').forEach(b => {
        b.textContent = postureState.running
          ? `⏸ Пауза (Шаг ${postureState.activeStepIndex + 1})`
          : (state.workouts.postureCompletedToday ? '🔄 Запустить заново' : '▶ Запустить по очереди');
      });
    }

    function startOrTogglePostureComplex() {
      if (postureState.doneSteps.every(Boolean)) resetPostureComplex(false);
      if (postureState.running) pausePostureComplex();
      else runPostureStepTimer();
      renderPostureComplex();
    }

    function selectAndRunPostureStep(stepIdx) {
      if (postureState.activeStepIndex === stepIdx && postureState.running) {
        pausePostureComplex(); renderPostureComplex(); return;
      }
      pausePostureComplex();
      postureState.activeStepIndex = stepIdx;
      postureState.doneSteps[stepIdx] = false;
      postureState.remainingSec = POSTURE_EXERCISES[stepIdx].durationSec;
      runPostureStepTimer();
      renderPostureComplex();
    }

    function runPostureStepTimer() {
      if (postureState.interval) clearInterval(postureState.interval);
      postureState.running = true;
      playClickSound(true);
      postureState.interval = setInterval(() => {
        postureState.remainingSec = Math.max(0, postureState.remainingSec - 1);
        if (postureState.remainingSec <= 0) {
          pausePostureComplex();
          const idx = postureState.activeStepIndex;
          postureState.doneSteps[idx] = true;
          if (idx < POSTURE_EXERCISES.length - 1) {
            playTimerFinishBeep();
            postureState.activeStepIndex = idx + 1;
            postureState.remainingSec = POSTURE_EXERCISES[idx + 1].durationSec;
            runPostureStepTimer();
          } else {
            finalizePostureComplexVictory();
          }
        }
        renderPostureComplex();
      }, 1000);
    }

    function pausePostureComplex() {
      if (postureState.interval) { clearInterval(postureState.interval); postureState.interval = null; }
      postureState.running = false;
    }

    function incrementPostureRep(stepIdx) {
      const target = POSTURE_EXERCISES[stepIdx].targetReps || 12;
      postureState.repsCount[stepIdx] = Math.min(target, (postureState.repsCount[stepIdx] || 0) + 1);
      playClickSound(true);
      if (postureState.repsCount[stepIdx] >= target && postureState.activeStepIndex === stepIdx) {
        pausePostureComplex();
        postureState.doneSteps[stepIdx] = true;
        if (stepIdx < POSTURE_EXERCISES.length - 1) {
          playTimerFinishBeep();
          postureState.activeStepIndex = stepIdx + 1;
          postureState.remainingSec = POSTURE_EXERCISES[stepIdx + 1].durationSec;
          runPostureStepTimer();
        } else {
          finalizePostureComplexVictory();
        }
      }
      renderPostureComplex();
    }

    function finishPostureComplexEarly() {
      finalizePostureComplexVictory();
    }

    function finalizePostureComplexVictory() {
      pausePostureComplex();
      postureState.doneSteps = [true, true, true];
      postureState.remainingSec = 0;
      state.workouts.postureCompletedToday = true;
      playTimerFinishBeep();

      const postureHabit = state.habits.find(h => h.isPosture || h.id === 'h2' || h.title.toLowerCase().includes('осанк'));
      if (postureHabit && !postureHabit.done) {
        postureHabit.done = true;
        addCoachXP(15, 'Разминка для осанки выполнена');
        checkAllHabitsCompleted();
      }
      saveState();
      renderChecklist();
      renderPostureComplex();
      showToast('🏆 Комплекс осанки выполнен! Галочка в чек-листе поставлена.');
    }

    function resetPostureComplex(showToastMsg = true) {
      pausePostureComplex();
      postureState.activeStepIndex = 0;
      postureState.remainingSec = POSTURE_EXERCISES[0].durationSec;
      postureState.doneSteps = [false, false, false];
      postureState.repsCount = [0, 0, 0];
      renderPostureComplex();
      if (showToastMsg) showToast('Таймеры осанки сброшены');
    }

    // =========================================================================
    // КОМПАКТНЫЙ ЧЕК-ЛИСТ
    // =========================================================================
    function renderChecklist() {
      const list = document.getElementById('habitsList');
      list.innerHTML = '';

      state.habits.forEach(habit => {
        const tState = activeHabitTimers[habit.id];
        const secLeft = tState ? tState.remainingSec : habit.timerMin * 60;
        const mm = String(Math.floor(secLeft / 60)).padStart(2, '0');
        const ss = String(secLeft % 60).padStart(2, '0');
        const isRunning = tState && tState.running;
        const isPostureHabit = habit.isPosture || habit.id === 'h2' || habit.title.toLowerCase().includes('осанк');
        const isEnglishHabit = habit.isEnglish || habit.id === 'h4' || habit.title.toLowerCase().includes('английск');

        const card = document.createElement('div');
        card.className = `glass-card rounded-xl p-3 transition border ${
          habit.done ? 'habit-done' : isPostureHabit ? 'border-emerald-500/35 bg-emerald-950/10' : isEnglishHabit ? 'border-sky-500/35 bg-sky-950/10' : 'border-slate-800'
        }`;

        card.innerHTML = `
          <div class="flex items-start justify-between gap-2.5">
            <label class="flex items-start gap-2.5 cursor-pointer flex-1 select-none">
              <input type="checkbox" ${habit.done ? 'checked' : ''} onchange="toggleHabit('${habit.id}')"
                class="mt-0.5 w-4 h-4 rounded accent-emerald-500 cursor-pointer shrink-0" />
              <div class="space-y-0.5 flex-1">
                <div class="flex items-center gap-1.5 flex-wrap">
                  <span class="habit-title font-bold text-xs sm:text-sm text-white">${escapeHtml(habit.title)}</span>
                  ${isPostureHabit ? `<span class="text-[9px] px-1.5 py-0.2 rounded bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">3 шага</span>` : ''}
                  ${isEnglishHabit ? `<span class="text-[9px] px-1.5 py-0.2 rounded bg-sky-500/20 text-sky-300 border border-sky-500/30">День ${state.english.cycleDay}</span>` : ''}
                </div>
                <p class="text-[11px] text-slate-400 leading-snug">${escapeHtml(habit.desc || '')}</p>
              </div>
            </label>

            <div class="flex items-center gap-1 shrink-0">
              <button onclick="openHabitModal('${habit.id}')" class="p-1 text-slate-400 hover:text-white text-xs">✏️</button>
              <button onclick="deleteHabit('${habit.id}')" class="p-1 text-slate-400 hover:text-rose-400 text-xs">🗑️</button>
            </div>
          </div>

          ${(habit.timerMin > 0 || isPostureHabit || isEnglishHabit || habit.isDiction) ? `
            <div class="mt-2 pt-2 border-t border-slate-800 flex flex-wrap items-center justify-between gap-1.5">
              ${habit.timerMin > 0 ? `
                <div class="flex items-center gap-1.5">
                  <span id="timer_disp_${habit.id}" class="mono text-xs font-bold px-2 py-0.5 rounded bg-slate-900 border border-slate-700 text-emerald-300">
                    ⏱ ${mm}:${ss}
                  </span>
                  <button onclick="toggleHabitTimer('${habit.id}')" class="px-2.5 py-0.5 rounded ${isRunning ? 'bg-amber-500 text-slate-950' : 'bg-emerald-500/20 text-emerald-300 border border-emerald-500/30'} text-xs font-bold">
                    ${isRunning ? 'Пауза' : 'Старт'}
                  </button>
                  <button onclick="resetHabitTimer('${habit.id}')" class="px-2 py-0.5 rounded bg-slate-800 text-slate-300 text-xs">↺</button>
                </div>
              ` : '<div></div>'}

              <div class="flex items-center gap-1.5">
                ${isPostureHabit ? `
                  <button onclick="switchTab('workouts')" class="px-2.5 py-1 rounded-lg bg-emerald-500 text-slate-950 font-bold text-[11px] flex items-center gap-1">
                    <span>🧘</span><span>Открыть 3 упражнения</span>
                  </button>
                ` : ''}

                ${isEnglishHabit ? `
                  <button onclick="switchTab('english')" class="px-2.5 py-1 rounded-lg bg-sky-500 text-slate-950 font-bold text-[11px] flex items-center gap-1">
                    <span>🇬🇧</span><span>AI Проверка & Anki</span>
                  </button>
                ` : ''}

                ${habit.isDiction ? `
                  <button onclick="rollDictionWord('${habit.id}')" class="px-2 py-0.5 rounded bg-indigo-500/20 text-indigo-300 text-xs font-bold border border-indigo-500/30">
                    🎲 Слово
                  </button>
                  <span id="diction_word_${habit.id}" class="text-xs font-bold text-amber-300 mono">${habit.currentWord ? '«' + escapeHtml(habit.currentWord) + '»' : ''}</span>
                ` : ''}
              </div>
            </div>
          ` : ''}
        `;

        list.appendChild(card);
      });

      updateProgressUI();
    }

    function toggleHabit(id) {
      const habit = state.habits.find(h => h.id === id);
      if (!habit) return;
      habit.done = !habit.done;
      playClickSound(habit.done);
      if (habit.done) addCoachXP(10, `Привычка: ${habit.title}`);
      checkAllHabitsCompleted();
      saveState();
      renderChecklist();
    }

    function checkAllHabitsCompleted() {
      const total = state.habits.length;
      const done = state.habits.filter(h => h.done).length;
      if (total > 0 && done === total) {
        if (!state.streakIncrementedToday) {
          state.streak += 1;
          state.streakIncrementedToday = true;
        }
        if (!state.victorySentToday) {
          state.victorySentToday = true;
          triggerContextualAlert('victory', false);
        }
      } else if (state.streakIncrementedToday) {
        state.streak = Math.max(0, state.streak - 1);
        state.streakIncrementedToday = false;
      }
    }

    function updateProgressUI() {
      const total = state.habits.length;
      const done = state.habits.filter(h => h.done).length;
      const remaining = Math.max(0, total - done);
      const pct = total > 0 ? Math.round((done / total) * 100) : 0;

      document.getElementById('progressText').textContent = `${done}/${total} (${pct}%)`;
      document.getElementById('progressBar').style.width = `${pct}%`;
      document.getElementById('streakCount').textContent = state.streak;
      document.getElementById('badgeTabChecklistTop').textContent = remaining;
      document.getElementById('badgeTabChecklistMob').textContent = remaining;
      document.getElementById('brainDumpInput').value = state.brainDumpDraft || '';
    }

    function toggleHabitTimer(id) {
      const habit = state.habits.find(h => h.id === id);
      if (!habit || habit.timerMin <= 0) return;
      if (!activeHabitTimers[id]) activeHabitTimers[id] = { remainingSec: habit.timerMin * 60, running: false, interval: null };
      const t = activeHabitTimers[id];
      if (t.running) {
        clearInterval(t.interval); t.running = false;
      } else {
        t.running = true;
        t.interval = setInterval(() => {
          t.remainingSec = Math.max(0, t.remainingSec - 1);
          const el = document.getElementById(`timer_disp_${id}`);
          if (el) el.textContent = `⏱ ${formatSecondsMMSS(t.remainingSec)}`;
          if (t.remainingSec <= 0) {
            clearInterval(t.interval); t.running = false; t.remainingSec = habit.timerMin * 60;
            playTimerFinishBeep();
            if (!habit.done) {
              habit.done = true;
              addCoachXP(10, `Таймер: ${habit.title}`);
              checkAllHabitsCompleted();
              saveState();
            }
            renderChecklist();
          }
        }, 1000);
      }
      renderChecklist();
    }

    function resetHabitTimer(id) {
      if (activeHabitTimers[id]) {
        clearInterval(activeHabitTimers[id].interval);
        delete activeHabitTimers[id];
      }
      renderChecklist();
    }

    function rollDictionWord(id) {
      const habit = state.habits.find(h => h.id === id);
      if (!habit) return;
      habit.currentWord = DICTION_WORDS[Math.floor(Math.random() * DICTION_WORDS.length)];
      playClickSound(true);
      saveState();
      const el = document.getElementById(`diction_word_${id}`);
      if (el) el.textContent = `«${habit.currentWord}»`;
    }

    function openHabitModal(editId = null) {
      document.getElementById('editHabitId').value = editId || '';
      if (editId) {
        const h = state.habits.find(item => item.id === editId);
        if (!h) return;
        document.getElementById('habitTitleInput').value = h.title;
        document.getElementById('habitDescInput').value = h.desc || '';
        document.getElementById('habitTimerInput').value = h.timerMin || 0;
        document.getElementById('habitDictionCheck').checked = !!h.isDiction;
      } else {
        document.getElementById('habitTitleInput').value = '';
        document.getElementById('habitDescInput').value = '';
        document.getElementById('habitTimerInput').value = 0;
        document.getElementById('habitDictionCheck').checked = false;
      }
      document.getElementById('habitModal').classList.remove('hidden');
      document.getElementById('habitModal').classList.add('flex');
    }

    function closeHabitModal() {
      document.getElementById('habitModal').classList.add('hidden');
      document.getElementById('habitModal').classList.remove('flex');
    }

    function saveHabitFromModal() {
      const editId = document.getElementById('editHabitId').value;
      const title = document.getElementById('habitTitleInput').value.trim();
      const desc = document.getElementById('habitDescInput').value.trim();
      const timerMin = Math.max(0, parseInt(document.getElementById('habitTimerInput').value || '0', 10));
      const isDiction = document.getElementById('habitDictionCheck').checked;
      if (!title) return;
      if (editId) {
        const h = state.habits.find(item => item.id === editId);
        if (h) { h.title = title; h.desc = desc; h.timerMin = timerMin; h.isDiction = isDiction; }
      } else {
        state.habits.push({ id: 'h_' + Date.now(), title, desc, timerMin, isDiction, done: false });
      }
      saveState();
      renderChecklist();
      closeHabitModal();
    }

    function deleteHabit(id) {
      if (!confirm('Удалить привычку?')) return;
      state.habits = state.habits.filter(h => h.id !== id);
      saveState();
      renderChecklist();
    }

    function resetTodayChecklist() {
      if (!confirm('Сбросить галочки за сегодня?')) return;
      state.habits.forEach(h => h.done = false);
      state.english.daytimeDone = false;
      state.english.eveningDone = false;
      state.workouts.postureCompletedToday = false;
      resetPostureComplex(false);
      saveState();
      renderChecklist();
      renderEnglishModule();
    }

    function manualEditStreak() {
      const val = prompt('Укажи количество дней серии (Streak):', state.streak);
      if (val !== null && !isNaN(parseInt(val, 10))) {
        state.streak = Math.max(0, parseInt(val, 10));
        saveState();
        renderChecklist();
      }
    }

    function saveBrainDumpDraft() {
      state.brainDumpDraft = document.getElementById('brainDumpInput').value;
      saveState();
    }

    function clearBrainDump() {
      state.brainDumpDraft = '';
      document.getElementById('aiBrainDumpResult').classList.add('hidden');
      playClickSound(true);
      saveState();
      renderChecklist();
      showToast('✨ Поле мыслей очищено!');
    }

    // АНГЛИЙСКИЙ
    function setEnglishCycleDay(d) {
      state.english.cycleDay = d === 2 ? 2 : 1;
      playClickSound(true);
      saveState();
      renderEnglishModule();
      renderChecklist();
    }

    function toggleEnglishBlock(p) {
      if (p === 'daytime') {
        state.english.daytimeDone = document.getElementById('chkEngDaytime').checked;
        if (state.english.daytimeDone) addCoachXP(15, `Английский (День ${state.english.cycleDay})`);
      } else {
        state.english.eveningDone = document.getElementById('chkEngEvening').checked;
        if (state.english.eveningDone) addCoachXP(10, 'Английский (Anki)');
      }
      if (state.english.daytimeDone && state.english.eveningDone) {
        const engH = state.habits.find(h => h.isEnglish || h.id === 'h4');
        if (engH && !engH.done) { engH.done = true; checkAllHabitsCompleted(); }
      }
      saveState();
      renderEnglishModule();
      renderChecklist();
    }

    function toggleEnglishTimer(p) {
      const t = englishTimers[p];
      const defaultSec = p === 'daytime' ? 15 * 60 : 5 * 60;
      const dispId = p === 'daytime' ? 'engTimerDayDisplay' : 'engTimerEveDisplay';
      const btnId = p === 'daytime' ? 'btnEngTimerDayToggle' : 'btnEngTimerEveToggle';

      if (t.running) {
        clearInterval(t.interval); t.running = false;
        document.getElementById(btnId).textContent = '▶ Старт';
      } else {
        t.running = true;
        document.getElementById(btnId).textContent = '⏸';
        t.interval = setInterval(() => {
          t.remainingSec = Math.max(0, t.remainingSec - 1);
          const el = document.getElementById(dispId);
          if (el) el.textContent = formatSecondsMMSS(t.remainingSec);
          if (t.remainingSec <= 0) {
            clearInterval(t.interval); t.running = false; t.remainingSec = defaultSec;
            playTimerFinishBeep();
            if (p === 'daytime') state.english.daytimeDone = true;
            else state.english.eveningDone = true;
            saveState(); renderEnglishModule(); renderChecklist();
          }
        }, 1000);
      }
    }

    function resetEnglishTimer(p) {
      const t = englishTimers[p];
      if (t.interval) clearInterval(t.interval);
      t.running = false; t.remainingSec = p === 'daytime' ? 15 * 60 : 5 * 60;
      renderEnglishModule();
    }

    function rollEnglishPattern() {
      state.english.patternIndex = (state.english.patternIndex + 1) % ENGLISH_PATTERNS.length;
      playClickSound(true);
      saveState();
      renderEnglishModule();
    }

    function renderEnglishModule() {
      const d = state.english.cycleDay || 1;
      document.getElementById('btnEngModeDay1').className = `py-2 rounded-lg font-bold transition text-center ${d === 1 ? 'bg-sky-500 text-slate-950' : 'text-slate-400'}`;
      document.getElementById('btnEngModeDay2').className = `py-2 rounded-lg font-bold transition text-center ${d === 2 ? 'bg-emerald-500 text-slate-950' : 'text-slate-400'}`;
      document.getElementById('engCycleHintBox').innerHTML = d === 1
        ? '📘 <b>День 1 (Теория):</b> посмотри 1-ю половину урока (15 мин). Проговаривай примеры за автором вслух!'
        : '🗣️ <b>День 2 (Практика):</b> досмотри 2-ю половину (15 мин). Отвечай вслух раньше автора!';

      document.getElementById('chkEngDaytime').checked = !!state.english.daytimeDone;
      document.getElementById('chkEngEvening').checked = !!state.english.eveningDone;
      document.getElementById('engTimerDayDisplay').textContent = formatSecondsMMSS(englishTimers.daytime.remainingSec);
      document.getElementById('engTimerEveDisplay').textContent = formatSecondsMMSS(englishTimers.evening.remainingSec);

      const doneB = (state.english.daytimeDone ? 1 : 0) + (state.english.eveningDone ? 1 : 0);
      document.getElementById('engFullStatusBadge').textContent = `${doneB}/2 блока`;

      const pattern = ENGLISH_PATTERNS[state.english.patternIndex || 0];
      document.getElementById('engPatternRuleBadge').textContent = pattern.rule;
      document.getElementById('engPatternMainText').textContent = pattern.template;
      document.getElementById('engPatternDrillText').innerHTML = pattern.drill;
    }

    // ТРЕНЕР
    function addCoachXP(amount, reason) {
      state.coach.xp = (state.coach.xp || 0) + amount;
      const timeStr = new Date().toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
      state.coach.history.unshift({ time: timeStr, amount, reason });
      state.coach.history = state.coach.history.slice(0, 10);
      saveState();
      renderCoach();
    }

    function completeDailyChallenge() {
      if (state.coach.challengeDone) return;
      state.coach.challengeDone = true;
      playTimerFinishBeep();
      const chTitle = state.coach.customChallengeText || COACH_CHALLENGES[state.coach.challengeIndex];
      addCoachXP(50, `Челлендж: ${chTitle}`);
      renderCoach();
    }

    function swapDailyChallenge() {
      if (state.coach.challengeDone) return;
      state.coach.customChallengeText = '';
      state.coach.challengeIndex = (state.coach.challengeIndex + 1) % COACH_CHALLENGES.length;
      saveState(); renderCoach();
    }

    function renderCoach() {
      const xp = state.coach.xp || 0;
      let curRank = RANKS[0];
      for (const r of RANKS) if (xp >= r.minXP) curRank = r;
      const span = Math.max(1, curRank.nextXP - curRank.minXP);
      const pct = Math.min(100, Math.round(((xp - curRank.minXP) / span) * 100));

      document.getElementById('headerRankBadge').textContent = `Ур. ${curRank.level} • ${curRank.title}`;
      document.getElementById('coachRankTitle').textContent = `Уровень ${curRank.level}: ${curRank.title}`;
      document.getElementById('coachTotalXP').textContent = xp;
      document.getElementById('coachXpBar').style.width = `${pct}%`;

      const activeCh = state.coach.customChallengeText || COACH_CHALLENGES[state.coach.challengeIndex] || COACH_CHALLENGES[0];
      document.getElementById('dailyChallengeText').textContent = `«${activeCh}»`;

      const histEl = document.getElementById('xpHistoryList');
      histEl.innerHTML = (state.coach.history || []).map(i => `
        <div class="flex justify-between py-0.5 border-b border-slate-800">
          <span>${escapeHtml(i.reason)}</span><span class="mono font-bold text-emerald-400">+${i.amount} XP</span>
        </div>
      `).join('');
    }

    // ТРЕНИРОВКИ
    function addWorkoutSet(type) {
      if (type === 'pullups') {
        const r = Math.max(1, parseInt(document.getElementById('inputPullups').value || '1', 10));
        state.workouts.pullupsReps += r; state.workouts.pullupsSets += 1;
      } else if (type === 'pushups') {
        const r = Math.max(1, parseInt(document.getElementById('inputPushups').value || '1', 10));
        state.workouts.pushupsReps += r; state.workouts.pushupsSets += 1;
      } else if (type === 'squats') {
        const r = Math.max(1, parseInt(document.getElementById('inputSquats').value || '1', 10));
        state.workouts.squatsReps += r; state.workouts.squatsSets += 1;
      }
      playClickSound(true); saveState(); renderWorkouts();
    }

    function toggleStopwatch(k) {
      const sw = stopwatches[k];
      const btnId = k === 'hang' ? 'btnHangToggle' : 'btnPlankToggle';
      const dispId = k === 'hang' ? 'hangStopwatchDisplay' : 'plankStopwatchDisplay';
      if (sw.interval) {
        clearInterval(sw.interval); sw.interval = null;
        document.getElementById(btnId).textContent = 'Старт';
      } else {
        document.getElementById(btnId).textContent = 'Пауза';
        sw.interval = setInterval(() => {
          sw.sec += 1;
          document.getElementById(dispId).textContent = k === 'hang' ? `Вис: ${formatSecondsMMSS(sw.sec)}` : formatSecondsMMSS(sw.sec);
        }, 1000);
      }
    }

    function saveStopwatchToVolume(k) {
      const sw = stopwatches[k];
      if (sw.interval) { clearInterval(sw.interval); sw.interval = null; }
      if (sw.sec <= 0) return;
      if (k === 'hang') { state.workouts.hangSec += sw.sec; state.workouts.pullupsSets += 1; }
      else { state.workouts.plankSec += sw.sec; state.workouts.plankSets += 1; }
      sw.sec = 0;
      playTimerFinishBeep();
      saveState(); renderWorkouts();
    }

    function resetTodayWorkouts() {
      state.workouts = { pullupsReps: 0, pullupsSets: 0, hangSec: 0, pushupsReps: 0, pushupsSets: 0, squatsReps: 0, squatsSets: 0, plankSec: 0, plankSets: 0, postureCompletedToday: state.workouts.postureCompletedToday, moodToday: state.workouts.moodToday };
      saveState(); renderWorkouts();
    }

    function renderWorkouts() {
      const w = state.workouts;
      document.getElementById('sumPullups').textContent = w.pullupsReps;
      document.getElementById('sumHangSec').textContent = w.hangSec;
      document.getElementById('sumPushups').textContent = w.pushupsReps;
      document.getElementById('sumSquats').textContent = w.squatsReps;
      document.getElementById('sumPlankSec').textContent = w.plankSec;
      if (w.moodToday) document.getElementById('currentMoodLabel').textContent = w.moodToday;
      renderPostureComplex();
    }

    // ФИНАНСЫ
    function addFinanceItem() {
      const name = document.getElementById('wishItemName').value.trim();
      const price = parseInt(document.getElementById('wishItemPrice').value || '0', 10);
      if (!name || price <= 0) return;
      state.finance.items.unshift({ id: 'fin_' + Date.now(), name, price, expiresAt: Date.now() + 48 * 3600 * 1000 });
      document.getElementById('wishItemName').value = '';
      document.getElementById('wishItemPrice').value = '';
      document.getElementById('aiFinancePreCheckResult').classList.add('hidden');
      saveState(); renderFinance();
    }

    function resolveFinanceItem(id, act) {
      const item = state.finance.items.find(i => i.id === id);
      if (item && act === 'saved') state.finance.savedTotal = (state.finance.savedTotal || 0) + item.price;
      state.finance.items = state.finance.items.filter(i => i.id !== id);
      saveState(); renderFinance();
    }

    function renderFinance() {
      document.getElementById('savedMoneyTotal').textContent = (state.finance.savedTotal || 0).toLocaleString('ru-RU');
      const listEl = document.getElementById('financeItemsList');
      if (!state.finance.items || state.finance.items.length === 0) {
        listEl.innerHTML = `<div class="p-3 text-center rounded-xl bg-slate-900 border border-slate-800 text-xs text-slate-400">Список пуст 🛡️</div>`;
        return;
      }
      const now = Date.now();
      listEl.innerHTML = state.finance.items.map(i => {
        const diff = Math.max(0, Math.floor((i.expiresAt - now) / 1000));
        const hh = String(Math.floor(diff / 3600)).padStart(2, '0');
        const mm = String(Math.floor((diff % 3600) / 60)).padStart(2, '0');
        return `
          <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800 flex justify-between items-center text-xs">
            <div>
              <div class="font-bold text-white">${escapeHtml(i.name)} (${i.price} ₽)</div>
              <div class="text-[10px] text-slate-400">Осталось: ${hh}:${mm}</div>
            </div>
            <div class="flex gap-1.5">
              <button onclick="resolveFinanceItem('${i.id}', 'saved')" class="px-2.5 py-1 rounded bg-emerald-500 text-slate-950 font-bold">Сэкономил</button>
              <button onclick="resolveFinanceItem('${i.id}', 'buy')" class="px-2 py-1 rounded bg-slate-800 text-slate-300">Купить</button>
            </div>
          </div>
        `;
      }).join('');
    }

    // УВЕДОМЛЕНИЯ И TELEGRAM
    async function requestPushPermissions() {
      if ('Notification' in window) {
        const p = await Notification.requestPermission();
        if (p === 'granted') showToast('🔔 Уведомления включены!');
      }
    }

    function triggerContextualAlert(type, isManual = false) {
      const total = state.habits.length;
      const done = state.habits.filter(h => h.done).length;
      let title = 'Система Режима';
      let msg = '';

      if (type === 'morning') {
        title = '☀️ 08:00 • Утренний чек'; msg = 'Доброе утро! Сделай разминку для осанки — 7 минут для легкой спины.';
      } else if (type === 'english') {
        if (!isManual && state.english.daytimeDone) return;
        title = '🇬🇧 18:00 • Дневной английский'; msg = 'Время для английского! 15 минут до вечера, пока голова свежая.';
      } else if (type === 'evening') {
        title = '🎯 21:00 • Вечерний фокус'; msg = 'Осталось закрыть чтение и 5 минут карточек. Не откладывай на ночь!';
      } else if (type === 'danger') {
        if (!isManual && (done / total >= 0.5)) return;
        title = '🔥 21:45 • Угроза срыва серии'; msg = '🔥 Серия под угрозой! Закрой 1-2 легких пункта, чтобы сохранить прогресс.';
      } else if (type === 'sleep') {
        title = '🌙 22:30 • Стоп-экран'; msg = 'Пора убрать телефон на стол экраном вниз. 30 минут до сна — разгрузи голову.';
      } else if (type === 'victory') {
        title = '🏆 100% ПЛАНА ВЫПОЛНЕНО!'; msg = 'Красава! 100% плана выполнено. Серия продлена, отдыхай с чистой совестью.';
      }

      playTimerFinishBeep();
      showToast(`${title}: ${msg}`);
      sendTelegramMessage(`*${title}*\n${msg}`);
    }

    function checkScheduledAlertsTick() {
      checkDayRollover();
      const hhmm = new Date().toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
      const today = getTodayISO();
      [
        { key: 'morning', time: state.notifications.sched_morning },
        { key: 'english', time: state.notifications.sched_english },
        { key: 'evening', time: state.notifications.sched_evening },
        { key: 'danger', time: state.notifications.sched_danger },
        { key: 'sleep', time: state.notifications.sched_sleep }
      ].forEach(s => {
        const stamp = `${today}_${s.key}_${s.time}`;
        if (hhmm === s.time && !state.notifications.sentLog[stamp]) {
          state.notifications.sentLog[stamp] = true;
          saveState();
          triggerContextualAlert(s.key, false);
        }
      });
    }

    function saveTelegramConfig() {
      state.telegram.botToken = document.getElementById('tgBotToken').value.trim();
      state.telegram.chatId = document.getElementById('tgChatId').value.trim();
      saveState();
    }

    async function sendTelegramMessage(txt) {
      const { botToken, chatId } = state.telegram;
      if (!botToken || !chatId) return false;
      try {
        const res = await fetch(`https://api.telegram.org/bot${botToken}/sendMessage`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ chat_id: chatId, text: txt, parse_mode: 'Markdown' })
        });
        const data = await res.json();
        return !!data.ok;
      } catch (e) { return false; }
    }

    async function testTelegramConnection() {
      const ok = await sendTelegramMessage(`✅ *Связь с @moyadisciplinabot установлена!* Серия: 🔥 ${state.streak} дн.`);
      showToast(ok ? '✈️ Доставлено в Telegram!' : 'Проверь Token и Chat ID', ok ? 'info' : 'warn');
    }

    async function sendDailyReportToTelegram() {
      const done = state.habits.filter(h => h.done).length;
      const total = state.habits.length;
      const lines = state.habits.map(h => `${h.done ? '✅' : '⬜'} ${h.title}`).join('\n');

      let aiComment = '';
      if (state.gemini && state.gemini.apiKey) {
        const res = await callGeminiAPI(
          'Дай 2 коротких предложения обратной связи по итогам дня пользователя (похвали за сделанное и мягко подбодри на завтра).',
          `Выполнено ${done} из ${total} привычек. Подтягивания: ${state.workouts.pullupsReps}, отжимания: ${state.workouts.pushupsReps}.`,
          { complexity: 'deep' }
        );
        if (res && res.text) aiComment = `\n\n✨ *Вердикт ИИ-тренера (${res.modelUsed}):*\n_${res.text}_`;
      }

      const ok = await sendTelegramMessage(`📊 *ОТЧЕТ ДНЯ (${state.lastDate})*\nПрогресс: *${done}/${total}* | Серия: *🔥 ${state.streak} дн.*\n\n${lines}${aiComment}`);
      showToast(ok ? '✈️ Отчет с ИИ-анализом отправлен!' : 'Укажи Token и Chat ID', ok ? 'info' : 'warn');
    }

    function openEmergencyMode() {
      document.getElementById('emergencyOverlay').classList.remove('hidden');
      document.getElementById('emergencyOverlay').classList.add('flex');
    }

    function closeEmergencyMode() {
      document.getElementById('emergencyOverlay').classList.add('hidden');
      document.getElementById('emergencyOverlay').classList.remove('flex');
    }

    function showToast(msg, type = 'info') {
      const c = document.getElementById('toastContainer');
      const t = document.createElement('div');
      t.className = `glass-card px-3 py-2 rounded-xl border ${type === 'warn' ? 'border-rose-500/50 text-rose-200' : 'border-emerald-500/40 text-emerald-200'} text-xs font-semibold shadow-2xl`;
      t.textContent = msg;
      c.appendChild(t);
      setTimeout(() => t.remove(), 3500);
    }

    function escapeHtml(s) {
      return String(s).replace(/[&<>"']/g, m => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[m]));
    }

    function initApp() {
      loadState();
      document.getElementById('currentDateLabel').textContent =
        new Date().toLocaleDateString('ru-RU', { weekday: 'long', day: 'numeric', month: 'long' });

      document.getElementById('tgBotToken').value = state.telegram.botToken || '';
      document.getElementById('tgChatId').value = state.telegram.chatId || '';
      document.getElementById('geminiApiKeyInput').value = (state.gemini && state.gemini.apiKey) || '';

      populateModelSelectDropdown();
      renderChecklist();
      renderEnglishModule();
      renderWorkouts();
      renderCoach();
      renderFinance();
      switchTab(state.activeTab || 'checklist');

      setInterval(() => {
        if (state.activeTab === 'finance') renderFinance();
        checkScheduledAlertsTick();
      }, 1000);
    }

    window.addEventListener('DOMContentLoaded', initApp);
  </script>
</body>
</html>
