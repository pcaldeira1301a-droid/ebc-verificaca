<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<style>body{margin:0}[hidden]{display:none!important}</style>
<title>Portal do EBC</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Exo+2:wght@600;700;800;900&family=IBM+Plex+Mono:wght@500&family=Source+Sans+3:wght@400;600;700&display=swap">
<style>
/* Layout: glass sidebar with icons + sticky "Quartel General" header + card-based content; verification is a separate pure-black flow. */
:root{
  --black:#000;
  --bg:#060b1a;
  --surface:#0b1530;
  --surface-2:#10204a;
  --line:#1d3566;
  --edge:rgba(90,175,255,.28);
  --navy:#0f2a66;
  --blue:#2b6be0;
  --cyan:#27c4f5;
  --ink:#031427;
  --blue-text:#8fd0ff;
  --fg:#f0f5ff;
  --muted:#9db0d0;
  --ok:#43c183;
  --warn:#e3ae45;
  --bad:#ea6258;
  --glass:linear-gradient(160deg,rgba(43,107,224,.30),rgba(15,42,102,.15) 55%,rgba(8,16,38,.88));
  --glow:inset 0 1px 0 rgba(255,255,255,.07),0 0 28px rgba(43,140,255,.09);
  --f-display:"Exo 2","Trebuchet MS",system-ui,sans-serif;
  --f-body:"Source Sans 3",system-ui,-apple-system,"Segoe UI",sans-serif;
  --f-mono:"IBM Plex Mono",ui-monospace,Menlo,monospace;
  color-scheme:dark;
}
*{box-sizing:border-box}
html{background:var(--bg)}
body{background-color:var(--bg);background-image:radial-gradient(1100px 560px at 75% -8%,#132c70 0%,transparent 62%),radial-gradient(800px 500px at 0% 100%,#0b1d4a 0%,transparent 60%);color:var(--fg);font:400 16px/1.55 var(--f-body);-webkit-text-size-adjust:100%}
body.vfy{background-color:var(--black);background-image:none}
body::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);z-index:60;background:var(--bg)}
body.vfy::before{background:var(--black)}
h1,h2,h3{margin:0;font-family:var(--f-display);letter-spacing:-.005em;text-wrap:balance;line-height:1.05}
p{margin:0}
a{color:var(--blue-text)}
.mono{font-family:var(--f-mono);font-weight:500}
:focus-visible{outline:2px solid var(--cyan);outline-offset:2px}
button,input,select,textarea{font:inherit;color:inherit}
.kick{font:700 11px var(--f-body);letter-spacing:.22em;text-transform:uppercase;color:var(--cyan)}

/* shared card surface */
.panel,.unit,.rk,.rank,.tile,.banner,.hero2,.hh,.post,.stat,details{border:1px solid var(--edge);border-radius:14px;background:var(--glass);box-shadow:var(--glow)}

