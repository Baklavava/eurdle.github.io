<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Eurdle — European History</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --blue:       #2c52a0;
  --blue-dark:  #1d3870;
  --blue-light: #3d6bc4;
  --blue-bg:    #eef2fa;
  --blue-mid:   #c8d7f5;
  --gold:       #f5c518;
  --white:      #ffffff;
  --off-white:  #f8f9fc;
  --text:       #1a2340;
  --muted:      #6b7ba0;
  --border:     #d8e2f5;
  --c-exact:    #1b7a35;
  --c-near:     #277a50;
  --c-close:    #b86800;
  --c-mid:      #b84800;
  --c-far:      #9e1a1a;
  --radius:     8px;
}
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Nunito',sans-serif;background:var(--white);color:var(--text);}

/* ═══ HEADER ═══ */
.hdr{background:var(--blue);padding:11px 14px 9px;text-align:center;position:relative;}
.hdr-stars{font-size:.55rem;letter-spacing:3px;color:var(--gold);margin-bottom:3px;}
.hdr-title{font-size:1.85rem;font-weight:900;color:#fff;letter-spacing:.25em;line-height:1;}
.hdr-sub{font-size:.6rem;font-weight:700;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.6);margin-top:2px;}
.streak-badge{
  position:absolute;right:10px;top:50%;transform:translateY(-50%);
  background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.3);
  border-radius:20px;padding:4px 9px;font-size:.72rem;font-weight:900;color:#fff;
  letter-spacing:.04em;display:none;
}
.streak-badge.show{display:block;}
.archive-hdr-btn{
  position:absolute;left:10px;top:50%;transform:translateY(-50%);
  background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.3);
  border-radius:20px;padding:4px 9px;font-size:.68rem;font-weight:800;color:#fff;
  cursor:pointer;transition:background .15s;display:none;letter-spacing:.04em;
  -webkit-tap-highlight-color:transparent;
}
.archive-hdr-btn:hover{background:rgba(255,255,255,.28);}
.archive-hdr-btn.show{display:block;}

/* ═══ MODE BANNER ═══ */
.mode-banner{
  background:var(--blue-bg);border-bottom:1px solid var(--blue-mid);
  text-align:center;padding:5px 12px;
  font-size:.65rem;font-weight:800;letter-spacing:.15em;text-transform:uppercase;
  color:var(--blue);display:none;
}
.mode-banner.show{display:block;}

/* ═══ BODY ═══ */
.body{max-width:430px;margin:0 auto;padding:11px 13px 16px;}

/* ═══ CLUE CARD ═══ */
.clue-card{
  background:var(--blue-bg);border:1px solid var(--blue-mid);
  border-left:4px solid var(--blue);border-radius:var(--radius);
  padding:11px 13px;margin-bottom:8px;
}
.clue-lbl{font-size:.56rem;font-weight:800;letter-spacing:.2em;text-transform:uppercase;color:var(--blue);margin-bottom:5px;}
.clue-txt{font-family:'Source Serif 4',serif;font-size:.87rem;line-height:1.62;color:var(--text);font-style:italic;}
.clue-region{font-size:.6rem;font-weight:700;color:var(--muted);margin-top:6px;}

