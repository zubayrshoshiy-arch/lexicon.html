
Ingiliz tili mini app
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Lexicon — Ingliz tili lugʻati</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,700;1,9..144,500&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --walnut-dark:#241c15;
    --walnut-mid:#382c21;
    --walnut-light:#4a3b2c;
    --brass:#c9a227;
    --brass-bright:#e0bb3f;
    --parchment:#f4ecd8;
    --parchment-dim:#e8dec4;
    --ink:#2a2118;
    --ink-soft:#5a4d3c;
    --teal:#4e8577;
    --teal-deep:#356257;
    --coral:#c0503e;
    --coral-deep:#9c3d2f;
    --off-white:#efe7d3;
    --off-white-dim:#bfb298;
  }
  *{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(ellipse at top, var(--walnut-light) 0%, var(--walnut-dark) 70%);
    color:var(--off-white);
    font-family:'Inter',sans-serif;
    min-height:100vh;
    display:flex;
    justify-content:center;
  }
  #app{
    width:100%;
    max-width:480px;
    min-height:100vh;
    display:flex;
    flex-direction:column;
    position:relative;
  }
  @media (prefers-reduced-motion: reduce){
    *{animation-duration:0.01ms !important; transition-duration:0.01ms !important;}
  }

  /* HEADER */
  header{
    padding:22px 20px 16px;
    position:relative;
  }
  .brand-row{
    display:flex; align-items:center; justify-content:space-between;
  }
  .brand{
    font-family:'Fraunces',serif;
    font-weight:700;
    font-size:26px;
    letter-spacing:0.3px;
    color:var(--parchment);
  }
  .brand em{
    font-style:italic;
    font-weight:500;
    color:var(--brass-bright);
  }
  .streak{
    display:flex; align-items:center; gap:6px;
    background:var(--walnut-dark);
    border:1px solid var(--brass);
    border-radius:20px;
    padding:6px 12px;
    font-size:13px;
    font-weight:600;
    color:var(--brass-bright);
  }
  .subtitle{
    font-size:12.5px;
    color:var(--off-white-dim);
    margin-top:4px;
    font-family:'IBM Plex Mono', monospace;
    letter-spacing:0.4px;
  }

  /* BRASS LABEL / SECTION EYEBROW */
  .plate{
    display:inline-flex;
    align-items:center;
    gap:6px;
    background:linear-gradient(180deg, var(--brass-bright), var(--brass));
    color:var(--walnut-dark);
    font-family:'IBM Plex Mono', monospace;
    font-size:11px;
    font-weight:500;
    letter-spacing:1.2px;
    text-transform:uppercase;
    padding:4px 10px;
    border-radius:3px;
    box-shadow:0 1px 0 rgba(0,0,0,0.3) inset, 0 2px 3px rgba(0,0,0,0.35);
  }

  main{
    flex:1;
    padding:4px 20px 100px;
    overflow-y:auto;
  }

  .screen{ display:none; }
  .screen.active{ display:block; animation:fadeIn 0.25s ease; }
  @keyframes fadeIn{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);} }

  /* SEARCH */
  .search-wrap{ margin:14px 0 16px; position:relative; }
  .search-wrap input{
    width:100%;
    background:var(--walnut-dark);
    border:1px solid var(--walnut-light);
    color:var(--off-white);
    border-radius:10px;
    padding:11px 14px 11px 38px;
    font-size:14.5px;
    font-family:'Inter',sans-serif;
  }
  .search-wrap input::placeholder{ color:var(--off-white-dim); }
  .search-wrap input:focus{ outline:none; border-color:var(--brass); }
  .search-icon{ position:absolute; left:13px; top:50%; transform:translateY(-50%); opacity:0.5; font-size:14px; }

  .cat-scroller{
    display:flex; gap:8px; overflow-x:auto; padding:2px 0 14px;
    scrollbar-width:none;
  }
  .cat-scroller::-webkit-scrollbar{ display:none; }
  .cat-chip{
    flex:0 0 auto;
    background:var(--walnut-mid);
    border:1px solid var(--walnut-light);
    color:var(--off-white-dim);
    font-size:12.5px;
    font-weight:600;
    padding:7px 13px;
    border-radius:16px;
    cursor:pointer;
    white-space:nowrap;
    font-family:'Inter',sans-serif;
  }
  .cat-chip.active{
    background:var(--teal);
    border-color:var(--teal);
    color:var(--off-white);
  }

  /* WORD LIST - CATALOG CARD */
  .word-row{
    display:flex;
    align-items:center;
    gap:12px;
    background:var(--parchment);
    border-radius:10px;
    padding:12px 14px;
    margin-bottom:9px;
    position:relative;
    cursor:pointer;
    box-shadow:0 2px 0 rgba(0,0,0,0.25), 0 4px 10px rgba(0,0,0,0.2);
  }
  .word-row .hole{
    width:10px; height:10px; border-radius:50%;
    background:var(--walnut-dark);
    box-shadow:inset 0 1px 2px rgba(0,0,0,0.6);
    flex:0 0 auto;
  }
  .word-row .wtext{ flex:1; min-width:0; }
  .word-row .en{
    font-family:'Fraunces',serif; font-weight:600; font-size:17px; color:var(--ink);
  }
  .word-row .ipa{
    font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft); margin-left:6px;
  }
  .word-row .uz{ font-size:13px; color:var(--ink-soft); margin-top:1px; }
  .word-row .status-dot{
    width:9px; height:9px; border-radius:50%; flex:0 0 auto;
    background:var(--off-white-dim);
  }
  .word-row .status-dot.known{ background:var(--teal); }
  .word-row .status-dot.review{ background:var(--coral); }

  .empty-note{
    text-align:center; color:var(--off-white-dim); font-size:13.5px; padding:30px 10px;
    font-family:'IBM Plex Mono',monospace;
  }

  /* FLASHCARD SCREEN */
  .card-stage{
    display:flex; flex-direction:column; align-items:center; padding-top:6px;
  }
  .card-progress{
    font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--off-white-dim); margin-bottom:14px;
  }
  .flip-card{
    width:100%;
    max-width:340px;
    height:230px;
    perspective:1200px;
    margin-bottom:22px;
  }
  .flip-inner{
    position:relative; width:100%; height:100%;
    transform-style:preserve-3d;
    transition:transform 0.5s cubic-bezier(.4,.2,.2,1);
  }
  .flip-card.flipped .flip-inner{ transform:rotateY(180deg); }
  .face{
    position:absolute; inset:0;
    backface-visibility:hidden;
    border-radius:14px;
    background:var(--parchment);
    box-shadow:0 3px 0 rgba(0,0,0,0.3), 0 10px 24px rgba(0,0,0,0.35);
    display:flex; flex-direction:column; align-items:center; justify-content:center;
    padding:24px;
    text-align:center;
  }
  .face .tab{
    position:absolute; top:-14px; left:24px;
    background:var(--brass); color:var(--walnut-dark);
    font-family:'IBM Plex Mono',monospace; font-size:10px; font-weight:600;
    letter-spacing:1px; text-transform:uppercase;
    padding:4px 10px; border-radius:3px 3px 0 0;
  }
  .face .hole{
    position:absolute; top:14px; right:16px;
    width:12px; height:12px; border-radius:50%;
    background:var(--walnut-dark); box-shadow:inset 0 1px 2px rgba(0,0,0,0.6);
  }
  .face-word{ font-family:'Fraunces',serif; font-weight:700; font-size:30px; color:var(--ink); }
  .face-ipa{ font-family:'IBM Plex Mono',monospace; font-size:13px; color:var(--ink-soft); margin-top:6px; }
  .face-example{ font-size:12.5px; color:var(--ink-soft); margin-top:14px; font-style:italic; line-height:1.5; }
  .back .face-word{ color:var(--teal-deep); }
  .flip-back{ transform:rotateY(180deg); }
  .tap-hint{ font-size:11px; color:var(--off-white-dim); margin-top:-10px; margin-bottom:18px; font-family:'IBM Plex Mono',monospace; }

  .judge-row{ display:flex; gap:12px; width:100%; max-width:340px; }
  .judge-btn{
    flex:1; padding:14px 0; border:none; border-radius:10px;
    font-family:'Inter',sans-serif; font-weight:700; font-size:14px;
    cursor:pointer; color:var(--off-white);
  }
  .judge-btn.no{ background:var(--coral); }
  .judge-btn.no:active{ background:var(--coral-deep); }
  .judge-btn.yes{ background:var(--teal); }
  .judge-btn.yes:active{ background:var(--teal-deep); }
  .deck-done{ text-align:center; padding:50px 20px; }
  .deck-done .big-emoji{ font-size:44px; margin-bottom:10px; }
  .deck-done h3{ font-family:'Fraunces',serif; color:var(--parchment); font-size:20px; margin:0 0 6px; }
  .deck-done p{ color:var(--off-white-dim); font-size:13.5px; margin:0 0 20px; }

  /* QUIZ */
  .quiz-head{ display:flex; justify-content:space-between; align-items:center; margin:14px 0 18px; }
  .quiz-score{ font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--brass-bright); }
  .quiz-q-card{
    background:var(--parchment); border-radius:14px; padding:26px 22px;
    text-align:center; margin-bottom:18px;
    box-shadow:0 3px 0 rgba(0,0,0,0.3), 0 10px 24px rgba(0,0,0,0.3);
  }
  .quiz-q-eyebrow{ font-family:'IBM Plex Mono',monospace; font-size:10.5px; color:var(--ink-soft); text-transform:uppercase; letter-spacing:1px; margin-bottom:8px; }
  .quiz-q-word{ font-family:'Fraunces',serif; font-weight:700; font-size:26px; color:var(--ink); }
  .quiz-options{ display:flex; flex-direction:column; gap:10px; }
  .quiz-opt{
    background:var(--walnut-mid); border:1.5px solid var(--walnut-light);
    color:var(--off-white); padding:13px 16px; border-radius:10px;
    font-size:14.5px; font-weight:500; text-align:left; cursor:pointer;
    font-family:'Inter',sans-serif;
  }
  .quiz-opt.correct{ background:var(--teal); border-color:var(--teal); }
  .quiz-opt.wrong{ background:var(--coral); border-color:var(--coral); }
  .quiz-opt.dim{ opacity:0.5; }
  .quiz-summary{ text-align:center; padding:40px 20px; }
  .quiz-summary .score-big{ font-family:'Fraunces',serif; font-size:48px; color:var(--brass-bright); font-weight:700; }
  .quiz-summary p{ color:var(--off-white-dim); font-size:13.5px; }

  /* PROGRESS */
  .stat-grid{ display:grid; grid-template-columns:1fr 1fr; gap:10px; margin:14px 0 20px; }
  .stat-box{
    background:var(--walnut-mid); border:1px solid var(--walnut-light);
    border-radius:12px; padding:16px;
  }
  .stat-box .num{ font-family:'Fraunces',serif; font-size:28px; font-weight:700; color:var(--brass-bright); }
  .stat-box .lbl{ font-size:11.5px; color:var(--off-white-dim); margin-top:2px; font-family:'IBM Plex Mono',monospace; }
  .cat-bar-row{ margin-bottom:12px; }
  .cat-bar-top{ display:flex; justify-content:space-between; font-size:12.5px; color:var(--off-white-dim); margin-bottom:5px; }
  .cat-bar-top span:first-child{ color:var(--off-white); font-weight:600; }
  .cat-bar-track{ height:8px; background:var(--walnut-mid); border-radius:4px; overflow:hidden; }
  .cat-bar-fill{ height:100%; background:linear-gradient(90deg, var(--teal-deep), var(--teal)); border-radius:4px; }

  /* GENERIC BUTTON */
  .primary-btn{
    display:block; width:100%; text-align:center;
    background:linear-gradient(180deg, var(--brass-bright), var(--brass));
    color:var(--walnut-dark); font-weight:700; font-size:14.5px;
    border:none; border-radius:10px; padding:14px 0; cursor:pointer;
    font-family:'Inter',sans-serif;
  }

  /* TAB BAR */
  nav.tabbar{
    position:fixed; bottom:0; left:50%; transform:translateX(-50%);
    width:100%; max-width:480px;
    background:var(--walnut-dark);
    border-top:1px solid var(--walnut-light);
    display:flex;
    padding:8px 6px calc(8px + env(safe-area-inset-bottom));
    box-shadow:0 -4px 16px rgba(0,0,0,0.4);
  }
  .tab-btn{
    flex:1; background:none; border:none; color:var(--off-white-dim);
    display:flex; flex-direction:column; align-items:center; gap:3px;
    padding:6px 0; cursor:pointer; font-family:'Inter',sans-serif;
    font-size:10.5px; font-weight:600; letter-spacing:0.2px;
  }
  .tab-btn .icon{ font-size:19px; }
  .tab-btn.active{ color:var(--brass-bright); }
  .tab-btn.active .icon{ filter:drop-shadow(0 0 6px rgba(201,162,39,0.5)); }
