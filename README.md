<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Morning Flow - Run For Recovery</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Billabong&display=swap" rel="stylesheet">
<style>
body { margin:0; font-family:'Poppins',sans-serif; background: linear-gradient(160deg,#FFD194,#D6A4A4); color:#fff; }
header{text-align:center;padding:1rem;}
header h1{ font-family:'Billabong', cursive; font-size:3rem; text-shadow:0 0 12px #fff; margin:0; letter-spacing:1px;}
main{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1rem;padding:1rem;justify-items:center;}
.card{ background: rgba(255,255,255,0.15); backdrop-filter: blur(15px); border-radius:20px; padding:1rem; box-shadow:0 12px 25px rgba(0,0,0,0.25); width:90%; max-width:360px; position:relative; }
.time-boxes {display:flex;justify-content:space-between;margin-top:1rem;}
.time-box{ flex:1; margin:0 0.3rem; background: rgba(255,111,97,0.3); border-radius:12px; text-align:center; padding:0.5rem; font-weight:600;}
textarea#journalInput{ width:100%; height:100px; border-radius:15px; border:none; padding:0.75rem; background: rgba(255,255,255,0.08); backdrop-filter: blur(10px); color:#fff; font-family:'Poppins',sans-serif; font-size:1rem; resize:vertical; box-shadow: 0 4px 15px rgba(0,0,0,0.25);}
#journalEntries{ max-height:180px; overflow-y:auto; margin-top:0.5rem;}
#journalEntries p{ background: rgba(255,255,255,0.08); padding:0.5rem; border-radius:12px; margin-bottom:0.5rem; word-wrap:break-word; font-family:'Poppins',sans-serif; font-size:0.95rem;}
button{ padding:0.5rem 1rem; border:none; border-radius:12px; background:#FF6F61; color:#fff; font-weight:600; cursor:pointer; margin-top:0.5rem; transition: transform 0.2s;}
button:hover{transform: scale(1.05);}
.habit-item{ display:flex; align-items:center; margin:0.5rem 0;}
.habit-item input[type="checkbox"]{ width:24px; height:24px; margin-right:0.6rem; cursor:pointer; accent-color:#FF6F61; transition: transform 0.2s;}
.habit-item input[type="checkbox"]:hover{transform: scale(1.2);}
.breathing-circle{ width:100px;height:100px;margin:1rem auto;border-radius:50%; background: linear-gradient(135deg,#FFD194,#FF6F61); display:flex;align-items:center;justify-content:center; font-weight:600;font-size:1.2rem;color:#fff; transition: width 4s ease-in-out,height 4s ease-in-out;}
footer{text-align:center;margin:1rem 0;font-size:0.8rem;}
footer a{color:#fff;text-decoration:none;}
.start-day-box{ background: rgba(255,255,255,0.12); padding:1rem; border-radius:18px; text-align:center; margin-bottom:1rem; box-shadow:0 6px 15px rgba(0,0,0,0.2);}
select#moodSelect{ width:100%; border-radius:12px; padding:0.5rem; margin-bottom:0.5rem; border:none; background: rgba(255,255,255,0.08); color:#fff; backdrop-filter: blur(5px); }
</style>
</head>
<body>
<header>
<h1>Morning Flow</h1>
</header>
<main>
<div class="card">
<h2>Sobriety Timer</h2>
<input type="date" id="sobrietyDate" style="border-radius:15px; padding:0.5rem; border:none; background:rgba(255,255,255,0.1); color:#fff; text-align:center;">
<div class="time-boxes">
<div class="time-box"><span id="days">00</span><br>Days</div>
<div class="time-box"><span id="hours">00</span><br>Hours</div>
<div class="time-box"><span id="minutes">00</span><br>Minutes</div>
<div class="time-box"><span id="seconds">00</span><br>Seconds</div>
</div>
<button onclick="shareSobriety()">Share My Sobriety</button>
</div>
<div class="card start-day-box">
<h2>Daily Reflection</h2>
<a href="https://www.aa.org/daily-reflection" target="_blank"><button>Read Daily Reflection</button></a>
</div>
<div class="card">
<h2>Box Breathing</h2>
<div class="breathing-circle" id="breathingCircle">Inhale</div>
<div style="text-align:center;"><span id="breathingTimer">4</span> sec</div>
</div>
<div class="card">
<h2>Daily Habits</h2>
<div class="habit-item"><input type="checkbox" class="habit-check"> Pray / Reflect</div>
<div class="habit-item"><input type="checkbox" class="habit-check"> Call Someone</div>
<div class="habit-item"><input type="checkbox" class="habit-check"> Read Daily Reflection</div>
<button onclick="checkHabits()">Complete Habits</button>
<div class="celebration-animation" id="celebration"></div>
</div>
<div class="card">
<h2>Journal</h2>
<label for="moodSelect">How are you feeling today?</label>
<select id="moodSelect">
<option value="" disabled selected>Select your mood</option>
<option value="Happy 😊">Happy 😊</option>
<option value="Sad 😢">Sad 😢</option>
<option value="Anxious 😰">Anxious 😰</option>
<option value="Excited 😃">Excited 😃</option>
<option value="Grateful 🙏">Grateful 🙏</option>
<option value="Tired 😴">Tired 😴</option>
<option value="Angry 😡">Angry 😡</option>
</select>
<textarea id="journalInput" placeholder="Write your gratitude or thoughts..."></textarea>
<div style="display:flex;gap:0.5rem;margin-top:0.5rem;"><button onclick="saveJournal()">Save Entry</button></div>
<div id="journalEntries"></div>
</div>
<div class="card">
<h2>Daily Quote</h2>
<div id="quote">Tap for another quote</div>
<button onclick="nextQuote()">Tap for another quote</button>
<h2>Action for Today</h2>
<div id="word"></div>
<h2>Bible Verse</h2>
<div id="verse">Tap for another verse</div>
<button onclick="nextVerse()">Tap for another verse</button>
</div>
<div class="card">
<h2>Meetings & Big Book</h2>
<p><a href="https://www.aa.org/pages/en_US/find-aa-resources" target="_blank">Online Meetings</a></p>
<p><a href="https://www.aa.org/pages/en_US/meeting-guide" target="_blank">In-Person Meetings</a></p>
<p><a href="https://share.google/C3Sj4Qc2yk8mIjMtV" target="_blank">Digital Big Book</a></p>
</div>
<div class="card">
<h2>Support Us</h2>
<button onclick="alert('Thank you for your support!')">Support Us</button>
</div>
</main>
<footer>
<p>Designed by Corey</p>
<p>Instagram: <a href="https://www.instagram.com/reverserunners?igsh=MzRlODBiNWFlZA==" target="_blank">@reverserunners</a></p>
<small>Suicide Hotline: 1-800-273-8255</small>
</footer>
<script>
// Sobriety Timer
const sobrietyDateInput = document.getElementById('sobrietyDate');
function updateTimer(){
  const now = new Date();
  const date = new Date(sobrietyDateInput.value);
  if(!date || !sobrietyDateInput.value) return;
  let diff = now - date;
  if(diff<0) diff=0;
  const d = Math.floor(diff/1000/60/60/24);
  const h = Math.floor(diff/1000/60/60)%24;
  const m = Math.floor(diff/1000/60)%60;
  const s = Math.floor(diff/1000)%60;
  document.getElementById('days').textContent=d;
  document.getElementById('hours').textContent=h;
  document.getElementById('minutes').textContent=m;
  document.getElementById('seconds').textContent=s;
}
sobrietyDateInput.addEventListener('change', updateTimer);
setInterval(updateTimer, 1000);

function shareSobriety(){
  alert(`I've been sober since ${sobrietyDateInput.value}`);
}

// Placeholder functions for other features
function saveJournal(){ alert('Journal saved!'); }
function checkHabits(){ alert('Habits completed!'); }
function nextQuote(){ document.getElementById('quote').textContent='Keep pushing forward!'; }
function nextVerse(){ document.getElementById('verse').textContent='Philippians 4:13 - I can do all things through Christ who strengthens me.'; }
</script>
</body>
</html>
