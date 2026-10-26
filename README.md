# Digital-journal
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Digital Journal</title>
<style>
*{box-sizing:border-box}
body{margin:0;padding:24px;background:#171521;color:#f7f1ff;font-family:Arial}
main{max-width:800px;margin:auto}
header{padding:20px 0}
form,.entry{background:#242235;border:1px solid #403953;border-radius:15px;padding:20px;margin:14px 0}
input,textarea,select{width:100%;padding:12px;margin:7px 0 14px;border-radius:8px;border:1px solid #514865;background:#171521;color:white}
button{background:#d5a6ff;color:#241235;padding:12px 16px;border:0;border-radius:8px;cursor:pointer;font-weight:bold}
.entry small{color:#c0b2d5}
</style>
</head>
<body>
<main>
<header><p>YOUR PRIVATE SPACE</p><h1>Dear Journal ✦</h1><p>Pause. Reflect. Begin again.</p></header>
<form id="form">
<label>Today's mood</label>
<select id="mood"><option>😊 Good</option><option>😌 Calm</option><option>😐 Okay</option><option>😔 Difficult</option><option>🔥 Motivated</option></select>
<label>Entry title</label><input id="title" placeholder="A small moment..." required>
<label>Your thoughts</label><textarea id="body" rows="5" placeholder="Write freely..." required></textarea>
<button>Save Entry</button>
</form>
<h2>Past Reflections</h2><div id="list"></div>
</main>
<script>
const $=id=>document.getElementById(id);
let entries=JSON.parse(localStorage.journal||"[]");
function esc(s){return String(s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]))}
function draw(){
$("list").innerHTML=entries.map((e,i)=>`
<article class="entry"><small>${e.date} · ${esc(e.mood)}</small>
<h2>${esc(e.title)}</h2><p style="white-space:pre-wrap">${esc(e.body)}</p>
<button onclick="del(${i})">Delete</button></article>`).join("")||"<p>Your first entry can start today.</p>";
localStorage.journal=JSON.stringify(entries);
}
function del(i){entries.splice(i,1);draw()}
$("form").onsubmit=e=>{
e.preventDefault();
entries.unshift({date:new Date().toLocaleDateString(),mood:$("mood").value,title:$("title").value,body:$("body").value});
$("title").value="";$("body").value="";draw();
};
draw();
</script>
</body>
</html>