</style>
</head>
<body>
<div id="app">

  <header>
    <div class="brand-row">
      <div class="brand">Lex<em>icon</em></div>
      <div class="streak">🔥 <span id="streakNum">0</span> kun</div>
    </div>
    <div class="subtitle">/// ingliz tili — soʻz kartotekasi</div>
  </header>

  <main>

    <!-- LUGʻAT -->
    <section class="screen active" id="screen-lugat">
      <span class="plate">📇 Kartoteka</span>
      <div class="search-wrap">
        <span class="search-icon">🔍</span>
        <input id="searchInput" type="text" placeholder="Soʻz qidirish...">
      </div>
      <div class="cat-scroller" id="catScroller"></div>
      <div id="wordList"></div>
    </section>

    <!-- KARTALAR -->
    <section class="screen" id="screen-cards">
      <span class="plate">🗂 Kartochkalar</span>
      <div class="card-stage" id="cardStage"></div>
    </section>

    <!-- VIKTORINA -->
    <section class="screen" id="screen-quiz">
      <span class="plate">✎ Viktorina</span>
      <div id="quizStage"></div>
    </section>

    <!-- NATIJA -->
    <section class="screen" id="screen-progress">
      <span class="plate">📊 Natijalar</span>
      <div id="progressStage"></div>
    </section>

  </main>

  <nav class="tabbar">
    <button class="tab-btn active" data-tab="lugat"><span class="icon">📇</span>Lugʻat</button>
    <button class="tab-btn" data-tab="cards"><span class="icon">🗂</span>Kartalar</button>
    <button class="tab-btn" data-tab="quiz"><span class="icon">✎</span>Viktorina</button>
    <button class="tab-btn" data-tab="progress"><span class="icon">📊</span>Natija</button>
  </nav>

