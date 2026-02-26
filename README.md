<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Holi & Dhuleti College Project</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Segoe UI, sans-serif;
}

body{
    min-height:100vh;
    background:linear-gradient(135deg,#12001f,#24003d);
    display:flex;
    align-items:center;
    justify-content:center;
    overflow:hidden;
    color:white;
}

.container{
    text-align:center;
    padding:25px;
    max-width:620px;
}

h1{
    font-size:32px;
    margin-bottom:10px;
}

p{
    margin-top:10px;
    line-height:1.6;
    display:none;
}

button{
    margin-top:15px;
    padding:12px 22px;
    border:none;
    border-radius:25px;
    background:linear-gradient(45deg,#ff0080,#ffcc00);
    color:#000;
    font-weight:600;
    font-size:15px;
    cursor:pointer;
}

.modeBtns{
    display:none;
    margin-top:10px;
}

.modeBtns button{
    margin:6px;
}

/* ---------------- REAL POWDER GULAL ---------------- */

.gulal{
    position:absolute;
    width:28px;
    height:22px;
    background:
        radial-gradient(circle at 30% 30%,
        rgba(255,255,255,0.9),
        var(--c) 40%,
        rgba(0,0,0,0.05) 70%);
    border-radius:45% 55% 60% 40% / 55% 40% 60% 45%;
    filter: blur(1.2px);
    pointer-events:none;
    opacity:0.95;
    animation:powder 950ms ease-out forwards;
}

@keyframes powder{
    to{
        transform:
            translate(var(--x),var(--y))
            scale(var(--s))
            rotate(var(--r));
        opacity:0;
        filter: blur(5px);
    }
}

/* ---------------- DHULETI WATER ---------------- */

.water{
    position:absolute;
    width:8px;
    height:14px;
    border-radius:50%;
    background:rgba(120,200,255,0.9);
    pointer-events:none;
    animation:waterMove 900ms ease-out forwards;
}

@keyframes waterMove{
    to{
        transform:translate(var(--x),var(--y));
        opacity:0;
    }
}

.drop{
    position:absolute;
    width:4px;
    height:12px;
    border-radius:50%;
    background:rgba(150,220,255,0.9);
    animation:fall 1.2s linear forwards;
    pointer-events:none;
}

@keyframes fall{
    to{
        transform:translateY(120px);
        opacity:0;
    }
}

.badge{
    margin-top:15px;
    font-size:18px;
    display:none;
}
</style>
</head>
<body>

<div class="container">
    <h1>Holi & Dhuleti Celebration</h1>

    <button id="startBtn">Start Wishing</button>

    <div class="modeBtns" id="modeBtns">
        <button id="holiBtn">Holi – Gulal</button>
        <button id="dhuletiBtn">Dhuleti – Water</button>
    </div>

    <p id="msg1">
        🌸 Wishing you and your family a very Happy Holi & Dhuleti!  
        May your life be filled with colours of happiness and success.
    </p>

    <p id="msg2">
        This is a college mini project using HTML, CSS and JavaScript.
        Click anywhere on the screen to enjoy gulal and water splash effects.
    </p>

    <div class="badge" id="badge">
        🎉 Happy Holi • Happy Dhuleti 🎉
    </div>
</div>

<script>
const startBtn = document.getElementById("startBtn");
const msg1 = document.getElementById("msg1");
const msg2 = document.getElementById("msg2");
const badge = document.getElementById("badge");
const modeBtns = document.getElementById("modeBtns");

const holiBtn = document.getElementById("holiBtn");
const dhuletiBtn = document.getElementById("dhuletiBtn");

let mode = "holi";

startBtn.onclick = () =>{
    msg1.style.display="block";
    msg2.style.display="block";
    badge.style.display="block";
    modeBtns.style.display="block";
    startBtn.style.display="none";
};

holiBtn.onclick = ()=> mode = "holi";
dhuletiBtn.onclick = ()=> mode = "dhuleti";

document.addEventListener("click",(e)=>{

    if(e.target.tagName==="BUTTON") return;

    if(mode === "holi"){
        holiEffect(e.clientX,e.clientY);
    }else{
        dhuletiEffect(e.clientX,e.clientY);
    }

});

/* ---------------- HOLI POWDER EFFECT ---------------- */

function holiEffect(x,y){

    const colors=[
        "#ff1744","#ffea00","#00e5ff",
        "#76ff03","#ff9100","#e040fb"
    ];

    for(let i=0;i<24;i++){

        const g=document.createElement("div");
        g.className="gulal";

        g.style.left=(x-12)+"px";
        g.style.top=(y-12)+"px";

        const color=colors[Math.floor(Math.random()*colors.length)];
        g.style.setProperty("--c",color);

        g.style.setProperty("--x",(Math.random()*240-120)+"px");
        g.style.setProperty("--y",(Math.random()*220-110)+"px");
        g.style.setProperty("--r",(Math.random()*360)+"deg");
        g.style.setProperty("--s",(0.8+Math.random()*1.2));

        document.body.appendChild(g);

        setTimeout(()=>g.remove(),950);
    }
}

/* ---------------- DHULETI WATER EFFECT ---------------- */

function dhuletiEffect(x,y){

    for(let i=0;i<28;i++){

        const w=document.createElement("div");
        w.className="water";

        w.style.left=x+"px";
        w.style.top=y+"px";

        w.style.setProperty("--x",(Math.random()*180-90)+"px");
        w.style.setProperty("--y",(Math.random()*-120)+"px");

        document.body.appendChild(w);

        setTimeout(()=>w.remove(),900);
    }

    for(let j=0;j<10;j++){

        const d=document.createElement("div");
        d.className="drop";

        d.style.left=(x + Math.random()*40-20)+"px";
        d.style.top=(y + 5)+"px";

        document.body.appendChild(d);

        setTimeout(()=>d.remove(),1200);
    }

}
</script>

</body>
</html>
