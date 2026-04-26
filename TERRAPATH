<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Maasai Mara Safari Tracker</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/proj4js/2.9.0/proj4.js"></script>
<style>
:root{--bg:#080f04;--sidebar:#0b1508;--card:#0f1f0a;--border:#2a4a18;--gold:#f0c040;--muted:#7a9a6a;}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Segoe UI',sans-serif;background:var(--bg);color:#e8f5e9;display:flex;flex-direction:column;height:100vh;overflow:hidden;}
#header{background:linear-gradient(90deg,#0a1f05,#0d2a08,#0a1f05);border-bottom:1px solid var(--border);padding:8px 16px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;box-shadow:0 2px 12px rgba(0,0,0,.6);}
#hLeft{display:flex;align-items:center;gap:10px;}
#hLogo{font-size:1.8em;}
#hText h1{font-size:0.9em;font-weight:700;color:var(--gold);letter-spacing:.5px;}
#hText p{font-size:0.62em;color:var(--muted);margin-top:1px;}
#hRight{display:flex;gap:6px;flex-wrap:wrap;align-items:center;}
.hbtn{display:flex;align-items:center;gap:5px;padding:6px 12px;border:none;border-radius:6px;cursor:pointer;font-weight:600;font-size:0.7em;transition:filter .2s;}
.hbtn:hover{filter:brightness(1.25);}
.hbtn-green{background:#1b5e20;color:#a5d6a7;}
.hbtn-amber{background:#4e2a00;color:#ffcc80;}
.hbtn-blue{background:#01304a;color:#81d4fa;}
.hbtn-red{background:#3e0000;color:#ef9a9a;}
.hbtn-sos{background:#7b0000;color:#ff5252;border:1.5px solid #ff1744;font-size:0.72em;letter-spacing:1px;}
.hbtn-sos:hover{background:#a00000;}
#liveTag{display:flex;align-items:center;gap:5px;font-size:0.68em;color:#69f0ae;font-weight:600;}
.liveDot{width:7px;height:7px;border-radius:50%;background:#69f0ae;animation:pulse 1.4s infinite;}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.4;transform:scale(1.3)}}
#main{display:flex;flex:1;overflow:hidden;}
#map{flex:1;min-height:0;}
#sidebar{width:250px;background:var(--sidebar);border-left:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden;}
.scard{padding:9px;border-bottom:1px solid var(--border);}
.scard-head{display:flex;align-items:center;justify-content:space-between;margin-bottom:7px;}
.scard-head h3{font-size:0.74em;font-weight:700;color:var(--gold);display:flex;align-items:center;gap:5px;}
.stag{font-size:0.6em;background:#1a3a0a;color:#8bc34a;padding:1px 7px;border-radius:10px;}
#carList{display:flex;flex-direction:column;gap:4px;max-height:230px;overflow-y:auto;padding-right:2px;}
#carList::-webkit-scrollbar{width:3px;}
#carList::-webkit-scrollbar-thumb{background:#2a4a18;}
.crow{background:var(--card);border:1px solid var(--border);border-radius:7px;padding:6px 8px;display:flex;flex-direction:column;gap:3px;transition:border-color .2s;}
.crow:hover{border-color:#4a8a28;}
.crow-top{display:flex;align-items:center;gap:5px;}
.cdot{width:9px;height:9px;border-radius:50%;flex-shrink:0;}
.cname{font-weight:700;font-size:0.72em;flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.badge{padding:1px 6px;border-radius:10px;font-size:0.6em;font-weight:700;}
.on{background:#1b3a0a;color:#69f0ae;border:1px solid #2a5a18;}
.off{background:#3e0000;color:#ff5252;border:1px solid #5a0000;animation:blink .6s infinite;}
.sos-badge{background:#7b0000;color:#ff5252;border:1px solid #ff1744;animation:blink .4s infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.4}}
.crow-mid{display:flex;align-items:center;gap:5px;font-size:0.62em;color:var(--muted);}
.spbar-wrap{flex:1;height:3px;background:#1a2a0a;border-radius:2px;}
.spbar{height:3px;border-radius:2px;transition:width .4s,background .4s;}
.crow-btns{display:flex;gap:4px;justify-content:flex-end;flex-wrap:wrap;}
.cbtn{padding:2px 7px;font-size:0.62em;border-radius:4px;border:none;cursor:pointer;font-weight:700;transition:filter .15s;}
.cbtn:hover{filter:brightness(1.3);}
.cbtn-notify{background:#01304a;color:#81d4fa;}
.cbtn-remove{background:#3e0000;color:#ef9a9a;}
.cbtn-sos{background:#7b0000;color:#ff5252;border:1px solid #ff1744;letter-spacing:.5px;}
#alertScroll{overflow-y:auto;flex:1;padding:7px;}
#alertScroll::-webkit-scrollbar{width:3px;}
#alertScroll::-webkit-scrollbar-thumb{background:#3a1000;}
.arow{display:flex;gap:6px;align-items:flex-start;padding:3px 0;border-bottom:1px solid #1a0a00;}
.aicon{font-size:0.85em;margin-top:1px;}
.atext{font-size:0.66em;line-height:1.5;color:#ffab91;}
.atime{font-size:0.57em;color:#5a3a2a;white-space:nowrap;}
.arow-sos .atext{color:#ff5252;font-weight:700;}
#logBox{height:100px;overflow-y:auto;padding:7px;border-top:1px solid var(--border);}
#logBox::-webkit-scrollbar{width:3px;}
#logBox::-webkit-scrollbar-thumb{background:#1a3a0a;}
.lrow{font-size:0.64em;color:#7cb87c;padding:2px 0;border-bottom:1px solid #0d1a0a;line-height:1.5;}
#coordBar{background:#060e03;padding:3px 10px;font-size:0.63em;color:#4a7a3a;border-top:1px solid var(--border);display:flex;justify-content:space-between;}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:9000;align-items:center;justify-content:center;backdrop-filter:blur(3px);}
.modal-bg.show{display:flex;}
.mbox{background:#0b1a06;border:1px solid #3a6a18;border-radius:12px;padding:20px;width:320px;display:flex;flex-direction:column;gap:11px;box-shadow:0 8px 40px rgba(0,0,0,.8);}
.mbox h2{color:var(--gold);font-size:0.92em;display:flex;align-items:center;gap:7px;}
.mfield label{display:block;font-size:0.67em;color:var(--muted);margin-bottom:3px;font-weight:600;}
.mfield input,.mfield select,.mfield textarea{width:100%;padding:6px 9px;background:#060e03;border:1px solid var(--border);border-radius:6px;color:#e8f5e9;font-size:0.74em;outline:none;transition:border-color .2s;font-family:inherit;}
.mfield input:focus,.mfield select:focus,.mfield textarea:focus{border-color:#4a8a28;}
.mfield textarea{resize:vertical;min-height:65px;}
.mbtns{display:flex;gap:8px;justify-content:flex-end;}
.mbtn{padding:6px 15px;border:none;border-radius:6px;cursor:pointer;font-weight:700;font-size:0.72em;}
.mbtn-cancel{background:#1a0a00;color:#ef9a9a;border:1px solid #3e0000;}
.mbtn-confirm{background:#1b5e20;color:#a5d6a7;border:1px solid #2d8a30;}
.mbtn-sos-confirm{background:#7b0000;color:#ff5252;border:1px solid #ff1744;}
#notifyInfo{background:#060e03;border:1px solid var(--border);border-radius:8px;padding:9px;display:flex;flex-direction:column;gap:5px;}
#notifyInfo .ni-row{display:flex;justify-content:space-between;font-size:0.68em;}
#notifyInfo .ni-label{color:var(--muted);}
#notifyInfo .ni-val{font-weight:700;color:#e8f5e9;}
#notifyCarName{font-size:0.95em;font-weight:700;margin-bottom:3px;}
#toast{position:fixed;bottom:22px;left:50%;transform:translateX(-50%) translateY(20px);background:#0d2a06;border:1px solid #3a6a18;color:#c8e6c9;padding:8px 18px;border-radius:22px;font-size:0.74em;font-weight:600;z-index:99999;opacity:0;transition:opacity .3s,transform .3s;pointer-events:none;display:flex;align-items:center;gap:7px;box-shadow:0 4px 20px rgba(0,0,0,.6);}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0);}
#mapLegend{position:absolute;bottom:28px;left:10px;z-index:1000;background:rgba(5,14,2,.88);border:1px solid #2a4a18;border-radius:8px;padding:8px 12px;font-size:0.67em;color:#c8e6c9;display:flex;flex-direction:column;gap:4px;}
.leg-row{display:flex;align-items:center;gap:7px;}
.leg-line{width:22px;height:4px;border-radius:2px;}

/* ── SOS Modal ── */
#sosModal .mbox{border-color:#ff1744;background:#1a0000;}
#sosModal h2{color:#ff5252;}
#sosInfo{background:#0d0000;border:1px solid #5a0000;border-radius:8px;padding:9px;display:flex;flex-direction:column;gap:5px;}
#sosInfo .ni-row{display:flex;justify-content:space-between;font-size:0.68em;}
#sosInfo .ni-label{color:#c07070;}
#sosInfo .ni-val{font-weight:700;color:#ffcdd2;}
#sosCarName{font-size:0.95em;font-weight:700;margin-bottom:3px;color:#ff5252;}
.sos-types{display:flex;flex-wrap:wrap;gap:5px;}
.sos-type-btn{padding:5px 10px;border-radius:6px;border:1px solid #5a0000;background:#2a0000;color:#ff8a80;font-size:0.68em;font-weight:600;cursor:pointer;transition:all .2s;}
.sos-type-btn:hover,.sos-type-btn.selected{background:#7b0000;border-color:#ff1744;color:#fff;}

/* ── SOS Popup Overlay ── */
#sosOverlay{display:none;position:fixed;inset:0;z-index:99000;pointer-events:none;}
#sosOverlay.show{display:block;}
#sosPopup{position:absolute;top:50%;left:50%;transform:translate(-50%,-60%);pointer-events:all;
  background:linear-gradient(135deg,#1a0000,#2d0000);border:2px solid #ff1744;border-radius:16px;
  padding:24px 28px;width:360px;box-shadow:0 0 60px rgba(255,23,68,.5),0 8px 40px rgba(0,0,0,.9);
  animation:sosEntry .35s cubic-bezier(.22,1,.36,1);}
@keyframes sosEntry{from{transform:translate(-50%,-55%) scale(.85);opacity:0}to{transform:translate(-50%,-60%) scale(1);opacity:1}}
#sosPopup .sos-flash{animation:sosFlash 1s infinite;}
@keyframes sosFlash{0%,100%{text-shadow:0 0 20px #ff1744,0 0 40px #ff1744}50%{text-shadow:none}}
#sosPopup h2{color:#ff1744;font-size:1.3em;display:flex;align-items:center;gap:10px;margin-bottom:10px;}
#sosPopup .sos-vehicle{font-size:1em;font-weight:700;margin-bottom:4px;}
#sosPopup .sos-details{font-size:0.74em;line-height:1.9;color:#ffcdd2;margin-bottom:14px;background:#0d0000;border-radius:8px;padding:8px 12px;border:1px solid #3a0000;}
#sosPopup .sos-actions{display:flex;gap:8px;}
#sosPopup .sos-dismiss{flex:1;padding:8px;border-radius:7px;border:1px solid #5a0000;background:#2a0000;color:#ff8a80;font-weight:700;font-size:0.74em;cursor:pointer;}
#sosPopup .sos-dismiss:hover{background:#3a0000;}
#sosPopup .sos-respond{flex:1;padding:8px;border-radius:7px;border:1px solid #ff1744;background:#7b0000;color:#fff;font-weight:700;font-size:0.74em;cursor:pointer;}
#sosPopup .sos-respond:hover{background:#a00000;}
#sosOverlayBg{display:none;position:fixed;inset:0;background:rgba(80,0,0,.18);z-index:98999;animation:sosBgPulse 1.2s infinite;}
#sosOverlayBg.show{display:block;}
@keyframes sosBgPulse{0%,100%{opacity:0}50%{opacity:1}}
#sosBadgeBar{display:none;position:fixed;top:0;left:0;right:0;z-index:97000;background:#7b0000;border-bottom:2px solid #ff1744;padding:5px 16px;font-size:0.72em;font-weight:700;color:#ff5252;display:none;align-items:center;gap:10px;animation:blink .6s infinite;}
#sosBadgeBar.show{display:flex;}
</style>
</head>
<body>

<div id="sosBadgeBar" id="sosBadgeBar">
  🆘 <span id="sosBadgeText">SOS ACTIVE</span>
  <button onclick="dismissAllSOS()" style="margin-left:auto;padding:2px 10px;border-radius:4px;border:1px solid #ff5252;background:#3a0000;color:#ff5252;cursor:pointer;font-weight:700;font-size:0.85em;">Dismiss All</button>
</div>

<div id="header">
  <div id="hLeft">
    <div id="hLogo">🦁</div>
    <div id="hText">
      <h1>Maasai Mara National Reserve — Safari Vehicle Tracker</h1>
      <p>📍 Real GeoJSON map layers · GPS tracking · Off-route detection · Speed limit 99 km/h</p>
    </div>
  </div>
  <div id="hRight">
    <div id="liveTag"><div class="liveDot"></div>LIVE</div>
    <button class="hbtn hbtn-green" onclick="openModal('addModal')">➕ Add Vehicle</button>
    <button class="hbtn hbtn-amber" id="btnOffRoute">⚠️ Force Off-Route</button>
    <button class="hbtn hbtn-sos" id="btnTestSOS">🆘 Test SOS</button>
    <button class="hbtn hbtn-blue" id="btnPause">⏸ Pause</button>
    <button class="hbtn hbtn-red" id="btnReset">🔄 Reset</button>
  </div>
</div>

<div id="main">
  <div id="map" style="position:relative;">
    <div id="mapLegend">
      <div style="color:#f0c040;font-weight:700;margin-bottom:3px;">Map Layers</div>
      <div class="leg-row"><div class="leg-line" style="background:#f0c040;"></div>Reserve Boundary</div>
      <div class="leg-row"><div class="leg-line" style="background:#ff6d00;height:6px;"></div>Major Roads Buffer</div>
      <div class="leg-row"><div class="leg-line" style="background:#8B6914;"></div>Minor Roads Buffer</div>
      <div class="leg-row"><div class="leg-line" style="background:#ff4444;height:2px;"></div>Major Routes</div>
    </div>
  </div>
  <div id="sidebar">
    <div class="scard">
      <div class="scard-head">
        <h3>🚙 Vehicles <span class="stag" id="vcount">0</span></h3>
      </div>
      <div id="carList"></div>
    </div>
    <div class="scard" style="flex:1;overflow:hidden;display:flex;flex-direction:column;padding-bottom:0;">
      <div class="scard-head" style="padding-bottom:5px;">
        <h3>🚨 Alerts</h3>
        <button class="cbtn cbtn-remove" style="font-size:0.58em;" onclick="document.getElementById('alertScroll').innerHTML=''">Clear</button>
      </div>
      <div id="alertScroll"></div>
    </div>
    <div id="logBox"></div>
  </div>
</div>
<div id="coordBar">
  <span id="coordText">🌍 Hover map for coordinates</span>
  <span>Maasai Mara NR · EPSG:32737 → WGS84</span>
</div>

<!-- Add Vehicle Modal -->
<div class="modal-bg" id="addModal">
  <div class="mbox">
    <h2>➕ Add Safari Vehicle</h2>
    <div class="mfield"><label>Vehicle Name</label><input id="vName" placeholder="e.g. Ranger 06" maxlength="20"/></div>
    <div class="mfield"><label>Vehicle Type</label>
      <select id="vType"><option>Jeep</option><option>Van</option><option>Bus</option><option>Land Cruiser</option><option>Ranger</option></select>
    </div>
    <div class="mfield"><label>Route</label>
      <select id="vRoute">
        <option value="0">Major Route 1 (North Loop)</option>
        <option value="1">Major Route 2 (South-East)</option>
        <option value="2">Major Route 3 (West Loop)</option>
      </select>
    </div>
    <div class="mfield"><label>Speed — <span id="speedVal">45</span> km/h</label>
      <input type="range" id="vSpeed" min="5" max="99" value="45" oninput="document.getElementById('speedVal').textContent=this.value"/>
    </div>
    <div class="mfield"><label>Color</label><input type="color" id="vColor" value="#00e5ff" style="height:32px;padding:2px;"/></div>
    <div class="mbtns">
      <button class="mbtn mbtn-cancel" onclick="closeModal('addModal')">Cancel</button>
      <button class="mbtn mbtn-confirm" onclick="addVehicle()">Add Vehicle</button>
    </div>
  </div>
</div>

<!-- Notify Modal -->
<div class="modal-bg" id="notifyModal">
  <div class="mbox" style="width:340px;">
    <h2>📣 Send Notification</h2>
    <div id="notifyInfo">
      <div id="notifyCarName"></div>
      <div class="ni-row"><span class="ni-label">Route</span><span class="ni-val" id="ni-route"></span></div>
      <div class="ni-row"><span class="ni-label">Speed</span><span class="ni-val" id="ni-speed"></span></div>
      <div class="ni-row"><span class="ni-label">Status</span><span class="ni-val" id="ni-status"></span></div>
      <div class="ni-row"><span class="ni-label">Position (UTM)</span><span class="ni-val" id="ni-pos"></span></div>
    </div>
    <div class="mfield">
      <label>⚠️ Warning / Message to Driver</label>
      <textarea id="notifyMsg" placeholder="e.g. Slow down — elephant crossing ahead."></textarea>
    </div>
    <div class="mbtns">
      <button class="mbtn mbtn-cancel" onclick="closeModal('notifyModal')">Cancel</button>
      <button class="mbtn mbtn-confirm" onclick="sendNotify()">📤 Send</button>
    </div>
  </div>
</div>

<!-- SOS Dispatch Modal -->
<div class="modal-bg" id="sosModal">
  <div class="mbox" style="width:360px;">
    <h2>🆘 Send SOS Alert</h2>
    <div id="sosInfo">
      <div id="sosCarName"></div>
      <div class="ni-row"><span class="ni-label">Route</span><span class="ni-val" id="sos-route"></span></div>
      <div class="ni-row"><span class="ni-label">Speed</span><span class="ni-val" id="sos-speed"></span></div>
      <div class="ni-row"><span class="ni-label">Status</span><span class="ni-val" id="sos-status"></span></div>
      <div class="ni-row"><span class="ni-label">GPS (UTM)</span><span class="ni-val" id="sos-pos"></span></div>
    </div>
    <div class="mfield">
      <label>Emergency Type</label>
      <div class="sos-types" id="sosTypeButtons">
        <div class="sos-type-btn selected" onclick="selectSosType(this,'🦁 Wildlife Encounter')">🦁 Wildlife</div>
        <div class="sos-type-btn" onclick="selectSosType(this,'🚗 Vehicle Breakdown')">🚗 Breakdown</div>
        <div class="sos-type-btn" onclick="selectSosType(this,'🤕 Medical Emergency')">🤕 Medical</div>
        <div class="sos-type-btn" onclick="selectSosType(this,'🔥 Fire / Hazard')">🔥 Fire/Hazard</div>
        <div class="sos-type-btn" onclick="selectSosType(this,'🧭 Lost / Off-Track')">🧭 Lost</div>
        <div class="sos-type-btn" onclick="selectSosType(this,'⚠️ General Emergency')">⚠️ General</div>
      </div>
    </div>
    <div class="mfield">
      <label>Additional Details (optional)</label>
      <textarea id="sosDetails" placeholder="e.g. Engine stalled, 3 passengers, need ranger assistance ASAP." style="border-color:#5a0000;"></textarea>
    </div>
    <div class="mbtns">
      <button class="mbtn mbtn-cancel" onclick="closeModal('sosModal')">Cancel</button>
      <button class="mbtn mbtn-sos-confirm" onclick="dispatchSOS()">🆘 Dispatch SOS</button>
    </div>
  </div>
</div>

<!-- SOS Dashboard Overlay -->
<div id="sosOverlayBg"></div>
<div id="sosOverlay">
  <div id="sosPopup">
    <h2><span class="sos-flash">🆘</span> <span id="sosPopupTitle">SOS ALERT</span></h2>
    <div class="sos-vehicle" id="sosPopupVehicle"></div>
    <div class="sos-details" id="sosPopupDetails"></div>
    <div class="sos-actions">
      <button class="sos-dismiss" onclick="dismissSOS()">✕ Dismiss</button>
      <button class="sos-respond" onclick="respondSOS()">📡 Respond &amp; Dispatch</button>
    </div>
  </div>
</div>

<div id="toast"><span id="toastIcon">✅</span><span id="toastMsg"></span></div>

<script>
proj4.defs('EPSG:32737','+proj=utm +zone=37 +south +datum=WGS84 +units=m +no_defs');
function utmToLatLng(x,y){const[lng,lat]=proj4('EPSG:32737','WGS84',[x,y]);return[lat,lng];}
function convertGeoJSON(gj){
  const clone=JSON.parse(JSON.stringify(gj));
  clone.features.forEach(f=>{
    const g=f.geometry;
    if(g.type==='Polygon')g.coordinates=g.coordinates.map(r=>r.map(c=>{const ll=utmToLatLng(c[0],c[1]);return[ll[1],ll[0]];}));
    if(g.type==='MultiPolygon')g.coordinates=g.coordinates.map(p=>p.map(r=>r.map(c=>{const ll=utmToLatLng(c[0],c[1]);return[ll[1],ll[0]];})));
    if(g.type==='LineString')g.coordinates=g.geometry.coordinates.map(c=>{const ll=utmToLatLng(c[0],c[1]);return[ll[1],ll[0]];});
    if(g.type==='MultiLineString')g.coordinates=g.coordinates.map(l=>l.map(c=>{const ll=utmToLatLng(c[0],c[1]);return[ll[1],ll[0]];}));
  });
  return clone;
}

const majorRoutesRaw={"type":"FeatureCollection","features":[{"type":"Feature","properties":{"fid":1},"geometry":{"type":"LineString","coordinates":[[60590.771195823974267,9863403.72797791287303],[59788.351638325926615,9862782.033545978367329],[58291.947598667386046,9862572.392400324344635],[55920.833951285778312,9861242.255476182326674],[55299.139519350348564,9861459.125626858323812],[54373.82687646971317,9860316.942833302542567],[53983.460605254455004,9859550.668300919234753],[53665.384384264238179,9858914.515858937054873],[53058.14796237381961,9858567.523617858067155],[53087.063982463834691,9857613.29495488665998],[53289.476123093976639,9857121.722613357007504],[53202.728062823916844,9855820.501709306612611],[52537.659600753468112,9855300.013347683474422],[51814.75909850296739,9854230.120604353025556],[51207.522676612548821,9853969.876423543319106],[50513.538194452070456,9853825.296323092654347],[49472.561471211360185,9853102.395820843055844],[48836.409029230919259,9852119.251137781888247],[49067.737189951076289,9851165.022474810481071],[49038.821169861061207,9848996.320968059822917],[48865.325049320941616,9847955.344244819134474],[48807.493009140904178,9846683.039360856637359],[49385.81341094130039,9845989.054878696799278],[50484.622174362055375,9845526.398557256907225],[52479.827560573423398,9844572.16989428550005],[53173.812042733901762,9844311.9257134757936],[53549.720303904163302,9844196.261633114889264],[53260.560103003961558,9843704.689291585236788],[52479.827560573423398,9843155.284909874200821],[51728.011038232914871,9842172.140226813033223],[50773.782375262257119,9842287.804307173937559],[50282.210033731913427,9841911.896046003326774],[50195.461973461860907,9841073.331463392823935],[50629.202274812152609,9840437.1790214125067],[50368.958094001980498,9839107.042097272351384],[50773.782375262257119,9838152.813434300944209],[50715.950335082205129,9836013.027947640046477],[50311.126053821928508,9835203.379385119304061],[50368.958094001965947,9834162.402661878615618],[50831.614415442287282,9833179.25797881744802],[52450.911540483401041,9832109.365235486999154],[52768.987761473625142,9831704.540954226627946],[53115.980002553864324,9830981.640451977029443],[54619.61304723489593,9829796.083628285676241],[55371.429569575411733,9829506.923427386209369],[56817.230574076405901,9828552.694764414802194],[57858.207297317123448,9827974.374362614005804],[59853.41268352849147,9827685.214161714538932],[61010.05348712929117,9827164.725800093263388],[62108.86225055003888,9826702.069478653371334],[62918.510813070592121,9826094.833056762814522],[64624.555998381765676,9825776.756835773587227],[65810.112822072580457,9825256.268474152311683],[67024.585665853403043,9824620.116032171994448],[68961.959011884740903,9825545.428675051778555],[69887.271654765369021,9825458.680614782497287],[70899.332357916064211,9826123.749076852574944],[71882.477040976751596,9825863.504896042868495],[72605.377543227237766,9825950.252956312149763],[73328.278045477738488,9824677.948072351515293],[74369.254768718456035,9824504.451951811090112],[74860.827110248792451,9824996.024293340742588],[76451.208215199891129,9824967.108273250982165],[77203.024737540399656,9825314.100514331832528],[78070.505340240997612,9825371.932554511353374],[78619.909721951378742,9825053.856333522126079],[80007.87868627232092,9824793.612152710556984],[80738.008193545319955,9824677.948072349652648],[81634.404816335925716,9824677.948072349652648],[82176.580193023808533,9824526.138966877013445],[82942.854725409328239,9824663.490062305703759],[84099.495529010106111,9824497.222946787253022],[84887.457076463164412,9824020.10861530341208],[85559.754543556118733,9823868.299509830772877],[86701.93733711191453,9822270.689399860799313],[86701.93733711191453,9821923.69715877994895],[87569.417939812497934,9821345.37675697915256],[88147.738341612901422,9820767.056355178356171],[89304.379145213693846,9820911.636455629020929],[90605.600049264583504,9821027.300535989925265],[90952.592290344822686,9821258.628696709871292],[91791.156872955398285,9821258.628696709871292],[92080.317073855592753,9821461.040837340056896],[92947.797676556190709,9821345.37675697915256],[93526.118078356594197,9821547.788897609338164],[94220.102560517072561,9821056.216556079685688],[95434.575404297909699,9821056.216556079685688],[96012.895806098298635,9821374.292777070775628],[96649.048248078746838,9821461.040837338194251],[97111.704569519060897,9821171.880636438727379],[97754.165442893456202,9821086.892158204689622],[98181.597312849800801,9821171.880636438727379]]}},{"type":"Feature","properties":{"fid":2},"geometry":{"type":"LineString","coordinates":[[99453.90219681065355,9838521.49269044958055],[96273.139986908456194,9837711.844127928838134],[96012.895806098284083,9837278.103826578706503],[96041.811826188306441,9837104.607706040143967],[95694.819585108067258,9836757.615464959293604],[95550.239484657970024,9835890.134862259030342],[94943.003062767544179,9835138.318339917808771],[94740.590922137402231,9834415.417837668210268],[94538.178781507274834,9833808.181415777653456],[94422.514701147185406,9833287.693054156377912],[93265.873897546392982,9832622.624592086300254],[92514.057375205884455,9831870.808069745078683],[92111.159303163003642,9831599.547123670578003],[90605.600049264568952,9831205.73960767313838],[88812.806803683342878,9831147.907567493617535],[88118.822321522864513,9830685.251246053725481],[87540.501919722461025,9830569.587165692821145],[87424.837839362386148,9830685.251246053725481],[87309.17375900229672,9829933.43472371250391],[87193.509678642221843,9829181.618201371282339],[84301.907669640233507,9826868.336594171822071],[82162.122182978782803,9825075.543348591774702],[81634.404816335925716,9824677.948072349652648],[80738.008193545319955,9824677.948072349652648],[80369.328937397542177,9823716.490404359996319],[80311.496897217512014,9822559.84960075840354],[80831.985258837870788,9821056.216556077823043],[81381.389640548237367,9820593.560234637930989],[81786.213921808521263,9820217.651973467320204],[80658.489138297751197,9819552.583511395379901],[80398.244957487564534,9818887.515049325302243],[80022.336696317302994,9818367.026687704026699],[79444.016294516914058,9817644.126185454428196],[78750.031812356435694,9817036.889763563871384],[78836.779872626502765,9816198.325180953368545],[78547.619671726293745,9814579.028055913746357],[78316.29151100612944,9814116.371734473854303],[78316.29151100612944,9812757.318790243938565],[77897.009219700848917,9811774.174107182770967],[77564.474988665620913,9811094.647635066881776],[77116.276677270318032,9810415.121162950992584],[77043.986627045262139,9809012.694188585504889],[76812.658466325097834,9808203.045626064762473]]}},{"type":"Feature","properties":{"fid":3},"geometry":{"type":"LineString","coordinates":[[83882.625378334952984,9862854.323596203699708],[83665.755227659814409,9861986.842993503436446],[83940.457418514997698,9860974.782290352508426],[84027.205478785050218,9859109.698994545266032],[83954.915428559994325,9854656.631900683045387],[83853.709358244945179,9853066.250795731320977],[82798.274624959216453,9850680.679138304665685],[81771.755911763510085,9849625.244405020028353],[80962.107349242956843,9848555.351661687716842],[80846.443268882867415,9847557.748968582600355],[79879.367167718359269,9846299.512381104752421],[79660.886445192052634,9845186.635321201756597],[79646.428435147041455,9843278.177995260804892],[79415.100274426877149,9842121.537191659212112],[79212.688133796735201,9841514.3007697686553],[78880.153902761507197,9840849.232307698577642],[78634.367731996346265,9840386.575986256822944],[77969.299269925890258,9840198.621855672448874],[77419.894888215509127,9839417.88931324146688],[77087.360657180281123,9838781.736871261149645],[76971.696576820191694,9838246.790499595925212],[77680.13906902569579,9836772.073475006967783],[78113.879370375987492,9835470.852570954710245],[78244.001460781073547,9834473.249877849593759],[77275.314787765411893,9833519.021214880049229],[77217.48274758538173,9832593.708572000265121],[77651.223048935673432,9831653.93791907466948],[77940.3832498358679,9830887.663386689499021],[78468.100616478754091,9829752.709598153829575],[79075.337038369165384,9828567.152774464339018],[79870.527590844721999,9827670.756151672452688],[80550.054062960174633,9826759.901518838480115],[80853.672273905394832,9825964.710966361686587],[81359.702625480742427,9825487.596634875983],[81634.404816335925716,9824677.948072349652648]]}}]};

const routePaths=majorRoutesRaw.features.map(f=>f.geometry.coordinates.map(c=>utmToLatLng(c[0],c[1])));
const routeNames=['Major Route 1 — North Loop','Major Route 2 — South-East','Major Route 3 — West Loop'];

const map=L.map('map',{center:[-1.5,35.2],zoom:10});
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{attribution:'© OpenStreetMap',maxZoom:19}).addTo(map);
map.on('mousemove',e=>{document.getElementById('coordText').textContent=`🌍 Lat: ${e.latlng.lat.toFixed(5)}  Lng: ${e.latlng.lng.toFixed(5)}`;});

const minorRoadsRaw={"type":"FeatureCollection","features":[{"type":"Feature","properties":{"fid":1},"geometry":{"type":"MultiPolygon","coordinates":[[[[92972.519,9833305.404],[92366.53,9832814.841],[92194.36,9832298.331],[93637.564,9830508.757],[95486.869,9829844.163],[95432.338,9828856.019],[95086.417,9828364.66],[95314.561,9828022.444],[96295.411,9827907.05],[96502.133,9826573.023],[96820.118,9825474.529],[96935.845,9824433.648],[97267.645,9823799.738],[97340.711,9821168.084],[97768.943,9820998.259],[98260.268,9821082.831],[98780.952,9820909.896],[99241.611,9821197.808],[100054.617,9821082.853],[100058.836,9821078.761],[100058.399,9821075.702],[99245.362,9821188.36],[98784.255,9820900.167],[98260.727,9821072.763],[97769.254,9820988.165],[97333.961,9821160.004],[97258.249,9823796.125],[96926.55,9824429.843],[96810.393,9825472.16],[96492.436,9826570.557],[96290.457,9827897.564],[95311.098,9828012.783],[95076.194,9828361.967],[95422.439,9828858.031],[95479.967,9829836.017],[93632.862,9830499.821],[92184.86,9832294.181],[92357.505,9832819.389],[92966.339,9833313.266],[93891.879,9833978.509],[93899.797,9833974.423],[92972.519,9833305.404]]]]}}]};

const boundaryRaw={"type":"FeatureCollection","features":[{"type":"Feature","properties":{"fid":1},"geometry":{"type":"Polygon","coordinates":[[[30327.066,9842805.89],[30334.062,9842831.195],[30388.678,9842885.644],[30605.628,9843043.707],[30931.66,9843244.748],[31097.088,9843433.927],[31358.2,9843735.205],[31552.798,9843971.25],[31751.196,9844203.534],[31986.325,9844495.075],[32191.366,9844648.267],[32372.52,9844830.472],[32538.011,9844985.744],[32764.588,9845213.769],[32963.618,9845396.542],[33110.172,9845539.402],[33432.214,9845699.792],[33704.835,9845930.047],[33937.032,9846197.357],[34029.752,9846302.451],[34257.614,9846417.469],[34451.089,9846525.431],[34643.724,9846648.727],[34843.418,9846762.886],[35038.504,9846878.921],[35209.808,9846964.51],[35385.925,9847085.084],[35519.353,9847145.046],[35807.104,9847242.408],[36057.371,9847245.537],[36345.459,9847304.693],[36420.327,9847550.731],[36458.894,9847800.471],[36598.458,9847913.713],[36743.434,9848030.192],[36902.429,9848184.361],[37203.157,9848450.698],[37488.345,9848619.613],[37664.772,9848717.849],[37895.346,9848829.093],[38122.684,9848932.797],[38527.513,9849144.421],[38958.349,9849352.86],[39237.618,9849497.543],[39518.891,9849736.93],[39860.615,9850104.479],[39956.773,9850259.608],[40121.492,9850234.061],[40684.147,9850012.259],[40952.55,9850174.136],[41061.638,9850370.177],[41237.87,9850581.397],[41569.591,9850778.352],[42062.073,9851046.063],[42497.147,9851307.217],[42894.358,9851534.944],[43207.167,9851703.342],[43618.278,9852040.851],[43981.647,9852097.953],[44383.279,9852271.874],[44592.164,9852392.744],[44717.65,9852501.638],[45102.571,9852626.566],[45327.681,9852761.45],[45662.647,9852958.927],[46764.304,9853669.339],[47201.288,9854083.266],[47976.43,9854396.589],[48573.837,9854752.659],[48952.424,9855104.066],[49326.322,9855677.128],[49652.772,9856116.68],[49875.459,9856411.874],[50126.367,9856672.677],[50822.837,9857407.645],[51084.665,9857614.658],[51225.58,9857558.927],[51134.962,9857319.904],[51165.54,9857165.004],[51425.615,9857109.462],[52008.191,9857252.42],[52475.494,9857677.111],[52247.846,9858468.706],[52292.475,9859024.005],[52484.744,9859379.394],[53071.742,9859466.388],[53268.456,9859750.763],[53427.831,9860364.34],[53577.188,9860450.651],[54040.721,9860518.078],[55296.876,9860791.159],[56241.095,9861031.472],[57183.153,9861263.167],[58194.513,9861505.718],[58363.487,9861510.277],[59555.108,9861447.52],[60199.304,9860932.04],[61175.352,9860150.239],[62220.788,9859319.067],[63736.879,9858107.767],[65372.222,9856810.618],[69905.101,9853194.242],[70859.304,9852472.801],[72455.452,9851236.014],[74277.079,9849844.716],[74836.644,9849372.279],[78772.43,9847665.148],[78021.475,9846570.006],[76926.334,9845787.762],[76425.697,9845161.967],[76241.567,9844489.036],[76050.22,9844035.535],[75455.715,9843785.217],[74892.499,9843566.189],[74391.863,9843034.263],[75228.864,9842658.786],[75815.547,9842322.421],[76801.175,9842119.037],[77614.708,9842134.682],[77630.353,9841508.887],[78318.728,9840163.427],[79820.637,9839146.51],[81823.181,9839240.379],[84545.391,9838927.482],[85296.345,9838286.042],[86641.805,9838332.976],[88435.176,9837459.136],[88394.869,9836953.572],[87937.54,9837193.731],[87212.168,9837138.749],[87016.963,9837321.267],[87122.089,9836613.736],[87458.314,9836276.579],[88260.725,9835583.13],[89199.98,9834638.252],[92111.159,9831599.547],[93577.627,9830036.188],[95889.988,9827635.512],[98327.07,9825083.538],[97434.167,9824473.591],[97264.232,9823835.059],[97392.189,9823408.496],[97656.331,9822418.415],[97693.781,9822247.499],[97714.073,9822098.06],[97749.574,9821919.076],[97812.346,9821701.293],[97862.226,9821502.978],[97805.121,9821349.907],[97707.9,9821078.207],[97754.165,9821086.892],[97786.063,9820956.831],[97723.281,9820800.255],[97715.177,9820639.744],[97663.301,9820590.454],[97509.059,9820574.586],[97416.47,9820438.657],[97321.393,9820331.22],[97224.554,9820301.474],[97152.997,9820208.866],[97041.132,9820106.506],[96807.477,9820002.852],[96547.947,9819838.931],[96037.749,9819399.264],[95839.312,9818977.362],[95485.295,9818383.118],[95165.391,9818081.433],[94976.377,9817246.602],[94881.644,9816953.929],[94631.461,9816420.088],[94225.337,9815911.765],[93810.492,9815437.835],[93507.202,9815523.302],[93005.381,9815247.073],[92052.209,9815494.788],[91597.816,9815327.255],[91374.159,9815087.025],[91270.821,9814768.514],[91073.471,9813780.933],[90874.751,9813524.614],[90637.21,9813186.492],[90418.591,9812007.447],[90551.151,9811756.058],[90867.009,9811329.733],[91053.754,9811050.491],[91197.391,9810667.932],[91033.89,9810117.026],[91151.77,9809618.28],[91240.159,9808976.724],[91186.252,9808861.018],[30327.066,9842805.89]]]}}]};

const majorBufferRaw={"type":"FeatureCollection","features":[{"type":"Feature","properties":{"fid":1},"geometry":{"type":"MultiPolygon","coordinates":[[[[59791.414,9862778.081],[55923.28,9861237.895],[55300.812,9861453.247],[54378.043,9860314.204],[53669.857,9858912.28],[53063.237,9858564.673],[53092.034,9857614.357],[53294.099,9857123.626],[53207.717,9855820.169],[52541.362,9855296.561],[51818.902,9854227.321],[51209.492,9853965.281],[50515.554,9853820.609],[49476.224,9853098.852],[48841.775,9852118.34],[49072.596,9851166.2],[49043.821,9848996.254],[48870.306,9847954.818],[48812.576,9846684.75],[49388.875,9845993.191],[50486.562,9845531.007],[52481.788,9844576.775],[53175.427,9844316.66],[53551.191,9844201.041],[53264.87,9843702.154],[52483.333,9843151.638],[51731.983,9842169.103],[50775.202,9842282.596],[50286.961,9841909.235],[50200.624,9841074.637],[50633.333,9840439.996],[50374.159,9839107.585],[50778.385,9838154.766],[50720.949,9836012.893],[50316.192,9835202.331],[50373.896,9834163.651],[50835.541,9833182.656],[52453.668,9832113.537],[52772.919,9831707.63],[53119.986,9830984.849],[54622.114,9829800.479],[55373.224,9829511.59],[56819.826,9828556.973],[57859.833,9827979.191],[59854.13,9827690.162],[61012.05,9827169.31],[62110.803,9826706.678],[62920.576,9826099.534],[64625.472,9825781.672],[65812.123,9825260.847],[67024.689,9824625.706],[68959.804,9825549.94],[69885.992,9825463.823],[70896.586,9826127.928],[71882.831,9825868.583],[72604.782,9825955.217],[73331.449,9824682.489],[74367.539,9824509.807],[74857.292,9824999.56],[76450.153,9824972.128],[77200.929,9825318.64],[78070.173,9825376.921],[78621.673,9825058.613],[80008.731,9824798.54],[80738.402,9824682.948],[81634.405,9824682.948],[82176.825,9824531.263],[82941.973,9824668.412],[84100.207,9824502.172],[84889.351,9824024.807],[85560.856,9823873.177],[86706.005,9822273.597],[86706.937,9821926.373],[87572.191,9821349.537],[88149.545,9820772.321],[89303.759,9820916.598],[90603.887,9821032.168],[90949.819,9821262.789],[91789.581,9821263.629],[92077.45,9821465.137],[92947.274,9821350.491],[93524.466,9821552.508],[94221.694,9821061.217],[95433.291,9821061.217],[96010.486,9821378.674],[96648.373,9821465.995],[97113.435,9821176.695],[97754.001,9821091.957],[98180.622,9821176.785],[97755.141,9821081.988],[97111.049,9821166.924],[96647.932,9821455.842],[96014.492,9821369.464],[95436.985,9821051.835],[94220.103,9821051.216],[93525.334,9821542.217],[92949.449,9821340.657],[92081.588,9821455.827],[91794.024,9821254.533],[90954.106,9821253.629],[90608.374,9821023.14],[89304.911,9820906.664],[88148.359,9820762.095],[87566.232,9821341.491],[86699.164,9821919.537],[86696.937,9821923.697],[86696.937,9822269.086],[85556.795,9823863.842],[84886.356,9824015.231],[84097.777,9824492.419],[82942.942,9824658.426],[82177.462,9824521.217],[81633.718,9824672.948],[80738.008,9824672.948],[80006.957,9824788.698],[78618.988,9825048.942],[78069.318,9825366.842],[77204.28,9825309.173],[76453.304,9824962.568],[74862.86,9824990.986],[74372.79,9824500.916],[73327.456,9824673.016],[72602.673,9825944.892],[71883.073,9825858.541],[70900.212,9826118.344],[69890.018,9825454.502],[68962.868,9825540.322],[67026.741,9824615.604],[65807.945,9825251.759],[64623.073,9825771.947],[62917.594,9826089.918],[62106.355,9826697.7],[61008.113,9827160.118],[59852.001,9827680.367],[57857.49,9827969.426],[56814.802,9828548.324],[55369.128,9829502.451],[54617.818,9829791.417],[53112.884,9830977.714],[52764.717,9831701.883],[52447.48,9832105.64],[50828.858,9833175.086],[50364.434,9834160.274],[50306.134,9835203.102],[50710.982,9836014.272],[50768.755,9838151.862],[50364.355,9839105.089],[50623.894,9840436.089],[50191.331,9841070.515],[50277.237,9841912.411],[50770.745,9842291.776],[51725.775,9842177.448],[52475.856,9843158.322],[53256.799,9843708.156],[53542.203,9844193.343],[53172.342,9844307.147],[52478.072,9844567.488],[50482.572,9845521.837],[49383.873,9845984.447],[48803.652,9846679.838],[48860.33,9847955.571],[49033.827,9848996.768],[49062.729,9851164.458],[48831.55,9852118.073],[49468.364,9853105.112],[50510.686,9853829.403],[51206.013,9853974.669],[51811.439,9854234.137],[52533.517,9855302.813],[53197.888,9855823.063],[53284.41,9857120.895],[53082.441,9857611.391],[53053.15,9858567.372],[53661.589,9858918.106],[53978.988,9859552.904],[54369.372,9860319.212],[55295.254,9861462.273],[55920.353,9861247.719],[58289.501,9862576.753],[59786.341,9862786.801],[60587.709,9863407.68],[60593.834,9863400.915],[59791.414,9862778.081]]]]}},{"type":"Feature","properties":{"fid":2},"geometry":{"type":"MultiPolygon","coordinates":[[[[96276.368,9837707.506],[96018.13,9837277.11],[96046.754,9837103.852],[95699.488,9836755.213],[95555.171,9835889.313],[94947.54,9835135.978],[94745.406,9834414.07],[94543.004,9833806.845],[94427.396,9833286.608],[93268.941,9832618.62],[92517.593,9831867.273],[92113.952,9831595.4],[90606.865,9831200.902],[88814.394,9831142.956],[88121.596,9830681.091],[87541.483,9830564.684],[87428.279,9830674.739],[87314.116,9829932.674],[87197.838,9829179.115],[84305.075,9826864.468],[82165.333,9825071.711],[81634.405,9824673.955],[80741.446,9824672.948],[80374.283,9823715.445],[80316.539,9822560.569],[80836.26,9821059.154],[81384.61,9820597.385],[81790.572,9820220.103],[80662.516,9819549.154],[80402.901,9818885.693],[80026.39,9818364.099],[79447.921,9817641.003],[78755.272,9817034.831],[78841.753,9816198.84],[78552.542,9814578.149],[78321.292,9814115.191],[78321.292,9812757.319],[77901.608,9811772.213],[77568.966,9811092.45],[77121.2,9810413.504],[77048.98,9809012.437],[76817.466,9808201.672],[77039.023,9809013.52],[77111.283,9810415.379],[77560.125,9811097.133],[77892.461,9811776.255],[78311.292,9812758.34],[78311.292,9814116.372],[78542.825,9814580.618],[78831.734,9816198.511],[78745.058,9817036.375],[79440.389,9817647.597],[80018.355,9818370.054],[80393.82,9818889.928],[80653.833,9819554.406],[81777.897,9820218.552],[81378.076,9820589.814],[80828.765,9821052.392],[80306.772,9822558.214],[80364.335,9823716.74],[80733.34,9824679.738],[80738.008,9824682.948],[81632.732,9824682.948],[82159.01,9825079.459],[84298.697,9826872.169],[87188.864,9829184.305],[87304.232,9829934.195],[87419.896,9830686.012],[87542.145,9830575.015],[88116.872,9830689.96],[88810.033,9831152.068],[90604.878,9831210.719],[92109.072,9831604.169],[92510.864,9831874.686],[93262.338,9832626.16],[94418.112,9833290.929],[94533.298,9833809.266],[94735.809,9834416.883],[94938.188,9835139.666],[95545.524,9835892.254],[95689.888,9836758.437],[96036.457,9837106.324],[96007.964,9837277.282],[96268.853,9837714.417],[99452.669,9838526.338],[96276.368,9837707.506]]]]}}]};

// Render layers
L.geoJSON(convertGeoJSON(boundaryRaw),{style:{color:'#f0c040',weight:2.5,fillOpacity:0.04,dashArray:'10 6'}}).addTo(map).bindPopup('<b>🔶 Maasai Mara National Reserve Boundary</b>');
L.geoJSON(convertGeoJSON(majorBufferRaw),{style:{color:'#ff6d00',weight:1.5,fillColor:'#ff6d00',fillOpacity:0.12}}).addTo(map).bindPopup('<b>🟠 Major Roads Buffer Zone</b>');
L.geoJSON(convertGeoJSON(minorRoadsRaw),{style:{color:'#8B6914',weight:1.5,fillColor:'#8B6914',fillOpacity:0.18}}).addTo(map).bindPopup('<b>🟤 Minor Roads Buffer Zone</b>');
majorRoutesRaw.features.forEach((f,i)=>{
  const colors=['#ff4444','#44aaff','#44ff88'];
  const lls=f.geometry.coordinates.map(c=>utmToLatLng(c[0],c[1]));
  L.polyline(lls,{color:colors[i],weight:3,opacity:0.85}).addTo(map).bindPopup(`<b>${routeNames[i]}</b>`);
});
const bCoords=boundaryRaw.features[0].geometry.coordinates[0];
map.fitBounds(L.latLngBounds(bCoords.map(c=>utmToLatLng(c[0],c[1]))).pad(0.05));

// ── Helpers ──
function haversine(la1,lo1,la2,lo2){
  const R=6371000,dL=(la2-la1)*Math.PI/180,dO=(lo2-lo1)*Math.PI/180;
  const a=Math.sin(dL/2)**2+Math.cos(la1*Math.PI/180)*Math.cos(la2*Math.PI/180)*Math.sin(dO/2)**2;
  return R*2*Math.atan2(Math.sqrt(a),Math.sqrt(1-a));
}
function distToSeg(px,py,ax,ay,bx,by){
  const dx=bx-ax,dy=by-ay;
  if(!dx&&!dy)return haversine(px,py,ax,ay);
  let t=((px-ax)*dx+(py-ay)*dy)/(dx*dx+dy*dy);
  t=Math.max(0,Math.min(1,t));
  return haversine(px,py,ax+t*dx,ay+t*dy);
}
function distToRoute(lat,lng,pts){
  let m=Infinity;
  for(let i=0;i<pts.length-1;i++){const d=distToSeg(lat,lng,pts[i][0],pts[i][1],pts[i+1][0],pts[i+1][1]);if(d<m)m=d;}
  return m;
}
function lerp(a,b,t){return a+(b-a)*t;}
function ts(){return new Date().toLocaleTimeString();}
function spColor(k){return k<40?'#29b6f6':k<70?'#ffa726':'#ef5350';}
function toast(msg,icon='✅',col='#c8e6c9'){
  const el=document.getElementById('toast');
  document.getElementById('toastMsg').textContent=msg;
  document.getElementById('toastIcon').textContent=icon;
  el.style.color=col;el.classList.add('show');
  clearTimeout(toast._t);toast._t=setTimeout(()=>el.classList.remove('show'),3200);
}
function addAlert(msg,icon='🚨',isSOS=false){
  const box=document.getElementById('alertScroll');
  const d=document.createElement('div');d.className='arow'+(isSOS?' arow-sos':'');
  d.innerHTML=`<span class="aicon">${icon}</span><div><div class="atext">${msg}</div><div class="atime">${ts()}</div></div>`;
  box.prepend(d);
}
function addLog(msg){
  const box=document.getElementById('logBox');
  const d=document.createElement('div');d.className='lrow';
  d.textContent=msg;box.appendChild(d);box.scrollTop=box.scrollHeight;
}
function openModal(id){document.getElementById(id).classList.add('show');}
function closeModal(id){document.getElementById(id).classList.remove('show');}
document.querySelectorAll('.modal-bg').forEach(m=>m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('show');}));

// ── SOS System ──
let activeSOS=[];
let currentSOSId=null;
let selectedSosType='🦁 Wildlife Encounter';

function selectSosType(el,type){
  document.querySelectorAll('.sos-type-btn').forEach(b=>b.classList.remove('selected'));
  el.classList.add('selected');
  selectedSosType=type;
}

function openSOSModal(id){
  const c=cars.find(c=>c.id===id);if(!c)return;
  currentSOSId=id;
  const nameEl=document.getElementById('sosCarName');
  nameEl.textContent=c.name;nameEl.style.color=c.color;
  document.getElementById('sos-route').textContent=routeNames[c.routeIdx];
  document.getElementById('sos-speed').textContent=c.actual_kmh+' km/h';
  document.getElementById('sos-status').innerHTML=c.offRoute
    ?'<span style="color:#ef5350">⚠️ OFF ROUTE</span>'
    :'<span style="color:#69f0ae">✅ On Route</span>';
  const utm=proj4('WGS84','EPSG:32737',[c.lng,c.lat]);
  document.getElementById('sos-pos').textContent=`${Math.round(utm[0])}, ${Math.round(utm[1])}`;
  document.getElementById('sosDetails').value='';
  // reset type selection
  document.querySelectorAll('.sos-type-btn').forEach((b,i)=>{b.classList.toggle('selected',i===0);});
  selectedSosType='🦁 Wildlife Encounter';
  map.flyTo([c.lat,c.lng],13,{duration:1.2});
  openModal('sosModal');
}

function dispatchSOS(){
  const c=cars.find(c=>c.id===currentSOSId);if(!c)return;
  const details=document.getElementById('sosDetails').value.trim();
  const utm=proj4('WGS84','EPSG:32737',[c.lng,c.lat]);
  const sosEntry={
    id:Date.now(),carId:c.id,carName:c.name,color:c.color,
    type:selectedSosType,details,
    route:routeNames[c.routeIdx],speed:c.actual_kmh,
    lat:c.lat,lng:c.lng,
    utm:`${Math.round(utm[0])}, ${Math.round(utm[1])}`,
    time:ts()
  };
  activeSOS.push(sosEntry);
  c.hasSOS=true;
  closeModal('sosModal');
  showSOSPopup(sosEntry);
  addAlert(`🆘 SOS from ${c.name} — ${selectedSosType}${details?' · '+details:''}`, '🆘', true);
  addLog(`🆘 SOS dispatched: ${c.name} [${selectedSosType}]`);
  updateSOSBadgeBar();
  toast(`SOS dispatched for ${c.name}`,'🆘','#ff8a80');
}

function showSOSPopup(sos){
  document.getElementById('sosPopupTitle').textContent='SOS ALERT — '+sos.type;
  const vEl=document.getElementById('sosPopupVehicle');
  vEl.textContent=sos.carName;vEl.style.color=sos.color;
  document.getElementById('sosPopupDetails').innerHTML=
    `<b>Emergency:</b> ${sos.type}<br>`+
    `<b>Route:</b> ${sos.route}<br>`+
    `<b>Speed:</b> ${sos.speed} km/h<br>`+
    `<b>GPS (UTM):</b> ${sos.utm}<br>`+
    `<b>Time:</b> ${sos.time}`+
    (sos.details?`<br><b>Notes:</b> ${sos.details}`:'');
  document.getElementById('sosOverlay').classList.add('show');
  document.getElementById('sosOverlayBg').classList.add('show');
  // fly map to vehicle
  map.flyTo([sos.lat,sos.lng],13,{duration:1.5});
}

function dismissSOS(){
  document.getElementById('sosOverlay').classList.remove('show');
  document.getElementById('sosOverlayBg').classList.remove('show');
}

function respondSOS(){
  const sos=activeSOS[activeSOS.length-1];
  if(sos){
    addAlert(`📡 Rangers dispatched to ${sos.carName} (${sos.type})`,'📡',true);
    addLog(`📡 Response confirmed: rangers en route to ${sos.carName}`);
    toast(`Rangers dispatched to ${sos.carName}`,'📡','#81d4fa');
    // mark resolved
    const c=cars.find(c=>c.id===sos.carId);
    if(c)c.hasSOS=false;
    activeSOS=activeSOS.filter(s=>s.id!==sos.id);
    updateSOSBadgeBar();
  }
  dismissSOS();
}

function dismissAllSOS(){
  activeSOS.forEach(s=>{const c=cars.find(c=>c.id===s.carId);if(c)c.hasSOS=false;});
  activeSOS=[];
  updateSOSBadgeBar();
  dismissSOS();
  addLog('✕ All SOS alerts dismissed');
}

function updateSOSBadgeBar(){
  const bar=document.getElementById('sosBadgeBar');
  if(activeSOS.length>0){
    bar.classList.add('show');
    document.getElementById('sosBadgeText').textContent=
      `🆘 ${activeSOS.length} ACTIVE SOS ALERT${activeSOS.length>1?'S':''} — ${activeSOS.map(s=>s.carName).join(', ')}`;
  } else {
    bar.classList.remove('show');
  }
}

// ── Notify Modal ──
let notifyTargetId=null;
function openNotifyModal(id){
  const c=cars.find(c=>c.id===id);if(!c)return;
  notifyTargetId=id;
  const nameEl=document.getElementById('notifyCarName');
  nameEl.textContent=c.name;nameEl.style.color=c.color;
  document.getElementById('ni-route').textContent=routeNames[c.routeIdx];
  document.getElementById('ni-speed').textContent=c.actual_kmh+' km/h';
  document.getElementById('ni-status').innerHTML=c.offRoute
    ?'<span style="color:#ef5350">⚠️ OFF ROUTE</span>'
    :'<span style="color:#69f0ae">✅ On Route</span>';
  const utm=proj4('WGS84','EPSG:32737',[c.lng,c.lat]);
  document.getElementById('ni-pos').textContent=`${Math.round(utm[0])}, ${Math.round(utm[1])}`;
  document.getElementById('notifyMsg').value='';
  map.flyTo([c.lat,c.lng],13,{duration:1.2});
  c.marker.openPopup();
  openModal('notifyModal');
}
function sendNotify(){
  const c=cars.find(c=>c.id===notifyTargetId);if(!c)return;
  const msg=document.getElementById('notifyMsg').value.trim();
  if(!msg){document.getElementById('notifyMsg').focus();return;}
  addAlert(`[${c.name}] ${msg}`,'📣');
  addLog(`📣 Sent to ${c.name}: "${msg}"`);
  toast(`Message sent to ${c.name}`,'📣','#81d4fa');
  closeModal('notifyModal');
}

// ── Car class ──
let nextId=1;
class Car{
  constructor({name,color,routeIdx,kmh}){
    this.id=nextId++;this.name=name;this.color=color;
    this.routeIdx=routeIdx;this.routePts=routePaths[routeIdx];
    this.kmh=Math.min(kmh,99);
    this.routeLen=this._rLen();
    this.tSpeed=(this.kmh/3.6)/(60*this.routeLen);
    this.t=Math.random();this.dir=Math.random()<.5?1:-1;
    this.lat=this.routePts[0][0];this.lng=this.routePts[0][1];
    this.prevLat=this.lat;this.prevLng=this.lng;
    this.offRoute=false;this.forcedOff=false;this.offDur=0;
    this.offLat=0;this.offLng=0;
    this.moved=false;this.actual_kmh=0;
    this.trail=[];this.lastLogF=0;
    this.hasSOS=false;
    this.marker=L.circleMarker([this.lat,this.lng],{radius:9,color,fillColor:color,fillOpacity:.92,weight:2.5})
      .addTo(map).bindPopup(()=>this._popup());
    this.ring=L.circleMarker([this.lat,this.lng],{radius:20,color:'#ff1744',fillOpacity:0,weight:2.5,opacity:0}).addTo(map);
    this.sosRing=L.circleMarker([this.lat,this.lng],{radius:28,color:'#ff1744',fillOpacity:0,weight:3,opacity:0,dashArray:'6 4'}).addTo(map);
    this.trailLine=L.polyline([],{color,weight:2.5,opacity:.5}).addTo(map);
    this.labelM=L.marker([this.lat,this.lng],{icon:L.divIcon({className:'',
      html:`<div style="background:rgba(5,14,2,.85);color:${color};padding:2px 6px;border-radius:4px;font-size:9px;font-weight:700;white-space:nowrap;border:1px solid ${color}50;">${name}</div>`,
      iconAnchor:[-12,10]}),interactive:false}).addTo(map);
  }
  _rLen(){let l=0;for(let i=0;i<this.routePts.length-1;i++)l+=haversine(...this.routePts[i],...this.routePts[i+1]);return l||1;}
  _popup(){
    return`<div style="font-family:'Segoe UI',sans-serif;min-width:180px;">
      <div style="font-weight:700;color:${this.color};margin-bottom:4px;">${this.name}</div>
      ${this.hasSOS?'<div style="color:#ff1744;font-weight:700;font-size:0.85em;margin-bottom:4px;">🆘 SOS ACTIVE</div>':''}
      <div style="font-size:0.8em;line-height:1.8;">
        <b>Route:</b> ${routeNames[this.routeIdx]}<br>
        <b>Speed:</b> ${this.actual_kmh} km/h<br>
        <b>Status:</b> ${this.offRoute?'<b style="color:red">⚠️ OFF ROUTE</b>':'✅ On Route'}
      </div>
    </div>`;
  }
  update(frame){
    this.prevLat=this.lat;this.prevLng=this.lng;
    if(this.forcedOff){
      this.offLat+=(Math.random()-.5)*.003;this.offLng+=(Math.random()-.5)*.003;
      this.lat=this.offLat;this.lng=this.offLng;this.offDur++;
      if(this.offDur>110){this.forcedOff=false;this.offDur=0;}
    } else {
      this.t+=this.tSpeed*this.dir;
      if(this.t>=1){this.t=1;this.dir=-1;}if(this.t<=0){this.t=0;this.dir=1;}
      const n=this.routePts.length-1,seg=Math.min(Math.floor(this.t*n),n-1),lt=(this.t*n)-seg;
      const a=this.routePts[seg],b=this.routePts[Math.min(seg+1,n)];
      this.lat=lerp(a[0],b[0],lt);this.lng=lerp(a[1],b[1],lt);
    }
    const dist=haversine(this.lat,this.lng,this.prevLat,this.prevLng);
    this.moved=dist>.1;this.actual_kmh=Math.round(dist*3.6*60);
    if(this.moved){this.trail.push([this.lat,this.lng]);if(this.trail.length>50)this.trail.shift();}
    const wasOff=this.offRoute;
    this.offRoute=this.forcedOff||(distToRoute(this.lat,this.lng,this.routePts)>600);
    if(this.offRoute&&!wasOff){addAlert(`${this.name} left designated route!`,'🚨');toast(`${this.name} is OFF ROUTE!`,'🚨','#ef9a9a');}
    if(!this.offRoute&&wasOff&&!this.forcedOff){addLog(`✅ ${this.name} returned to route`);toast(`${this.name} back on route`,'✅','#a5d6a7');}
    const ll=[this.lat,this.lng];
    const col=this.hasSOS?'#ff1744':this.offRoute?'#ff6600':this.color;
    this.marker.setLatLng(ll).setStyle({color:col,fillColor:col});
    this.ring.setLatLng(ll).setStyle({opacity:this.offRoute?.8:0});
    this.sosRing.setLatLng(ll).setStyle({opacity:this.hasSOS?.9:0});
    this.trailLine.setLatLngs(this.trail);
    this.labelM.setLatLng(ll);
    if(this.moved&&frame-this.lastLogF>90){
      addLog(`🚙 ${this.name} → (${this.lat.toFixed(4)},${this.lng.toFixed(4)}) ${this.actual_kmh}km/h`);
      this.lastLogF=frame;
    }
  }
  remove(){this.marker.remove();this.ring.remove();this.sosRing.remove();this.trailLine.remove();this.labelM.remove();}
}

let cars=[],paused=false,frame=0;
const defaults=[
  {name:'Jeep K-1',color:'#00e5ff',routeIdx:0,kmh:45},
  {name:'Jeep K-2',color:'#ff6b35',routeIdx:1,kmh:60},
  {name:'Cruiser K-3',color:'#b9f542',routeIdx:2,kmh:40},
  {name:'Van K-4',color:'#e040fb',routeIdx:0,kmh:55},
  {name:'Bus K-5',color:'#ffd740',routeIdx:1,kmh:35},
];

function initCars(){
  cars.forEach(c=>c.remove());cars=defaults.map(d=>new Car(d));
  activeSOS=[];updateSOSBadgeBar();dismissSOS();
  document.getElementById('alertScroll').innerHTML='';
  document.getElementById('logBox').innerHTML='';
  addLog('✅ 5 vehicles loaded on real Maasai Mara routes');
  toast('Map loaded with real GeoJSON layers','🗺️','#fff9c4');
}

function updatePanel(){
  document.getElementById('vcount').textContent=cars.length;
  document.getElementById('carList').innerHTML=cars.map(c=>`
    <div class="crow" style="${c.hasSOS?'border-color:#ff1744;box-shadow:0 0 8px rgba(255,23,68,.3);':''}">
      <div class="crow-top">
        <div class="cdot" style="background:${c.hasSOS?'#ff1744':c.color};box-shadow:0 0 5px ${c.hasSOS?'#ff1744':c.color}66"></div>
        <span class="cname" style="color:${c.hasSOS?'#ff5252':c.color}">${c.name}</span>
        <span class="badge ${c.hasSOS?'sos-badge':c.offRoute?'off':'on'}">${c.hasSOS?'🆘 SOS':c.offRoute?'OFF ROAD':'On Route'}</span>
      </div>
      <div class="crow-mid">
        <span>${c.moved?c.actual_kmh+' km/h':'idle'}</span>
        <div class="spbar-wrap"><div class="spbar" style="width:${Math.min(c.actual_kmh,99)}%;background:${spColor(c.actual_kmh)}"></div></div>
        <span style="font-size:0.6em;color:#4a6a3a">R${c.routeIdx+1}</span>
      </div>
      <div class="crow-btns">
        <button class="cbtn cbtn-sos" onclick="openSOSModal(${c.id})">🆘 SOS</button>
        <button class="cbtn cbtn-notify" onclick="openNotifyModal(${c.id})">📣 Notify</button>
        <button class="cbtn cbtn-remove" onclick="removeCar(${c.id})">✕</button>
      </div>
    </div>`).join('');
}

function removeCar(id){
  const i=cars.findIndex(c=>c.id===id);if(i<0)return;
  if(!confirm(`Remove ${cars[i].name}?`))return;
  const n=cars[i].name;
  activeSOS=activeSOS.filter(s=>s.carId!==id);
  updateSOSBadgeBar();
  cars[i].remove();cars.splice(i,1);
  addLog(`🗑️ ${n} removed`);toast(`${n} removed`,'🗑️','#ef9a9a');
}

function addVehicle(){
  const name=document.getElementById('vName').value.trim()||`Vehicle ${nextId}`;
  const type=document.getElementById('vType').value;
  const ri=parseInt(document.getElementById('vRoute').value);
  const kmh=parseInt(document.getElementById('vSpeed').value);
  const color=document.getElementById('vColor').value;
  const car=new Car({name:`${type} — ${name}`,color,routeIdx:ri,kmh});
  cars.push(car);
  closeModal('addModal');
  addLog(`➕ ${car.name} added (${kmh}km/h, R${ri+1})`);
  toast(`${car.name} added`,'➕','#a5d6a7');
  map.flyTo([car.lat,car.lng],12,{duration:1});
  document.getElementById('vName').value='';
  document.getElementById('vSpeed').value=45;
  document.getElementById('speedVal').textContent='45';
}

document.getElementById('btnPause').onclick=()=>{
  paused=!paused;
  document.getElementById('btnPause').textContent=paused?'▶ Resume':'⏸ Pause';
  toast(paused?'Tracking paused':'Tracking resumed',paused?'⏸':'▶','#fff9c4');
};
document.getElementById('btnOffRoute').onclick=()=>{
  if(!cars.length){toast('No vehicles on map','⚠️','#f99');return;}
  const c=cars[Math.floor(Math.random()*cars.length)];
  c.forcedOff=true;c.offDur=0;c.offLat=c.lat;c.offLng=c.lng;
  addAlert(`Manual trigger: ${c.name} forced off route!`,'⚠️');
};
document.getElementById('btnReset').onclick=()=>{if(confirm('Reset all vehicles?'))initCars();};
document.getElementById('btnTestSOS').onclick=()=>{
  if(!cars.length){toast('No vehicles on map','⚠️','#f99');return;}
  const c=cars[Math.floor(Math.random()*cars.length)];
  currentSOSId=c.id;
  selectedSosType='⚠️ General Emergency';
  const utm=proj4('WGS84','EPSG:32737',[c.lng,c.lat]);
  const sos={id:Date.now(),carId:c.id,carName:c.name,color:c.color,
    type:'⚠️ General Emergency',details:'Test SOS — simulated emergency alert.',
    route:routeNames[c.routeIdx],speed:c.actual_kmh,
    lat:c.lat,lng:c.lng,utm:`${Math.round(utm[0])}, ${Math.round(utm[1])}`,time:ts()};
  activeSOS.push(sos);c.hasSOS=true;
  showSOSPopup(sos);
  addAlert(`🆘 TEST SOS from ${c.name}`,'🆘',true);
  updateSOSBadgeBar();
  toast(`Test SOS triggered for ${c.name}`,'🆘','#ff8a80');
};

function loop(){
  requestAnimationFrame(loop);
  if(paused)return;
  frame++;
  cars.forEach(c=>c.update(frame));
  if(frame%3===0)updatePanel();
}
initCars();
loop();
</script>
</body>
</html>