</div>

<script>
/* ---------------- WORD BANK ---------------- */
const WORDS = [
  {id:1,en:"apple",ipa:"/ˈæpəl/",uz:"olma",cat:"Ovqat",ex:"She eats an apple every morning."},
  {id:2,en:"bread",ipa:"/bred/",uz:"non",cat:"Ovqat",ex:"We bought fresh bread today."},
  {id:3,en:"water",ipa:"/ˈwɔːtər/",uz:"suv",cat:"Ovqat",ex:"Drink more water in summer."},
  {id:4,en:"rice",ipa:"/raɪs/",uz:"guruch",cat:"Ovqat",ex:"Rice is a staple food in Uzbekistan."},
  {id:5,en:"meat",ipa:"/miːt/",uz:"goʻsht",cat:"Ovqat",ex:"He doesn't eat meat on Mondays."},
  {id:6,en:"sugar",ipa:"/ˈʃʊɡər/",uz:"shakar",cat:"Ovqat",ex:"Add two spoons of sugar to the tea."},
  {id:7,en:"breakfast",ipa:"/ˈbrekfəst/",uz:"nonushta",cat:"Ovqat",ex:"What did you have for breakfast?"},
  {id:8,en:"family",ipa:"/ˈfæməli/",uz:"oila",cat:"Oila",ex:"My family lives in Tashkent."},
  {id:9,en:"brother",ipa:"/ˈbrʌðər/",uz:"aka/uka",cat:"Oila",ex:"My brother works as an engineer."},
  {id:10,en:"sister",ipa:"/ˈsɪstər/",uz:"opa/singil",cat:"Oila",ex:"My sister studies medicine."},
  {id:11,en:"parents",ipa:"/ˈperənts/",uz:"ota-ona",cat:"Oila",ex:"His parents are very supportive."},
  {id:12,en:"friend",ipa:"/frend/",uz:"doʻst",cat:"Oila",ex:"She is my best friend."},
  {id:13,en:"neighbor",ipa:"/ˈneɪbər/",uz:"qoʻshni",cat:"Oila",ex:"Our neighbor is very kind."},
  {id:14,en:"work",ipa:"/wɜːrk/",uz:"ish",cat:"Ish",ex:"I go to work by bus."},
  {id:15,en:"salary",ipa:"/ˈsæləri/",uz:"maosh",cat:"Ish",ex:"He got a salary increase this year."},
  {id:16,en:"meeting",ipa:"/ˈmiːtɪŋ/",uz:"yigʻilish",cat:"Ish",ex:"The meeting starts at 9 AM."},
  {id:17,en:"deadline",ipa:"/ˈdedlaɪn/",uz:"muddat",cat:"Ish",ex:"We must finish before the deadline."},
  {id:18,en:"colleague",ipa:"/ˈkɒliːɡ/",uz:"hamkasb",cat:"Ish",ex:"My colleague helped me with the report."},
  {id:19,en:"manager",ipa:"/ˈmænɪdʒər/",uz:"menejer",cat:"Ish",ex:"The manager approved our project."},
  {id:20,en:"journey",ipa:"/ˈdʒɜːrni/",uz:"sayohat",cat:"Sayohat",ex:"Our journey to Samarkand was amazing."},
  {id:21,en:"airport",ipa:"/ˈeəpɔːrt/",uz:"aeroport",cat:"Sayohat",ex:"We arrived at the airport early."},
  {id:22,en:"luggage",ipa:"/ˈlʌɡɪdʒ/",uz:"yuk",cat:"Sayohat",ex:"Please don't forget your luggage."},
  {id:23,en:"ticket",ipa:"/ˈtɪkɪt/",uz:"chipta",cat:"Sayohat",ex:"I bought two train tickets."},
  {id:24,en:"passport",ipa:"/ˈpæspɔːrt/",uz:"passport",cat:"Sayohat",ex:"Keep your passport safe while traveling."},
  {id:25,en:"hotel",ipa:"/hoʊˈtel/",uz:"mehmonxona",cat:"Sayohat",ex:"We stayed at a small hotel."},
  {id:26,en:"mountain",ipa:"/ˈmaʊntən/",uz:"tog'",cat:"Tabiat",ex:"The mountain was covered with snow."},
  {id:27,en:"river",ipa:"/ˈrɪvər/",uz:"daryo",cat:"Tabiat",ex:"The river flows through the valley."},
  {id:28,en:"forest",ipa:"/ˈfɒrɪst/",uz:"o'rmon",cat:"Tabiat",ex:"We walked through the quiet forest."},
  {id:29,en:"weather",ipa:"/ˈweðər/",uz:"ob-havo",cat:"Tabiat",ex:"The weather is cold today."},
  {id:30,en:"sunrise",ipa:"/ˈsʌnraɪz/",uz:"quyosh chiqishi",cat:"Tabiat",ex:"We watched the sunrise from the hill."},
  {id:31,en:"happy",ipa:"/ˈhæpi/",uz:"baxtli",cat:"His-tuyg'u",ex:"She looks happy today."},
  {id:32,en:"tired",ipa:"/ˈtaɪərd/",uz:"charchagan",cat:"His-tuyg'u",ex:"I feel tired after work."},
  {id:33,en:"worried",ipa:"/ˈwʌrid/",uz:"xavotirli",cat:"His-tuyg'u",ex:"He was worried about the exam."},
  {id:34,en:"excited",ipa:"/ɪkˈsaɪtɪd/",uz:"hayajonlangan",cat:"His-tuyg'u",ex:"They are excited about the trip."},
  {id:35,en:"proud",ipa:"/praʊd/",uz:"faxrlangan",cat:"His-tuyg'u",ex:"Her parents are proud of her."},
  {id:36,en:"schedule",ipa:"/ˈskedʒuːl/",uz:"jadval",cat:"Vaqt",ex:"Check the schedule before you leave."},
  {id:37,en:"appointment",ipa:"/əˈpɔɪntmənt/",uz:"uchrashuv",cat:"Vaqt",ex:"I have a doctor's appointment tomorrow."},
  {id:38,en:"early",ipa:"/ˈɜːrli/",uz:"erta",cat:"Vaqt",ex:"He always arrives early."},
  {id:39,en:"deadline",ipa:"/ˈdedlaɪn/",uz:"muddat",cat:"Vaqt",ex:"The report deadline is Friday."},
  {id:40,en:"weekend",ipa:"/ˈwiːkend/",uz:"dam olish kuni",cat:"Vaqt",ex:"What are your weekend plans?"},
  {id:41,en:"clean",ipa:"/kliːn/",uz:"tozalamoq",cat:"Kundalik",ex:"I clean my room every Sunday."},
  {id:42,en:"cook",ipa:"/kʊk/",uz:"pishirmoq",cat:"Kundalik",ex:"My mother cooks dinner every evening."},
  {id:43,en:"study",ipa:"/ˈstʌdi/",uz:"o'qimoq",cat:"Kundalik",ex:"I study English every day."},
  {id:44,en:"exercise",ipa:"/ˈeksərsaɪz/",uz:"mashq qilmoq",cat:"Kundalik",ex:"He exercises in the morning."},
  {id:45,en:"shopping",ipa:"/ˈʃɒpɪŋ/",uz:"xarid qilish",cat:"Kundalik",ex:"We went shopping for groceries."},
  {id:46,en:"remember",ipa:"/rɪˈmembər/",uz:"eslamoq",cat:"Kundalik",ex:"Do you remember his name?"},
  {id:47,en:"decide",ipa:"/dɪˈsaɪd/",uz:"qaror qilmoq",cat:"Kundalik",ex:"We need to decide today."},
  {id:48,en:"improve",ipa:"/ɪmˈpruːv/",uz:"yaxshilamoq",cat:"Kundalik",ex:"I want to improve my English."},
  {id:49,en:"borrow",ipa:"/ˈbɒroʊ/",uz:"qarz olmoq",cat:"Kundalik",ex:"Can I borrow your pen?"},
  {id:50,en:"explain",ipa:"/ɪkˈspleɪn/",uz:"tushuntirmoq",cat:"Kundalik",ex:"Could you explain this word?"}
];
const CATEGORIES = [...new Set(WORDS.map(w=>w.cat))];

