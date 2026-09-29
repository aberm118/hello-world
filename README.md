# human-artifact
 <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Each new way of sending a message replaced the last</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@600;800&family=Source+Serif+4:wght@400;600&display=swap">
<style>
:root{--bg:#e6edf1;--ink:#16303b;--soft:#4b6672;--card:#fff;--line:#b9c9d1;--blue:#1f4fe0;--gold:#f2c230}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:18px/1.6 "Source Serif 4",Georgia,serif}
main{max-width:720px;margin:0 auto;padding:40px 20px 80px}
h1{font:800 clamp(2rem,6vw,3.2rem)/1.05 "Bricolage Grotesque",Arial,sans-serif;margin:0 0 14px}
.lead{color:var(--soft);margin:0 0 24px}
.tools{display:flex;gap:10px;align-items:center;flex-wrap:wrap;margin-bottom:28px}
.toggle{font:600 15px "Bricolage Grotesque",Arial,sans-serif;border:2px solid var(--ink);background:var(--card);color:var(--ink);padding:9px 16px;border-radius:999px;cursor:pointer}
.toggle[aria-pressed="true"]{background:var(--ink);color:#fff}
.hint{font-size:15px;color:var(--soft)}
ol{list-style:none;margin:0;padding:0 0 0 26px;border-left:4px solid var(--blue)}
li{position:relative;margin:0 0 18px}
li::before{content:"";position:absolute;left:-36px;top:20px;width:16px;height:16px;border-radius:50%;background:var(--bg);border:4px solid var(--blue)}
li.open::before{background:var(--gold)}
.head{width:100%;text-align:left;background:var(--card);border:2px solid var(--line);border-radius:12px;padding:14px 18px;cursor:pointer;color:inherit;font:inherit;display:grid;grid-template-columns:1fr auto;gap:2px 12px}
.head:hover,.head:focus-visible{border-color:var(--blue);outline:none}
.yr{font:600 14px "Bricolage Grotesque",Arial,sans-serif;color:var(--blue)}
.name{font:800 1.3rem/1.2 "Bricolage Grotesque",Arial,sans-serif;grid-column:1}
.time{grid-column:2;grid-row:1/3;align-self:center;background:var(--gold);padding:4px 10px;border-radius:8px;font:600 14px "Bricolage Grotesque",Arial,sans-serif;text-align:center}
.body{display:none;background:var(--card);border:2px solid var(--blue);border-top:0;border-radius:0 0 12px 12px;padding:14px 18px;margin-top:-6px}
li.open .body{display:block}
li.open .head{border-color:var(--blue);border-radius:12px 12px 0 0}
.body p{margin:0 0 10px}
.replaced{font-weight:600}
.ghost{display:none;border-left:4px solid var(--gold);padding:6px 12px;background:#fff8dc;margin:10px 0}
body.ghosts .ghost{display:block}
.src{font-size:14px;color:var(--soft);margin:0}
footer{margin-top:36px;font-size:14px;color:var(--soft)}
@media (prefers-reduced-motion:no-preference){.body{animation:o .2s ease-out}@keyframes o{from{opacity:0}to{opacity:1}}}
</style>
</head>
<body>
<main>
<h1>Every way of sending a message was replaced by a faster one</h1>
<p class="lead">Follow one job, getting words from one person to another far away, through five technologies. Each one superseded the last. Click any stop to open it.</p>
<div class="tools">
  <button class="toggle" id="ghostBtn" aria-pressed="false">Show what survived</button>
  <button class="toggle" id="allBtn" aria-pressed="false">Open all</button>
  <span class="hint">Yellow badge = time to send a message across the U.S.</span>
</div>
<ol id="tl"></ol>
<footer>Sources are listed on each stop. The "what survived" notes are my own interpretation of the course idea that older technologies leave a ghostly presence in newer ones.</footer>
</main>
<script>
const stops=[
{yr:"1860",name:"Pony Express",time:"About 10 days",
 what:"Riders on relay horses carried mail between Missouri and California, swapping horses at stations along the route.",
 replaced:"Replaced: months-long mail by ship or wagon.",
 ghost:"Relay stations handed the mail along one hop at a time. Internet data is still passed hop by hop between routers (my analogy).",
 src:"Source: Smithsonian National Postal Museum, Pony Express history."},
{yr:"1844; coast to coast 1861",name:"Telegraph",time:"Minutes",
 what:"Samuel Morse sent \"What hath God wrought\" from Washington to Baltimore on May 24, 1844. Messages became electrical signals on a wire. In October 1861 the line reached the West Coast and the Pony Express closed within days.",
 replaced:"Replaced: the Pony Express, which had run for only about 18 months.",
 ghost:"We still say \"wire money.\" Money transfers by telegraph became a business, and the word outlived the wires.",
 src:"Source: Library of Congress, Morse and the telegraph; Smithsonian National Postal Museum."},
{yr:"1876",name:"Telephone",time:"Live voice",
 what:"Alexander Graham Bell was granted his patent on March 7, 1876. For the first time, people could hear each other's voice instead of reading coded taps.",
 replaced:"Replaced: telegraph for personal, everyday conversation (telegraph kept business and news uses for decades).",
 ghost:"We \"hang up\" and \"dial\" a phone that has no hook and no dial.",
 src:"Source: U.S. Patent No. 174,465; Library of Congress, Alexander Graham Bell papers."},
{yr:"1971",name:"Email",time:"Seconds",
 what:"Ray Tomlinson sent the first email between computers on the ARPANET and chose the @ sign to separate user from machine.",
 replaced:"Replaced: paper letters and internal memos for most written office communication.",
 ghost:"\"CC\" still means carbon copy, from paper made with carbon sheets. We also still use an \"inbox\" and \"folders.\"",
 src:"Source: Computer History Museum, history of email; Ray Tomlinson obituaries (2016)."},
{yr:"1992",name:"Text message (SMS)",time:"Seconds",
 what:"On December 3, 1992, engineer Neil Papworth sent \"Merry Christmas\" over the Vodafone network. It was the first SMS.",
 replaced:"Replaced: many short phone calls and pagers.",
 ghost:"The 160-character limit came from the original SMS design and shaped the way people abbreviate messages.",
 src:"Source: BBC News and Vodafone coverage of the first SMS; GSM standards history."}
];
const tl=document.getElementById("tl");
stops.forEach((s,i)=>{
 const li=document.createElement("li");
 li.innerHTML=`<button class="head" aria-expanded="false" aria-controls="b${i}">
 <span class="yr">${s.yr}</span><span class="name">${s.name}</span><span class="time">${s.time}</span></button>
 <div class="body" id="b${i}"><p>${s.what}</p><p class="replaced">${s.replaced}</p>
 <div class="ghost"><strong>What survived:</strong> ${s.ghost}</div><p class="src">${s.src}</p></div>`;
 const b=li.querySelector(".head");
 b.onclick=()=>{const o=li.classList.toggle("open");b.setAttribute("aria-expanded",o)};
 tl.appendChild(li);
});
const g=document.getElementById("ghostBtn");
g.onclick=()=>{const on=document.body.classList.toggle("ghosts");g.setAttribute("aria-pressed",on)};
const a=document.getElementById("allBtn");
a.onclick=()=>{const on=a.getAttribute("aria-pressed")!=="true";a.setAttribute("aria-pressed",on);
 a.textContent=on?"Close all":"Open all";
 tl.querySelectorAll("li").forEach(li=>{li.classList.toggle("open",on);li.querySelector(".head").setAttribute("aria-expanded",on)})};
</script>
</body>
</html>
