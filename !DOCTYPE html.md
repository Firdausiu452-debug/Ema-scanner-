```
<!DOCTYPE html>
<html lang="en">

```
```
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta http-equiv="Content-Security-Policy" content="default-src 'self' 'unsafe-inline' 'unsafe-eval' https:; connect-src 'self' https://*.deriv.com wss://*.derivws.com wss://*.binaryws.com ws://*.derivws.com ws://*.binaryws.com;">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="EMA Scanner">
<meta name="theme-color" content="#0a0f1e">
<title>EMA 200 Scanner</title>
<style>
:root{--bg:#0a0f1e;--sur:#111827;--card:#1a2235;--bdr:rgba(255,255,255,.08);--acc:#00e5ff;--bull:#00e676;--bear:#ff5252;--warn:#ffab40;--txt:#e8eaf6;--mut:#90a4ae;--r:10px;font-family:'Segoe UI',system-ui,-apple-system,sans-serif;}
*{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--txt);min-height:100vh;padding:16px 14px;padding-top:max(env(safe-area-inset-top,0px),16px);padding-bottom:max(env(safe-area-inset-bottom,0px),24px);}
header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
.logo{display:flex;align-items:center;gap:10px;}
.logo-icon{width:38px;height:38px;background:rgba(0,229,255,.1);border:1px solid rgba(0,229,255,.35);border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:20px;}
.logo h1{font-size:15px;font-weight:700;}
.logo p{font-size:10px;color:var(--mut);}
.scan-btn{background:var(--acc);color:#000;border:none;padding:10px 18px;border-radius:var(--r);font-weight:700;font-size:13px;cursor:pointer;white-space:nowrap;}
.scan-btn:disabled{opacity:.45;cursor:not-allowed;}
.sbar{display:flex;align-items:center;justify-content:space-between;padding:8px 12px;background:var(--sur);border-radius:8px;margin-bottom:8px;border:1px solid var(--bdr);}
.dot{width:7px;height:7px;border-radius:50%;background:var(--mut);display:inline-block;margin-right:7px;flex-shrink:0;}
.dot.live{background:var(--bull);animation:pulse 2s infinite;}
.dot.err{background:var(--bear);}
.dot.warn{background:var(--warn);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
.stxt{font-size:11px;color:var(--mut);}
.stime{font-size:10px;color:var(--mut);}
.pbar{height:3px;background:rgba(255,255,255,.05);border-radius:2px;margin-bottom:12px;overflow:hidden;}
.pfill{height:100%;background:var(--acc);border-radius:2px;transition:width .4s ease;width:0%;}
.row{display:flex;gap:8px;margin-bottom:12px;align-items:center;}
select{background:var(--card);border:1px solid var(--bdr);color:var(--txt);padding:6px 8px;border-radius:7px;font-size:11px;flex:1;}
.stog{display:flex;align-items:center;gap:5px;padding:6px 10px;background:var(--card);border:1px solid var(--bdr);border-radius:7px;font-size:11px;cursor:pointer;user-select:none;white-space:nowrap;}
.stog input{accent-color:var(--acc);}
.dbg{background:rgba(255,82,82,.07);border:1px solid rgba(255,82,82,.25);border-radius:var(--r);padding:11px 13px;margin-bottom:12px;display:none;}
.dbg h4{font-size:12px;color:var(--bear);margin-bottom:5px;}
.dbg pre{font-size:10px;color:var(--mut);white-space:pre-wrap;word-break:break-all;line-height:1.5;max-height:140px;overflow-y:auto;}
.apanel{background:var(--card);border:1px solid var(--bdr);border-radius:var(--r);padding:12px;margin-bottom:12px;}
.apanel h3{font-size:11px;color:var(--mut);letter-spacing:.8px;margin-bottom:10px;text-transform:uppercase;}
.ai{display:flex;align-items:flex-start;gap:10px;padding:9px 10px;border-radius:8px;margin-bottom:5px;background:rgba(255,255,255,.03);border:1px solid transparent;animation:fi .3s ease;}
@keyframes fi{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:translateY(0)}}
.ai.b{border-color:rgba(0,230,118,.2);}
.ai.s{border-color:rgba(255,82,82,.2);}
.adot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:4px;animation:pulse 1.5s infinite;}
.adot.b{background:var(--bull);}
.adot.s{background:var(--bear);}
.at{flex:1;}
.ap{font-size:13px;font-weight:700;}
.ad{font-size:10px;color:var(--mut);margin-top:2px;line-height:1.5;}
.atime{font-size:10px;color:var(--mut);white-space:nowrap;}
.empty{text-align:center;color:var(--mut);font-size:12px;padding:12px 0;}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:9px;}
.card{background:var(--card);border:1px solid var(--bdr);border-radius:var(--r);padding:11px;position:relative;overflow:hidden;transition:border-color .2s;}
.card.bull{border-color:rgba(0,230,118,.4);}
.card.bear{border-color:rgba(255,82,82,.4);}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:transparent;}
.card.bull::before{background:var(--bull);}
.card.bear::before{background:var(--bear);}
.card.loading::before{background:linear-gradient(90deg,transparent,var(--acc),transparent);animation:scanline 1s infinite;}
@keyframes scanline{0%{transform:translateX(-100%)}100%{transform:translateX(100%)}}
.ch{display:flex;align-items:center;justify-content:space-between;margin-bottom:5px;}
.cn{font-size:13px;font-weight:700;}
.cpx{font-size:9px;color:var(--acc);font-weight:600;margin-bottom:5px;min-height:13px;}
.pxtick{color:var(--bull);}
.pxtick.dn{color:var(--bear);}
.badge{font-size:9px;font-weight:700;padding:2px 7px;border-radius:20px;}
.bb{background:rgba(0,230,118,.15);color:var(--bull);}
.bs{background:rgba(255,82,82,.15);color:var(--bear);}
.bw{background:rgba(144,164,174,.12);color:var(--mut);}
.bl{background:rgba(255,171,64,.1);color:var(--warn);}
.bsig{background:rgba(0,229,255,.2);color:var(--acc);animation:pulse 1s infinite;}
.tfs{display:flex;gap:4px;margin-bottom:5px;}
.tf{flex:1;text-align:center;padding:4px 1px;border-radius:5px;font-size:9px;font-weight:600;background:rgba(255,255,255,.04);border:1px solid transparent;}
.tf.bu{background:rgba(0,230,118,.1);border-color:rgba(0,230,118,.25);color:var(--bull);}
.tf.be{background:rgba(255,82,82,.1);border-color:rgba(255,82,82,.25);color:var(--bear);}
.tf.no{color:var(--mut);}
.tfl{display:block;font-size:8px;font-weight:400;opacity:.7;margin-bottom:1px;}
.m15{margin-top:5px;padding-top:5px;border-top:1px solid var(--bdr);}
.m15l{font-size:8px;color:var(--mut);margin-bottom:3px;letter-spacing:.5px;}
.ccs{display:flex;gap:4px;}
.cc{flex:1;font-size:8px;text-align:center;padding:3px 2px;border-radius:4px;background:rgba(255,255,255,.04);color:var(--mut);border:1px solid transparent;}
.cc.on{background:rgba(0,229,255,.1);border-color:rgba(0,229,255,.25);color:var(--acc);}
.emav{font-size:8px;color:var(--mut);text-align:center;margin-top:3px;}
.errt{font-size:8px;color:var(--bear);text-align:center;margin-top:3px;}
</style>
</head>
<body>
<header>
  <div class="logo">
    <div class="logo-icon">📡</div>
    <div><h1>EMA 200 Scanner</h1><p>Deriv Volatility · Live Data</p></div>
  </div>
  <button class="scan-btn" id="scanBtn" onclick="runScan()">Scan Now</button>
</header>
<div class="sbar">
  <div style="display:flex;align-items:center;">
    <span class="dot" id="sDot"></span>
    <span class="stxt" id="sTxt">Ready — tap Scan Now</span>
  </div>
  <span class="stime" id="sTime"></span>
</div>
<div class="pbar"><div class="pfill" id="pFill"></div></div>
<div class="dbg" id="dbgBox">
  <h4>⚠️ Connection Status / Debug Logs</h4>
  <pre id="dbgTxt"></pre>
</div>
<div class="row">
  <label style="font-size:11px;color:var(--mut);white-space:nowrap;">Auto:</label>
  <select id="autoInt" onchange="setAuto()">
    <option value="0">Off</option>
    <option value="60">1 min</option>
    <option value="300">5 min</option>
    <option value="900">15 min</option>
  </select>
  <label class="stog"><input type="checkbox" id="snd" checked> 🔔 Sound</label>
</div>
<div class="apanel">
  <h3>🔥 Live Signals</h3>
  <div id="alertList"><div class="empty">No signals yet — tap Scan Now</div></div>
</div>
<div class="grid" id="grid"></div>
<script>
var PAIRS=[
  {n:"Volatility 10", s:"VIX10",  sym:"R_10"},
  {n:"Volatility 25", s:"VIX25",  sym:"R_25"},
  {n:"Volatility 50", s:"VIX50",  sym:"R_50"},
  {n:"Volatility 75", s:"VIX75",  sym:"R_75"},
  {n:"Volatility 100",s:"VIX100", sym:"R_100"},
  {n:"Crash 1000",    s:"CRASH",  sym:"CRASH1000INDEX"},
  {n:"Boom 1000",     s:"BOOM",   sym:"BOOM1000INDEX"},
  {n:"Step Index",    s:"STEP",   sym:"stpRNG"}
];
var EP1="wss://ws.derivws.com/websockets/v3?app_id=1089";
var EP2="wss://ws.binaryws.com/websockets/v3?app_id=1089";
var ENDPOINTS=[EP1,EP2];
var st={},alerts=[],autoTmr=null,scanning=false;
var ws=null,pending={},rid=1;
var pingTimer=null,reconnectTimer=null,intentionalClose=false;
var debugLog=[];
PAIRS.forEach(function(p){
  st[p.sym]={n:p.n,s:p.s,sym:p.sym,status:"none",price:null,prevPrice:null,ema:{},tf:{"1D":null,"4H":null,"1H":null},m15:{bounce:false,candle:false},loading:false,err:null};
});
function dbgLog(msg){
  var t=new Date().toLocaleTimeString();
  debugLog.push(t+": "+msg);
  if(debugLog.length>40)debugLog.shift();
  var box=document.getElementById("dbgBox");
  var pre=document.getElementById("dbgTxt");
  box.style.display="block";
  pre.textContent=debugLog.join("\n");
  pre.scrollTop=pre.scrollHeight;
}
function dbgClear(){
  debugLog=[];
  document.getElementById("dbgBox").style.display="none";
  document.getElementById("dbgTxt").textContent="";
}
function calcEMA(closes,period){
  if(closes.length<period)return null;
  var k=2/(period+1),e=0,i;
  for(i=0;i<period;i++)e+=closes[i];
  e/=period;
  for(i=period;i<closes.length;i++)e=closes[i]*k+e*(1-k);
  return e;
}
function candlePattern(candles){
  if(candles.length<2)return false;
  var c=candles[candles.length-1],p=candles[candles.length-2];
  var body=Math.abs(c.close-c.open);
  if(body===0)return false;
  var lo=Math.min(c.close,c.open)-c.low;
  var hi=c.high-Math.max(c.close,c.open);
  var pin=lo>body*2||hi>body*2;
  var eng=body>Math.abs(p.close-p.open)*1.1&&((c.close>c.open&&p.close<p.open)||(c.close<c.open&&p.close>p.open));
  return pin||eng;
}
function startPing(){
  stopPing();
  pingTimer=setInterval(function(){
    if(ws&&ws.readyState===1){try{ws.send('{"ping":1}');}catch(e){dbgLog("Ping err: "+e);}}
  },30000);
}
function stopPing(){if(pingTimer){clearInterval(pingTimer);pingTimer=null;}}
function scheduleReconnect(){
  if(reconnectTimer||intentionalClose)return;
  setStatus("Disconnected — reconnecting…","warn");
  reconnectTimer=setTimeout(function(){
    reconnectTimer=null;
    connectWS().catch(function(e){dbgLog("Reconnect failed: "+e.message);scheduleReconnect();});
  },3000);
}
function connectWS(){
  dbgClear();
  return new Promise(function(resolve,reject){
    var tried=0,errors=[];
    function tryNext(){
      if(tried>=ENDPOINTS.length){reject(new Error("All endpoints failed:\n"+errors.join("\n")));return;}
      var url=ENDPOINTS[tried++];
      dbgLog("Trying: "+url);
      var sock;
      try{sock=new WebSocket(url);}
      catch(e){var es="WebSocket() threw: "+e.name+" — "+e.message;dbgLog(es);errors.push(url+" → "+es);tryNext();return;}
      var t=setTimeout(function(){var es=url+" → Timeout (readyState="+sock.readyState+")";dbgLog(es);errors.push(es);try{sock.close();}catch(x){}tryNext();},9000);
      sock.onopen=function(){clearTimeout(t);ws=sock;intentionalClose=false;attachHandlers(sock);startPing();setStatus("Connected to Deriv","live");dbgClear();resolve(sock);};
      sock.onerror=function(ev){clearTimeout(t);var es=url+" → onerror | readyState="+sock.readyState;dbgLog(es);errors.push(es);try{sock.close();}catch(x){}tryNext();};
      sock.onclose=function(ev){clearTimeout(t);if(ws!==sock)dbgLog(url+" → closed before open | code="+ev.code);};
    }
    tryNext();
  });
}
function attachHandlers(sock){
  sock.onmessage=function(e){
    try{
      var d=JSON.parse(e.data);
      if(d.msg_type==="ping")return;
      if(d.msg_type==="tick"&&d.tick){
        var sym=d.tick.symbol,price=parseFloat(d.tick.quote);
        if(st[sym]){st[sym].prevPrice=st[sym].price;st[sym].price=price;updateLiveTick(sym,price);}
        return;
      }
      var id=d.req_id;
      if(id&&pending[id]){var cb=pending[id];delete pending[id];if(d.error)cb.rej(new Error(d.error.message||"API error"));else cb.res(d);}
    }catch(ex){dbgLog("MSG err: "+ex);}
  };
  sock.onclose=function(ev){ws=null;stopPing();dbgLog("WS closed: code="+ev.code+" wasClean="+ev.wasClean);if(!intentionalClose)scheduleReconnect();};
  sock.onerror=function(ev){dbgLog("WS error: "+ev.type);};
}
function updateLiveTick(sym,price){
  var el=document.getElementById("price-"+sym);
  if(!el)return;
  var s=st[sym];
  var dir=(s.prevPrice&&price>s.prevPrice)?"up":(s.prevPrice&&price<s.prevPrice)?"dn":"";
  var dp=price>100?2:5;
  el.innerHTML='<span class="pxtick'+(dir==="dn"?" dn":"")+'">'+(dir==="up"?"▲":dir==="dn"?"▼":"●")+" "+price.toFixed(dp)+"</span>";
}
function send(payload){
  return new Promise(function(res,rej){
    if(!ws||ws.readyState!==1){rej(new Error("Not connected"));return;}
    var id=rid++;payload.req_id=id;
    var t=setTimeout(function(){if(pending[id]){delete pending[id];rej(new Error("Timeout"));}},20000);
    pending[id]={res:function(d){clearTimeout(t);res(d);},rej:function(e){clearTimeout(t);rej(e);}};
    try{ws.send(JSON.stringify(payload));}catch(e){delete pending[id];clearTimeout(t);rej(e);}
  });
}
function subscribeTicks(){
  PAIRS.forEach(function(pair){
    if(ws&&ws.readyState===1){try{ws.send(JSON.stringify({ticks:pair.sym,subscribe:1}));}catch(e){}}
  });
}
function getCandles(sym,gran,count){
  return send({ticks_history:sym,end:"latest",count:count,granularity:gran,style:"candles",adjust_start_time:1}).then(function(d){
    if(!d.candles||!d.candles.length)throw new Error("No data");
    return d.candles.map(function(c){return{open:+c.open,high:+c.high,low:+c.low,close:+c.close};});
  });
}
function analyzePair(pair){
  var s=st[pair.sym];s.loading=true;s.err=null;updateCard(pair.sym);
  return Promise.all([getCandles(pair.sym,1440,220),getCandles(pair.sym,240,220),getCandles(pair.sym,60,220),getCandles(pair.sym,15,25)]).then(function(r){
    var c1D=r[0],c4H=r[1],c1H=r[2],c15=r[3];
    var price=c15[c15.length-1].close;s.price=price;
    var e1D=calcEMA(c1D.map(function(c){return c.close;}),200);
    var e4H=calcEMA(c4H.map(function(c){return c.close;}),200);
    var e1H=calcEMA(c1H.map(function(c){return c.close;}),200);
    var e15v=calcEMA(c15.map(function(c){return c.close;}),Math.min(15,c15.length-1));
    s.ema={"1D":e1D,"4H":e4H,"1H":e1H,"M15":e15v};
    var d1D=e1D?(price>e1D?"bull":"bear"):null;
    var d4H=e4H?(price>e4H?"bull":"bear"):null;
    var d1H=e1H?(price>e1H?"bull":"bear"):null;
    s.tf={"1D":d1D,"4H":d4H,"1H":d1H};
    var aligned=d1D&&d4H&&d1H&&d1D===d4H&&d4H===d1H;
    var bounce=e15v!==null&&Math.abs(price-e15v)/e15v<0.005;
    var candle=candlePattern(c15);
    s.m15={bounce:bounce,candle:candle};
    if(aligned&&bounce&&candle)s.status=d1D==="bull"?"signal_bull":"signal_bear";
    else if(aligned)s.status=d1D==="bull"?"aligned_bull":"aligned_bear";
    else s.status="none";
    s.loading=false;updateCard(pair.sym);return s;
  }).catch(function(ex){s.err=ex.message.length>25?"Fetch failed":ex.message;s.status="none";s.loading=false;updateCard(pair.sym);return s;});
}
function updateCard(sym){
  var s=st[sym];
  var card=document.getElementById("card-"+sym);
  if(!card)return;
  card.className="card"+(s.loading?" loading":s.status==="signal_bull"||s.status==="aligned_bull"?" bull":s.status==="signal_bear"||s.status==="aligned_bear"?" bear":"");
  var badge=document.getElementById("badge-"+sym);
  if(badge){
    if(s.loading){badge.className="badge bl";badge.textContent="LOADING";}
    else if(s.status==="signal_bull"){badge.className="badge bsig";badge.textContent="▲ BUY";}
    else if(s.status==="signal_bear"){badge.className="badge bsig";badge.textContent="▼ SELL";}
    else if(s.status==="aligned_bull"){badge.className="badge bb";badge.textContent="BULLISH";}
    else if(s.status==="aligned_bear"){badge.className="badge bs";badge.textContent="BEARISH";}
    else{badge.className="badge bw";badge.textContent="WAIT";}
  }
  var pxEl=document.getElementById("price-"+sym);
  if(pxEl&&s.price&&!s.loading){var dp=s.price>100?2:5;pxEl.innerHTML='<span class="pxtick">● '+s.price.toFixed(dp)+"</span>";}
  var tfsEl=document.getElementById("tfs-"+sym);
  if(tfsEl){tfsEl.innerHTML=["1D","4H","1H"].map(function(tf){var v=s.tf[tf],cl="no",lb="—";if(v==="bull"){cl="bu";lb="▲";}if(v==="bear"){cl="be";lb="▼";}return'<div class="tf '+cl+'"><span class="tfl">'+tf+"</span>"+lb+"</div>";}).join("");}
  var b=document.getElementById("cc-bounce-"+sym);
  var c=document.getElementById("cc-candle-"+sym);
  var emv=document.getElementById("emav-"+sym);
  var ert=document.getElementById("errt-"+sym);
  if(b)b.className="cc"+(s.m15.bounce?" on":"");
  if(c)c.className="cc"+(s.m15.candle?" on":"");
  if(emv){var e15=s.ema["M15"];emv.textContent=e15?"EMA ~"+e15.toFixed(e15>100?2:5):"";}
  if(ert)ert.textContent=s.err||"";
}
function buildGrid(){
  var g=document.getElementById("grid");g.innerHTML="";
  PAIRS.forEach(function(pair){
    var div=document.createElement("div");
    div.className="card";div.id="card-"+pair.sym;
    div.innerHTML='<div class="ch"><span class="cn">'+pair.s+'</span><span class="badge bw" id="badge-'+pair.sym+'">WAIT</span></div>'
      +'<div class="cpx" id="price-'+pair.sym+'">—</div>'
      +'<div class="tfs" id="tfs-'+pair.sym+'">'+["1D","4H","1H"].map(function(tf){return'<div class="tf no"><span class="tfl">'+tf+"</span>—</div>";}).join("")+"</div>"
      +'<div class="m15"><div class="m15l">M15 CONFIRM</div>'
      +'<div class="ccs"><div class="cc" id="cc-bounce-'+pair.sym+'">Bounce</div><div class="cc" id="cc-candle-'+pair.sym+'">Pattern</div></div>'
      +'<div class="emav" id="emav-'+pair.sym+'"></div><div class="errt" id="errt-'+pair.sym+'"></div></div>';
    g.appendChild(div);
  });
}
function runScan(){
  if(scanning)return;scanning=true;
  var btn=document.getElementById("scanBtn");btn.disabled=true;btn.textContent="Scanning…";
  setStatus("Connecting…","");setP(0);
  var doScan=function(){
    setStatus("Fetching live candles…","live");
    var newAlerts=[],chain=Promise.resolve();
    PAIRS.forEach(function(pair,i){
      chain=chain.then(function(){
        setStatus("Scanning "+pair.s+" ("+(i+1)+"/"+PAIRS.length+")…","live");
        setP(Math.round((i/PAIRS.length)*100));
        return analyzePair(pair).then(function(s){
          if(s.status==="signal_bull"||s.status==="signal_bear"){
            var type=s.status==="signal_bull"?"bull":"bear";
            var dup=alerts.filter(function(a){return a.sym===pair.sym&&Date.now()-a.ts<90000&&a.type===type;}).length>0;
            if(!dup){newAlerts.push({sym:pair.sym,pair:s.s,type:type,time:new Date(),ts:Date.now()});playAlert(type);}
          }
        });
      });
    });
    return chain.then(function(){
      alerts=newAlerts.concat(alerts).slice(0,12);renderAlerts();setP(100);
      setStatus("Done · "+PAIRS.length+" pairs · "+new Date().toLocaleTimeString(),"live");
      document.getElementById("sTime").textContent=new Date().toLocaleTimeString([],{hour:"2-digit",minute:"2-digit"});
      btn.disabled=false;btn.textContent="Scan Now";scanning=false;
      subscribeTicks();
    });
  };
  var ensureConn=(ws&&ws.readyState===1)?Promise.resolve():connectWS();
  ensureConn.then(doScan).catch(function(ex){setStatus("Failed — see debug below","err");dbgLog("SCAN FAILED: "+ex.message);setP(0);btn.disabled=false;btn.textContent="Scan Now";scanning=false;});
}
function renderAlerts(){
  var l=document.getElementById("alertList");
  if(!alerts.length){l.innerHTML='<div class="empty">No signals yet — tap Scan Now</div>';return;}
  l.innerHTML=alerts.map(function(a){var dir=a.type==="bull"?"▲ BUY SIGNAL":"▼ SELL SIGNAL";var clr=a.type==="bull"?"var(--bull)":"var(--bear)";return'<div class="ai '+(a.type==="bull"?"b":"s")+'"><div class="adot '+(a.type==="bull"?"b":"s")+'"></div><div class="at"><div class="ap">'+a.pair+' <span style="color:'+clr+';font-weight:500;">'+dir+'</span></div><div class="ad">1D/4H/1H '+(a.type==="bull"?"above":"below")+' EMA 200 · M15 bounce + pattern confirmed</div></div><div class="atime">'+a.time.toLocaleTimeString([],{hour:"2-digit",minute:"2-digit"})+"</div></div>";}).join("");
}
function playAlert(type){
  if(!document.getElementById("snd").checked)return;
  try{var ctx=new(window.AudioContext||window.webkitAudioContext)();var freqs=type==="bull"?[330,440,550]:[550,440,330];freqs.forEach(function(f,i){var o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.frequency.value=f;o.type="sine";var t=ctx.currentTime+i*0.13;g.gain.setValueAtTime(0.18,t);g.gain.exponentialRampToValueAtTime(0.001,t+0.22);o.start(t);o.stop(t+0.25);});}catch(e){}
}
function setStatus(t,type){document.getElementById("sTxt").textContent=t;document.getElementById("sDot").className="dot"+(type?" "+type:"");}
function setP(v){document.getElementById("pFill").style.width=v+"%";}
function setAuto(){
  if(autoTmr)clearInterval(autoTmr);
  var v=parseInt(document.getElementById("autoInt").value);
  if(v>0){autoTmr=setInterval(runScan,v*1000);setStatus("Auto-scan every "+(v>=60?v/60+" min":v+"s"),"live");}
}
document.addEventListener("visibilitychange",function(){
  if(!document.hidden&&(!ws||ws.readyState!==1))connectWS().then(subscribeTicks).catch(function(){});
});
buildGrid();
renderAlerts();
</script>
</body>
</html>

```