/* ---------------- STATE ---------------- */
let progress = { known:{}, streak:0, lastDate:null, quizBest:0 };
let activeCat = "Barchasi";
let deck = [];
let deckIdx = 0;
let quiz = { qs:[], idx:0, score:0, locked:false };

/* ---------------- STORAGE ---------------- */
async function loadProgress(){
  try{
    const r = await window.storage.get('lexicon-progress', false);
    if(r && r.value){ progress = JSON.parse(r.value); }
  }catch(e){ /* first run, no data yet */ }
  updateStreakToday();
  renderStreak();
}
async function saveProgress(){
  try{ await window.storage.set('lexicon-progress', JSON.stringify(progress), false); }
  catch(e){ console.error('Saqlashda xatolik', e); }
}
function updateStreakToday(){
  const today = new Date().toISOString().slice(0,10);
  if(progress.lastDate === today) return;
  const y = new Date(Date.now()-86400000).toISOString().slice(0,10);
  progress.streak = (progress.lastDate === y) ? progress.streak + 1 : 1;
  progress.lastDate = today;
  saveProgress();
}
function renderStreak(){ document.getElementById('streakNum').textContent = progress.streak; }

/* ---------------- TABS ---------------- */
document.querySelectorAll('.tab-btn').forEach(btn=>{
  btn.addEventListener('click', ()=>switchTab(btn.dataset.tab));
});
function switchTab(name){
  document.querySelectorAll('.tab-btn').forEach(b=>b.classList.toggle('active', b.dataset.tab===name));
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('screen-'+name).classList.add('active');
  if(name==='cards') startDeck();
  if(name==='quiz') startQuiz();
  if(name==='progress') renderProgress();
}