/* shell */
.shell{display:grid;grid-template-columns:272px minmax(0,1fr);min-height:100vh}
.side{position:sticky;top:0;height:100vh;display:flex;flex-direction:column;background:linear-gradient(180deg,rgba(11,24,58,.96),rgba(6,12,28,.98));border-right:1px solid var(--line)}
.brand{display:flex;align-items:center;gap:12px;text-decoration:none;color:var(--fg);padding:20px 14px 18px max(16px,env(safe-area-inset-left,0px));border-bottom:1px solid var(--line)}
.brand svg{width:40px;height:45px;flex:none;filter:drop-shadow(0 0 10px rgba(39,196,245,.45))}
.brand b{font:800 13px/1.1 var(--f-display);letter-spacing:.04em;display:block;text-transform:uppercase}
.brand small{display:block;color:var(--cyan);font:700 11px var(--f-body);letter-spacing:.16em;text-transform:uppercase;margin-top:4px}
.nav{flex:1;overflow:auto;display:flex;flex-direction:column;gap:3px;padding:6px 12px 10px max(12px,env(safe-area-inset-left,0px))}
.nav h4{margin:16px 6px 6px;font:700 11px var(--f-body);letter-spacing:.2em;text-transform:uppercase;color:#5f78a8}
.nav a{display:flex;align-items:center;gap:12px;padding:10px 12px;border-radius:10px;color:#dbe6fb;text-decoration:none;font-weight:600;border:1px solid transparent}
.nav a:hover{background:rgba(80,150,255,.10)}
.nav a[aria-current="page"]{background:linear-gradient(90deg,rgba(39,196,245,.24),rgba(43,107,224,.12));border-color:rgba(39,196,245,.4);color:#fff}
.nav a[aria-current="page"]::after{content:"›";margin-left:auto;color:var(--cyan);font-weight:900}
.ni{width:20px;height:20px;flex:none;fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;stroke-linejoin:round}
.side-foot{padding:12px 12px 16px max(12px,env(safe-area-inset-left,0px));border-top:1px solid var(--line);display:grid;gap:10px}
.side-foot .two{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.me{display:flex;align-items:center;gap:12px;padding:10px 12px;border-radius:12px;border:1px solid var(--edge);background:var(--glass);text-decoration:none;color:var(--fg)}
.av{width:38px;height:38px;border-radius:10px;flex:none;display:grid;place-items:center;background:linear-gradient(145deg,#bfe6ff,#4aa8ff);color:var(--ink);font:900 18px var(--f-display);text-transform:uppercase}
.mt{display:grid;min-width:0;flex:1}
.mt b{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.mt small{color:var(--muted);font-size:12px}
.gt{color:var(--muted)}
.scrim{display:none}
.main{min-width:0}
.head{position:sticky;top:env(safe-area-inset-top,0px);z-index:40;background:rgba(6,11,26,.86);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);border-bottom:1px solid var(--line);padding:14px max(16px,env(safe-area-inset-right,0px)) 14px max(16px,env(safe-area-inset-left,0px))}
.head-in{max-width:1040px;margin-inline:auto;display:flex;align-items:center;gap:12px}
.head h2{font-size:clamp(22px,4vw,34px);font-weight:900;text-transform:uppercase;letter-spacing:.01em;margin-top:2px}
.head .ttl{flex:1;min-width:0}
.menu{display:none;min-height:42px;padding:8px 12px;border:1px solid var(--edge);border-radius:10px;background:var(--glass);font-weight:700;cursor:pointer}
.live{display:inline-flex;align-items:center;gap:8px;font:700 11px var(--f-body);letter-spacing:.16em;text-transform:uppercase;color:var(--blue-text)}
.live::before{content:"";width:7px;height:7px;border-radius:50%;background:var(--cyan);box-shadow:0 0 8px var(--cyan)}
.outer{padding:26px max(16px,env(safe-area-inset-right,0px)) 0 max(16px,env(safe-area-inset-left,0px))}
.wrap{max-width:1040px;margin-inline:auto;display:flex;flex-direction:column;gap:24px;min-height:calc(100vh - 110px)}
.view{display:flex;flex-direction:column;gap:22px;animation:in .28s ease-out}
@keyframes in{from{opacity:.2;transform:translateY(6px)}to{opacity:1;transform:none}}
.foot{margin-top:auto;padding-block:24px 34px;border-top:1px solid var(--line);color:#6f87b6;font:700 12px var(--f-body);letter-spacing:.2em;text-transform:uppercase}
.vh h1{font-size:clamp(30px,5vw,46px);font-weight:900}
.vh p{color:var(--muted);max-width:62ch;margin-top:10px}

/* buttons */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:11px 18px;border:1px solid rgba(120,190,255,.38);border-radius:10px;background:rgba(120,190,255,.16);font:800 12.5px var(--f-body);letter-spacing:.1em;text-transform:uppercase;text-decoration:none;color:#fff;cursor:pointer;min-height:44px}
.btn:hover{background:rgba(120,190,255,.28)}
.btn.primary{background:var(--cyan);border-color:var(--cyan);color:var(--ink);box-shadow:0 0 22px rgba(39,196,245,.35)}
.btn.primary:hover{background:#5ad4fb}
.btn.out{background:transparent;border:1.5px solid var(--cyan);color:#fff}
.btn.out:hover{background:rgba(39,196,245,.16)}
.btn.sm{padding:7px 12px;font-size:11.5px;min-height:36px}
.btn[disabled]{opacity:.4;cursor:not-allowed}
.btn.danger:hover{border-color:var(--bad);color:var(--bad);background:transparent}
.chip{display:inline-flex;align-items:center;gap:6px;font:800 11px var(--f-body);letter-spacing:.12em;text-transform:uppercase;padding:4px 9px;border-radius:6px;border:1px solid var(--line);width:max-content}
.chip.ok{color:var(--ok);border-color:rgba(67,193,131,.45);background:rgba(67,193,131,.09)}
.chip.no{color:var(--warn);border-color:rgba(227,174,69,.45);background:rgba(227,174,69,.09)}
.chip.ex{color:var(--blue-text);border-color:rgba(143,208,255,.4)}

/* home */
.banner{display:flex;align-items:center;gap:16px;flex-wrap:wrap;padding:16px 18px}
.bi{width:50px;height:50px;border-radius:12px;flex:none;display:grid;place-items:center;background:linear-gradient(145deg,#6fe0ff,#1d8fe8);box-shadow:0 0 20px rgba(39,196,245,.45)}
.bi svg{width:24px;height:24px}
.banner .bt{flex:1 1 260px;display:grid;gap:3px;min-width:0}
.banner .bt b{font:900 22px/1.1 var(--f-display)}
.banner .bt span:last-child{color:var(--muted);font-size:14.5px}
.hero2{position:relative;overflow:hidden;padding:clamp(24px,4vw,40px);display:grid;gap:18px;border-color:rgba(39,196,245,.5);background:radial-gradient(700px 300px at 88% 60%,rgba(60,160,255,.28),transparent 65%),linear-gradient(160deg,#0f2a66 0%,#0a1630 58%,#070d1b 100%)}
.hero2>*:not(.bigshield){position:relative;z-index:1}
.hero2 h1{font-size:clamp(38px,8vw,68px);font-weight:900;line-height:1}
.hero2 p{color:#c8d6f0;max-width:52ch}
.bigshield{position:absolute;right:clamp(-20px,2vw,28px);bottom:-26px;width:clamp(120px,26vw,240px);height:auto;filter:drop-shadow(0 0 26px rgba(76,201,255,.55));opacity:.9;z-index:0}
.cta{display:flex;flex-wrap:wrap;gap:10px}
.tiles{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,270px),1fr));gap:14px}
.tile{display:grid;grid-template-columns:auto minmax(0,1fr) auto;gap:2px 14px;align-items:center;padding:16px;text-decoration:none;color:var(--fg)}
.tile:hover{border-color:var(--cyan)}
.ti{grid-row:1/3;width:46px;height:46px;border-radius:12px;display:grid;place-items:center;background:rgba(160,210,255,.16);border:1px solid rgba(160,210,255,.3)}
.ti svg{width:24px;height:24px;fill:none;stroke:#fff;stroke-width:2;stroke-linecap:round;stroke-linejoin:round}
.tile b{font:800 15px var(--f-display);text-transform:uppercase;letter-spacing:.04em}
.tile small{color:var(--muted);font-size:13px;grid-column:2}
.tg{grid-row:1/3;grid-column:3;font:800 11px var(--f-body);letter-spacing:.14em;text-transform:uppercase;color:var(--blue-text);align-self:start}
.sec-head{display:flex;align-items:end;justify-content:space-between;gap:8px 14px;flex-wrap:wrap}
.sec-head h2{font-size:clamp(24px,4vw,32px);font-weight:900;margin-top:4px}
.sec-head a{font:800 12px var(--f-body);letter-spacing:.12em;text-transform:uppercase;text-decoration:none}
.cols{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,320px),1fr));gap:16px}
.post{padding:18px;display:grid;gap:8px;align-content:start;min-width:0}
.post .kick{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.post b{font:800 19px/1.2 var(--f-display)}
.post p{color:var(--muted);font-size:15px}
.date{font:500 12px var(--f-mono);color:var(--blue-text)}
.empty{color:var(--muted);font-style:italic}

/* generic blocks */
.panel{padding:20px;display:flex;flex-direction:column;gap:14px;min-width:0}
.panel>h2{font-size:24px;font-weight:800}
.list{list-style:none;margin:0;padding:0;display:flex;flex-direction:column}
.list li{padding:14px 0;border-top:1px solid var(--line);display:grid;gap:4px}
.list li:first-child{border-top:0;padding-top:2px}
.list b{font-weight:700}
.list p{color:var(--muted);font-size:15px}

/* hierarchy */
.hh{padding:clamp(20px,4vw,36px);display:flex;gap:20px;align-items:center;justify-content:space-between;flex-wrap:wrap;border-color:rgba(39,196,245,.5);background:radial-gradient(700px 320px at 92% 50%,rgba(60,160,255,.30),transparent 62%),linear-gradient(160deg,#0f2a66 0%,#0a1630 55%,#070d1b 100%)}
.hh .tx{flex:1 1 300px;display:grid;gap:12px;min-width:0}
.hh h1{font-size:clamp(32px,6vw,56px);font-weight:900}
.hh p{color:#c8d6f0;max-width:52ch}
.hh svg{width:clamp(84px,16vw,130px);height:auto;filter:drop-shadow(0 0 22px rgba(76,201,255,.55))}
.stats{display:flex;gap:10px;flex-wrap:wrap;margin-top:4px}
.stat{padding:8px 14px;display:grid;background:rgba(8,18,44,.7)}
.stat b{font:900 28px/1 var(--f-display)}
.stat span{font:700 11px var(--f-body);letter-spacing:.16em;text-transform:uppercase;color:var(--muted)}
.rg{display:flex;flex-direction:column;gap:14px}
.rg-head{display:flex;align-items:end;justify-content:space-between;gap:6px 14px;flex-wrap:wrap}
.rg-head h2{font-size:clamp(26px,4vw,34px);font-weight:900}
.rg-head span{font:700 12px var(--f-body);letter-spacing:.16em;text-transform:uppercase;color:var(--cyan)}
.rk-grid{list-style:none;margin:0;padding:0;display:grid;grid-template-columns:repeat(auto-fill,minmax(min(100%,250px),1fr));gap:12px}
.rk{display:grid;grid-template-columns:auto minmax(0,1fr);gap:2px 14px;align-items:center;padding:14px}
.rk .ic{grid-row:1/3;width:50px;height:50px;border-radius:12px;display:grid;place-items:center;background:linear-gradient(145deg,#6fe0ff,#2b6be0);box-shadow:0 0 18px rgba(76,201,255,.45)}
.rk .ic svg{width:26px;height:26px}
.rk .nm{font:800 18px/1.1 var(--f-display);overflow-wrap:anywhere}
.rk .pos{font:500 12px var(--f-mono);color:var(--cyan)}
.rk.elite{border-color:#fff;background:linear-gradient(160deg,#2b6be0,#0f2a66 70%);box-shadow:0 0 34px rgba(76,201,255,.4),inset 0 1px 0 rgba(255,255,255,.25)}
.rk.elite .ic{background:#fff;box-shadow:0 0 22px rgba(255,255,255,.55)}
.ranks{list-style:none;margin:0;padding:0;display:grid;grid-template-columns:repeat(auto-fill,minmax(min(100%,210px),1fr));gap:10px}
.rank{padding:10px 14px;display:grid;grid-template-columns:auto 1fr;gap:4px 12px;align-items:baseline}
.rank .n{color:var(--cyan);font-size:13px}
.rank .nm{font:800 16px/1.1 var(--f-display)}

/* discord prompt */
.dcm{position:fixed;inset:0;z-index:90;display:grid;place-items:center;padding:max(16px,env(safe-area-inset-top,0px)) max(16px,env(safe-area-inset-right,0px)) max(16px,env(safe-area-inset-bottom,0px)) max(16px,env(safe-area-inset-left,0px));background:rgba(0,4,14,.78);backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px)}
.dcm-box{width:100%;max-width:440px;border:1px solid rgba(39,196,245,.5);border-radius:16px;padding:26px;display:grid;gap:14px;background:radial-gradient(500px 240px at 90% 0%,rgba(60,160,255,.28),transparent 65%),linear-gradient(160deg,#0f2a66 0%,#0a1630 60%,#070d1b 100%);box-shadow:0 0 50px rgba(43,140,255,.25)}
.dcm-box h2{font-size:clamp(28px,7vw,38px);font-weight:900}
.dcm-box p{color:#c8d6f0}
.dcm-box .cta .btn{flex:1 1 140px}

/* shop */
.shop{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,260px),1fr));gap:14px}
.item{border:1px solid var(--edge);border-radius:14px;background:var(--glass);box-shadow:var(--glow);padding:16px;display:grid;gap:10px;align-content:start;min-width:0}
.item .ic{width:50px;height:50px;border-radius:12px;display:grid;place-items:center;background:linear-gradient(145deg,#6fe0ff,#2b6be0);box-shadow:0 0 18px rgba(76,201,255,.45)}
.item .ic svg{width:26px;height:26px}
.item b{font:800 19px/1.15 var(--f-display)}
.item p{color:var(--muted);font-size:15px}
.item .pr{display:flex;align-items:center;justify-content:space-between;gap:10px;flex-wrap:wrap;margin-top:4px}
.item .pr strong{font:900 22px var(--f-display);color:var(--cyan)}

.vals{list-style:none;margin:0;padding:0;display:grid}
.vals li{display:flex;justify-content:space-between;gap:14px;padding:11px 0;border-top:1px solid var(--line);font-weight:600}
.vals li:first-child{border-top:0}
.vals li.no,.vals li.no strong{color:var(--bad)}
.vals li.no strong{font-size:15px;text-transform:uppercase;letter-spacing:.06em}
.vals strong{font:900 20px var(--f-display);color:var(--cyan);font-variant-numeric:tabular-nums}

.shop-foot{flex-direction:row;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px}
.shop-foot h2{font-size:26px;font-weight:800;margin-top:4px}
.toast{position:fixed;left:50%;bottom:max(20px,env(safe-area-inset-bottom,0px));transform:translateX(-50%);z-index:95;max-width:min(92vw,420px);padding:14px 18px;border-radius:12px;border:1px solid var(--cyan);background:#0a1630;color:#fff;font-weight:700;box-shadow:0 0 30px rgba(39,196,245,.35)}

/* units */
.units{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,300px),1fr));gap:14px;align-items:start}
.ubtn{background:none;border:0;padding:0;margin:0;text-align:left;color:inherit;cursor:pointer;display:grid;gap:6px;width:100%}
.ubtn b{font:900 46px/.95 var(--f-display);letter-spacing:.03em}
.ubtn span:not(.uc){color:var(--muted);font-weight:600}
.ubtn .uc{font:800 12px var(--f-body);letter-spacing:.14em;text-transform:uppercase;color:var(--cyan)}
.ubtn[aria-expanded="true"] .uc{color:var(--blue-text)}
.roles{margin-top:14px}
.roles li{justify-content:flex-start}
.unit{padding:20px;display:grid;gap:6px}
.unit b{font:900 46px/.95 var(--f-display);letter-spacing:.03em}
.unit span{color:var(--muted);font-weight:600}

/* forms */
.form{display:grid;gap:14px;max-width:560px}
.field{display:grid;gap:6px}
.field label{font:700 12px var(--f-body);letter-spacing:.14em;text-transform:uppercase;color:var(--muted)}
.field input,.field textarea,.field select{background:rgba(4,10,26,.75);border:1px solid var(--line);border-radius:10px;padding:11px 12px;min-height:44px;width:100%}
.field textarea{min-height:96px;resize:vertical}
.field input:focus,.field textarea:focus,.field select:focus{border-color:var(--cyan);outline:none;box-shadow:0 0 0 2px rgba(39,196,245,.35)}
.msg{font-weight:600}
.msg.err{color:var(--bad)}
.msg.good{color:var(--ok)}
.note{border:1px dashed var(--line);border-radius:10px;padding:10px 12px;color:var(--muted);font-size:14px}

/* rules */
details summary{cursor:pointer;padding:14px 16px;font:700 17px var(--f-display);list-style:none;display:flex;justify-content:space-between;gap:12px}
details summary::-webkit-details-marker{display:none}
details summary::after{content:"+";color:var(--cyan);font-family:var(--f-mono)}
details[open] summary::after{content:"–"}
details p{padding:0 16px 16px;color:var(--muted);max-width:66ch}

/* record */
.record{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,420px),1fr));gap:18px;align-items:start}
.dl{display:grid;grid-template-columns:minmax(110px,170px) minmax(0,1fr);gap:0}
.dl dt,.dl dd{margin:0;padding:12px 0;border-top:1px solid var(--line)}
.dl dt:first-of-type,.dl dd:first-of-type{border-top:0}
.dl dt{font:700 12px var(--f-body);letter-spacing:.14em;text-transform:uppercase;color:var(--muted);padding-right:10px}
.dl dd{font-weight:600;overflow-wrap:anywhere}
.timeline{list-style:none;margin:0;padding:0;display:grid}
.timeline li{display:grid;grid-template-columns:auto 1fr;gap:14px;padding:10px 0;border-top:1px solid var(--line)}
.timeline li:first-child{border-top:0}
.profile-head{display:flex;gap:16px;align-items:center;flex-wrap:wrap}
.avatar{width:64px;height:64px;border-radius:14px;background:linear-gradient(145deg,#bfe6ff,#4aa8ff);color:var(--ink);display:grid;place-items:center;font:900 30px var(--f-display);text-transform:uppercase}

/* admin */
.tabs{display:flex;gap:6px;flex-wrap:wrap}
.tab{padding:9px 14px;border:1px solid var(--edge);border-radius:10px;background:var(--glass);cursor:pointer;font-weight:700;min-height:40px}
.tab[aria-pressed="true"]{background:linear-gradient(90deg,rgba(39,196,245,.28),rgba(43,107,224,.18));border-color:var(--cyan)}
.rows{display:flex;flex-direction:column}
.row{display:flex;flex-wrap:wrap;gap:10px 16px;align-items:center;padding:12px 0;border-top:1px solid var(--line)}
.row:first-child{border-top:0}
.row .grow{flex:1 1 200px;min-width:0;display:grid;gap:2px}
.row .grow b{overflow-wrap:anywhere}
.row .grow small{color:var(--muted)}
.row select{background:rgba(4,10,26,.75);border:1px solid var(--line);border-radius:8px;padding:7px 8px;min-height:36px;max-width:100%}
.row .btns{display:flex;gap:6px;flex-wrap:wrap}
.inline-form{display:flex;flex-wrap:wrap;gap:10px;align-items:end;border-top:1px solid var(--line);padding-top:16px}
.inline-form .field{flex:1 1 180px}

/* verification, pure black */
#vfy{min-height:100vh;background:var(--black);display:grid;place-items:center;padding:max(24px,env(safe-area-inset-top,0px)) max(16px,env(safe-area-inset-right,0px)) 40px max(16px,env(safe-area-inset-left,0px))}
.vbox{width:100%;max-width:560px;display:flex;flex-direction:column;gap:22px;align-items:flex-start}
.vbox svg.lg{width:64px;height:72px;filter:drop-shadow(0 0 14px rgba(39,196,245,.5))}
.vt{font:900 clamp(34px,10vw,76px)/1 var(--f-display);letter-spacing:-.01em;margin:0;text-wrap:balance}
.vt.ok{color:var(--ok)}
.vs{color:var(--muted);max-width:46ch}
.vopts{display:grid;gap:10px;width:100%}
.opt{display:grid;gap:4px;text-align:left;padding:16px;border:1px solid var(--line);border-radius:12px;background:#05070c;cursor:pointer;width:100%;box-shadow:none}
.opt b{font:800 19px var(--f-display)}
.opt span{color:var(--muted);font-size:14px}
.opt:hover{border-color:var(--cyan);background:var(--surface)}
.steps{list-style:none;margin:0;padding:0;display:flex;gap:6px;width:100%}
.steps li{flex:1;border-top:3px solid var(--line);padding-top:6px;font:700 11px var(--f-body);letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
.steps li.done{border-color:var(--blue);color:var(--fg)}
.steps li.now{border-color:var(--cyan);color:var(--cyan)}
.bot{width:100%;border:1px solid var(--line);border-radius:12px;background:#05070c;padding:16px;display:grid;gap:8px}
.bot .hd{font:800 13px var(--f-body);letter-spacing:.16em;text-transform:uppercase;color:var(--cyan)}
.codebox{display:flex;gap:10px;align-items:center;flex-wrap:wrap;border:1px solid var(--cyan);border-radius:10px;background:var(--surface);padding:12px;width:100%}
.codebox code{flex:1 1 200px;font:500 15px var(--f-mono);overflow-wrap:anywhere;user-select:all}
.demo{width:100%;border:1px dashed rgba(227,174,69,.5);color:var(--warn);border-radius:10px;padding:9px 12px;font-size:13px;font-weight:600}
.chk{list-style:none;margin:0;padding:0;display:grid;gap:8px;width:100%}
.chk li{display:flex;gap:10px;color:var(--muted)}
.chk li::before{content:"";width:10px;height:10px;margin-top:7px;border:1px solid var(--line);border-radius:50%;flex:none}
.chk li.on{color:var(--fg)}
.chk li.on::before{background:var(--cyan);border-color:var(--cyan)}
.bar{width:100%;height:4px;background:var(--surface-2)}
.bar i{display:block;height:100%;background:var(--cyan);transition:width 1.1s linear}
.back{color:var(--muted);font-size:14px}

@media (max-width:899px){
  .shell{display:block}
  .menu{display:inline-flex;align-items:center}
  .side{position:fixed;inset:0 auto 0 0;width:min(310px,86vw);height:100%;z-index:70;transform:translateX(-104%);transition:transform .22s ease;padding-top:env(safe-area-inset-top,0px)}
  .side.open{transform:none}
  .scrim.show{display:block;position:fixed;inset:0;z-index:65;background:rgba(0,0,0,.62)}
  .outer{padding-top:20px}
  .wrap{min-height:calc(100vh - 90px)}
  .dl{grid-template-columns:1fr}
  .dl dt{padding-bottom:0;border-top:1px solid var(--line)}
  .dl dd{border-top:0;padding-top:2px}
}
@media (max-width:560px){.head .live{display:none}}
@media (prefers-reduced-motion:reduce){
  .view{animation:none}
  .side{transition:none}
  .bar i{transition:none}
}
</style>

<svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
  <symbol id="logo" viewBox="0 0 64 72">
    <path d="M32 2 L60 12 V36 C60 54 48 65 32 70 C16 65 4 54 4 36 V12 Z" fill="#0f2a66" stroke="#8fd0ff" stroke-width="2.5" stroke-linejoin="round"/>
    <polygon points="32,16 33.9,21.4 39.6,21.5 35,25 36.7,30.5 32,27.2 27.3,30.5 29,25 24.4,21.5 30.1,21.4" fill="#ffffff"/>
    <text x="32" y="50" text-anchor="middle" font-family="Exo 2, Trebuchet MS, sans-serif" font-weight="900" font-size="16" letter-spacing="1" fill="#ffffff">EBC</text>
    <path d="M18 57 L32 62 L46 57" fill="none" stroke="#8fd0ff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
  </symbol>
</svg>

<div class="shell" id="shell">
  <aside class="side" id="side" aria-label="Menu lateral">
    <a class="brand" href="#inicio">
      <svg viewBox="0 0 64 72" role="img" aria-label="Logo do EBC"><use href="#logo"/></svg>
      <span><b>Exército Brasileiro</b><small>de Combate · EBC</small></span>
    </a>
    <nav class="nav" id="nav">
      <h4>Quartel General</h4>
      <a href="#inicio" data-v="inicio"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M3 11l9-8 9 8M5 10v10h14V10"/></svg>Início</a>
      <a href="#sobre" data-v="sobre"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l8 3v6c0 5-3.500 8-8 9-4.500-1-8-4-8-9V6z"/></svg>Sobre o EBC</a>
      <a href="#noticias" data-v="noticias"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M4 5h13v14H6a2 2 0 0 1-2-2zM17 9h3v8a2 2 0 0 1-2 2M7 9h7M7 13h7"/></svg>Notícias</a>
      <h4>Consulta</h4>
      <a href="#hierarquia" data-v="hierarquia"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l9 5-9 5-9-5zM3 13l9 5 9-5"/></svg>Hierarquia</a>
      <a href="#unidades" data-v="unidades"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M5 5l9 9M19 5l-9 9M4 20l4-4M20 20l-4-4"/></svg>Unidades</a>
      <a href="#regulamentos" data-v="regulamentos"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M5 4h14v16H5zM9 9h6M9 13h6M9 17h3"/></svg>Regulamentos</a>
      <h4>Acesso</h4>
      <a href="#alistamento" data-v="alistamento"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><circle cx="10" cy="8" r="3.500"/><path d="M3 20c0-4 3.500-6 7-6s7 2 7 6M19 8v6M16 11h6"/></svg>Alistamento</a>
      <a href="#verificacao" data-v="verificacao"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l8 3v6c0 5-3.500 8-8 9-4.500-1-8-4-8-9V6zM8.500 12l2.500 2.500 4.500-5"/></svg>Verificação</a>
      <a href="#militar" data-v="militar"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><polygon points="12,2 14.350,8.760 21.510,8.910 15.800,13.240 17.880,20.090 12,16 6.120,20.090 8.200,13.240 2.490,8.910 9.650,8.760"/></svg>Área do Militar</a>
      <a href="#perfil" data-v="perfil"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="8" r="4"/><path d="M4 21c0-4.500 3.500-7 8-7s8 2.500 8 7"/></svg>Perfil</a>
      <h4>Loja</h4>
      <a href="#compras" data-v="compras"><svg class="ni" viewBox="0 0 24 24" aria-hidden="true"><path d="M5 8h14l-1 12H6zM9 8V6a3 3 0 0 1 6 0v2"/></svg>Compras</a>
    </nav>
    <div class="side-foot">
      <div class="two">
        <a class="btn sm lnk-discord" href="https://discord.com" target="_blank" rel="noopener">Discord ↗</a>
        <a class="btn sm lnk-roblox" href="https://www.roblox.com" target="_blank" rel="noopener">Roblox ↗</a>
      </div>
      <a class="me" id="me" href="#perfil"></a>
    </div>
  </aside>
  <div class="scrim" id="scrim"></div>

  <div class="main">
    <header class="head">
      <div class="head-in">
        <button class="menu" id="menu" type="button" aria-expanded="false" aria-controls="side">Menu</button>
        <div class="ttl"><span class="kick">Centro de operações</span><h2>Quartel General</h2></div>
        <span class="live">Portal EBC</span>
        <a class="btn sm out" id="hd-verify" href="#verificacao">✓ Verificar</a>
      </div>
    </header>

    <div class="outer"><div class="wrap">
      <!-- INÍCIO -->
      <section class="view" data-view="inicio">
        <div class="banner">
          <span class="bi"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 2l2.200 7.800L22 12l-7.800 2.200L12 22l-2.200-7.800L2 12l7.800-2.200z" fill="#031427"/></svg></span>
          <div class="bt"><span class="kick">Portal oficial do jogo</span><b>Seu quartel começa aqui</b><span>Acesse a verificação, conheça as unidades e acompanhe as informações da comunidade.</span></div>
          <a class="btn primary" href="#sobre">Explorar ↗</a>
        </div>
        <div class="hero2">
          <svg class="bigshield" viewBox="0 0 100 112" aria-hidden="true"><path d="M50 4 L94 19 V56 C94 84 76 100 50 108 C24 100 6 84 6 56 V19 Z" fill="rgba(76,201,255,.10)" stroke="#6cc8ff" stroke-width="3" stroke-linejoin="round"/><polygon points="50,28 56.2,45.5 74.7,46 60,57.2 65.3,75 50,64.5 34.7,75 40,57.2 25.3,46 43.8,45.5" fill="#cfe9ff"/></svg>
          <span class="kick">Bem-vindo ao quartel</span>
          <h1 id="home-title">Olá, Militar</h1>
          <p>Este é o painel central do Exército Brasileiro de Combate. Prepare-se para a missão, confira as informações e entre no jogo.</p>
          <div class="cta">
            <a class="btn lnk-roblox" href="https://www.roblox.com" target="_blank" rel="noopener">Entrar no jogo ↗</a>
            <a class="btn out" href="#verificacao">✓ Verificar conta ↗</a>
          </div>
        </div>
        <div class="tiles">
          <a class="tile" href="#verificacao"><span class="ti"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l8 3v6c0 5-3.500 8-8 9-4.500-1-8-4-8-9V6zM8.500 12l2.500 2.500 4.500-5"/></svg></span><b>Verificação</b><small>Discord + Roblox</small><span class="tg">Acessar</span></a>
          <a class="tile" href="#unidades"><span class="ti"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M5 5l9 9M19 5l-9 9M4 20l4-4M20 20l-4-4"/></svg></span><b id="tile-units">6 unidades</b><small>Conheça as unidades</small><span class="tg">EBC</span></a>
          <a class="tile" href="#hierarquia"><span class="ti"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l9 5-9 5-9-5zM3 13l9 5 9-5"/></svg></span><b>Hierarquia</b><small>Praças e oficiais</small><span class="tg">Consultar</span></a>
        </div>
        <div class="sec-head"><div><span class="kick">Fique por dentro</span><h2>Comunicados do quartel</h2></div><a href="#regulamentos">Regulamentos ↗</a></div>
        <div class="cols" id="home-posts"></div>
      </section>

      <!-- SOBRE -->
      <section class="view" data-view="sobre" hidden>
        <div class="vh"><h1>Sobre o EBC</h1><p>O Exército Brasileiro de Combate é uma comunidade militar no Roblox, organizada por patentes, unidades especiais e regulamentos próprios.</p></div>
        <div class="cols">
          <div class="panel"><h2>Disciplina</h2><p>Cada militar cumpre ordens, horários e regulamentos. A organização é o que mantém as operações funcionando.</p></div>
          <div class="panel"><h2>Honra</h2><p>A patente se conquista em serviço. Promoções ficam registradas no histórico de cada militar.</p></div>
          <div class="panel"><h2>Lealdade</h2><p>Compromisso com a unidade, com os colegas e com o comando, dentro e fora das operações.</p></div>
        </div>
        <div class="panel">
          <h2>Objetivo do site</h2>
          <p>Reunir em um só lugar a verificação dos militares, a hierarquia, as unidades especiais, e a Área do Militar, com integração segura com o Roblox.</p>
        </div>
      </section>

      <!-- HIERARQUIA -->
      <section class="view" data-view="hierarquia" hidden>
        <div class="hh">
          <div class="tx">
            <span class="kick">Consulta</span>
            <h1>Hierarquia oficial</h1>
            <p>Praças e oficiais do EBC, do menor ao maior. O número é a posição na cadeia de comando.</p>
            <div class="stats" id="rank-stats"></div>
          </div>
          <svg viewBox="0 0 64 72" role="img" aria-label="Escudo do EBC"><use href="#logo"/></svg>
        </div>
        <div id="rank-groups" style="display:flex;flex-direction:column;gap:30px"></div>
      </section>

      <!-- UNIDADES -->
      <section class="view" data-view="unidades" hidden>
        <div class="vh"><h1>Unidades especiais</h1><p>Cada unidade tem uma função própria dentro do EBC. Militares são transferidos pelo comando.</p></div>
        <div class="units" id="unit-grid"></div>
      </section>

      <!-- ALISTAMENTO -->
      <section class="view" data-view="alistamento" hidden>
        <div class="vh"><h1>Alistamento</h1><p>Preencha o formulário para entrar no EBC. Todo recruta começa na patente mais baixa e precisa se verificar.</p></div>
        <form class="panel form" id="enlist-form" novalidate>
          <div class="field"><label for="al-user">Usuário Roblox</label><input id="al-user" autocomplete="off" placeholder="SeuUsuario"></div>
          <div class="field"><label for="al-dc">Usuário Discord</label><input id="al-dc" autocomplete="off" placeholder="seu_usuario"></div>
          <div class="field"><label for="al-msg">Por que quer entrar?</label><textarea id="al-msg" placeholder="Conte em poucas linhas."></textarea></div>
          <div><button class="btn primary" type="submit">Enviar alistamento</button></div>
          <p class="msg" id="al-msg-out" role="status"></p>
        </form>
      </section>

      <!-- REGULAMENTOS -->
      <section class="view" data-view="regulamentos" hidden>
        <div class="vh"><h1>Regulamentos</h1><p>Regras gerais válidas para todos os militares, de qualquer patente.</p></div>
        <div style="display:grid;gap:10px">
          <details open><summary>Art. 1 · Hierarquia e respeito</summary><p>Ordens de patente superior devem ser cumpridas durante atividades oficiais. Desrespeito a qualquer militar é infração.</p></details>
          <details><summary>Art. 2 · Verificação</summary><p>Todo militar mantém a conta verificada. A verificação pela bio do perfil Roblox é o método aceito pelo EBC.</p></details>
          <details><summary>Art. 3 · Segurança da conta</summary><p>O EBC nunca pede senha, cookie ou código de login da Roblox. Quem pedir isso deve ser denunciado ao comando.</p></details>
          <details><summary>Art. 4 · Conduta em serviço</summary><p>Sem spam, sem exploits e sem trapaça em treinamentos e operações. Quem infringir pode ser rebaixado ou desligado.</p></details>
          <details><summary>Art. 5 · Identificação</summary><p>Use o nome de usuário verificado e mantenha a patente atual visível durante as atividades.</p></details>
          <details><summary>Art. 6 · Promoções e rebaixamentos</summary><p>São decididos pelo comando e registrados no histórico do militar.</p></details>
        </div>
      </section>

      <!-- NOTÍCIAS -->
      <section class="view" data-view="noticias" hidden>
        <div class="vh"><h1>Notícias do Exército</h1><p>Comunicados e novidades do EBC.</p></div>
        <div class="cols" id="news-full"></div>
      </section>

      <!-- ÁREA DO MILITAR -->
      <section class="view" data-view="militar" hidden>
        <div class="vh"><h1>Área do Militar</h1><p id="mil-sub"></p></div>
        <div class="record" id="mil-record"></div>
      </section>

      <!-- PERFIL -->
      <section class="view" data-view="perfil" hidden>
        <div class="vh"><h1>Perfil</h1></div>
        <div class="panel" id="perfil-box"></div>
      </section>

      <!-- COMPRAS -->
      <section class="view" data-view="compras" hidden>
        <div class="hh">
          <div class="tx">
            <span class="kick">Loja</span>
            <h1>Compras</h1>
            <p>Itens e vantagens do EBC.</p>
          </div>
          <svg viewBox="0 0 64 72" role="img" aria-label="Escudo do EBC"><use href="#logo"/></svg>
        </div>
        <div class="shop" id="shop-grid"></div>
        <div class="panel shop-foot">
          <div><span class="kick">Como comprar</span><h2>Compre pelo Discord</h2><p class="vs" style="margin-top:6px">Entre no Discord do EBC e vá em compras.</p></div>
          <a class="btn primary buy-dc" href="https://discord.gg/zcvNBgw2S" target="_blank" rel="noopener">Entrar no Discord ↗</a>
        </div>
        <div class="toast" id="toast" role="status" aria-live="polite" hidden>Vá em compras no Discord para comprar.</div>
      </section>

      <footer class="foot">EBC — Disciplina, Honra e Lealdade.</footer>
    </div></div>
  </div>
</div>

<!-- DISCORD -->
<div class="dcm" id="dcm" role="dialog" aria-modal="true" aria-labelledby="dcm-t" hidden>
  <div class="dcm-box">
    <span class="kick">Comunidade EBC</span>
    <h2 id="dcm-t">Entre no Discord</h2>
    <p>O Discord oficial do EBC tem avisos, treinamentos e o suporte da verificação.</p>
    <div class="cta">
      <a class="btn primary" id="dcm-yes" href="https://discord.gg/zcvNBgw2S" target="_blank" rel="noopener">Entrar</a>
      <button class="btn" id="dcm-no" type="button">Sair</button>
    </div>
  </div>
</div>

<!-- VERIFICAÇÃO -->
<section id="vfy" hidden aria-live="polite">
  <div class="vbox" id="vfy-stage"></div>
</section>

<script>
(function(){
'use strict';
/* Opcional: endereço do Worker de verificacao-worker.js. Vazio = o site consulta o Roblox direto. */
var API_URL='';
var LINKS={discord:'https://discord.gg/zcvNBgw2S',roblox:'https://www.roblox.com'};
var KEY='ebc-portal-v1';
var VIEWS=['inicio','sobre','hierarquia','unidades','alistamento','regulamentos','noticias','militar','perfil','verificacao','compras'];
var RANKS0=['Recruta','Soldado','Cabo','3º Combatente','2º Combatente','1º Combatente','Subtenente','Cadete','Aspirante a Oficial','2º Tenente','1º Tenente','Capitão','Major','Tenente-Coronel','Coronel','General de Brigada','General de Divisão','General de Exército','Elite Militar','Elite Secreta','Elite Real','Marechal','Vice-Presidente','Subcomandante','Comandante','Presidente'];
var UNITS0=[
  {s:'CIE',n:'Centro de Inteligência do Exército'},
  {s:'FEE',n:'Forças Especiais do Exército'},
  {s:'BAC',n:'Batalhões de Ações de Comando'},
  {s:'PE',n:'Polícia do Exército'},
  {s:'CIGS',n:'Centro de Instrução de Guerra na Selva'}
];
function today(){return new Date().toLocaleDateString('pt-BR')}
function seed(){
  return {
    v:4,
    profile:null,
    lastPraca:'Cadete',
    ranks:RANKS0.slice(),
    units:UNITS0.map(function(u){return {s:u.s,n:u.n}}),
    roster:[
      {u:'ex_militar_01',id:'1000001',rank:'Coronel',unit:'CIE',since:'14/03/2025',hist:[{d:'14/03/2025',t:'Entrada no EBC como Recruta'},{d:'02/07/2025',t:'Promovido a Soldado'},{d:'19/10/2025',t:'Promovido a Major'},{d:'05/02/2026',t:'Promovido a Coronel'}]},
      {u:'ex_militar_02',id:'1000002',rank:'Capitão',unit:'FEE',since:'30/05/2025',hist:[{d:'30/05/2025',t:'Entrada no EBC como Recruta'},{d:'11/01/2026',t:'Promovido a Capitão'}]},
      {u:'ex_militar_03',id:'1000003',rank:'Cabo',unit:'PE',since:'08/09/2025',hist:[{d:'08/09/2025',t:'Entrada no EBC como Recruta'},{d:'21/12/2025',t:'Promovido a Cabo'}]},
      {u:'ex_militar_04',id:'1000004',rank:'Aspirante a Oficial',unit:'BAC',since:'17/01/2026',hist:[{d:'17/01/2026',t:'Entrada no EBC como Recruta'},{d:'25/06/2026',t:'Promovido a Aspirante a Oficial'}]},
      {u:'ex_militar_05',id:'1000005',rank:'Soldado',unit:'',since:'22/09/2026',hist:[{d:'22/09/2026',t:'Entrada no EBC como Recruta'},{d:'30/10/2026',t:'Promovido a Soldado'}]}
    ],
    pend:[
      {u:'ex_candidato_01',code:'EBC-4F8K2Q',when:'08/11/2026 17:42',note:'Bio não encontrada na primeira checagem'},
      {u:'ex_candidato_02',code:'EBC-9M3TX7',when:'08/11/2026 17:55',note:'Perfil com bio muito longa'}
    ],
    avisos:[
      {t:'Verificação obrigatória',b:'Todo militar precisa estar verificado para acessar a Área do Militar.',d:'08/11/2026'}
    ],
    enlist:[
      {u:'ex_recruta_01',dc:'ex_recruta_01',msg:'Quero servir na Polícia do Exército.'},
      {u:'ex_recruta_02',dc:'ex_recruta_02',msg:'Jogo todos os dias e quero fazer parte de uma unidade.'}
    ]
  };
}
function load(){try{var r=localStorage.getItem(KEY);var o=r?JSON.parse(r):null;if(!(o&&o.ranks&&o.roster&&o.units))return null;
  if(!(o.v>=2)){o.v=2;o.ranks=RANKS0.slice();o.units=o.units.filter(function(u){return u.s!=='CIA'});o.roster.forEach(function(m){if(m.unit==='CIA')m.unit='';if(o.ranks.indexOf(m.rank)<0)m.rank=o.ranks[0]})}
  if(!(o.v>=3)){o.v=3;o.avisos=(o.avisos||[]).filter(function(a){return a.t==='Verificação obrigatória'})}
  {o.v=4;o.ranks=RANKS0.slice();o.lastPraca='Cadete';o.roster.forEach(function(m){if(m.rank==='Sub-Combatente')m.rank='Subtenente';if(o.ranks.indexOf(m.rank)<0)m.rank=o.ranks[0]})}
  return o}catch(e){return null}}
var S=load()||seed();
function save(){try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){}}
var NEWS=[
  {t:'Nova turma de recrutas em formação',b:'Os alistamentos aprovados entram na patente de Recruta e seguem para instrução básica.',d:'05/11/2026'},
  {t:'Seleção para as Forças Especiais',b:'A FEE avalia militares indicados pelos comandantes de cada unidade.',d:'01/11/2026'},
  {t:'Regulamento atualizado',b:'Os artigos sobre verificação e segurança da conta foram revisados.',d:'28/10/2026'}
];
var $=function(s,r){return (r||document).querySelector(s)};
var $$=function(s,r){return Array.prototype.slice.call((r||document).querySelectorAll(s))};
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
function me(){return S.profile?S.roster.filter(function(m){return m.u===S.profile.user})[0]||null:null}
function unitName(s){if(!s)return 'Sem unidade';var u=S.units.filter(function(x){return x.s===s})[0];return u?u.s+' — '+u.n:s}

$$('.lnk-discord').forEach(function(a){a.href=LINKS.discord});
$$('.lnk-roblox').forEach(function(a){a.href=LINKS.roblox});

/* ---------- renderers ---------- */
function renderSide(){
  var p=S.profile;
  $('#me').innerHTML='<span class="av">'+esc((p?p.user:'M').charAt(0))+'</span><span class="mt"><b>'+esc(p?p.user:'Militar')+'</b><small>'+(p?'Verificado · ver perfil':'Não verificado · ver perfil')+'</small></span><span class="gt">›</span>';
  var hv=$('#hd-verify');
  hv.textContent=p?'✓ Verificado':'✓ Verificar';
  hv.setAttribute('href',p?'#perfil':'#verificacao');
}
function post(n,tag,ex){return '<article class="post"><span class="kick">'+esc(tag)+(ex?' <span class="chip ex">Exemplo</span>':'')+'</span><b>'+esc(n.t)+'</b><p>'+esc(n.b)+'</p><span class="date">'+esc(n.d)+'</span></article>'}
function renderHome(){
  $('#home-title').textContent='Olá, '+(S.profile?S.profile.user:'Militar');
  $('#tile-units').textContent=S.units.length+(S.units.length===1?' unidade':' unidades');
  $('#home-posts').innerHTML=S.avisos.length?S.avisos.map(function(a){return post(a,'Aviso oficial')}).join(''):'<p class="empty">Nenhum aviso no momento.</p>';
  $('#news-full').innerHTML=NEWS.map(function(n){return post(n,'Notícia',true)}).join('');
}
var ICON={
  chev:'<svg viewBox="0 0 24 24" aria-hidden="true"><path d="M4 12l8-7 8 7M4 19l8-7 8 7" fill="none" stroke="#fff" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></svg>',
  star:'<svg viewBox="0 0 24 24" aria-hidden="true"><polygon points="12,2 14.35,8.76 21.51,8.91 15.8,13.24 17.88,20.09 12,16 6.12,20.09 8.2,13.24 2.49,8.91 9.65,8.76" fill="#fff"/></svg>',
  elite:'<svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 2l9 3v7c0 5-4 8.5-9 10-5-1.5-9-5-9-10V5z" fill="#0f2a66"/><polygon points="12,6.5 13.3,10.3 17.3,10.4 14.1,12.8 15.3,16.6 12,14.3 8.7,16.6 9.9,12.8 6.7,10.4 10.7,10.3" fill="#fff"/></svg>'
};
function cutIdx(){var i=S.ranks.indexOf(S.lastPraca||'Cadete');return (i<0?6:i)+1}
function renderHier(){
  var n=S.ranks.length,cut=cutIdx();
  $('#rank-stats').innerHTML='<div class="stat"><b>'+cut+'</b><span>Praças</span></div><div class="stat"><b>'+(n-cut)+'</b><span>Oficiais</span></div><div class="stat"><b>'+n+'</b><span>Patentes</span></div>';
  var groups=[{t:'Praças',from:0,to:cut,ic:'chev'},{t:'Oficiais',from:cut,to:n,ic:'star'}];
  $('#rank-groups').innerHTML=groups.map(function(g){
    if(g.to<=g.from)return '';
    var items=S.ranks.slice(g.from,g.to).map(function(r,k){
      var ei=S.ranks.indexOf('Elite Militar'),i=g.from+k,elite=i===n-1,topIc=ei>-1&&i>=ei;
      return '<li class="rk'+(elite?' elite':'')+'"><span class="ic">'+(topIc?ICON.elite:ICON[g.ic])+'</span><span class="pos">Patente '+String(i+1).padStart(2,'0')+'</span><span class="nm">'+esc(r)+'</span></li>';
    }).join('');
    return '<div class="rg"><div class="rg-head"><h2>'+g.t+'</h2><span>'+esc(S.ranks[g.from])+' ao '+esc(S.ranks[g.to-1])+'</span></div><ol class="rk-grid">'+items+'</ol></div>';
  }).join('');
}
var UROLES={
  CIE:['Comandante','Subcomandante','Oficiais de Investigação','Agentes Especializados','Agente Formado','Agente Praça','Agente Estagiário'],
  CIGS:['Comandante','Subcomandante','Oficiais','Graduado','Praças','Aluno'],
  PE:['Comandante','Subcomandante','Oficiais','Graduados','Praças','Candidato'],
  BAC:['Comando','Subcomando','Oficial de Ação','Agente de Combate','Praça','Candidato'],
  FEE:['Comandante','Subcomandante','Oficiais Especializados','Graduados Formado','Praça','Candidato']
};
function renderUnits(){
  $('#unit-grid').innerHTML=S.units.length?S.units.map(function(u,i){
    var r=UROLES[u.s];
    if(!r)return '<div class="unit"><b>'+esc(u.s)+'</b><span>'+esc(u.n)+'</span></div>';
    return '<div class="unit"><button type="button" class="ubtn" data-unit="'+i+'" aria-expanded="false" aria-controls="ur-'+i+'"><b>'+esc(u.s)+'</b><span>'+esc(u.n)+'</span><span class="uc">Ver cargos ›</span></button><ul class="vals roles" id="ur-'+i+'" hidden>'+r.map(function(x){return '<li><span>'+esc(x)+'</span></li>'}).join('')+'</ul></div>';
  }).join(''):'<p class="empty">Nenhuma unidade cadastrada.</p>';
}
function recordHtml(m,example){
  var verified=example||!!S.profile;
  return '<div class="panel"><div class="profile-head"><div class="avatar">'+esc(m.u.charAt(0))+'</div><div><h2 style="font-size:28px;font-weight:900">'+esc(m.u)+'</h2><span class="chip '+(verified?'ok':'no')+'" style="margin-top:6px">'+(verified?'Verificado':'Não verificado')+'</span>'+(example?' <span class="chip ex">Exemplo</span>':'')+'</div></div>'
   +'<dl class="dl"><dt>Nome do militar</dt><dd>'+esc(m.u)+'</dd><dt>ID Roblox</dt><dd class="mono">'+esc(m.id||'—')+'</dd><dt>Patente</dt><dd>'+esc(m.rank)+'</dd><dt>Unidade</dt><dd>'+esc(unitName(m.unit))+'</dd><dt>Data de entrada</dt><dd>'+esc(m.since)+'</dd><dt>Status de verificação</dt><dd>'+(verified?'Verificado':'Pendente')+'</dd></dl></div>'
   +'<div class="panel"><h2>Histórico de promoções</h2><ul class="timeline">'+m.hist.slice().reverse().map(function(h){return '<li><span class="date">'+esc(h.d)+'</span><span>'+esc(h.t)+'</span></li>'}).join('')+'</ul></div>';
}
function renderMilitar(){
  var m=me();
  if(m){$('#mil-sub').textContent='Seus dados de serviço no EBC.';$('#mil-record').innerHTML=recordHtml(m,false)}
  else{
    $('#mil-sub').innerHTML='Você ainda não está verificado. Abaixo, um registro de exemplo. <a href="#verificacao">Verificar-se agora</a>.';
    $('#mil-record').innerHTML=recordHtml(S.roster[0]||seed().roster[0],true);
  }
}
function renderPerfil(){
  var p=S.profile,m=me();
  if(!p){$('#perfil-box').innerHTML='<h2>Sem perfil verificado</h2><p class="vs">Faça a verificação pela bio para criar seu perfil de militar neste navegador.</p><div><a class="btn primary" href="#verificacao">Verificar-se</a></div>';return}
  $('#perfil-box').innerHTML='<div class="profile-head"><div class="avatar">'+esc(p.user.charAt(0))+'</div><div><h2 style="font-size:28px;font-weight:900">'+esc(p.user)+'</h2><span class="chip ok" style="margin-top:6px">Verificado</span></div></div>'
   +'<dl class="dl"><dt>ID Roblox</dt><dd class="mono">'+esc(p.id)+'</dd><dt>Patente</dt><dd>'+esc(m?m.rank:S.ranks[0])+'</dd><dt>Unidade</dt><dd>'+esc(m?unitName(m.unit):'Sem unidade')+'</dd><dt>Verificado em</dt><dd>'+esc(p.date)+'</dd></dl>'
   +'<div class="cta"><a class="btn primary" href="#militar">Abrir Área do Militar</a><a class="btn" href="#verificacao">Refazer verificação</a><button class="btn danger" type="button" data-act="unverify">Remover verificação</button></div>';
}

/* admin */
var A={tab:'militares'};
var TABS=[['militares','Militares'],['patentes','Patentes'],['unidades','Unidades'],['verificacoes','Verificações'],['avisos','Avisos'],['alistamentos','Alistamentos']];
function renderAdmin(){
  if(!$('#adm-tabs'))return;
  $('#adm-tabs').innerHTML=TABS.map(function(t){
    var c='';if(t[0]==='verificacoes')c=' ('+S.pend.length+')';if(t[0]==='alistamentos')c=' ('+S.enlist.length+')';
    return '<button type="button" class="tab" data-act="tab" data-t="'+t[0]+'" aria-pressed="'+(A.tab===t[0])+'">'+t[1]+c+'</button>';
  }).join('');
  var h='';
  if(A.tab==='militares'){
    h='<h2>Gerenciar militares</h2><div class="rows">'+S.roster.map(function(m){
      var i=S.ranks.indexOf(m.rank);
      return '<div class="row"><div class="grow"><b>'+esc(m.u)+'</b><small><span class="mono">'+esc(m.id||'—')+'</span> · entrou em '+esc(m.since)+'</small></div>'
       +'<span class="chip ex">'+esc(m.rank)+'</span>'
       +'<select aria-label="Unidade de '+esc(m.u)+'" data-act="setunit" data-u="'+esc(m.u)+'"><option value="">Sem unidade</option>'+S.units.map(function(u){return '<option value="'+esc(u.s)+'"'+(m.unit===u.s?' selected':'')+'>'+esc(u.s)+'</option>'}).join('')+'</select>'
       +'<div class="btns"><button type="button" class="btn sm" data-act="promote" data-u="'+esc(m.u)+'"'+(i>=S.ranks.length-1?' disabled':'')+'>Promover</button><button type="button" class="btn sm" data-act="demote" data-u="'+esc(m.u)+'"'+(i<=0?' disabled':'')+'>Rebaixar</button></div></div>';
    }).join('')+'</div>';
  }else if(A.tab==='patentes'){
    h='<h2>Adicionar patentes</h2><ol class="ranks">'+S.ranks.map(function(r,i){return '<li class="rank"><span class="n mono">'+String(i+1).padStart(2,'0')+'</span><span class="nm">'+esc(r)+'</span></li>'}).join('')+'</ol>'
     +'<form class="inline-form" data-form="rank"><div class="field"><label for="rk-name">Nome da patente</label><input id="rk-name" autocomplete="off"></div><div class="field"><label for="rk-pos">Inserir antes de</label><select id="rk-pos">'+S.ranks.map(function(r,i){return '<option value="'+i+'"'+(i===S.ranks.length-1?' selected':'')+'>'+esc(r)+'</option>'}).join('')+'</select></div><button class="btn primary" type="submit">Adicionar</button></form><p class="msg" id="adm-msg" role="status"></p>';
  }else if(A.tab==='unidades'){
    h='<h2>Gerenciar unidades</h2><div class="rows">'+S.units.map(function(u,i){return '<div class="row"><div class="grow"><b>'+esc(u.s)+'</b><small>'+esc(u.n)+'</small></div><button type="button" class="btn sm danger" data-act="rmunit" data-i="'+i+'">Remover</button></div>'}).join('')+'</div>'
     +'<form class="inline-form" data-form="unit"><div class="field" style="flex:0 1 120px"><label for="un-s">Sigla</label><input id="un-s" maxlength="8" autocomplete="off"></div><div class="field"><label for="un-n">Nome da unidade</label><input id="un-n" autocomplete="off"></div><button class="btn primary" type="submit">Adicionar</button></form><p class="msg" id="adm-msg" role="status"></p>';
  }else if(A.tab==='verificacoes'){
    h='<h2>Aprovar verificações</h2>'+(S.pend.length?'<div class="rows">'+S.pend.map(function(p,i){return '<div class="row"><div class="grow"><b>'+esc(p.u)+'</b><small><span class="mono">'+esc(p.code)+'</span> · '+esc(p.when)+' · '+esc(p.note)+'</small></div><div class="btns"><button type="button" class="btn sm primary" data-act="okpend" data-i="'+i+'">Aprovar</button><button type="button" class="btn sm danger" data-act="nopend" data-i="'+i+'">Recusar</button></div></div>'}).join('')+'</div>':'<p class="empty">Nenhuma verificação aguardando aprovação.</p>');
  }else if(A.tab==='avisos'){
    h='<h2>Gerenciar avisos</h2>'+(S.avisos.length?'<div class="rows">'+S.avisos.map(function(a,i){return '<div class="row"><div class="grow"><b>'+esc(a.t)+'</b><small>'+esc(a.d)+' · '+esc(a.b)+'</small></div><button type="button" class="btn sm danger" data-act="rmaviso" data-i="'+i+'">Remover</button></div>'}).join('')+'</div>':'<p class="empty">Nenhum aviso publicado.</p>')
     +'<form class="inline-form" data-form="aviso"><div class="field"><label for="av-t">Título</label><input id="av-t" autocomplete="off"></div><div class="field" style="flex:2 1 260px"><label for="av-b">Texto</label><input id="av-b" autocomplete="off"></div><button class="btn primary" type="submit">Publicar aviso</button></form><p class="msg" id="adm-msg" role="status"></p>';
  }else{
    h='<h2>Gerenciar alistamentos</h2>'+(S.enlist.length?'<div class="rows">'+S.enlist.map(function(e,i){return '<div class="row"><div class="grow"><b>'+esc(e.u)+'</b><small>Discord: '+esc(e.dc||'—')+' · '+esc(e.msg||'')+'</small></div><div class="btns"><button type="button" class="btn sm primary" data-act="okenl" data-i="'+i+'">Aceitar</button><button type="button" class="btn sm danger" data-act="noenl" data-i="'+i+'">Recusar</button></div></div>'}).join('')+'</div>':'<p class="empty">Nenhum alistamento pendente.</p>');
  }
  $('#adm-body').innerHTML=h;
}
function addMilitar(u,id){
  if(S.roster.some(function(m){return m.u===u}))return;
  S.roster.push({u:u,id:id||'—',rank:S.ranks[0],unit:'',since:today(),hist:[{d:today(),t:'Entrada no EBC como '+S.ranks[0]}]});
}
var SHOP=[
  {k:'01',s:'CIE',n:'Centro de Inteligência do Exército',v:[['Comandante',50],['Subcomandante',40],['Oficiais de Investigação',25],['Agentes Especializados',18],['Agente Formado',10],['Agente Praça',6],['Agente Estagiário',3]]},
  {k:'02',s:'BAC',n:'Batalhão de Ações de Comando',v:[['Comandante','Não vende',1],['Subcomandante','Não vende',1],['Oficial de Ação',35],['Agente de Combate',25],['Praça',10],['Candidato',5]]}
];
var BUY='<a class="btn sm primary buy-dc" href="'+LINKS.discord+'" target="_blank" rel="noopener">Comprar ↗</a>';
var PRICES=[
  {g:'Alto Comando',v:[['Combatente','60'],['Sub-Combatente','50']]},
  {g:'Presidente',v:[['Presidente','45'],['Vice-Presidente','40']]},
  {g:'Oficiais da Elite',v:[['Elite Secreta','37'],['Elite Real','35'],['Elite Militar','34']]},
  {g:'Oficiais Generais',v:[['General de Exército','32'],['General de Divisão','28'],['General de Brigada','25']]},
  {g:'Oficiais Superiores',v:[['Coronel','23,50'],['Tenente-Coronel','20'],['Major','18']]},
  {g:'Oficiais Intermediários',v:[['Capitão','17']]},
  {g:'Oficiais Subalternos',v:[['Primeiro-Tenente','15'],['Segundo-Tenente','13'],['Aspirante a Oficial','10']]},
  {g:'Praças Especiais',v:[['Cadete','9,50']]},
  {g:'Graduados',v:[['Subtenente','8,5'],['Primeiro-Combatente','7'],['Segundo-Combatente','6'],['Terceiro-Combatente','4']]},
  {g:'Praças',v:[['Cabo','2'],['Soldado','1']]}
];
function renderShop(){
  var rk=PRICES.map(function(p){
    return '<article class="item"><b>'+esc(p.g)+'</b><ul class="vals">'+p.v.map(function(r){return '<li><span>'+esc(r[0])+'</span><strong>'+esc(r[1])+'</strong></li>'}).join('')+'</ul><div class="pr">'+BUY+'</div></article>';
  }).join('');
  if(!SHOP.length){$('#shop-grid').innerHTML='<div class="panel" style="grid-column:1/-1"><h2>Em breve</h2><p class="vs">Os itens e valores do EBC serão publicados aqui.</p></div>';return}
  $('#shop-grid').innerHTML=rk+SHOP.map(function(s){
    return '<article class="item"><span class="kick">Divisão à venda · '+esc(s.k)+'</span><b style="font-size:26px">'+esc(s.s)+' — '+esc(s.n)+'</b><ul class="vals">'+s.v.map(function(r){return '<li'+(r[2]?' class="no"':'')+'><span>'+esc(r[0])+'</span><strong>'+esc(r[1])+'</strong></li>'}).join('')+'</ul><div class="pr">'+BUY+'</div></article>';
  }).join('');
}
function renderAll(){renderShop();renderSide();renderHome();renderHier();renderUnits();renderMilitar();renderPerfil();renderAdmin()}

/* ---------- verification ---------- */
var V={step:'intro'},T=[];
var ALPHA='ABCDEFGHJKMNPQRSTUVWXYZ23456789';
function makeCode(){var c='';for(var i=0;i<6;i++)c+=ALPHA.charAt(Math.floor(Math.random()*ALPHA.length));return 'EBC-'+c}
function stepper(n){return '<ol class="steps">'+['Usuário','Bio','Análise','Aprovado'].map(function(t,i){return '<li class="'+(i+1<n?'done':(i+1===n?'now':''))+'">'+t+'</li>'}).join('')+'</ol>'}
var DEMO='';
var RBX='https://users.roproxy.com';
/* Sem API_URL, o site consulta o Roblox direto (pelo espelho roproxy). Com API_URL, usa o Worker. */
function startReq(username){
  if(API_URL)return api('/start',{username:username});
  return fetch(RBX+'/v1/usernames/users',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({usernames:[username],excludeBannedUsers:true})}).then(function(r){
    if(!r.ok)throw new Error('roblox_error');
    return r.json();
  }).then(function(j){
    var u=j&&j.data&&j.data[0];
    if(!u)throw new Error('user_not_found');
    return {ok:true,userId:u.id,name:u.name,code:makeCode(),exp:Date.now()+900000,sig:''};
  });
}
function verifyReq(){
  if(API_URL)return api('/verify',{userId:V.uid,name:V.user,code:V.code,exp:V.exp,sig:V.sig});
  return fetch(RBX+'/v1/users/'+encodeURIComponent(V.uid)).then(function(r){
    if(!r.ok)throw new Error('roblox_error');
    return r.json();
  }).then(function(j){
    var ok=String(j.description||'').toUpperCase().indexOf(String(V.code).toUpperCase())>-1;
    return ok?{ok:true,userId:V.uid,name:j.name,token:''}:{ok:false};
  });
}
function api(path,body){
  return fetch(API_URL.replace(/\/$/,'')+path,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(body)}).then(function(r){
    return r.json().then(function(j){if(!r.ok)throw new Error(j.error||'erro');return j});
  });
}
function vfyRender(){
  var h='',logo='<svg class="lg" viewBox="0 0 64 72" aria-hidden="true"><use href="#logo"/></svg>';
  if(V.step==='intro'){
    h=logo+'<h1 class="vt">Verifique-se</h1><p class="vs">Confirme sua identidade para acessar a área principal do EBC.</p><button class="btn primary" data-act="v-start" type="button">Verificar</button><a class="back" href="#inicio">Voltar ao site</a>';
  }else if(V.step==='back'){
    h=logo+'<h1 class="vt ok">Verificado</h1><p class="vs">Conta verificada: <b>'+esc(S.profile.user)+'</b>.</p><div class="cta"><button class="btn primary" data-act="v-back" type="button">Me verifiquei</button><button class="btn" data-act="v-start" type="button">Verificar outra conta</button></div><a class="back" href="#inicio">Voltar ao site</a>';
  }else if(V.step==='method'){
    h=logo+'<h1 class="vt" style="font-size:clamp(30px,8vw,56px)">Como verificar?</h1><div class="vopts"><button class="opt" data-act="v-roblox" type="button"><b>Verificar pela Roblox</b><span>Login oficial da Roblox. Disponível quando o servidor do EBC estiver conectado.</span></button><button class="opt" data-act="v-bio" type="button"><b>Verificar pela Bio</b><span>Você coloca um código na bio do seu perfil e o BOT confere.</span></button></div><a class="back" href="#inicio">Voltar ao site</a>';
  }else if(V.step==='roblox'){
    h=logo+'<h1 class="vt" style="font-size:clamp(30px,8vw,56px)">Roblox</h1><p class="vs">A verificação pela Roblox exige um servidor com login oficial, que ainda não está conectado a este site. Use a verificação pela bio.</p><div class="cta"><button class="btn primary" data-act="v-bio" type="button">Verificar pela Bio</button><button class="btn" data-act="v-start" type="button">Voltar</button></div>';
  }else if(V.step==='form'){
    h=stepper(1)+DEMO+'<h1 class="vt" style="font-size:clamp(30px,8vw,56px)">Seu perfil</h1><form class="form" id="vfy-form" style="width:100%" novalidate><div class="field"><label for="v-user">Usuário Roblox</label><input id="v-user" autocomplete="off" value="'+esc(V.user||'')+'" placeholder="SeuUsuario"></div><p class="msg err" id="v-err" role="alert"></p><div><button class="btn primary" type="submit">Gerar bio oficial</button></div></form><p class="vs" style="font-size:14px">O EBC nunca pede a senha da sua conta Roblox.</p>';
  }else if(V.step==='bio'){
    h=stepper(2)+DEMO+'<div class="bot"><div class="hd">EBC BOT — Verificação</div><p><b>Olá, militar! 🇧🇷</b></p><p>Para continuar, você precisa verificar sua identidade.</p><p>Coloque a bio oficial solicitada no seu perfil Roblox.</p><p>Após colocar a bio e salvar, clique em Verificar Bio. O BOT procura o código por até 1 minuto.</p></div><div class="codebox"><code id="v-code">Verificação EBC: '+esc(V.code)+'</code><button class="btn sm" data-act="v-copy" type="button" id="v-copy">Copiar</button></div><div class="cta"><button class="btn primary" data-act="v-check" type="button">Verificar Bio</button><button class="btn" data-act="v-start" type="button">Voltar</button></div><p class="vs" style="font-size:14px">Perfil: <b>'+esc(V.user)+'</b>. O EBC nunca pede a senha da sua conta Roblox.</p>';
  }else if(V.step==='checking'){
    h=stepper(3)+'<h1 class="vt" style="font-size:clamp(28px,7vw,48px)">Você está se verificando, não saia.</h1><div class="bot"><div class="hd">EBC BOT — Verificação</div><p>Aguarde enquanto nossa IA analisa sua verificação.</p><p>Procurando o código na bio de <b>'+esc(V.user)+'</b>. Tempo restante: <b class="mono">'+V.left+'s</b></p></div><div class="bar"><i style="width:'+Math.round((60-V.left)/60*100)+'%"></i></div>'+(V.msg?'<p class="msg err">'+esc(V.msg)+'</p>':'');
  }else if(V.step==='fail'){
    h=stepper(3)+'<h1 class="vt" style="font-size:clamp(28px,7vw,48px)">Bio não encontrada</h1><div class="bot"><div class="hd">EBC BOT — Verificação</div><p>Não achei o código <b class="mono">'+esc(V.code)+'</b> na bio de <b>'+esc(V.user)+'</b>. Sem ele você não entra no site.</p><p>Confira se colocou o código na bio do perfil Roblox e se salvou. Depois tente de novo.</p></div>'+(V.msg?'<p class="msg err">'+esc(V.msg)+'</p>':'')+'<div class="cta"><button class="btn primary" data-act="v-retry" type="button">Tentar de novo</button><button class="btn" data-act="v-start" type="button">Voltar</button></div>';
  }else if(V.step==='done'){
    h=stepper(5)+'<div class="bot"><div class="hd">EBC BOT — Verificação</div><p><b>VERIFICAÇÃO APROVADA</b></p></div><h1 class="vt ok" style="font-size:clamp(30px,8vw,56px)">Você foi verificado com sucesso!</h1><a class="btn primary" href="#militar">Entrar no Site</a>';
  }
  $('#vfy-stage').innerHTML=h;
  var f=$('#v-user');if(f&&!f.value)try{f.focus()}catch(e){}
}
function clearT(){T.forEach(clearTimeout);T=[]}
function vfyInit(){clearT();V=S.profile?{step:'back'}:{step:'intro'};vfyRender()}
/* O BOT confere a bio a cada 10 s durante 1 minuto. Achou o código: entra. Não achou: não entra. */
function runCheck(){
  clearT();V.step='checking';V.left=60;V.msg='';
  var busy=false,done=false;
  function attempt(){
    if(busy||done)return;busy=true;
    verifyReq().then(function(j){
      busy=false;if(done)return;
      if(j&&j.ok){
        done=true;clearT();
        S.profile={user:j.name,id:String(j.userId),token:j.token,date:today()};
        addMilitar(j.name,String(j.userId));save();
        V.step='done';vfyRender();renderAll();
      }
    }).catch(function(){busy=false;V.msg='Não consegui falar com o servidor de verificação. Vou tentar de novo.'});
  }
  function tick(){
    if(done||V.step!=='checking')return;
    if(V.left%10===0)attempt();
    vfyRender();
    if(V.left<=0){
      T.push(setTimeout(function(){if(!done&&V.step==='checking'){done=true;V.step='fail';vfyRender()}},2500));
      return;
    }
    V.left--;T.push(setTimeout(tick,1000));
  }
  tick();
}

/* ---------- routing ---------- */
function closeDrawer(){$('#side').classList.remove('open');$('#scrim').classList.remove('show');$('#menu').setAttribute('aria-expanded','false')}
function route(){
  var h=(location.hash||'').slice(1);
  var v=VIEWS.indexOf(h)>-1?h:'inicio';
  var isV=v==='verificacao';
  document.body.classList.toggle('vfy',isV);
  $('#shell').hidden=isV;$('#vfy').hidden=!isV;
  $$('[data-view]').forEach(function(s){s.hidden=s.dataset.view!==v});
  $$('#nav a').forEach(function(a){if(a.dataset.v===v)a.setAttribute('aria-current','page');else a.removeAttribute('aria-current')});
  closeDrawer();
  if(isV)$('#dcm').hidden=true;
  if(isV)vfyInit();else clearT();
  try{window.scrollTo(0,0)}catch(e){}
}
window.addEventListener('hashchange',route);

/* ---------- events ---------- */
$('#menu').addEventListener('click',function(){var o=!$('#side').classList.contains('open');$('#side').classList.toggle('open',o);$('#scrim').classList.toggle('show',o);$('#menu').setAttribute('aria-expanded',String(o))});
$('#scrim').addEventListener('click',closeDrawer);

document.addEventListener('click',function(e){
  var b=e.target.closest('[data-act]');if(!b)return;
  var a=b.dataset.act,i=+b.dataset.i,u=b.dataset.u,m;
  if(a==='tab'){A.tab=b.dataset.t;renderAdmin();return}
  if(a==='v-start'){V={step:'method'};vfyRender();return}
  if(a==='v-roblox'){V.step='roblox';vfyRender();return}
  if(a==='v-bio'){V={step:'form'};vfyRender();return}
  if(a==='v-back'){location.hash='#militar';return}
  if(a==='v-check'){runCheck();return}
  if(a==='v-retry'){V.step='bio';vfyRender();return}
  if(a==='v-copy'){
    var txt='Verificação EBC: '+V.code,btn=$('#v-copy');
    var done=function(){btn.textContent='Copiado';setTimeout(function(){if($('#v-copy'))$('#v-copy').textContent='Copiar'},1500)};
    var fb=function(){try{var r=document.createRange();r.selectNodeContents($('#v-code'));var s=window.getSelection();s.removeAllRanges();s.addRange(r);btn.textContent='Selecionado'}catch(x){}};
    try{navigator.clipboard.writeText(txt).then(done,fb)}catch(x){fb()}
    return;
  }
  if(a==='unverify'){S.profile=null;save();renderAll();return}
  if(a==='promote'||a==='demote'){
    m=S.roster.filter(function(x){return x.u===u})[0];if(!m)return;
    var k=S.ranks.indexOf(m.rank),n=a==='promote'?k+1:k-1;
    if(n<0||n>=S.ranks.length)return;
    m.rank=S.ranks[n];m.hist.push({d:today(),t:(a==='promote'?'Promovido a ':'Rebaixado a ')+m.rank});
    save();renderAll();return;
  }
  if(a==='rmunit'){var rm=S.units.splice(i,1)[0];S.roster.forEach(function(x){if(rm&&x.unit===rm.s)x.unit=''});save();renderAll();return}
  if(a==='okpend'){var p=S.pend.splice(i,1)[0];if(p)addMilitar(p.u,'—');save();renderAll();return}
  if(a==='nopend'){S.pend.splice(i,1);save();renderAll();return}
  if(a==='rmaviso'){S.avisos.splice(i,1);save();renderAll();return}
  if(a==='okenl'){var en=S.enlist.splice(i,1)[0];if(en)addMilitar(en.u,'—');save();renderAll();return}
  if(a==='noenl'){S.enlist.splice(i,1);save();renderAll();return}
});

document.addEventListener('change',function(e){
  var s=e.target.closest('[data-act="setunit"]');if(!s)return;
  var m=S.roster.filter(function(x){return x.u===s.dataset.u})[0];if(!m||m.unit===s.value)return;
  m.unit=s.value;m.hist.push({d:today(),t:s.value?'Transferido para '+s.value:'Removido da unidade'});
  save();renderAll();
});

document.addEventListener('submit',function(e){
  var f=e.target;e.preventDefault();
  if(f.id==='vfy-form'){
    var u=$('#v-user').value.trim(),err=$('#v-err');
    V.user=u;
    if(!/^[A-Za-z0-9_]{3,20}$/.test(u)){err.textContent='Digite seu usuário Roblox: de 3 a 20 letras, números ou underline.';return}
    err.textContent='Procurando o perfil...';
    startReq(u).then(function(j){
      V.user=j.name;V.uid=j.userId;V.code=j.code;V.exp=j.exp;V.sig=j.sig;V.step='bio';vfyRender();
    }).catch(function(x){
      var e2=$('#v-err');if(!e2)return;
      e2.textContent=x&&x.message==='user_not_found'?'Não achei esse usuário no Roblox. Confira o nome.':'Não consegui falar com o servidor de verificação. Tente de novo em instantes.';
    });
    return;
  }
  if(f.id==='enlist-form'){
    var user=$('#al-user').value.trim(),dc=$('#al-dc').value.trim(),msg=$('#al-msg').value.trim(),out=$('#al-msg-out');
    if(!/^[A-Za-z0-9_]{3,20}$/.test(user)){out.className='msg err';out.textContent='Digite seu usuário Roblox: de 3 a 20 letras, números ou underline.';return}
    S.enlist.push({u:user,dc:dc,msg:msg});save();renderAdmin();
    f.reset();out.className='msg good';out.textContent='Alistamento enviado. O comando vai analisar sua solicitação.';return;
  }
  var kind=f.dataset.form,msgEl;
  if(kind==='rank'){
    var nm=$('#rk-name').value.trim(),pos=+$('#rk-pos').value;
    msgEl=$('#adm-msg');
    if(!nm){msgEl.className='msg err';msgEl.textContent='Digite o nome da patente.';return}
    if(S.ranks.indexOf(nm)>-1){msgEl.className='msg err';msgEl.textContent='Essa patente já existe.';return}
    S.ranks.splice(pos,0,nm);save();renderAll();return;
  }
  if(kind==='unit'){
    var s=$('#un-s').value.trim().toUpperCase(),n=$('#un-n').value.trim();msgEl=$('#adm-msg');
    if(!s||!n){msgEl.className='msg err';msgEl.textContent='Preencha a sigla e o nome da unidade.';return}
    if(S.units.some(function(x){return x.s===s})){msgEl.className='msg err';msgEl.textContent='Já existe uma unidade com essa sigla.';return}
    S.units.push({s:s,n:n});save();renderAll();return;
  }
  if(kind==='aviso'){
    var t=$('#av-t').value.trim(),b=$('#av-b').value.trim();msgEl=$('#adm-msg');
    if(!t){msgEl.className='msg err';msgEl.textContent='Digite o título do aviso.';return}
    S.avisos.unshift({t:t,b:b,d:today()});save();renderAll();return;
  }
});

/* discord prompt: shown on entry until the visitor picks Entrar */
function closeDc(remember){
  $('#dcm').hidden=true;
  if(remember){try{localStorage.setItem('ebc-dc','1')}catch(e){}}
}
document.addEventListener('click',function(e){
  var b=e.target.closest('.ubtn');if(!b)return;
  var open=b.getAttribute('aria-expanded')==='true',ul=$('#'+b.getAttribute('aria-controls'));
  b.setAttribute('aria-expanded',String(!open));
  b.querySelector('.uc').textContent=open?'Ver cargos ›':'Fechar ‹';
  if(ul)ul.hidden=open;
});
var toastT=null;
document.addEventListener('click',function(e){
  if(!e.target.closest('.buy-dc'))return;
  var t=$('#toast');t.hidden=false;clearTimeout(toastT);
  toastT=setTimeout(function(){t.hidden=true},7000);
});
$('#dcm-yes').addEventListener('click',function(){closeDc(true)});
$('#dcm-no').addEventListener('click',function(){closeDc(false)});
document.addEventListener('keydown',function(e){if(e.key==='Escape'&&!$('#dcm').hidden)closeDc(false)});

renderAll();route();
(function(){
  var seen=false;try{seen=localStorage.getItem('ebc-dc')==='1'}catch(e){}
  if(!seen&&(location.hash||'').slice(1)!=='verificacao'){$('#dcm').hidden=false;try{$('#dcm-yes').focus()}catch(e){}}
})();
})();
</script>

</html>
