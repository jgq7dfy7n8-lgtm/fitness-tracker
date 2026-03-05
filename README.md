# fitness-tracker<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<title>Fitness Tracker</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
body{background:#0a0f14;color:#fff;font-family:system-ui,-apple-system,sans-serif;max-width:480px;margin:0 auto;padding-bottom:80px;min-height:100vh;}
input,select,button{font-family:inherit;outline:none;}
.card{background:#111c27;border-radius:16px;padding:18px;border:1px solid #1e3448;margin-bottom:10px;}
.inp{background:#0d1820;border:2px solid #1e3448;border-radius:10px;padding:12px 14px;color:#fff;font-size:14px;width:100%;}
.btn{background:#39ff84;border:none;border-radius:10px;color:#000;padding:12px 20px;font-weight:800;font-size:13px;cursor:pointer;}
.lbl{font-size:10px;color:#4a7090;letter-spacing:3px;font-weight:700;margin-bottom:10px;display:block;text-transform:uppercase;}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px;}
.nav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;background:#080d12;border-top:2px solid #1e3448;padding:8px 4px 14px;display:flex;gap:2px;z-index:100;}
.nav button{flex:1;padding:6px 2px;background:none;border:1px solid transparent;border-radius:8px;color:#4a7090;font-size:7px;letter-spacing:0.4px;cursor:pointer;font-family:inherit;font-weight:700;display:flex;flex-direction:column;align-items:center;gap:3px;}
.nav button.active{background:#39ff8422;border-color:#39ff8466;color:#39ff84;}
.nav button span.icon{font-size:16px;}
.tab{display:none;padding:16px 16px 0;}
.tab.active{display:block;}
.header{background:linear-gradient(180deg,#0d2a1a,#0a0f14);padding:24px 16px 0;border-bottom:1px solid #1e3448;}
.pill{background:#39ff8422;border:1px solid #39ff8455;border-radius:12px;padding:10px 14px;text-align:right;}
.progress-bar{height:6px;background:#1e3448;border-radius:999px;overflow:hidden;margin-bottom:14px;}
.progress-fill{height:100%;border-radius:999px;background:linear-gradient(90deg,#39ff84,#00d4ff);transition:width 0.8s ease;}
.row{display:flex;align-items:center;gap:8px;}
.between{display:flex;justify-content:space-between;align-items:center;}
.seg{display:flex;background:#152638;border-radius:10px;padding:4px;margin-bottom:14px;}
.seg button{flex:1;padding:8px 4px;background:none;border:none;border-radius:8px;color:#6b8aaa;font-size:10px;letter-spacing:2px;cursor:pointer;font-family:inherit;font-weight:400;}
.seg button.active{background:#39ff84;color:#0d1a27;font-weight:700;}
.meal-item{background:#122030;border-radius:10px;padding:10px 14px;margin-bottom:6px;display:flex;justify-content:space-between;align-items:center;}
.rm-btn{background:none;border:none;color:#6b8aaa;cursor:pointer;font-size:18px;line-height:1;padding:0 4px;}
.rest-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:16px;}
.rest-btn{background:#111c27;border-radius:12px;padding:12px 6px;cursor:pointer;border:1px solid #2a4060;display:flex;flex-direction:column;align-items:center;gap:6px;font-family:inherit;}
.rest-btn span{font-size:10px;font-weight:800;color:#fff;}
</style>
</head>
<body>

<!-- HEADER -->

<div class="header" id="header">
  <div class="between" style="margin-bottom:14px;">
    <div>
      <div style="font-size:10px;letter-spacing:4px;color:#39ff84;font-weight:700;margin-bottom:4px;">10 LB CUT</div>
      <div style="font-size:34px;font-weight:900;letter-spacing:-2px;line-height:1;" id="hdr-weight">180<span style="font-size:14px;font-weight:500;color:#4a7090;margin-left:4px;">lbs</span></div>
      <div style="font-size:12px;color:#4a7090;margin-top:4px;font-weight:600;" id="hdr-lost">Start: 180 lbs</div>
    </div>
    <div class="pill">
      <div style="font-size:10px;color:#39ff84;font-weight:700;letter-spacing:2px;">GOAL</div>
      <div style="font-size:22px;font-weight:900;color:#39ff84;" id="hdr-goal">170</div>
      <div style="font-size:10px;color:#4a7090;margin-top:2px;" id="hdr-days">-- d left</div>
    </div>
  </div>
  <div class="progress-bar"><div class="progress-fill" id="hdr-prog" style="width:0%"></div></div>
  <div class="row" style="padding-bottom:14px;gap:8px;">
    <input type="date" id="sel-date" style="background:#0d1820;border:1px solid #1e3448;border-radius:8px;color:#fff;padding:7px 12px;font-size:12px;font-weight:600;">
    <button onclick="setToday()" style="background:#1e3448;border:none;border-radius:8px;color:#39ff84;padding:7px 12px;font-size:11px;cursor:pointer;font-weight:700;">TODAY</button>
  </div>
</div>

<!-- TABS -->

<div class="tab active" id="tab-home"></div>
<div class="tab" id="tab-food"></div>
<div class="tab" id="tab-lift"></div>
<div class="tab" id="tab-weight"></div>
<div class="tab" id="tab-stats"></div>
<div class="tab" id="tab-goals"></div>

<!-- NAV -->

<nav class="nav">
  <button class="active" onclick="showTab('home',this)"><span class="icon">⚡</span><span>HOME</span></button>
  <button onclick="showTab('food',this)"><span class="icon">🍽️</span><span>FOOD</span></button>
  <button onclick="showTab('lift',this)"><span class="icon">💪</span><span>LIFT</span></button>
  <button onclick="showTab('weight',this)"><span class="icon">⚖️</span><span>WEIGHT</span></button>
  <button onclick="showTab('stats',this)"><span class="icon">📈</span><span>STATS</span></button>
  <button onclick="showTab('goals',this)"><span class="icon">⚙️</span><span>GOALS</span></button>
</nav>

<script>
// ── STORAGE ──────────────────────────────────────────────────────
function load(k,d){try{const s=localStorage.getItem(k);return s?JSON.parse(s):d;}catch(e){return d;}}
function save(k,v){try{localStorage.setItem(k,JSON.stringify(v));}catch(e){}}

// ── STATE ─────────────────────────────────────────────────────────
let settings = load('ft_s3', {goalWeight:170,startWeight:180,goalDate:'2026-05-06',startDate:'2026-03-03',dailyCal:2000,dailyProtein:170});
let logs     = load('ft_l3', {});
let weights  = load('ft_w3', {});
let schedule = load('ft_sc3', {});
let selDate  = new Date().toISOString().split('T')[0];
let curTab   = 'home';
let wkMode   = 'today';
let menuRest = null;

// ── HELPERS ───────────────────────────────────────────────────────
function today(){ return new Date().toISOString().split('T')[0]; }
function todayDOW(){ return new Date().getDay(); }
function daysSince(d){ return Math.max(0,Math.round((new Date()-new Date(d))/(864e5))); }
function h(tag,cls,style,html,attrs){
  const a=attrs?Object.entries(attrs).map(([k,v])=>` ${k}="${v}"`).join(''):'';
  return `<${tag}${cls?` class="${cls}"`:''}${style?` style="${style}"`:''}${a}>${html||''}</${tag}>`;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }

// ── DATA ──────────────────────────────────────────────────────────
const MEAL_SECS = [
  {key:'breakfast',label:'Breakfast',emoji:'🌅',color:'#f59e0b'},
  {key:'lunch',    label:'Lunch',    emoji:'☀️', color:'#22d3ee'},
  {key:'dinner',   label:'Dinner',   emoji:'🌙', color:'#a78bfa'},
  {key:'snacks',   label:'Snacks',   emoji:'🍎', color:'#39ff84'},
];

const WORKOUTS = {
  'Push Day':{emoji:'💪',duration:'45 min',focus:'Chest · Shoulders · Triceps',
    exercises:[
      {name:'Bench Press',sets:'4×8-10',note:'Bar to mid-chest, elbows 45°. Rest 90s.'},
      {name:'Dumbbell Incline Press',sets:'3×10-12',note:'30-45° bench. Full stretch at bottom. Rest 75s.'},
      {name:'Dumbbell Lateral Raise',sets:'3×15',note:'Lead with elbows, raise to shoulder height. Rest 60s.'},
      {name:'Cable Overhead Tricep Extension',sets:'3×12-15',note:'Rope, high pulley. Elbows forward. Rest 60s.'},
      {name:'Cable Tricep Pushdown',sets:'3×12-15',note:'Elbows pinned. Full lockout every rep. Rest 60s.'},
      {name:'Apple Fitness+ Core',sets:'10 min',note:'Core class to finish. Non-negotiable.'},
    ]},
  'Pull Day':{emoji:'🔗',duration:'45 min',focus:'Back · Biceps · Rear Delts',
    exercises:[
      {name:'Wide-Grip Lat Pulldown',sets:'4×8-10',note:'Pull to upper chest. Full dead hang at top. Rest 90s.'},
      {name:'Close-Grip Lat Pulldown',sets:'3×10-12',note:'Neutral grip, pull to sternum. Rest 75s.'},
      {name:'Seated Cable Row',sets:'3×10-12',note:'Pull to navel, drive elbows back. Torso upright. Rest 75s.'},
      {name:'Cable Bicep Curl',sets:'3×12-15',note:'Elbows pinned. Full extension at bottom. Rest 60s.'},
      {name:'Dumbbell Hammer Curl',sets:'3×12',note:'Neutral grip. Full extension, squeeze at top. Rest 60s.'},
      {name:'Apple Fitness+ Core',sets:'10 min',note:'Core class to finish.'},
    ]},
  'Lower Body':{emoji:'🦵',duration:'45 min',focus:'Quads · Hamstrings · Glutes · Calves',
    exercises:[
      {name:'Back Squat',sets:'4×6-8',note:'Hit parallel every rep. Rest 2 min.'},
      {name:'Romanian Deadlift',sets:'3×10',note:'Hinge at hips, feel hamstring stretch. Rest 90s.'},
      {name:'Walking Lunges',sets:'3×10 each leg',note:'Torso upright, front knee tracks toes. Rest 75s.'},
      {name:'Leg Press',sets:'3×12-15',note:'90° knee bend, don\'t lock out at top. Rest 75s.'},
      {name:'Leg Curl',sets:'3×12-15',note:'2s up, 3s down. Full range. Rest 60s.'},
      {name:'Calf Raises',sets:'3×20',note:'Full stretch at bottom, full contraction at top. Rest 45s.'},
      {name:'Apple Fitness+ Core',sets:'10 min',note:'Core class to finish.'},
    ]},
  'Upper Body':{emoji:'🏋️',duration:'45 min',focus:'Chest · Back · Biceps · Triceps',
    exercises:[
      {name:'Bench Press',sets:'4×8-10',note:'Heaviest compound first. Rest 90s.'},
      {name:'Wide-Grip Lat Pulldown',sets:'3×10-12',note:'Full dead hang at top. Rest 75s.'},
      {name:'Dumbbell Shoulder Press',sets:'3×10-12',note:'Full lockout overhead. Rest 75s.'},
      {name:'Seated Cable Row',sets:'3×10-12',note:'Pause at contraction. Rest 75s.'},
      {name:'Bicep Curl + Tricep Pushdown',sets:'3 supersets × 12',note:'No rest between exercises. Rest 75s between sets.'},
      {name:'Apple Fitness+ Core',sets:'10 min',note:'Core class to finish.'},
    ]},
  'Active Recovery':{emoji:'🧘',duration:'25-35 min',focus:'Mobility · Flexibility',
    exercises:[
      {name:'Easy Walk',sets:'15-20 min',note:'Conversational pace. Outdoors preferred.'},
      {name:'Hip Flexor Stretch',sets:'2×45s each side',note:'Kneeling lunge, shift weight forward.'},
      {name:'Pigeon Pose',sets:'2×60s each side',note:'Let gravity work over the full minute.'},
      {name:'Thoracic Rotation',sets:'2×10 each side',note:'Side lying, rotate top arm open behind you.'},
      {name:'Hamstring Stretch',sets:'2×45s each side',note:'Flat back. Feel it in belly of hamstring.'},
      {name:'Foam Roll',sets:'5 min',note:'Pause 20-30s on tight spots.'},
    ]},
};

const RESTAURANTS = {
  'Naya':{emoji:'🫓',color:'#f59e0b',items:[
    {name:'Chicken Shawarma Salad',cal:380,protein:32,carbs:18,fat:18,emoji:'🥗'},
    {name:'Beef Shawarma Salad',cal:430,protein:34,carbs:18,fat:22,emoji:'🥗'},
    {name:'Chicken Shawarma Bowl',cal:480,protein:36,carbs:52,fat:12,emoji:'🫓'},
    {name:'Beef Shawarma Bowl',cal:530,protein:38,carbs:52,fat:16,emoji:'🫓'},
    {name:'Falafel Bowl',cal:560,protein:18,carbs:72,fat:22,emoji:'🧆'},
    {name:'Garlic Whip',cal:60,protein:0,carbs:2,fat:6,emoji:'🧄'},
    {name:'Hummus',cal:120,protein:6,carbs:10,fat:7,emoji:'🫘'},
  ]},
  'Chipotle':{emoji:'🌯',color:'#ef4444',items:[
    {name:'Chicken Burrito Bowl',cal:650,protein:40,carbs:70,fat:17,emoji:'🌯'},
    {name:'Steak Burrito Bowl',cal:680,protein:38,carbs:70,fat:20,emoji:'🌯'},
    {name:'Chicken Burrito',cal:860,protein:42,carbs:96,fat:24,emoji:'🌯'},
    {name:'Chicken Tacos (3)',cal:525,protein:36,carbs:54,fat:18,emoji:'🌮'},
    {name:'Chicken Bowl (no rice)',cal:440,protein:40,carbs:22,fat:17,emoji:'🥗'},
    {name:'Chips + Guac',cal:510,protein:5,carbs:60,fat:28,emoji:'🥑'},
  ]},
  'Cava':{emoji:'🥙',color:'#22d3ee',items:[
    {name:'Chicken Bowl',cal:620,protein:40,carbs:65,fat:18,emoji:'🥙'},
    {name:'Chicken Salad',cal:480,protein:38,carbs:22,fat:22,emoji:'🥗'},
    {name:'Lamb Bowl',cal:680,protein:38,carbs:65,fat:24,emoji:'🥙'},
    {name:'Falafel Bowl',cal:700,protein:22,carbs:78,fat:28,emoji:'🧆'},
    {name:'Braised Lamb + Greens',cal:420,protein:34,carbs:14,fat:26,emoji:'🥗'},
    {name:'Crazy Feta',cal:70,protein:2,carbs:2,fat:6,emoji:'🧀'},
  ]},
  'Dos Toros':{emoji:'🌮',color:'#a78bfa',items:[
    {name:'Chicken Burrito',cal:780,protein:42,carbs:84,fat:24,emoji:'🌯'},
    {name:'Chicken Bowl',cal:620,protein:40,carbs:68,fat:16,emoji:'🥗'},
    {name:'Steak Bowl',cal:660,protein:37,carbs:68,fat:19,emoji:'🥗'},
    {name:'Chicken Taco',cal:270,protein:18,carbs:24,fat:9,emoji:'🌮'},
    {name:'Steak Taco',cal:290,protein:17,carbs:24,fat:11,emoji:'🌮'},
    {name:'Chips',cal:230,protein:3,carbs:32,fat:10,emoji:'🥨'},
  ]},
  'Westville':{emoji:'🥗',color:'#39ff84',items:[
    {name:'Grilled Chicken Sandwich',cal:620,protein:42,carbs:52,fat:18,emoji:'🥪'},
    {name:'Turkey Burger',cal:650,protein:44,carbs:48,fat:22,emoji:'🍔'},
    {name:'Grilled Salmon',cal:540,protein:46,carbs:22,fat:28,emoji:'🐟'},
    {name:'Market Plate',cal:620,protein:28,carbs:58,fat:24,emoji:'🥗'},
    {name:'Chicken Avocado Wrap',cal:680,protein:40,carbs:52,fat:26,emoji:'🌯'},
    {name:'Sweet Potato Fries',cal:320,protein:4,carbs:48,fat:14,emoji:'🍠'},
  ]},
  'Chirp':{emoji:'🍗',color:'#f97316',items:[
    {name:'Classic Chicken Sandwich',cal:680,protein:42,carbs:58,fat:26,emoji:'🍗'},
    {name:'Spicy Chicken Sandwich',cal:700,protein:42,carbs:60,fat:28,emoji:'🌶️'},
    {name:'Chicken Tenders (4pc)',cal:520,protein:38,carbs:36,fat:22,emoji:'🍗'},
    {name:'Chicken & Waffles',cal:890,protein:44,carbs:84,fat:38,emoji:'🧇'},
    {name:'Side Fries',cal:360,protein:5,carbs:48,fat:17,emoji:'🍟'},
    {name:'Chicken Wrap',cal:620,protein:38,carbs:54,fat:20,emoji:'🌯'},
  ]},
};

const FOODS = {
  'banana':[105,1,27,0,'🍌'],'apple':[95,0,25,0,'🍎'],'orange':[62,1,15,0,'🍊'],
  'blueberries':[84,1,21,0,'🫐'],'strawberries':[49,1,12,0,'🍓'],'avocado':[160,2,9,15,'🥑'],
  'broccoli':[55,4,11,1,'🥦'],'spinach':[23,3,4,0,'🥬'],'sweet potato':[103,2,24,0,'🍠'],
  'white rice':[206,4,45,0,'🍚'],'brown rice':[216,5,45,2,'🍚'],'rice':[206,4,45,0,'🍚'],
  'oats':[150,5,27,3,'🌾'],'oatmeal':[150,5,27,3,'🌾'],'pasta':[220,8,43,1,'🍝'],
  'quinoa':[222,8,39,4,'🌾'],'egg':[78,6,0,5,'🥚'],'eggs':[78,6,0,5,'🥚'],
  'scrambled eggs':[78,6,0,5,'🍳'],'egg white':[17,4,0,0,'🥚'],
  'chicken breast':[165,31,0,4,'🍗'],'grilled chicken':[165,31,0,4,'🍗'],'chicken':[165,31,0,4,'🍗'],
  'salmon':[208,28,0,10,'🐟'],'tuna':[154,34,0,1,'🐟'],'shrimp':[84,18,0,1,'🍤'],
  'turkey':[135,30,0,1,'🦃'],'ground beef':[250,26,0,17,'🥩'],'steak':[271,26,0,18,'🥩'],
  'bacon':[135,9,0,11,'🥓'],'tofu':[94,10,2,5,'🫘'],
  'greek yogurt':[130,17,9,0,'🥛'],'cottage cheese':[110,14,5,2,'🧀'],
  'cheddar cheese':[113,7,0,9,'🧀'],'milk':[122,8,12,5,'🥛'],
  'whole wheat toast':[69,4,12,1,'🍞'],'toast':[79,3,15,1,'🍞'],
  'bagel':[270,10,53,2,'🥯'],'wrap':[210,5,33,5,'🌯'],'pita':[165,5,33,1,'🫓'],
  'almonds':[164,6,6,14,'🌰'],'peanut butter':[188,8,6,16,'🥜'],'almond butter':[196,7,7,18,'🥜'],
  'black coffee':[2,0,0,0,'☕'],'coffee':[5,0,1,0,'☕'],'latte':[120,6,12,5,'☕'],
  'protein shake':[150,25,8,3,'🥤'],'protein powder':[120,25,3,2,'🥤'],
  'omelette':[200,14,2,15,'🍳'],'pancakes':[350,8,58,10,'🥞'],
  'granola':[216,5,36,7,'🌾'],'sandwich':[350,20,35,12,'🥪'],
  'caesar salad':[360,10,20,28,'🥗'],'garden salad':[100,3,15,4,'🥗'],
  'soup':[150,8,18,5,'🍲'],'pizza':[285,12,36,10,'🍕'],
  'burger':[540,28,42,28,'🍔'],'fries':[365,4,48,17,'🍟'],
  'sushi':[300,15,42,6,'🍱'],'burrito':[780,42,84,24,'🌯'],
  'taco':[210,12,20,9,'🌮'],'cookie':[140,2,20,6,'🍪'],
  'chocolate':[170,2,20,10,'🍫'],'ice cream':[207,4,24,11,'🍦'],
  'chips':[152,2,15,10,'🥨'],'hummus':[166,8,14,10,'🫘'],
  'guacamole':[150,2,9,14,'🥑'],'black beans':[114,8,20,1,'🫘'],
};

function guessEmoji(t){
  const map=[['banana','🍌'],['apple','🍎'],['egg','🥚'],['chicken','🍗'],['salmon','🐟'],
    ['beef','🥩'],['steak','🥩'],['rice','🍚'],['oat','🌾'],['pasta','🍝'],['bread','🍞'],
    ['salad','🥗'],['soup','🍲'],['burger','🍔'],['pizza','🍕'],['taco','🌮'],
    ['burrito','🌯'],['coffee','☕'],['shake','🥤'],['protein','🥤'],['yogurt','🥛'],
    ['cheese','🧀'],['avocado','🥑'],['broccoli','🥦'],['fries','🍟']];
  for(const [k,e] of map) if(t.toLowerCase().includes(k)) return e;
  return '🍽️';
}

function estimateNutrition(raw){
  const t=raw.toLowerCase();
  let cal=0,p=0,c=0,f=0,matched=[];
  const keys=Object.keys(FOODS).sort((a,b)=>b.split(' ').length-a.split(' ').length);
  for(const key of keys){
    if(!t.includes(key)) continue;
    if(matched.some(m=>m.includes(key)||key.includes(m))) continue;
    let [fc,fp,fcar,ff]=FOODS[key];
    let qty=1;
    const before=t.slice(0,t.indexOf(key)).split(/[\s,]+/).slice(-3).join(' ');
    const nm=before.match(/\b(\d+)\b/);
    if(nm){const n=parseInt(nm[1]);if(n>=1&&n<=10)qty=n;}
    if(key==='egg'||key==='eggs'){const nm2=before.match(/\b(\d+)\b/);if(nm2)qty=parseInt(nm2[1]);}
    cal+=Math.round(fc*qty);p+=Math.round(fp*qty);c+=Math.round(fcar*qty);f+=Math.round(ff*qty);
    matched.push(key);
  }
  if(!matched.length) return null;
  const name=raw.trim().replace(/\b\w/g,l=>l.toUpperCase()).slice(0,50);
  return {name,cal,protein:p,carbs:c,fat:f,emoji:FOODS[matched[0]]?.[4]||guessEmoji(raw),note:`Est. from: ${matched.join(', ')}`};
}

// ── COMPUTED ──────────────────────────────────────────────────────
function getSettings(){ return settings; }
function getDayLog(){ return logs[selDate]||{breakfast:[],lunch:[],dinner:[],snacks:[],workouts:[]}; }
function getAllFoods(){
  const d=getDayLog();
  return [...(d.breakfast||[]),...(d.lunch||[]),...(d.dinner||[]),...(d.snacks||[])];
}
function getTotals(){
  return getAllFoods().reduce((a,f)=>({cal:a.cal+f.cal,protein:a.protein+(f.protein||0),carbs:a.carbs+(f.carbs||0),fat:a.fat+(f.fat||0)}),{cal:0,protein:0,carbs:0,fat:0});
}
function getCurrentWeight(){
  const e=Object.entries(weights).sort().reverse()[0];
  return e?e[1]:(settings.startWeight||180);
}
function getAllWeightEntries(){ return Object.entries(weights).sort(); }
function getProgress(){
  const sw=settings.startWeight||180,gw=settings.goalWeight||170;
  const lost=sw-getCurrentWeight();
  const range=Math.abs(sw-gw)||10;
  return Math.min(100,Math.max(0,(lost/range)*100));
}
function getDaysLeft(){
  const gd=settings.goalDate||'2026-05-06',sd=settings.startDate||'2026-03-03';
  const total=Math.round((new Date(gd)-new Date(sd))/864e5);
  return Math.max(0,total-daysSince(sd));
}

// ── MUTATIONS ─────────────────────────────────────────────────────
function addMealItem(sec,item){
  if(!logs[selDate]) logs[selDate]={breakfast:[],lunch:[],dinner:[],snacks:[],workouts:[]};
  logs[selDate][sec]=[...(logs[selDate][sec]||[]),item];
  save('ft_l3',logs); render();
}
function removeMealItem(sec,id){
  if(!logs[selDate]) return;
  logs[selDate][sec]=(logs[selDate][sec]||[]).filter(f=>f.id!==id);
  save('ft_l3',logs); render();
}
function addWorkout(name){
  if(!name||!name.trim()) return;
  if(!logs[selDate]) logs[selDate]={breakfast:[],lunch:[],dinner:[],snacks:[],workouts:[]};
  logs[selDate].workouts=[...(logs[selDate].workouts||[]),{name,id:Date.now()}];
  save('ft_l3',logs); render();
}
function removeWorkout(id){
  if(!logs[selDate]) return;
  logs[selDate].workouts=(logs[selDate].workouts||[]).filter(w=>w.id!==id);
  save('ft_l3',logs); render();
}
function logWeight(val){
  if(!val) return;
  weights[selDate]=parseFloat(val);
  save('ft_w3',weights); render();
}
function removeWeight(date){
  delete weights[date];
  save('ft_w3',weights); render();
}
function saveSettings(s){
  settings={...settings,...s};
  save('ft_s3',settings); render();
}
function saveSchedule(s){
  schedule=s; save('ft_sc3',schedule); render();
}

// ── RENDER HEADER ─────────────────────────────────────────────────
function renderHeader(){
  const cw=getCurrentWeight();
  const sw=settings.startWeight||180;
  const gw=settings.goalWeight||170;
  const lost=sw-cw;
  document.getElementById('hdr-weight').innerHTML=cw+'<span style="font-size:14px;font-weight:500;color:#4a7090;margin-left:4px;">lbs</span>';
  document.getElementById('hdr-lost').textContent=lost>0?`${lost.toFixed(1)} lbs lost`:`Start: ${sw} lbs`;
  document.getElementById('hdr-lost').style.color=lost>0?'#39ff84':'#4a7090';
  document.getElementById('hdr-goal').textContent=gw;
  document.getElementById('hdr-days').textContent=getDaysLeft()+'d left';
  document.getElementById('hdr-prog').style.width=getProgress()+'%';
}

// ── RENDER HOME ───────────────────────────────────────────────────
function renderHome(){
  const el=document.getElementById('tab-home');
  const t=getTotals();
  const d=getDayLog();
  const DAILY_CAL=settings.dailyCal||2000;
  const DAILY_PRO=settings.dailyProtein||170;
  const todayWk=schedule[todayDOW()];
  const allFoods=getAllFoods();
  const cw=getCurrentWeight();
  const sw=settings.startWeight||180;
  const lost=sw-cw;
  const allWkDays=Object.values(logs).filter(dl=>dl.workouts&&dl.workouts.length>0).length;

  let wkBanner='';
  if(todayWk&&todayWk!=='Rest Day'){
    const done=(d.workouts||[]).some(w=>w.name===todayWk);
    wkBanner=`<div onclick="showTab('lift',document.querySelector('.nav button:nth-child(3)'))" style="background:linear-gradient(135deg,#0d2818,#0a1f14);border:2px solid #39ff8444;border-radius:16px;padding:18px;margin-bottom:14px;cursor:pointer;display:flex;justify-content:space-between;align-items:center;">
      <div>
        <div style="font-size:10px;color:#39ff84;letter-spacing:3px;font-weight:700;margin-bottom:4px;">TODAY'S WORKOUT</div>
        <div style="font-size:20px;font-weight:800;">${WORKOUTS[todayWk]?.emoji||'💪'} ${todayWk}</div>
        <div style="font-size:12px;color:#4a7090;margin-top:4px;">${WORKOUTS[todayWk]?.duration||''}</div>
      </div>
      <div style="font-size:28px;">${done?'✅':'▷'}</div>
    </div>`;
  } else if(todayWk==='Rest Day'){
    wkBanner=`<div class="card" style="text-align:center;padding:24px;margin-bottom:14px;">
      <div style="font-size:28px;margin-bottom:8px;">🧘</div>
      <div style="font-size:18px;font-weight:800;">Rest Day</div>
      <div style="font-size:12px;color:#4a7090;margin-top:4px;">Recovery is part of the plan</div>
    </div>`;
  }

  let mealSummary='';
  if(allFoods.length===0){
    mealSummary='<div style="color:#4a6580;font-size:13px;">Nothing logged yet</div>';
  } else {
    mealSummary=MEAL_SECS.map(sec=>{
      const items=d[sec.key]||[];
      if(!items.length) return '';
      return `<div style="margin-bottom:8px;">
        <span style="font-size:10px;color:${sec.color};letter-spacing:2px;font-weight:800;">${sec.emoji} ${sec.label.toUpperCase()}</span>
        ${items.map(f=>`<div style="display:flex;justify-content:space-between;font-size:12px;color:#b0c4dc;padding-left:8px;margin-top:2px;"><span>${esc(f.name)}</span><span style="color:#f59e0b;">${f.cal}</span></div>`).join('')}
      </div>`;
    }).join('');
  }

  el.innerHTML=`
    ${wkBanner}
    <div class="grid2">
      <div class="card" style="background:${t.cal>DAILY_CAL?'#200a0a':'#111c27'}">
        <div class="lbl">Calories</div>
        <div style="font-size:30px;font-weight:900;color:${t.cal>DAILY_CAL?'#ef4444':'#fff'}">${t.cal}</div>
        <div style="font-size:11px;color:#4a7090;">of ${DAILY_CAL}</div>
      </div>
      <div class="card" style="background:${t.protein>=DAILY_PRO?'#0a2010':'#111c27'}">
        <div class="lbl">Protein</div>
        <div style="font-size:30px;font-weight:900;">${t.protein}g</div>
        <div style="font-size:11px;color:#4a7090;">of ${DAILY_PRO}g</div>
      </div>
    </div>
    <div class="grid2">
      <div class="card">
        <div class="lbl">Weight</div>
        <div style="font-size:26px;font-weight:900;">${cw}</div>
        <div style="font-size:11px;color:${lost>0?'#39ff84':'#4a7090'}">${lost>0?`-${lost.toFixed(1)} lbs`:'at start'}</div>
      </div>
      <div class="card">
        <div class="lbl">Workouts</div>
        <div style="font-size:26px;font-weight:900;">${allWkDays}</div>
        <div style="font-size:11px;color:#4a7090;">sessions done</div>
      </div>
    </div>
    <div class="card">
      <div class="lbl">Today's Meals</div>
      ${mealSummary}
    </div>`;
}

// ── RENDER FOOD ───────────────────────────────────────────────────
function renderFood(){
  const el=document.getElementById('tab-food');
  const d=getDayLog();
  const t=getTotals();
  const DAILY_CAL=settings.dailyCal||2000;

  if(menuRest){
    const r=RESTAURANTS[menuRest];
    const items=r.items.map((item,i)=>`
      <div class="card" style="display:flex;justify-content:space-between;align-items:center;">
        <div style="flex:1;">
          <div style="font-size:14px;font-weight:700;margin-bottom:2px;">${item.emoji} ${esc(item.name)}</div>
          <div style="font-size:11px;color:#6b8aaa;">P ${item.protein}g · C ${item.carbs}g · F ${item.fat}g</div>
        </div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:6px;">
          <span style="font-size:18px;font-weight:900;color:#f59e0b;">${item.cal}</span>
          <button class="btn" style="padding:6px 12px;font-size:11px;" onclick="addRestItem(${i})">+ Add</button>
        </div>
      </div>`).join('');
    el.innerHTML=`
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:16px;">
        <button onclick="menuRest=null;renderFood();" style="background:#1e3448;border:none;border-radius:8px;color:#fff;padding:8px 14px;cursor:pointer;font-weight:700;font-size:13px;">← Back</button>
        <div style="font-size:18px;font-weight:800;">${r.emoji} ${menuRest}</div>
      </div>
      ${items}`;
    return;
  }

  const restBtns=Object.entries(RESTAURANTS).map(([name,r])=>`
    <button class="rest-btn" style="border-color:${r.color}44;" onclick="menuRest='${name}';renderFood();">
      <span style="font-size:20px;">${r.emoji}</span>
      <span>${name}</span>
    </button>`).join('');

  const mealLoggers=MEAL_SECS.map(sec=>{
    const items=d[sec.key]||[];
    const secCal=items.reduce((a,f)=>a+f.cal,0);
    const hints={breakfast:'e.g. 3 eggs, toast, banana',lunch:'e.g. chicken shawarma salad',dinner:'e.g. 8oz salmon, broccoli',snacks:'e.g. banana, greek yogurt'};
    const itemsHtml=items.map(f=>`
      <div class="meal-item">
        <div>
          <div style="font-size:14px;font-weight:700;">${f.emoji||'🍽️'} ${esc(f.name)}</div>
          <div style="font-size:11px;color:#6b8aaa;">${f.cal} cal · P ${f.protein}g</div>
          ${f.note?`<div style="font-size:10px;color:#4a6580;font-style:italic;">${esc(f.note)}</div>`:''}
        </div>
        <button class="rm-btn" onclick="removeMealItem('${sec.key}','${f.id}')">×</button>
      </div>`).join('');
    return `
      <div style="margin-bottom:20px;">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
          <div style="display:flex;align-items:center;gap:7px;">
            <span style="font-size:15px;">${sec.emoji}</span>
            <span style="font-size:13px;font-weight:800;color:${sec.color};letter-spacing:2px;">${sec.label.toUpperCase()}</span>
          </div>
          ${items.length?`<span style="font-size:11px;color:#6b8aaa;">${secCal} cal</span>`:''}
        </div>
        ${itemsHtml}
        <div style="display:flex;gap:8px;margin-top:4px;">
          <input class="inp" id="food-inp-${sec.key}" placeholder="${hints[sec.key]||'describe food...'}" onkeydown="if(event.key==='Enter')addFoodFromInput('${sec.key}')">
          <button class="btn" onclick="addFoodFromInput('${sec.key}')" style="border-radius:10px;padding:10px 16px;">+</button>
        </div>
      </div>`;
  }).join('');

  const allFoods=getAllFoods();
  const totalBar=allFoods.length?`
    <div class="card" style="margin-top:8px;">
      <div style="display:flex;justify-content:space-between;font-size:13px;font-weight:700;">
        <span>Total</span>
        <span style="color:${t.cal>DAILY_CAL?'#ef4444':'#f59e0b'}">${t.cal} / ${DAILY_CAL} cal</span>
      </div>
    </div>`:'';

  el.innerHTML=`
    <div style="margin-bottom:20px;">
      <div class="lbl">NYC Restaurants</div>
      <div class="rest-grid">${restBtns}</div>
    </div>
    <div class="lbl">Food Log — ${selDate}</div>
    ${mealLoggers}
    ${totalBar}`;
}

function addFoodFromInput(sec){
  const inp=document.getElementById('food-inp-'+sec);
  if(!inp||!inp.value.trim()) return;
  const raw=inp.value.trim();
  const result=estimateNutrition(raw);
  if(result){
    addMealItem(sec,{...result,id:Date.now()});
  } else {
    const name=raw.replace(/\b\w/g,l=>l.toUpperCase()).slice(0,50);
    addMealItem(sec,{name,cal:0,protein:0,carbs:0,fat:0,emoji:guessEmoji(raw),note:'Could not estimate',id:Date.now()});
  }
  inp.value='';
}

function addRestItem(idx){
  const r=RESTAURANTS[menuRest];
  const item=r.items[idx];
  const h=new Date().getHours();
  const sec=h<11?'breakfast':h<15?'lunch':h<21?'dinner':'snacks';
  addMealItem(sec,{...item,id:Date.now()});
}

// ── RENDER LIFT ───────────────────────────────────────────────────
function renderLift(){
  const el=document.getElementById('tab-lift');
  const d=getDayLog();
  const todayWk=schedule[todayDOW()];

  const seg=`<div class="seg">
    ${[['today','TODAY'],['library','LIBRARY'],['schedule','SCHEDULE']].map(([m,l])=>`
      <button class="${wkMode===m?'active':''}" onclick="wkMode='${m}';renderLift();">${l}</button>`).join('')}
  </div>`;

  let content='';
  if(wkMode==='today'){
    let wkContent='';
    if(todayWk&&todayWk!=='Rest Day'&&WORKOUTS[todayWk]){
      const exercises=WORKOUTS[todayWk].exercises.map(ex=>`
        <div class="card">
          <div style="font-weight:700;font-size:13px;">${ex.name}</div>
          <div style="font-size:12px;color:#22d3ee;margin-top:2px;">${ex.sets}</div>
          <div style="font-size:11px;color:#7a9bbd;margin-top:2px;">${ex.note}</div>
        </div>`).join('');
      wkContent=`<div style="font-size:10px;color:#39ff84;letter-spacing:2px;margin-bottom:10px;">TODAY: ${todayWk}</div>${exercises}`;
    } else if(todayWk==='Rest Day'){
      wkContent=`<div class="card" style="text-align:center;padding:28px;"><div style="font-size:28px;margin-bottom:8px;">🧘</div><div style="font-size:18px;font-weight:800;">Rest Day</div></div>`;
    } else {
      wkContent=`<div class="card" style="text-align:center;padding:24px;"><div style="font-size:13px;color:#4a7090;">No schedule set. Go to SCHEDULE tab.</div></div>`;
    }
    const logged=(d.workouts||[]).map(w=>`
      <div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px;padding:8px 12px;background:#1a2535;border-radius:8px;">
        <span style="font-size:13px;color:#39ff84;">${esc(w.name)}</span>
        <button class="rm-btn" onclick="removeWorkout('${w.id}')">×</button>
      </div>`).join('');
    content=`${wkContent}
      <div style="margin-top:14px;">
        <div class="lbl">Log Workout</div>
        <div style="display:flex;gap:8px;">
          <input class="inp" id="wk-inp" placeholder="e.g. Push Day" onkeydown="if(event.key==='Enter'){addWorkout(document.getElementById('wk-inp').value);}">
          <button class="btn" onclick="addWorkout(document.getElementById('wk-inp').value)">+</button>
        </div>
        ${logged}
      </div>`;
  } else if(wkMode==='library'){
    content=Object.entries(WORKOUTS).map(([name,plan])=>`
      <div class="card">
        <div style="display:flex;gap:12px;align-items:center;margin-bottom:8px;">
          <span style="font-size:24px;">${plan.emoji}</span>
          <div>
            <div style="font-weight:800;font-size:15px;">${name}</div>
            <div style="font-size:11px;color:#39ff84;">${plan.duration} · ${plan.focus}</div>
          </div>
        </div>
        ${plan.exercises.slice(0,4).map((ex,i)=>`<div style="font-size:12px;color:#7a9bbd;margin-bottom:2px;">${i+1}. ${ex.name} — ${ex.sets}</div>`).join('')}
        ${plan.exercises.length>4?`<div style="font-size:11px;color:#4a7090;margin-top:2px;">+${plan.exercises.length-4} more</div>`:''}
        <button class="btn" style="width:100%;margin-top:10px;text-align:center;" onclick="addWorkout('${name}')">✓ Log This Workout</button>
      </div>`).join('');
  } else {
    // Schedule
    const days=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
    const opts=['','Push Day','Pull Day','Lower Body','Upper Body','Active Recovery','Rest Day'];
    const rows=days.map((day,i)=>`
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:10px;">
        <div style="width:82px;font-size:12px;color:#b0c4dc;">${day}</div>
        <select style="flex:1;background:#0d1a27;border:1px solid #2a4060;border-radius:8px;color:#eef4fb;padding:8px 10px;font-size:12px;font-family:inherit;" onchange="schedule[${i}]=this.value;save('ft_sc3',schedule);">
          ${opts.map(o=>`<option value="${o}" ${(schedule[i]||'')===(o)?'selected':''}>${o||'— off —'}</option>`).join('')}
        </select>
      </div>`).join('');
    content=`
      <div style="font-size:10px;color:#7a9bbd;letter-spacing:2px;margin-bottom:14px;">SET YOUR WEEKLY SCHEDULE</div>
      ${rows}
      <button class="btn" style="width:100%;margin-top:8px;" onclick="alert('Schedule saved!')">✓ Save Schedule</button>`;
  }

  el.innerHTML=seg+content;
}

// ── RENDER WEIGHT ─────────────────────────────────────────────────
function renderWeight(){
  const el=document.getElementById('tab-weight');
  const entries=getAllWeightEntries();
  const cw=getCurrentWeight();
  const sw=settings.startWeight||180;
  const gw=settings.goalWeight||170;

  let chartHtml='';
  if(entries.length>=2){
    const vals=entries.map(([,w])=>w);
    const all=[...vals,gw,sw];
    const mn=Math.min(...all)-1,mx=Math.max(...all)+1,rng=mx-mn||1;
    const W=320,H=120,P=20;
    const toY=v=>P+((mx-v)/rng)*(H-P*2);
    const toX=i=>P+(i/(entries.length-1))*(W-P*2);
    const pts=entries.map(([,w],i)=>`${toX(i)},${toY(w)}`).join(' ');
    const goalY=toY(gw);
    const dots=entries.map(([date,w],i)=>`
      <circle cx="${toX(i)}" cy="${toY(w)}" r="4" fill="${w<=gw?'#39ff84':'#f59e0b'}" stroke="#0a1420" stroke-width="1.5"/>
      ${(i===0||i===entries.length-1||entries.length<=6)?`<text x="${toX(i)}" y="${toY(w)-8}" text-anchor="middle" fill="#fff" font-size="8" font-family="sans-serif" font-weight="700">${w}</text>`:''}`).join('');
    chartHtml=`<div style="background:#0a1420;border-radius:16px;padding:16px;border:1px solid #1e3448;margin-bottom:14px;">
      <svg width="100%" viewBox="0 0 ${W} ${H}" style="display:block;">
        <line x1="${P}" y1="${goalY}" x2="${W-P}" y2="${goalY}" stroke="#39ff84" stroke-width="1.5" stroke-dasharray="6,4" opacity="0.5"/>
        <polygon points="${toX(0)},${H-P} ${pts} ${toX(entries.length-1)},${H-P}" fill="#39ff8415"/>
        <polyline points="${pts}" fill="none" stroke="#39ff84" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
        ${dots}
      </svg>
      <div style="display:flex;justify-content:space-between;margin-top:6px;font-size:10px;color:#4a7090;">
        <span>${entries[0][0].slice(5)}</span>
        <span>${entries[entries.length-1][0].slice(5)}</span>
      </div>
    </div>`;
  }

  const history=[...entries].reverse().map(([date,w])=>{
    const diff=sw-w;
    return `<div class="card" style="display:flex;justify-content:space-between;align-items:center;">
      <div>
        <div style="font-size:12px;color:#4a7090;">${date}</div>
        <div style="font-size:22px;font-weight:900;">${w} lbs</div>
      </div>
      <div style="display:flex;align-items:center;gap:10px;">
        <span style="font-size:12px;font-weight:700;color:${diff>0?'#39ff84':diff<0?'#ef4444':'#4a7090'}">${diff>0?'-'+diff.toFixed(1):diff<0?'+'+Math.abs(diff).toFixed(1):'start'}</span>
        <button class="rm-btn" onclick="removeWeight('${date}')">×</button>
      </div>
    </div>`;
  }).join('');

  el.innerHTML=`
    <div class="card" style="margin-bottom:14px;border:2px solid #a78bfa44;">
      <div class="lbl">Log Weight</div>
      <div style="display:flex;gap:8px;">
        <input type="number" step="0.1" placeholder="178.5" id="wt-inp" class="inp" style="flex:1;font-size:24px;font-weight:900;text-align:center;" onkeydown="if(event.key==='Enter')logWeight(this.value)">
        <button class="btn" style="background:#a78bfa;" onclick="logWeight(document.getElementById('wt-inp').value)">LOG</button>
      </div>
      ${weights[selDate]?`<div style="margin-top:10px;display:flex;justify-content:space-between;align-items:center;"><span style="font-size:12px;color:#a78bfa;">Logged: ${weights[selDate]} lbs</span><button onclick="removeWeight('${selDate}')" style="background:none;border:none;color:#6b8aaa;cursor:pointer;font-size:13px;">Remove</button></div>`:''}
    </div>
    ${chartHtml}
    ${entries.length===0?'<div class="card" style="text-align:center;padding:24px;color:#4a7090;">No weights logged yet</div>':history}`;
}

// ── RENDER STATS ──────────────────────────────────────────────────
function renderStats(){
  const el=document.getElementById('tab-stats');
  const sw=settings.startWeight||180;
  const gw=settings.goalWeight||170;
  const cw=getCurrentWeight();
  const lost=Math.max(0,sw-cw);
  const prog=getProgress();
  const dl=getDaysLeft();
  const gd=settings.goalDate||'2026-05-06';
  const entries=getAllWeightEntries();

  let chartHtml='';
  if(entries.length>=2){
    const vals=entries.map(([,w])=>w);
    const all=[...vals,gw,sw];
    const mn=Math.min(...all)-1,mx=Math.max(...all)+1,rng=mx-mn||1;
    const W=320,H=120,P=20;
    const toY=v=>P+((mx-v)/rng)*(H-P*2);
    const toX=i=>P+(i/(entries.length-1))*(W-P*2);
    const pts=entries.map(([,w],i)=>`${toX(i)},${toY(w)}`).join(' ');
    const goalY=toY(gw);
    const dots=entries.map(([date,w],i)=>`<circle cx="${toX(i)}" cy="${toY(w)}" r="4" fill="${w<=gw?'#39ff84':'#f59e0b'}" stroke="#0a1420" stroke-width="1.5"/>`).join('');
    chartHtml=`<div style="background:#0a1420;border-radius:16px;padding:16px;border:1px solid #1e3448;margin-bottom:14px;">
      <svg width="100%" viewBox="0 0 ${W} ${H}" style="display:block;">
        <line x1="${P}" y1="${goalY}" x2="${W-P}" y2="${goalY}" stroke="#39ff84" stroke-width="1.5" stroke-dasharray="6,4" opacity="0.5"/>
        <polygon points="${toX(0)},${H-P} ${pts} ${toX(entries.length-1)},${H-P}" fill="#39ff8415"/>
        <polyline points="${pts}" fill="none" stroke="#39ff84" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
        ${dots}
      </svg>
    </div>`;
  }

  el.innerHTML=`
    <div class="grid2">
      ${[['STARTED',sw+' lbs'],['CURRENT',cw+' lbs'],['GOAL',gw+' lbs'],['LOST',lost.toFixed(1)+' lbs']].map(([lbl,val])=>`
        <div class="card" style="padding:14px;">
          <div class="lbl">${lbl}</div>
          <div style="font-size:22px;font-weight:900;">${val}</div>
        </div>`).join('')}
    </div>
    <div class="card" style="margin-bottom:14px;">
      <div class="lbl">Progress to Goal</div>
      <div style="display:flex;justify-content:space-between;font-size:12px;font-weight:600;color:#4a7090;margin-bottom:6px;">
        <span>${sw} lbs</span><span style="color:#39ff84;">${prog.toFixed(0)}% done</span><span>${gw} lbs</span>
      </div>
      <div style="height:12px;background:#1e3448;border-radius:999px;overflow:hidden;">
        <div style="height:100%;border-radius:999px;background:linear-gradient(90deg,#39ff84,#00d4ff);width:${prog}%;transition:width 1s;"></div>
      </div>
      <div style="font-size:11px;color:#4a7090;text-align:center;margin-top:8px;">${dl} days until ${gd}</div>
    </div>
    ${chartHtml}`;
}

// ── RENDER GOALS ──────────────────────────────────────────────────
function renderGoals(){
  const el=document.getElementById('tab-goals');
  const s=settings;
  el.innerHTML=`
    <div class="card" style="margin-bottom:12px;border:2px solid #39ff8422;">
      <div class="lbl">Weight Goal</div>
      <div class="grid2" style="margin-bottom:0;">
        <div><div class="lbl">Start</div><input type="number" step="0.5" value="${s.startWeight||180}" class="inp" style="font-size:20px;font-weight:900;text-align:center;" id="g-sw"></div>
        <div><div class="lbl">Goal</div><input type="number" step="0.5" value="${s.goalWeight||170}" class="inp" style="font-size:20px;font-weight:900;text-align:center;border-color:#39ff84;" id="g-gw"></div>
      </div>
    </div>
    <div class="card" style="margin-bottom:12px;border:2px solid #00d4ff22;">
      <div class="lbl">Timeline</div>
      <div class="grid2" style="margin-bottom:0;">
        <div><div class="lbl">Start Date</div><input type="date" value="${s.startDate||'2026-03-03'}" class="inp" style="font-size:13px;" id="g-sd"></div>
        <div><div class="lbl">Goal Date</div><input type="date" value="${s.goalDate||'2026-05-06'}" class="inp" style="font-size:13px;border-color:#00d4ff;" id="g-gd"></div>
      </div>
    </div>
    <div class="card" style="margin-bottom:16px;border:2px solid #f59e0b22;">
      <div class="lbl">Daily Targets</div>
      <div class="grid2" style="margin-bottom:0;">
        <div><div class="lbl">Calories</div><input type="number" step="50" value="${s.dailyCal||2000}" class="inp" style="font-size:20px;font-weight:900;text-align:center;border-color:#f59e0b;" id="g-cal"></div>
        <div><div class="lbl">Protein (g)</div><input type="number" step="5" value="${s.dailyProtein||170}" class="inp" style="font-size:20px;font-weight:900;text-align:center;border-color:#39ff84;" id="g-pro"></div>
      </div>
    </div>
    <button class="btn" style="width:100%;font-size:15px;padding:16px;margin-bottom:10px;" onclick="applySettings()">✓ Save Changes</button>
    <div id="g-saved" style="text-align:center;font-size:12px;color:#4a7090;display:none;">All goals saved ✓</div>`;
}

function applySettings(){
  saveSettings({
    startWeight:parseFloat(document.getElementById('g-sw').value)||180,
    goalWeight:parseFloat(document.getElementById('g-gw').value)||170,
    startDate:document.getElementById('g-sd').value||'2026-03-03',
    goalDate:document.getElementById('g-gd').value||'2026-05-06',
    dailyCal:parseInt(document.getElementById('g-cal').value)||2000,
    dailyProtein:parseInt(document.getElementById('g-pro').value)||170,
  });
  document.getElementById('g-saved').style.display='block';
  setTimeout(()=>{const el=document.getElementById('g-saved');if(el)el.style.display='none';},2000);
}

// ── NAV / ROUTING ─────────────────────────────────────────────────
function showTab(name, btn){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('.nav button').forEach(b=>b.classList.remove('active'));
  document.getElementById('tab-'+name).classList.add('active');
  if(btn) btn.classList.add('active');
  curTab=name;
  menuRest=null;
  renderTab(name);
}

function renderTab(name){
  if(name==='home') renderHome();
  else if(name==='food') renderFood();
  else if(name==='lift') renderLift();
  else if(name==='weight') renderWeight();
  else if(name==='stats') renderStats();
  else if(name==='goals') renderGoals();
}

function setToday(){
  selDate=today();
  document.getElementById('sel-date').value=selDate;
  render();
}

function render(){
  renderHeader();
  renderTab(curTab);
}

// ── INIT ──────────────────────────────────────────────────────────
document.getElementById('sel-date').value=selDate;
document.getElementById('sel-date').addEventListener('change',function(){
  selDate=this.value; render();
});
render();
</script>

</body>
</html>