/* ---------------- LUGʻAT ---------------- */
function renderCatScroller(){
  const el = document.getElementById('catScroller');
  const cats = ["Barchasi", ...CATEGORIES];
  el.innerHTML = cats.map(c=>`<button class="cat-chip ${c===activeCat?'active':''}" data-cat="${c}">${c}</button>`).join('');
  el.querySelectorAll('.cat-chip').forEach(chip=>{
    chip.addEventListener('click', ()=>{ activeCat = chip.dataset.cat; renderCatScroller(); renderWordList(); });
  });
}
function renderWordList(){
  const q = document.getElementById('searchInput').value.trim().toLowerCase();
  let list = WORDS.filter(w => activeCat==="Barchasi" || w.cat===activeCat);
  if(q) list = list.filter(w => w.en.toLowerCase().includes(q) || w.uz.toLowerCase().includes(q));
  const el = document.getElementById('wordList');
  if(list.length===0){ el.innerHTML = `<div class="empty-note">Hech narsa topilmadi. Boshqa soʻz bilan qidiring.</div>`; return; }
  el.innerHTML = list.map(w=>{
    const st = progress.known[w.id];
    const dotClass = st==='known' ? 'known' : (st==='review' ? 'review' : '');
    return `<div class="word-row" data-id="${w.id}">
      <div class="hole"></div>
      <div class="wtext">
        <div><span class="en">${w.en}</span><span class="ipa">${w.ipa}</span></div>
        <div class="uz">${w.uz}</div>
      </div>
      <div class="status-dot ${dotClass}"></div>
    </div>`;
  }).join('');
  el.querySelectorAll('.word-row').forEach(row=>{
    row.addEventListener('click', ()=>{
      const id = row.dataset.id;
      const cur = progress.known[id];
      progress.known[id] = cur==='known' ? undefined : 'known';
      if(progress.known[id]===undefined) delete progress.known[id];
      saveProgress();
      renderWordList();
    });
  });
}
document.getElementById('searchInput').addEventListener('input', renderWordList);