/* ═══ HINTS ═══ */
.hints{margin-bottom:7px;}
.hint-row{
  display:flex;align-items:flex-start;gap:7px;
  background:var(--white);border:1px solid var(--border);
  border-radius:var(--radius);padding:7px 10px;margin-bottom:5px;
  font-family:'Source Serif 4',serif;font-size:.79rem;line-height:1.45;color:var(--text);
  animation:hintIn .3s cubic-bezier(.16,1,.3,1) both;
}
@keyframes hintIn{from{opacity:0;transform:translateY(-5px);}to{opacity:1;transform:translateY(0);}}
.hint-tag{
  flex-shrink:0;font-family:'Nunito',sans-serif;
  font-size:.54rem;font-weight:800;letter-spacing:.1em;text-transform:uppercase;
  padding:2px 5px;border-radius:20px;margin-top:2px;
}
.hint-tag.before{background:#dce9ff;color:var(--blue);}
.hint-tag.after{background:#fddede;color:var(--c-far);}

/* ═══ GUESS ROWS ═══ */
.guesses{margin-bottom:8px;}
.g-row{
  display:flex;align-items:center;gap:9px;
  padding:4px 0;border-bottom:1px solid var(--border);
  animation:rowIn .25s ease both;
}
@keyframes rowIn{from{opacity:0;transform:translateX(-4px);}to{opacity:1;transform:translateX(0);}}
.g-chip{
  font-weight:900;font-size:.88rem;
  padding:5px 12px;border-radius:20px;
  flex-shrink:0;color:#fff;min-width:90px;text-align:center;
}
.g-chip.exact{background:var(--c-exact);}
.g-chip.near {background:var(--c-near);}
.g-chip.close{background:var(--c-close);}
.g-chip.mid  {background:var(--c-mid);}
.g-chip.far  {background:var(--c-far);}
.g-arrow{font-size:1rem;color:var(--muted);flex-shrink:0;width:16px;text-align:center;}

/* ═══ STATUS BAR ═══ */
.status-bar{
  display:flex;justify-content:space-between;align-items:center;
  font-size:.64rem;font-weight:700;color:var(--muted);
  letter-spacing:.1em;text-transform:uppercase;margin-bottom:7px;
}
.dots{display:flex;gap:4px;}
.dot{width:8px;height:8px;border-radius:50%;background:var(--border);}
.dot.ok  {background:var(--c-exact);}
.dot.bad {background:var(--c-far);}

/* ═══ INPUT DISPLAY ═══ */
.input-wrap{
  border:2px solid var(--blue-mid);border-radius:var(--radius);
  background:var(--off-white);height:50px;
  display:flex;align-items:center;justify-content:center;
  margin-bottom:7px;position:relative;transition:border-color .2s;
}
.input-wrap.active{border-color:var(--blue);}
.input-wrap.shake{animation:shake .35s ease;}
@keyframes shake{
  0%,100%{transform:translateX(0);}20%{transform:translateX(-5px);}
  40%{transform:translateX(5px);}60%{transform:translateX(-3px);}80%{transform:translateX(3px);}
}
.yr-digits{font-size:1.8rem;font-weight:900;color:var(--blue);letter-spacing:.15em;min-width:80px;text-align:center;}
.yr-digits.empty{color:#b0bcd8;font-size:.88rem;font-weight:600;letter-spacing:.04em;}
.cursor{display:inline-block;width:2px;height:1.6rem;background:var(--blue);margin-left:2px;vertical-align:middle;animation:blink 1s step-end infinite;}
@keyframes blink{50%{opacity:0;}}
.era-pill{
  position:absolute;right:9px;
  font-size:.58rem;font-weight:800;letter-spacing:.1em;text-transform:uppercase;
  background:var(--blue);color:#fff;padding:3px 8px;border-radius:20px;
  cursor:pointer;user-select:none;transition:background .15s;
  -webkit-tap-highlight-color:transparent;
}
.era-pill.bc{background:var(--c-far);}

/* ═══ NUMPAD ═══ */
.numpad{display:grid;grid-template-columns:repeat(3,1fr);gap:5px;margin-bottom:5px;}
.key{
  font-family:'Nunito',sans-serif;font-weight:800;font-size:1.18rem;
  padding:12px 0;border:none;border-radius:6px;
  background:var(--blue-bg);color:var(--text);
  cursor:pointer;transition:background .1s,transform .08s;
  user-select:none;-webkit-tap-highlight-color:transparent;
}
.key:hover{background:var(--blue-mid);}
.key:active{transform:scale(.92);}
.key.del{font-size:.95rem;background:#f0e4e4;color:var(--c-far);}
.key.bc{font-size:.66rem;letter-spacing:.05em;background:#fde8e8;color:var(--c-far);}
.key.bc.on{background:var(--c-far);color:#fff;}
.enter-btn{
  width:100%;font-family:'Nunito',sans-serif;font-weight:900;
  font-size:.8rem;letter-spacing:.2em;text-transform:uppercase;
  padding:12px;border:none;border-radius:6px;
  background:var(--blue);color:#fff;
  cursor:pointer;transition:background .15s,transform .08s;
  user-select:none;-webkit-tap-highlight-color:transparent;
}
.enter-btn:hover{background:var(--blue-dark);}
.enter-btn:active{transform:scale(.98);}
.enter-btn:disabled{opacity:.35;cursor:default;transform:none;}

/* ═══ RESULT PANEL ═══ */
.result{margin-top:8px;}
.msg{
  border-radius:var(--radius);padding:10px 12px;text-align:center;
  font-size:.83rem;line-height:1.45;margin-bottom:7px;display:none;
}
.msg.win {display:block;background:#e6f7eb;border:1px solid #7dc48a;color:var(--c-exact);}
.msg.lose{display:block;background:#fdecea;border:1px solid #e8a8a8;color:var(--c-far);}
.msg-title{font-weight:900;font-size:1rem;display:block;margin-bottom:3px;}
.act-row{display:flex;gap:6px;}
.act-btn{
  flex:1;font-family:'Nunito',sans-serif;font-weight:800;
  font-size:.68rem;letter-spacing:.12em;text-transform:uppercase;
  padding:9px 6px;border:2px solid;border-radius:var(--radius);
  cursor:pointer;transition:all .15s;text-align:center;display:none;
  -webkit-tap-highlight-color:transparent;
}
.btn-share  {border-color:var(--blue);color:var(--blue);background:transparent;}
.btn-share:hover{background:var(--blue);color:#fff;}
.btn-archive{border-color:var(--blue-light);color:var(--blue-light);background:transparent;}
.btn-archive:hover{background:var(--blue-light);color:#fff;}
.btn-random {border-color:var(--c-exact);color:var(--c-exact);background:transparent;}
.btn-random:hover{background:var(--c-exact);color:#fff;}

/* ═══ ARCHIVE OVERLAY ═══ */
.arc-overlay{
  position:fixed;inset:0;background:rgba(13,27,60,.78);
  z-index:200;display:none;align-items:flex-start;justify-content:center;
  padding:10px;overflow-y:auto;
}
.arc-overlay.open{display:flex;}
.arc-panel{
  background:var(--white);border-radius:10px;
  width:100%;max-width:430px;overflow:hidden;
  box-shadow:0 20px 60px rgba(0,0,0,.45);
  animation:panelIn .25s cubic-bezier(.16,1,.3,1);
  margin-top:4px;
}
@keyframes panelIn{from{opacity:0;transform:translateY(-12px);}to{opacity:1;transform:translateY(0);}}
.arc-hdr{
  background:var(--blue);padding:13px 15px;
  display:flex;align-items:center;justify-content:space-between;
}
.arc-hdr-title{font-size:.9rem;font-weight:900;color:#fff;letter-spacing:.1em;text-transform:uppercase;}
.arc-close{
  background:rgba(255,255,255,.2);border:none;color:#fff;
  width:28px;height:28px;border-radius:50%;cursor:pointer;
  font-size:1rem;font-weight:700;display:flex;align-items:center;justify-content:center;
  transition:background .15s;flex-shrink:0;
}
.arc-close:hover{background:rgba(255,255,255,.35);}
.arc-body{padding:11px 13px;max-height:72vh;overflow-y:auto;}
.arc-random{
  width:100%;font-family:'Nunito',sans-serif;font-weight:800;
  font-size:.72rem;letter-spacing:.14em;text-transform:uppercase;
  padding:10px;border-radius:6px;
  background:var(--blue-bg);border:2px solid var(--blue-mid);color:var(--blue);
  cursor:pointer;margin-bottom:10px;transition:all .15s;
  -webkit-tap-highlight-color:transparent;
}
.arc-random:hover{background:var(--blue);color:#fff;border-color:var(--blue);}
.arc-section{font-size:.58rem;font-weight:800;letter-spacing:.18em;text-transform:uppercase;color:var(--muted);margin-bottom:6px;padding-left:2px;}
.arc-item{
  display:flex;align-items:center;gap:9px;
  padding:8px 9px;border-radius:6px;margin-bottom:4px;
  cursor:pointer;border:1px solid var(--border);
  transition:background .12s,border-color .12s;
}
.arc-item:hover{background:var(--blue-bg);border-color:var(--blue-mid);}
.arc-item.played{border-color:#b8dfc1;}
.arc-date{font-size:.68rem;font-weight:800;color:var(--blue);flex-shrink:0;width:78px;line-height:1.3;}
.arc-preview{font-family:'Source Serif 4',serif;font-size:.73rem;font-style:italic;color:var(--muted);flex:1;overflow:hidden;white-space:nowrap;text-overflow:ellipsis;}
.arc-done{flex-shrink:0;font-size:.56rem;font-weight:800;letter-spacing:.07em;text-transform:uppercase;padding:2px 6px;border-radius:10px;background:#e6f7eb;color:var(--c-exact);}
.arc-empty{text-align:center;color:var(--muted);font-size:.82rem;padding:20px 0;}

/* ═══ TOAST ═══ */
.toast{
  position:fixed;bottom:20px;left:50%;transform:translateX(-50%) translateY(60px);
  background:var(--text);color:#fff;padding:8px 18px;border-radius:20px;
  font-size:.75rem;font-weight:700;letter-spacing:.06em;z-index:300;
  transition:transform .3s cubic-bezier(.16,1,.3,1),opacity .3s;
  opacity:0;pointer-events:none;white-space:nowrap;
}
.toast.show{transform:translateX(-50%) translateY(0);opacity:1;}
</style>
</head>
<body>

<!-- ── HEADER ── -->
<div class="hdr">
  <button class="archive-hdr-btn" id="archiveHdrBtn" onclick="openArchive()">📚 Archive</button>
  <div class="hdr-stars">★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★</div>
  <div class="hdr-title">EURDLE</div>
  <div class="hdr-sub">European History — Guess the Year</div>
  <div class="streak-badge" id="streakBadge"></div>
</div>

<div class="mode-banner" id="modeBanner"></div>

<!-- ── GAME BODY ── -->
<div class="body">

  <div class="clue-card">
    <div class="clue-lbl">📜 The Event</div>
    <div class="clue-txt" id="clueText"></div>
    <div class="clue-region" id="clueRegion"></div>
  </div>

  <div class="hints" id="hintsEl"></div>
  <div class="guesses" id="guessesEl"></div>

  <div class="status-bar">
    <span id="attemptsLbl">6 attempts left</span>
    <div class="dots" id="dotsEl"></div>
  </div>

  <div class="input-wrap" id="inputWrap">
    <div class="yr-digits empty" id="yrDisplay">Enter a year…</div>
    <div class="era-pill" id="eraPill" onclick="toggleEra()">AD</div>
  </div>

  <div class="numpad">
    <button class="key" onclick="pressKey('7')">7</button>
    <button class="key" onclick="pressKey('8')">8</button>
    <button class="key" onclick="pressKey('9')">9</button>
    <button class="key" onclick="pressKey('4')">4</button>
    <button class="key" onclick="pressKey('5')">5</button>
    <button class="key" onclick="pressKey('6')">6</button>
    <button class="key" onclick="pressKey('1')">1</button>
    <button class="key" onclick="pressKey('2')">2</button>
    <button class="key" onclick="pressKey('3')">3</button>
    <button class="key bc" id="bcKey" onclick="toggleEra()">BC / AD</button>
    <button class="key" onclick="pressKey('0')">0</button>
    <button class="key del" onclick="deleteLast()">⌫</button>
  </div>
  <button class="enter-btn" id="enterBtn" onclick="submitGuess()">Guess ↵</button>

  <div class="result" id="resultEl">
    <div class="msg" id="msgEl">
      <span class="msg-title" id="msgTitle"></span>
      <span id="msgBody"></span>
    </div>
    <div class="act-row">
      <button class="act-btn btn-share"   id="btnShare"   onclick="shareResult()">🔗 Share</button>
      <button class="act-btn btn-archive" id="btnArchive" onclick="openArchive()">📚 Archive</button>
      <button class="act-btn btn-random"  id="btnRandom"  onclick="playRandomArchive()">🎲 Random</button>
    </div>
  </div>
</div>

<!-- ── ARCHIVE OVERLAY ── -->
<div class="arc-overlay" id="arcOverlay">
  <div class="arc-panel">
    <div class="arc-hdr">
      <span class="arc-hdr-title">📚 Past Chronicles</span>
      <button class="arc-close" onclick="closeArchive()">✕</button>
    </div>
    <div class="arc-body">
      <button class="arc-random" onclick="playRandomArchive();closeArchive();">🎲 Play a Random Challenge</button>
      <div class="arc-section">All Past Daily Challenges</div>
      <div id="arcList"></div>
    </div>
  </div>
</div>

<!-- ── TOAST ── -->
<div class="toast" id="toast"></div>

<script>
// ════════════════════════════════════════════════
//  EVENTS  (fixed order — never reorder existing entries)
// ════════════════════════════════════════════════
const EVENTS = [
  {year:-490,text:"Athenian and Plataean forces repel a Persian landing force at Marathon, ending the first Persian invasion of Greece.",region:"Ancient Greece"},
  {year:-399,text:"The philosopher Socrates is tried by an Athenian jury on charges of impiety and corrupting the youth, and is condemned to death by hemlock.",region:"Ancient Greece"},
  {year:-338,text:"Philip II of Macedon defeats the combined forces of Athens and Thebes at the Battle of Chaeronea, establishing Macedonian supremacy over Greece.",region:"Ancient Greece"},
  {year:-264,text:"Rome and Carthage clash for the first time over control of Sicily, igniting the First Punic War that will last more than two decades.",region:"Roman Republic"},
  {year:-218,text:"The Carthaginian general Hannibal crosses the Alps with war elephants, bringing the fight directly to Roman soil in a daring invasion of Italy.",region:"Roman Republic"},
  {year:-146,text:"Roman legions raze Carthage to the ground and sell its inhabitants into slavery, ending the Third Punic War and Carthaginian civilisation entirely.",region:"Roman Republic"},
  {year:-44,text:"Julius Caesar is assassinated on the Ides of March by a group of senators including Brutus and Cassius, plunging the Roman Republic into devastating civil war.",region:"Roman Republic"},
  {year:-27,text:"The Roman Senate grants Octavian the title of Augustus, marking the birth of the Roman Empire and the end of five centuries of republican government.",region:"Roman Empire"},
  {year:79,text:"Mount Vesuvius erupts catastrophically, burying the Roman city of Pompeii under metres of volcanic ash and preserving it for nearly two millennia.",region:"Roman Empire"},
  {year:313,text:"The Edict of Milan, issued by emperors Constantine and Licinius, grants religious tolerance throughout the Roman Empire, ending Christian persecution.",region:"Roman Empire"},
  {year:410,text:"Visigothic forces under Alaric sack Rome for the first time in eight centuries, sending shockwaves of disbelief through the late Roman world.",region:"Western Roman Empire"},
  {year:476,text:"The last Western Roman Emperor, Romulus Augustulus, is deposed by the Germanic chieftain Odoacer, conventionally marking the fall of Western Rome.",region:"Western Roman Empire"},
  {year:529,text:"Emperor Justinian I promulgates the Corpus Juris Civilis, a comprehensive codification of Roman law that would shape European legal systems for a thousand years.",region:"Byzantine Empire"},
  {year:732,text:"Charles Martel halts the northward advance of an Umayyad army near Tours and Poitiers, in a battle later seen as saving Christian Western Europe.",region:"Frankish Kingdom"},
  {year:800,text:"Pope Leo III crowns Charlemagne as Emperor of the Romans in St Peter's Basilica on Christmas Day, reviving the imperial title in the Christian West.",region:"Frankish Empire"},
  {year:843,text:"The three grandsons of Charlemagne sign the Treaty of Verdun, dividing his empire into three kingdoms that foreshadow modern France, Germany and Italy.",region:"Frankish Empire"},
  {year:1066,text:"Duke William of Normandy defeats King Harold II at the Battle of Hastings and is crowned King of England, transforming its language, culture and institutions.",region:"England / Normandy"},
  {year:1095,text:"Pope Urban II calls upon Christian knights at the Council of Clermont to march east and reclaim Jerusalem from Muslim rule, launching the First Crusade.",region:"France / Papal States"},
  {year:1215,text:"English barons force King John to affix his seal to Magna Carta at Runnymede, establishing for the first time that the king was subject to the rule of law.",region:"England"},
  {year:1302,text:"Flemish urban militias defeat a French cavalry army at the Battle of the Golden Spurs near Courtrai, a remarkable upset of medieval military assumptions.",region:"Flanders"},
  {year:1347,text:"The Black Death arrives in Sicily aboard Genoese trading ships and over the following years kills an estimated third of Europe's entire population.",region:"Europe"},
  {year:1415,text:"Henry V of England wins a stunning victory over a much larger French force at Agincourt, again demonstrating the devastating power of the English longbow.",region:"France"},
  {year:1429,text:"Joan of Arc leads French forces to relieve the siege of Orléans, reinvigorating French resistance in the Hundred Years' War and changing its eventual outcome.",region:"France"},
  {year:1453,text:"Ottoman forces under Sultan Mehmed II breach the walls of Constantinople with cannon fire, ending the Byzantine Empire after over a thousand years of existence.",region:"Byzantine Empire"},
  {year:1492,text:"Christopher Columbus, sailing under Castilian patronage, makes landfall in the Caribbean, opening sustained European contact with the Americas.",region:"Spain"},
  {year:1517,text:"Martin Luther publishes his Ninety-Five Theses in Wittenberg, igniting the Protestant Reformation that will permanently divide Western Christianity.",region:"Holy Roman Empire"},
  {year:1534,text:"Henry VIII of England breaks with Rome and is declared Supreme Head of the Church of England by the Act of Supremacy, triggering the English Reformation.",region:"England"},
  {year:1571,text:"A combined Christian fleet defeats the Ottoman navy at the Battle of Lepanto off Greece, halting Ottoman naval expansion in the Mediterranean for good.",region:"Mediterranean"},
  {year:1588,text:"The Spanish Armada, sent to invade England, is scattered by English ships and wrecked by Atlantic storms, ending Spain's attempt to overthrow Queen Elizabeth I.",region:"England / Spain"},
  {year:1618,text:"The Defenestration of Prague — the hurling of royal officials from a castle window — ignites the Thirty Years' War, Europe's most destructive conflict to that date.",region:"Holy Roman Empire"},
  {year:1648,text:"The Peace of Westphalia ends the Thirty Years' War, reshaping the map of Europe and establishing principles of state sovereignty foundational to international relations.",region:"Europe"},
  {year:1649,text:"King Charles I of England is tried and executed at Whitehall, the first European monarch formally condemned and beheaded by his own government.",region:"England"},
  {year:1687,text:"Isaac Newton publishes his Principia Mathematica in London, laying out the laws of motion and universal gravitation, transforming natural philosophy forever.",region:"England"},
  {year:1688,text:"William of Orange lands in England and marches on London; James II flees, and Parliament offers the crown jointly to William and Mary in the Glorious Revolution.",region:"England"},
  {year:1689,text:"The English Parliament passes the Bill of Rights, limiting royal power and guaranteeing parliamentary elections and free speech, establishing constitutional monarchy.",region:"England"},
  {year:1707,text:"The Acts of Union unite the Kingdom of England and the Kingdom of Scotland into a single new entity: the Kingdom of Great Britain.",region:"Great Britain"},
  {year:1762,text:"Jean-Jacques Rousseau publishes The Social Contract, arguing that political authority derives from the people — profoundly shaping democratic thought worldwide.",region:"France / Geneva"},
  {year:1776,text:"Adam Smith publishes The Wealth of Nations in London, laying the foundations of modern economics and arguing for free markets and the division of labour.",region:"Great Britain"},
  {year:1789,text:"Parisian crowds storm the Bastille fortress on the 14th of July, releasing prisoners and seizing arms in the opening act of the French Revolution.",region:"France"},
  {year:1793,text:"Louis XVI of France is guillotined on the Place de la Révolution, followed ten months later by Marie Antoinette, during the radical Terror phase of the Revolution.",region:"France"},
  {year:1804,text:"Napoleon Bonaparte crowns himself Emperor of the French in Notre-Dame Cathedral in Paris, at a ceremony attended by Pope Pius VII he had summoned from Rome.",region:"France"},
  {year:1805,text:"Admiral Horatio Nelson is killed at the moment of his greatest triumph at Trafalgar, where the Royal Navy destroys a combined Franco-Spanish fleet off Spain.",region:"Spain / Atlantic"},
  {year:1812,text:"Napoleon's Grande Armée invades Russia, reaches Moscow only to find it abandoned and burning; the catastrophic winter retreat devastates the French army.",region:"Russia / France"},
  {year:1815,text:"Napoleon is decisively defeated at Waterloo by allied forces under Wellington and Blücher, ending the Napoleonic era and leading to his final exile to St Helena.",region:"Belgium / Europe"},
  {year:1821,text:"Greece begins its war of independence against the Ottoman Empire, rallying Philhellene support across Europe and eventually securing statehood in 1830.",region:"Greece / Ottoman Empire"},
  {year:1825,text:"The world's first public steam railway to carry passengers opens between Stockton and Darlington in northern England, inaugurating the railway age.",region:"Great Britain"},
  {year:1848,text:"A wave of revolutionary uprisings sweeps France, the Austrian Empire, the German states and Italy simultaneously, though most are ultimately suppressed.",region:"Europe"},
  {year:1848,text:"Karl Marx and Friedrich Engels publish The Communist Manifesto in London, calling on the workers of the world to unite against the capitalist system.",region:"Great Britain"},
  {year:1859,text:"Charles Darwin publishes On the Origin of Species in London, presenting the theory of evolution by natural selection and transforming humanity's understanding of life.",region:"Great Britain"},
  {year:1861,text:"Tsar Alexander II issues the Emancipation Reform, freeing approximately twenty-three million serfs in Russia and transforming its social and economic structure.",region:"Russia"},
  {year:1864,text:"The First Geneva Convention is signed, establishing rules for the humane treatment of wounded soldiers and the neutrality of medical personnel in wartime.",region:"Switzerland"},
  {year:1866,text:"Prussia defeats Austria at the Battle of Königgrätz in just seven weeks, confirming Prussian dominance in the German world and excluding Austria from unification.",region:"Prussia / Austria"},
  {year:1867,text:"The Austro-Hungarian Compromise creates the Dual Monarchy, granting Hungary equal status with Austria within a single empire under Emperor Franz Joseph I.",region:"Austria-Hungary"},
  {year:1871,text:"The German Empire is proclaimed in the Hall of Mirrors at Versailles while Paris is still under siege, unifying the German states under Prussian leadership.",region:"Germany / France"},
  {year:1871,text:"The Paris Commune seizes control of the French capital for ten weeks before being violently suppressed by the French Army in the bloody Semaine sanglante.",region:"France"},
  {year:1884,text:"The Berlin Conference divides Africa among European colonial powers without consulting any African peoples, dramatically accelerating the Scramble for Africa.",region:"Germany / Europe"},
  // ── 1900–1919 ──
  {year:1904,text:"The Entente Cordiale is signed between France and Great Britain, resolving colonial disputes and forming the diplomatic partnership that will shape First World War alliances.",region:"France / Great Britain"},
  {year:1905,text:"The Russian Revolution erupts following the Bloody Sunday massacre in St Petersburg, forcing Tsar Nicholas II to issue the October Manifesto and create a parliament.",region:"Russia"},
  {year:1907,text:"The Triple Entente is formally consolidated between France, Russia and Great Britain, creating the alliance that will face the Triple Alliance in the coming world war.",region:"Europe"},
  {year:1908,text:"Austria-Hungary formally annexes Bosnia-Herzegovina, provoking a major international crisis and sharply escalating great-power tensions in the Balkans.",region:"Austria-Hungary / Bosnia"},
  {year:1912,text:"The First Balkan War erupts as Serbia, Bulgaria, Greece and Montenegro unite to expel Ottoman forces from nearly all of their remaining European territory.",region:"Balkans"},
  {year:1914,text:"Archduke Franz Ferdinand of Austria-Hungary is assassinated in Sarajevo by a Bosnian Serb nationalist, triggering the chain of mobilisations that begins the First World War.",region:"Bosnia / Europe"},
  {year:1915,text:"The British-led Gallipoli campaign attempts to knock the Ottoman Empire out of the war and open a supply route to Russia, but ends in a costly Allied withdrawal after eight months.",region:"Ottoman Empire / Gallipoli"},
  {year:1916,text:"The Battle of Verdun and the Battle of the Somme — the two longest and bloodiest battles on the Western Front — are both fought in the same catastrophic year.",region:"France"},
  {year:1917,text:"The Bolshevik Revolution, led by Vladimir Lenin, overthrows the Provisional Government in Petrograd, bringing the Communist Party to power in Russia.",region:"Russia"},
  {year:1918,text:"The First World War ends with an armistice signed at 11 am on the 11th of November, after four years of fighting that killed approximately seventeen million people.",region:"Europe"},
  {year:1918,text:"The Spanish flu pandemic, spread in part by returning soldiers, sweeps across Europe killing tens of millions in one of the deadliest outbreaks in recorded history.",region:"Europe / Global"},
  {year:1919,text:"The Treaty of Versailles is signed in the Hall of Mirrors, officially ending the First World War and imposing severe reparations and territorial losses on Germany.",region:"France / Europe"},
  // ── 1920–1939 ──
  {year:1920,text:"The League of Nations holds its inaugural council meeting in Paris, establishing the first major intergovernmental organisation aimed at maintaining world peace.",region:"Europe / Global"},
  {year:1921,text:"The Irish Free State is established following the Anglo-Irish Treaty, partitioning Ireland and granting the twenty-six southern counties independence from Britain.",region:"Ireland / Great Britain"},
  {year:1922,text:"The Union of Soviet Socialist Republics is formally established, uniting Russia, Ukraine, Belarus and the Transcaucasian republics under single communist rule.",region:"Soviet Union"},
  {year:1922,text:"Benito Mussolini leads the Fascist March on Rome and is appointed Prime Minister of Italy, beginning the first fascist dictatorship in Europe.",region:"Italy"},
  {year:1923,text:"The Weimar Republic suffers catastrophic hyperinflation, with prices doubling every few days; German citizens famously wheel barrows of banknotes to buy a loaf of bread.",region:"Germany"},
  {year:1925,text:"The Locarno Treaties normalise relations between Germany, France, Belgium, Britain and Italy and pave the way for Germany to join the League of Nations.",region:"Europe"},
  {year:1929,text:"The Wall Street Crash triggers the Great Depression, devastating European economies, fuelling political extremism and contributing to the rise of fascism across the continent.",region:"Europe"},
  {year:1929,text:"The Lateran Treaty between Mussolini's government and the Holy See creates the independent Vatican City State and resolves the long-standing Roman Question.",region:"Italy / Vatican"},
  {year:1933,text:"Adolf Hitler is appointed Chancellor of Germany; within months he dismantles the Weimar Republic's democratic institutions and establishes a totalitarian one-party state.",region:"Germany"},
  {year:1935,text:"The Nuremberg Laws are enacted in Germany, stripping Jewish citizens of their German citizenship and legally institutionalising racial antisemitism in the Reich.",region:"Germany"},
  {year:1936,text:"The Spanish Civil War begins when General Franco launches a military coup against the elected Republican government, drawing in foreign powers as a prelude to the wider war.",region:"Spain"},
  {year:1936,text:"Nazi Germany remilitarises the Rhineland in violation of the Versailles Treaty; France and Britain fail to respond, emboldening Hitler to pursue further territorial ambitions.",region:"Germany / Europe"},
  {year:1937,text:"German and Italian aircraft bomb the Basque town of Guernica on market day during the Spanish Civil War, killing hundreds of civilians and inspiring Picasso's famous painting.",region:"Spain"},
  {year:1938,text:"Germany announces the Anschluss — the annexation of Austria — incorporating it into the Third Reich without military resistance or meaningful international opposition.",region:"Germany / Austria"},
  {year:1938,text:"Britain and France sign the Munich Agreement ceding the Sudetenland to Nazi Germany, an act Chamberlain declared would bring 'peace for our time' — it did not.",region:"Czechoslovakia / Europe"},
  {year:1938,text:"Kristallnacht — the Night of Broken Glass — sees Nazi stormtroopers destroy Jewish businesses, homes and synagogues across Germany and Austria in an organised national pogrom.",region:"Germany"},
  {year:1939,text:"Germany and the Soviet Union sign the Molotov-Ribbentrop Pact, secretly dividing Eastern Europe into spheres of influence before Germany invades Poland.",region:"Germany / Soviet Union"},
  {year:1939,text:"Nazi Germany invades Poland on the 1st of September; Britain and France declare war two days later, beginning the Second World War in Europe.",region:"Europe"},
  // ── 1940–1945 ──
  {year:1940,text:"The Dunkirk evacuation rescues over 330,000 Allied troops from the beaches of northern France as German forces close in, in a dramatic operation Churchill called a miracle of deliverance.",region:"France / Great Britain"},
  {year:1940,text:"France falls to Germany in just six weeks; the collaborationist Vichy regime is established while Britain stands alone under new Prime Minister Winston Churchill.",region:"France / Great Britain"},
  {year:1940,text:"The Battle of Britain is fought in the skies above England between the Royal Air Force and the Luftwaffe, in the first major campaign conducted entirely by air power.",region:"Great Britain"},
  {year:1941,text:"Operation Barbarossa — Germany's invasion of the Soviet Union — begins on 22 June as the largest land invasion in history, ultimately proving fatal to Hitler's war aims.",region:"Soviet Union"},
  {year:1942,text:"The Wannsee Conference in Berlin coordinates the implementation of the Holocaust, the systematic genocide of six million European Jews by the Nazi regime.",region:"Germany"},
  {year:1943,text:"The German Sixth Army surrenders at Stalingrad following a catastrophic encirclement by Soviet forces, marking the definitive turning point of the war on the Eastern Front.",region:"Soviet Union"},
  {year:1944,text:"Allied forces land on five beaches along the Normandy coast on D-Day, the largest seaborne invasion in history, opening the long-awaited second front in Western Europe.",region:"France"},
  {year:1944,text:"The Warsaw Uprising begins as the Polish Home Army launches a major revolt against German occupation, fighting for sixty-three days before being brutally crushed.",region:"Poland"},
  {year:1945,text:"The Yalta Conference convenes as Roosevelt, Churchill and Stalin meet in Crimea to negotiate the post-war order, dividing Europe into Western and Soviet spheres.",region:"Soviet Union / Europe"},
  {year:1945,text:"The Second World War in Europe ends with Germany's unconditional surrender on 8 May — Victory in Europe Day — following the fall of Berlin and Hitler's death.",region:"Europe"},
  {year:1945,text:"The Nuremberg Trials begin, putting senior Nazi officials on trial for war crimes, crimes against humanity and the newly defined crime of aggression.",region:"Germany"},
  // ── 1946–1960 ──
  {year:1946,text:"Winston Churchill delivers his Iron Curtain speech in Fulton, Missouri, declaring that a curtain has descended across Europe dividing the communist East from the democratic West.",region:"Europe / USA"},
  {year:1947,text:"The United States announces the Marshall Plan, offering billions of dollars to rebuild Western European economies devastated by the war and resist communist expansion.",region:"Europe / USA"},
  {year:1948,text:"The Soviet Union blockades West Berlin, prompting the Western Allies to supply the city entirely by air for nearly a year in the Berlin Airlift — an early Cold War confrontation.",region:"Germany"},
  {year:1948,text:"The Universal Declaration of Human Rights is adopted by the United Nations General Assembly in Paris, setting out for the first time a global standard of fundamental rights.",region:"France / Global"},
  {year:1949,text:"The North Atlantic Treaty is signed in Washington, creating NATO as a collective defence alliance among Western democracies against Soviet expansion in Europe.",region:"Europe / North America"},
  {year:1949,text:"West Germany and East Germany are formally established as separate states, dividing Germany into two nations along ideological lines for the next four decades.",region:"Germany"},
  {year:1950,text:"French Foreign Minister Robert Schuman proposes pooling French and German coal and steel production, in what becomes the Schuman Declaration — the founding moment of European integration.",region:"France / Western Europe"},
  {year:1951,text:"The Treaty of Paris establishes the European Coal and Steel Community, pooling the heavy industries of France, West Germany, Italy and the Benelux countries.",region:"Western Europe"},
  {year:1953,text:"Joseph Stalin dies in Moscow, ending nearly three decades of totalitarian rule and triggering a power struggle within the Soviet Communist Party.",region:"Soviet Union"},
  {year:1954,text:"The European Convention on Human Rights enters into force, establishing the European Court of Human Rights and creating a binding regional human rights system.",region:"Council of Europe"},
  {year:1955,text:"The Warsaw Pact is signed in Poland, creating a military alliance of the Soviet Union and its Eastern Bloc satellite states as a direct counterweight to NATO.",region:"Eastern Europe"},
  {year:1956,text:"Khrushchev delivers his Secret Speech denouncing Stalin's cult of personality to the 20th Congress of the Communist Party, shocking the entire Soviet establishment.",region:"Soviet Union"},
  {year:1956,text:"The Hungarian Uprising sees thousands of Hungarians rise against Soviet domination; Soviet tanks crush the revolt and Prime Minister Imre Nagy is arrested and later executed.",region:"Hungary / Soviet Union"},
  {year:1956,text:"The Suez Crisis erupts as Britain and France secretly collude with Israel to attack Egypt after Nasser nationalises the Suez Canal, only to be forced to withdraw by the US and Soviet Union.",region:"Egypt / Europe"},
  {year:1957,text:"The Treaties of Rome are signed by six nations, establishing the European Economic Community and Euratom — the foundational treaties of what would become the European Union.",region:"Western Europe"},
  // ── 1961–1980 ──
  {year:1961,text:"East Germany constructs the Berlin Wall overnight, sealing the border between East and West Berlin to prevent the mass emigration of its citizens to the West.",region:"Germany"},
  {year:1962,text:"The Cuban Missile Crisis brings the world to the brink of nuclear war for thirteen days as the US and Soviet Union confront each other over Soviet missiles in Cuba.",region:"Soviet Union / Cuba"},
  {year:1963,text:"The Élysée Treaty of Friendship is signed by de Gaulle and Adenauer, reconciling France and West Germany and laying the cornerstone of European integration.",region:"France / Germany"},
  {year:1965,text:"France triggers the Empty Chair Crisis by boycotting EEC Council meetings for seven months, paralyzing European institutions in a dispute over qualified majority voting.",region:"France / EEC"},
  {year:1968,text:"The Prague Spring — a period of political liberalisation in Czechoslovakia — is crushed by a Soviet-led Warsaw Pact invasion, dashing hopes of socialism with a human face.",region:"Czechoslovakia / Soviet Union"},
  {year:1968,text:"The May 1968 student protests in Paris escalate into a general strike of ten million workers, nearly toppling President de Gaulle and shaking Western capitalist societies.",region:"France"},
  {year:1973,text:"The United Kingdom, Ireland and Denmark join the European Economic Community, expanding it from six to nine member states in the first enlargement of the organisation.",region:"Western Europe"},
  {year:1974,text:"The Carnation Revolution in Portugal ends nearly fifty years of authoritarian rule, as the military overthrows the Estado Novo regime in an almost entirely bloodless coup.",region:"Portugal"},
  {year:1975,text:"The Helsinki Accords are signed by thirty-five nations including the USSR, recognising post-war European borders and committing signatories to respect human rights.",region:"Europe"},
  {year:1975,text:"Francisco Franco, dictator of Spain since the Civil War, dies after thirty-six years in power; King Juan Carlos I subsequently steers Spain's transition to democracy.",region:"Spain"},
  {year:1979,text:"The first direct elections to the European Parliament are held, allowing citizens of member states to directly vote for their parliamentary representatives for the first time.",region:"European Community"},
  {year:1979,text:"Margaret Thatcher becomes the United Kingdom's first female Prime Minister, beginning eleven years of transformative Conservative government and the Thatcherite era.",region:"Great Britain"},
  {year:1979,text:"The Soviet Union invades Afghanistan, beginning a decade-long occupation that drains Soviet resources and fuels the mujahideen insurgency that hastens the USSR's eventual collapse.",region:"Soviet Union / Afghanistan"},
  // ── 1980–1992 ──
  {year:1980,text:"Poland's Solidarity movement — the first independent trade union in a communist bloc country — is founded under Lech Wałęsa's leadership at the Gdańsk shipyard.",region:"Poland"},
  {year:1981,text:"Greece becomes the tenth member state of the European Community in the first Mediterranean enlargement, marking the return of a post-dictatorship democracy to European institutions.",region:"Greece / European Community"},
  {year:1981,text:"Martial law is declared in Poland by General Jaruzelski, suspending Solidarity and interning thousands of activists in an attempt to forestall a Soviet-style intervention.",region:"Poland"},
  {year:1985,text:"The Schengen Agreement is signed by France, West Germany and the Benelux states, establishing the framework to abolish internal border controls between signatory countries.",region:"Western Europe"},
  {year:1985,text:"Mikhail Gorbachev becomes General Secretary of the Soviet Communist Party and launches his reform programmes of glasnost (openness) and perestroika (restructuring).",region:"Soviet Union"},
  {year:1986,text:"Spain and Portugal join the European Community in the second Mediterranean enlargement, bringing the total membership to twelve states.",region:"Spain / Portugal / EEC"},
  {year:1986,text:"The Single European Act is signed, committing EC member states to complete a fully integrated Single Market by 1992 — the most significant treaty revision since Rome.",region:"European Community"},
  {year:1986,text:"The Chernobyl nuclear power plant explodes in northern Ukraine, causing the world's worst civil nuclear disaster and spreading radioactive contamination across large parts of Europe.",region:"Soviet Ukraine"},
  {year:1989,text:"The Berlin Wall falls on the night of 9 November as East Germans breach the checkpoints, symbolising the collapse of communist regimes across Eastern Europe.",region:"Germany"},
  {year:1989,text:"The Velvet Revolution sees mass peaceful protests topple Czechoslovakia's communist government within days; playwright Václav Havel becomes President by year's end.",region:"Czechoslovakia"},
  {year:1990,text:"Germany is officially reunified on the 3rd of October, ending four decades of division and resurrecting a united Germany at the heart of Europe for the first time since 1945.",region:"Germany"},
  {year:1991,text:"Yugoslavia begins its violent dissolution as Slovenia and Croatia declare independence; the ensuing wars will last a decade and claim over a hundred thousand lives.",region:"Yugoslavia"},
  {year:1991,text:"The Soviet Union formally dissolves on Christmas Day, breaking into fifteen independent republics and ending the Cold War that had shaped global politics for over forty years.",region:"Soviet Union"},
  {year:1992,text:"The Maastricht Treaty is signed, transforming the European Community into the European Union with common citizenship, a single currency timetable and expanded powers.",region:"Western Europe"},
  {year:1992,text:"Black Wednesday strikes as currency speculators force the British pound out of the European Exchange Rate Mechanism, costing the UK billions and humiliating John Major's government.",region:"Great Britain / Europe"},
  // ── 1993–2004 ──
  {year:1993,text:"The Single Market is completed across the European Community, creating the world's largest trading area and abolishing tariffs and trade barriers between member states.",region:"European Community"},
  {year:1993,text:"Czechoslovakia peacefully divides into the Czech Republic and Slovakia in the Velvet Divorce, effective on the first day of the year following a negotiated separation.",region:"Czech Republic / Slovakia"},
  {year:1994,text:"The Channel Tunnel opens, linking Great Britain to the European continent by rail for the first time in history through thirty-one miles under the English Channel.",region:"France / Great Britain"},
  {year:1995,text:"The Schengen Area enters into force, eliminating passport controls at the borders of France, Germany, Belgium, Luxembourg, the Netherlands, Spain and Portugal.",region:"Western Europe"},
  {year:1995,text:"Austria, Sweden and Finland join the European Union in the fourth enlargement, bringing membership to fifteen states and extending the EU into the Nordic region.",region:"European Union"},
  {year:1995,text:"The Srebrenica massacre takes place as Bosnian Serb forces execute some eight thousand Bosniak Muslim men and boys, the worst atrocity in Europe since the Holocaust.",region:"Bosnia"},
  {year:1995,text:"The Dayton Agreement ends the Bosnian War, partitioning Bosnia-Herzegovina into two entities and establishing an international peacekeeping force under NATO command.",region:"Bosnia / Europe"},
  {year:1997,text:"The Treaty of Amsterdam is signed, reforming EU institutions, strengthening social policy and incorporating the Schengen Agreement into the EU treaty framework.",region:"European Union"},
  {year:1998,text:"The Good Friday Agreement is signed in Belfast, providing a framework for power-sharing in Northern Ireland and effectively ending three decades of sectarian conflict.",region:"Northern Ireland / Ireland / Great Britain"},
  {year:1998,text:"The European Central Bank is established in Frankfurt, tasked with managing monetary policy for the future eurozone and maintaining price stability for the single currency.",region:"European Union"},
  {year:1999,text:"The euro is launched as an accounting currency across eleven EU member states, with notes and coins to follow in 2002, completing the most ambitious monetary project in history.",region:"European Union"},
  {year:1999,text:"NATO conducts its first combat operations in the Kosovo War, launching a seventy-eight-day air campaign against Yugoslavia to halt the ethnic cleansing of Kosovo Albanians.",region:"Yugoslavia / Kosovo"},
  {year:2001,text:"The September 11 attacks on the United States lead NATO to invoke Article 5 for the first time, committing all member states to treat the attack as an attack on them all.",region:"Europe / USA"},
  {year:2002,text:"Euro banknotes and coins enter circulation across twelve European Union member states on 1 January, replacing national currencies in the most visible step of monetary union.",region:"European Union"},
  {year:2004,text:"Ten countries join the European Union in its largest single expansion, bringing in eight former communist states alongside Cyprus and Malta in a historic reunification of Europe.",region:"European Union"},
  {year:2004,text:"The Madrid train bombings kill nearly two hundred people in coordinated attacks on commuter trains, in the worst terrorist attack on European soil since the Lockerbie bombing.",region:"Spain"},
  // ── 2005–2016 ──
  {year:2005,text:"Pope John Paul II dies in Rome after twenty-six years as the most-travelled pontiff in history; his funeral draws the largest-ever gathering of heads of state to the Vatican.",region:"Vatican / Poland / Europe"},
  {year:2005,text:"Voters in France and the Netherlands reject the proposed European Constitution in referenda, forcing the EU to abandon the constitutional project and begin treaty reform afresh.",region:"France / Netherlands / EU"},
  {year:2005,text:"London suicide bombers kill fifty-two people on the Underground and a bus on 7 July, in the deadliest attack on British soil since the Second World War.",region:"Great Britain"},
  {year:2007,text:"Romania and Bulgaria join the European Union, expanding the bloc to twenty-seven member states and extending the Single Market to the Black Sea region.",region:"European Union"},
  {year:2007,text:"The Treaty of Lisbon is signed, replacing the failed Constitutional Treaty, reforming EU institutions and creating the permanent post of European Council President.",region:"European Union"},
  {year:2008,text:"Kosovo declares independence from Serbia, becoming Europe's newest state; the move is recognised by the United States and most EU members but contested by Serbia and Russia.",region:"Kosovo / Europe"},
  {year:2008,text:"Russia invades Georgia in a five-day war, recognising the breakaway regions of South Ossetia and Abkhazia — the first use of Russian military force in Europe since the Cold War.",region:"Russia / Georgia"},
  {year:2009,text:"The Treaty of Lisbon enters into force, fundamentally restructuring EU governance; Herman Van Rompuy becomes the first permanent President of the European Council.",region:"European Union"},
  {year:2010,text:"The Greek sovereign debt crisis erupts as Greece reveals its deficit is far larger than disclosed; the EU and IMF agree the first of three international bailouts, launching the eurozone crisis.",region:"Greece / European Union"},
  {year:2011,text:"The Arab Spring uprisings across North Africa and the Middle East send hundreds of thousands of refugees toward Europe, beginning a sustained migration pressure on EU borders.",region:"Europe / North Africa"},
  {year:2012,text:"ECB President Mario Draghi pledges to do 'whatever it takes' to preserve the euro, a brief statement that effectively ends the immediate existential threat to the single currency.",region:"European Union"},
  {year:2012,text:"The European Union is awarded the Nobel Peace Prize for its contribution over six decades to the advancement of peace, reconciliation, democracy and human rights in Europe.",region:"European Union"},
  {year:2013,text:"Croatia becomes the twenty-eighth member state of the European Union, the second former Yugoslav republic to join after Slovenia.",region:"Croatia / European Union"},
  {year:2013,text:"Edward Snowden reveals the mass surveillance programmes of the NSA and GCHQ, sparking a major debate in Europe about privacy, digital rights and transatlantic intelligence sharing.",region:"USA / Europe"},
  {year:2014,text:"Russia annexes Crimea from Ukraine following the Euromaidan revolution in Kyiv, in the first forcible annexation of European territory since the Second World War.",region:"Russia / Ukraine"},
  {year:2014,text:"Flight MH17 is shot down over eastern Ukraine, killing all 298 people aboard; an independent investigation concludes it was struck by a Russian-supplied surface-to-air missile.",region:"Ukraine / Russia / Europe"},
  {year:2014,text:"Scotland votes in a referendum on independence from the United Kingdom; the No campaign wins by 55% to 45%, keeping Scotland within the union for the time being.",region:"Scotland / Great Britain"},
  {year:2015,text:"The Paris attacks of November kill 130 people across the Bataclan theatre and other sites, in the deadliest attack on French soil since the Second World War.",region:"France"},
  {year:2015,text:"Over one million refugees and migrants cross into Europe — many fleeing the Syrian civil war — triggering the continent's most severe migration crisis since World War II.",region:"Europe"},
  {year:2016,text:"The United Kingdom votes in a referendum to leave the European Union by 52% to 48%, shocking the political establishment and beginning years of contentious Brexit negotiations.",region:"Great Britain"},
  // ── 2017–2024 ──
  {year:2017,text:"Emmanuel Macron is elected President of France, defeating Marine Le Pen of the National Front in the second round and halting the immediate wave of populist electoral victories in Europe.",region:"France"},
  {year:2017,text:"The United Kingdom formally triggers Article 50, notifying the European Union of its intention to leave and beginning the two-year withdrawal negotiation process.",region:"Great Britain / EU"},
  {year:2017,text:"Catalonia holds an independence referendum banned by Madrid; Spanish police clash with voters, and the regional government briefly declares independence before backing down under pressure.",region:"Spain / Catalonia"},
  {year:2019,text:"The European Green Deal is proposed by the new Commission under Ursula von der Leyen, pledging to make Europe the first climate-neutral continent by 2050.",region:"European Union"},
  {year:2019,text:"Notre-Dame Cathedral in Paris catches fire during renovation work and is severely damaged, with its medieval spire collapsing; France pledges full restoration.",region:"France"},
  {year:2020,text:"The United Kingdom formally leaves the European Union on 31 January, becoming the first member state to exit in the bloc's history, ending forty-seven years of British membership.",region:"Great Britain / EU"},
  {year:2020,text:"The COVID-19 pandemic forces near-total lockdowns across Europe; the EU launches its NextGenerationEU recovery fund — the first joint EU borrowing programme in history.",region:"Europe"},
  {year:2021,text:"The COP26 climate summit in Glasgow brings together world leaders to accelerate climate action, resulting in the Glasgow Climate Pact on limiting temperature rise.",region:"Great Britain / Global"},
  {year:2022,text:"Russia launches a full-scale invasion of Ukraine on 24 February, beginning the largest conventional military conflict in Europe since the Second World War.",region:"Ukraine / Russia"},
  {year:2022,text:"Finland and Sweden apply to join NATO following Russia's invasion of Ukraine, ending decades of Nordic non-alignment in a historic geopolitical shift for northern Europe.",region:"Finland / Sweden / NATO"},
  {year:2023,text:"Finland officially joins NATO as its thirty-first member, extending the alliance's border with Russia by over 1,300 kilometres in a major strategic expansion.",region:"Finland / NATO"},
  {year:2023,text:"The European Union adopts the AI Act — the world's first comprehensive legal framework for regulating artificial intelligence — setting a global benchmark for AI governance.",region:"European Union"},
  {year:2024,text:"European Parliament elections see significant gains for far-right and nationalist parties across France, Germany and Italy, prompting Macron to call snap parliamentary elections.",region:"European Union"},
  {year:2024,text:"Ukraine is formally granted candidate status for EU membership, opening accession negotiations as a landmark moment in Europe's response to Russian aggression.",region:"Ukraine / European Union"},
];

// ════════════════════════════════════════════════
//  DETERMINISTIC DAILY SYSTEM
// ════════════════════════════════════════════════
// Build a fixed shuffle of event indices once — same result for every user
const SHUFFLED = (function(){
  const arr = Array.from({length:EVENTS.length},(_,i)=>i);
  let s = 314159265; // NEVER change this seed
  const rng = ()=>{ s=(Math.imul(s,1664525)+1013904223)>>>0; return s/0xFFFFFFFF; };
  for(let i=arr.length-1;i>0;i--){
    const j=Math.floor(rng()*(i+1));
    [arr[i],arr[j]]=[arr[j],arr[i]];
  }
  return arr;
})();

const EPOCH_MS = new Date('2025-01-01T00:00:00Z').getTime();

function todayStr(){
  const n=new Date();
  return `${n.getFullYear()}-${pad(n.getMonth()+1)}-${pad(n.getDate())}`;
}
function pad(n){return String(n).padStart(2,'0');}
function dateToStr(d){return `${d.getUTCFullYear()}-${pad(d.getUTCMonth()+1)}-${pad(d.getUTCDate())}`;}
function dayIndex(dateStr){
  return Math.floor((new Date(dateStr+'T00:00:00Z').getTime()-EPOCH_MS)/86400000);
}
function eventForDate(dateStr){
  const n=dayIndex(dateStr);
  if(n<0)return null;
  return EVENTS[SHUFFLED[n%SHUFFLED.length]];
}
function fmtDate(dateStr){
  return new Date(dateStr+'T00:00:00Z').toLocaleDateString('en-GB',{day:'numeric',month:'short',year:'numeric',timeZone:'UTC'});
}
function yesterdayStr(){
  const d=new Date(); d.setDate(d.getDate()-1);
  return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`;
}

// ════════════════════════════════════════════════
//  PERSISTENCE
// ════════════════════════════════════════════════
const SK='eurdle_v2';
function loadUD(){try{return JSON.parse(localStorage.getItem(SK))||mkUD();}catch{return mkUD();}}
function mkUD(){return{streak:0,best:0,lastPlayed:null,history:{}};}
function saveUD(){try{localStorage.setItem(SK,JSON.stringify(UD));}catch{}}

let UD=loadUD();

// ════════════════════════════════════════════════
//  GAME STATE
// ════════════════════════════════════════════════
const MAX=6;
let mode='daily';      // 'daily' | 'archive'
let curEvent=null;
let curDate=null;
let guesses=[];
let hints=[];
let input='';
let bc=false;
let over=false;

// ════════════════════════════════════════════════
//  HINTS
// ════════════════════════════════════════════════
function buildHints(ev){
  const pool=EVENTS
    .filter(e=>e!==ev && Math.abs(e.year-ev.year)>=2)
    .sort((a,b)=>Math.abs(b.year-ev.year)-Math.abs(a.year-ev.year));
  const later=pool.filter(e=>e.year>ev.year);
  const earlier=pool.filter(e=>e.year<ev.year);
  const h=[];
  let l=0,e=0;
  while(h.length<5){
    if(l<later.length)   h.push({type:'before',text:later[l++].text});
    if(h.length>=5)break;
    if(e<earlier.length) h.push({type:'after', text:earlier[e++].text});
    if(l>=later.length && e>=earlier.length)break;
  }
  return h;
}

// ════════════════════════════════════════════════
//  KEYBOARD & NUMPAD
// ════════════════════════════════════════════════
function pressKey(d){
  if(over)return;
  if(input.length>=4)return;
  input+=d; renderInput();
}
function deleteLast(){
  if(over)return;
  input=input.slice(0,-1); renderInput();
}
function toggleEra(){
  if(over)return;
  bc=!bc; renderInput();
}
document.addEventListener('keydown',e=>{
  if(document.getElementById('arcOverlay').classList.contains('open'))return;
  if(over)return;
  if(e.key>='0'&&e.key<='9') pressKey(e.key);
  else if(e.key==='Backspace') deleteLast();
  else if(e.key==='Enter') submitGuess();
});

// ════════════════════════════════════════════════
//  RENDER INPUT
// ════════════════════════════════════════════════
function renderInput(){
  const d=document.getElementById('yrDisplay');
  const p=document.getElementById('eraPill');
  const b=document.getElementById('bcKey');
  p.textContent=bc?'BC':'AD';
  p.className='era-pill'+(bc?' bc':'');
  b.className='key bc'+(bc?' on':'');
  if(!input){d.className='yr-digits empty';d.textContent='Enter a year\u2026';}
  else{d.className='yr-digits';d.innerHTML=input+'<span class="cursor"></span>';}
}

// ════════════════════════════════════════════════
//  CHIP HELPERS  (NO distance numbers shown)
// ════════════════════════════════════════════════
function chipCls(diff){
  if(diff===0)  return'exact';
  if(diff<=5)   return'near';
  if(diff<=15)  return'close';
  if(diff<=30)  return'mid';
  return'far';
}
function chipEmoji(diff){
  if(diff===0)  return'🟩';
  if(diff<=5)   return'🟩';
  if(diff<=15)  return'🟨';
  if(diff<=30)  return'🟧';
  return'🟥';
}
function fmtYear(y){return y<0?Math.abs(y)+' BC':y+' AD';}

// ════════════════════════════════════════════════
//  RENDER GUESSES
// ════════════════════════════════════════════════
function renderGuesses(){
  const c=document.getElementById('guessesEl');
  c.innerHTML='';
  guesses.forEach(g=>{
    const diff=Math.abs(g-curEvent.year);
    const cls=chipCls(diff);
    const arrow=g<curEvent.year?'↑':g>curEvent.year?'↓':'✓';
    const row=document.createElement('div');
    row.className='g-row';
    row.innerHTML=`<div class="g-chip ${cls}">${fmtYear(g)}</div><div class="g-arrow">${arrow}</div>`;
    c.appendChild(row);
  });
}

// ════════════════════════════════════════════════
//  RENDER HINTS
// ════════════════════════════════════════════════
function renderHints(){
  const s=document.getElementById('hintsEl');
  s.innerHTML='';
  const n=Math.min(guesses.length,hints.length);
  for(let i=0;i<n;i++){
    const h=hints[i];
    const row=document.createElement('div');
    row.className='hint-row';
    row.innerHTML=`<span class="hint-tag ${h.type}">${h.type==='before'?'Before':'After'}</span><span>${h.text}</span>`;
    s.appendChild(row);
  }
}

// ════════════════════════════════════════════════
//  RENDER DOTS
// ════════════════════════════════════════════════
function renderDots(){
  const d=document.getElementById('dotsEl');
  const l=document.getElementById('attemptsLbl');
  d.innerHTML='';
  for(let i=0;i<MAX;i++){
    const dot=document.createElement('div');
    dot.className='dot';
    if(i<guesses.length){
      const diff=Math.abs(guesses[i]-curEvent.year);
      dot.className+=(diff===0)?' ok':' bad';
    }
    d.appendChild(dot);
  }
  if(!over){const left=MAX-guesses.length;l.textContent=left+(left===1?' attempt left':' attempts left');}
  else l.textContent='';
}

// ════════════════════════════════════════════════
//  STREAK BADGE
// ════════════════════════════════════════════════
function updateStreak(){
  const b=document.getElementById('streakBadge');
  if(UD.streak>0){b.textContent=`🔥 ${UD.streak}`;b.className='streak-badge show';}
  else b.className='streak-badge';
}

// ════════════════════════════════════════════════
//  SUBMIT
// ════════════════════════════════════════════════
function submitGuess(){
  if(over)return;
  if(!input){shake();return;}
  let yr=parseInt(input,10);
  if(isNaN(yr)){shake();return;}
  if(bc)yr=-yr;
  guesses.push(yr);
  input='';bc=false;
  renderInput();renderGuesses();renderDots();
  const diff=Math.abs(yr-curEvent.year);
  if(diff===0)endGame(true);
  else if(guesses.length>=MAX)endGame(false);
  else renderHints();
}
function shake(){
  const w=document.getElementById('inputWrap');
  w.classList.remove('shake');void w.offsetWidth;w.classList.add('shake');
}

// ════════════════════════════════════════════════
//  END GAME
// ════════════════════════════════════════════════
function endGame(won){
  over=true;
  renderHints();renderDots();

  // Persist daily result & update streak
  if(mode==='daily'){
    const today=todayStr();
    if(!UD.history[today]){ // first time completing today
      if(won){
        const yest=yesterdayStr();
        UD.streak=(UD.lastPlayed===yest)?UD.streak+1:1;
        UD.best=Math.max(UD.best,UD.streak);
      } else {
        UD.streak=0;
      }
      UD.lastPlayed=today;
      UD.history[today]={won,guesses:guesses.slice(),eventYear:curEvent.year};
      saveUD();
    }
    updateStreak();
    document.getElementById('archiveHdrBtn').classList.add('show');
    document.getElementById('btnArchive').style.display='';
    document.getElementById('btnRandom').style.display='none';
  } else {
    // archive mode
    document.getElementById('btnArchive').style.display='none';
    document.getElementById('btnRandom').style.display='';
  }

  // Show message
  const msg=document.getElementById('msgEl');
  const title=document.getElementById('msgTitle');
  const body=document.getElementById('msgBody');
  const yrStr=fmtYear(curEvent.year);
  if(won){
    const p=['Remarkable!','Excellent!','Well Done!','Good Work!','Close Call!','Just Made It!'];
    title.textContent=p[Math.min(guesses.length-1,5)];
    const sk=mode==='daily'&&UD.streak>1?` 🔥 ${UD.streak}-day streak!`:'';
    body.textContent=`The year was ${yrStr}. Found in ${guesses.length}/6.${sk}`;
    msg.className='msg win';
  } else {
    title.textContent='Not This Time…';
    body.textContent=`The answer was ${yrStr}.`;
    msg.className='msg lose';
  }
  document.getElementById('enterBtn').disabled=true;
  document.getElementById('btnShare').style.display='';
}

// ════════════════════════════════════════════════
//  SHARE
// ════════════════════════════════════════════════
function shareResult(){
  const won=guesses.length>0&&guesses[guesses.length-1]===curEvent.year;
  const score=won?`${guesses.length}/6`:'X/6';
  const emojiLine=guesses.map(g=>{
    const diff=Math.abs(g-curEvent.year);
    const dir=g<curEvent.year?'↑':g>curEvent.year?'↓':'✓';
    return chipEmoji(diff)+dir;
  }).join('  ');
  const streakLine=mode==='daily'&&UD.streak>0?`🔥 Streak: ${UD.streak}\n`:'';
  const dateLine=mode==='daily'?`EURDLE 🇪🇺  ${fmtDate(curDate)}`:`EURDLE 🇪🇺  Archive — ${fmtDate(curDate)}`;
  const text=`${dateLine}\n${streakLine}${score}\n\n${emojiLine}\n\nGuess the year of European historical events!`;
  if(navigator.share){
    navigator.share({title:'Eurdle',text}).catch(()=>copyText(text));
  } else {
    copyText(text);
  }
}
function copyText(t){
  const btn=document.getElementById('btnShare');
  navigator.clipboard.writeText(t).then(()=>{
    showToast('Result copied to clipboard!');
    const orig=btn.textContent;
    btn.textContent='✓ Copied!';
    setTimeout(()=>{btn.textContent=orig;},2000);
  }).catch(()=>{prompt('Copy this result:',t);});
}
function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
}

// ════════════════════════════════════════════════
//  ARCHIVE
// ════════════════════════════════════════════════
function openArchive(){
  buildArchiveList();
  document.getElementById('arcOverlay').classList.add('open');
}
function closeArchive(){
  document.getElementById('arcOverlay').classList.remove('open');
}

function buildArchiveList(){
  const list=document.getElementById('arcList');
  list.innerHTML='';
  const today=todayStr();
  const entries=[];
  let d=new Date('2025-01-01T00:00:00Z');
  const todayD=new Date(today+'T00:00:00Z');
  while(d<todayD){
    const ds=dateToStr(d);
    const ev=eventForDate(ds);
    if(ev)entries.push({dateStr:ds,event:ev});
    d.setUTCDate(d.getUTCDate()+1);
  }
  entries.reverse();
  if(!entries.length){
    list.innerHTML='<div class="arc-empty">No past challenges yet. Check back tomorrow!</div>';
    return;
  }
  entries.forEach(({dateStr,event})=>{
    const played=!!UD.history[dateStr];
    const item=document.createElement('div');
    item.className='arc-item'+(played?' played':'');
    const prev=event.text.length>62?event.text.slice(0,62)+'…':event.text;
    item.innerHTML=`
      <div class="arc-date">${fmtDate(dateStr)}</div>
      <div class="arc-preview">${prev}</div>
      ${played?'<div class="arc-done">✓</div>':''}`;
    item.onclick=()=>{ startArchive(dateStr); closeArchive(); };
    list.appendChild(item);
  });
}

function playRandomArchive(){
  const today=todayStr();
  const todayD=new Date(today+'T00:00:00Z');
  const start=new Date('2025-01-01T00:00:00Z');
  const total=Math.floor((todayD-start)/86400000);
  if(total<=0){showToast('No archived games yet!');return;}
  const rnd=Math.floor(Math.random()*total);
  const d=new Date(start); d.setUTCDate(d.getUTCDate()+rnd);
  startArchive(dateToStr(d));
}

function startArchive(dateStr){
  mode='archive';
  curDate=dateStr;
  curEvent=eventForDate(dateStr);
  if(!curEvent){showToast('Event not found.');return;}
  hints=buildHints(curEvent);
  guesses=[];input='';bc=false;over=false;

  document.getElementById('clueText').textContent=curEvent.text;
  document.getElementById('clueRegion').textContent='📍 '+curEvent.region;
  document.getElementById('modeBanner').textContent='📅 Archive — '+fmtDate(dateStr);
  document.getElementById('modeBanner').classList.add('show');
  document.getElementById('enterBtn').disabled=false;
  document.getElementById('msgEl').className='msg';
  document.getElementById('btnShare').style.display='none';
  document.getElementById('btnArchive').style.display='none';
  document.getElementById('btnRandom').style.display='none';
  renderInput();renderGuesses();renderHints();renderDots();
}

// ════════════════════════════════════════════════
//  INIT DAILY
// ════════════════════════════════════════════════
function initDaily(){
  mode='daily';
  curDate=todayStr();
  curEvent=eventForDate(curDate);
  hints=buildHints(curEvent);

  document.getElementById('clueText').textContent=curEvent.text;
  document.getElementById('clueRegion').textContent='📍 '+curEvent.region;
  document.getElementById('modeBanner').classList.remove('show');

  updateStreak();

  // Show archive button if daily already completed ever (not just today)
  const dailyDone=!!UD.history[curDate];
  if(dailyDone||UD.lastPlayed){
    document.getElementById('archiveHdrBtn').classList.add('show');
  }

  const existing=UD.history[curDate];
  if(existing){
    // Restore completed state
    guesses=existing.guesses.slice();
    over=true;
    renderGuesses();renderHints();renderDots();
    const won=existing.won;
    const msg=document.getElementById('msgEl');
    const title=document.getElementById('msgTitle');
    const body=document.getElementById('msgBody');
    if(won){
      const p=['Remarkable!','Excellent!','Well Done!','Good Work!','Close Call!','Just Made It!'];
      title.textContent=p[Math.min(guesses.length-1,5)];
      const sk=UD.streak>1?` 🔥 ${UD.streak}-day streak!`:'';
      body.textContent=`The year was ${fmtYear(curEvent.year)}. Found in ${guesses.length}/6.${sk}`;
      msg.className='msg win';
    } else {
      title.textContent='Not This Time…';
      body.textContent=`The answer was ${fmtYear(curEvent.year)}.`;
      msg.className='msg lose';
    }
    document.getElementById('enterBtn').disabled=true;
    document.getElementById('btnShare').style.display='';
    document.getElementById('btnArchive').style.display='';
    document.getElementById('btnRandom').style.display='none';
    document.getElementById('archiveHdrBtn').classList.add('show');
  } else {
    guesses=[];over=false;input='';bc=false;
    document.getElementById('msgEl').className='msg';
    document.getElementById('enterBtn').disabled=false;
    document.getElementById('btnShare').style.display='none';
    document.getElementById('btnArchive').style.display='none';
    document.getElementById('btnRandom').style.display='none';
    renderGuesses();renderHints();renderDots();
  }
  renderInput();
}

// ── Start ──
initDaily();
</script>
</body>
</html>