/* ---------------- KARTALAR (FLASHCARDS) ---------------- */
function startDeck(){
  // review words needing practice first, then unknown, then known
  const unfamiliar = WORDS.filter(w=>progress.known[w.id]!=='known');
  deck = unfamiliar.length ? shuffle(unfamiliar) : shuffle(WORDS.slice());
  deckIdx = 0;
  renderCard();
}
function shuffle(arr){ const a=arr.slice(); for(let i=a.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [a[i],a[j]]=[a[j],a[i]]; } return a; }
function renderCard(){
  const stage = document.getElementById('cardStage');
  if(deckIdx >= deck.length){
    stage.innerHTML = `<div class="deck-done">
      <div class="big-emoji">📚</div>
      <h3>Toʻplam tugadi!</h3>
      <p>Siz ${deck.length} ta kartochkani koʻrib chiqdingiz.</p>
      <button class="primary-btn" id="restartDeck">Qaytadan boshlash</button>
    </div>`;
    document.getElementById('restartDeck').addEventListener('click', startDeck);
    return;
  }
  const w = deck[deckIdx];
  stage.innerHTML = `
    <div class="card-progress">${deckIdx+1} / ${deck.length} — ${w.cat}</div>
    <div class="flip-card" id="flipCard">
      <div class="flip-inner">
        <div class="face front">
          <span class="tab">Ingliz tilida</span>
          <div class="hole"></div>
          <div class="face-word">${w.en}</div>
          <div class="face-ipa">${w.ipa}</div>
        </div>
        <div class="face back flip-back">
          <span class="tab">Tarjima</span>
          <div class="hole"></div>
          <div class="face-word">${w.uz}</div>
          <div class="face-example">${w.ex}</div>
        </div>
      </div>
    </div>
    <div class="tap-hint">kartaga bosing — aylantirish</div>
    <div class="judge-row">
      <button class="judge-btn no" id="btnNo">🔁 Takrorlash kerak</button>
      <button class="judge-btn yes" id="btnYes">✓ Bilaman</button>
    </div>
  `;
  const flip = document.getElementById('flipCard');
  flip.addEventListener('click', ()=> flip.classList.toggle('flipped'));
  document.getElementById('btnYes').addEventListener('click', (e)=>{ e.stopPropagation(); judge(w,'known'); });
  document.getElementById('btnNo').addEventListener('click', (e)=>{ e.stopPropagation(); judge(w,'review'); });
}
function judge(w, status){
  progress.known[w.id] = status;
  saveProgress();
  deckIdx++;
  renderCard();
}

/* ---------------- VIKTORINA (QUIZ) ---------------- */
function startQuiz(){
  const pool = shuffle(WORDS.slice()).slice(0, 10);
  quiz.qs = pool.map(w=>{
    const wrongPool = shuffle(WORDS.filter(x=>x.id!==w.id)).slice(0,3).map(x=>x.uz);
    const options = shuffle([w.uz, ...wrongPool]);
    return { word:w, options, answer:w.uz };
  });
  quiz.idx = 0; quiz.score = 0; quiz.locked = false;
  renderQuiz();
}
function renderQuiz(){
  const stage = document.getElementById('quizStage');
  if(quiz.idx >= quiz.qs.length){
    if(quiz.score > progress.quizBest){ progress.quizBest = quiz.score; saveProgress(); }
    stage.innerHTML = `<div class="quiz-summary">
      <div class="score-big">${quiz.score}/${quiz.qs.length}</div>
      <p>toʻgʻri javob. Eng yaxshi natija: ${progress.quizBest}/${quiz.qs.length}</p>
      <button class="primary-btn" id="restartQuiz">Yana urinib koʻrish</button>
    </div>`;
    document.getElementById('restartQuiz').addEventListener('click', startQuiz);
    return;
  }
  const q = quiz.qs[quiz.idx];
  stage.innerHTML = `
    <div class="quiz-head">
      <span class="card-progress" style="margin:0">Savol ${quiz.idx+1} / ${quiz.qs.length}</span>
      <span class="quiz-score">Ball: ${quiz.score}</span>
    </div>
    <div class="quiz-q-card">
      <div class="quiz-q-eyebrow">Bu soʻz nima maʼnoni bildiradi?</div>
      <div class="quiz-q-word">${q.word.en}</div>
    </div>
    <div class="quiz-options" id="quizOptions">
      ${q.options.map(o=>`<button class="quiz-opt" data-opt="${o}">${o}</button>`).join('')}
    </div>
  `;
  quiz.locked = false;
  document.querySelectorAll('.quiz-opt').forEach(btn=>{
    btn.addEventListener('click', ()=> answerQuiz(btn, q));
  });
}
function answerQuiz(btn, q){
  if(quiz.locked) return;
  quiz.locked = true;
  const chosen = btn.dataset.opt;
  const correct = chosen === q.answer;
  if(correct) quiz.score++;
  document.querySelectorAll('.quiz-opt').forEach(b=>{
    if(b.dataset.opt === q.answer) b.classList.add('correct');
    else if(b===btn) b.classList.add('wrong');
    else b.classList.add('dim');
    b.disabled = true;
  });
  progress.known[q.word.id] = correct ? 'known' : 'review';
  saveProgress();
  setTimeout(()=>{ quiz.idx++; renderQuiz(); }, 900);
}

/* ---------------- PROGRESS ---------------- */
function renderProgress(){
  const known = Object.values(progress.known).filter(v=>v==='known').length;
  const review = Object.values(progress.known).filter(v=>v==='review').length;
  const total = WORDS.length;
  const stage = document.getElementById('progressStage');
  let catRows = CATEGORIES.map(cat=>{
    const catWords = WORDS.filter(w=>w.cat===cat);
    const catKnown = catWords.filter(w=>progress.known[w.id]==='known').length;
    const pct = Math.round((catKnown/catWords.length)*100);
    return `<div class="cat-bar-row">
      <div class="cat-bar-top"><span>${cat}</span><span>${catKnown}/${catWords.length}</span></div>
      <div class="cat-bar-track"><div class="cat-bar-fill" style="width:${pct}%"></div></div>
    </div>`;
  }).join('');
  stage.innerHTML = `
    <div class="stat-grid">
      <div class="stat-box"><div class="num">${known}</div><div class="lbl">BILAMAN</div></div>
      <div class="stat-box"><div class="num">${review}</div><div class="lbl">TAKRORLASH</div></div>
      <div class="stat-box"><div class="num">${total-known-review}</div><div class="lbl">YANGI</div></div>
      <div class="stat-box"><div class="num">${progress.streak}</div><div class="lbl">KUNLIK SERIYA</div></div>
    </div>
    <span class="plate" style="margin-bottom:10px; display:inline-block">Kategoriyalar boʻyicha</span>
    ${catRows}
  `;
}

/* ---------------- INIT ---------------- */
(async function init(){
  await loadProgress();
  renderCatScroller();
  renderWordList();
})();
</script>
</body>
</html>
