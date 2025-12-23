<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Penggenapan Sisa Angka 2 Digit</title>

<style>
body{
  font-family:Arial,sans-serif;
  background:#f4f4f4;
  padding:20px
}
.box{
  max-width:700px;
  margin:auto;
  background:#fff;
  padding:16px;
  border-radius:8px;
  box-shadow:0 2px 8px rgba(0,0,0,.1)
}
textarea{
  width:100%;
  padding:10px;
  font-family:monospace;
  font-size:14px
}
#input{height:80px}
.result-box{
  border:1px solid #ccc;
  background:#fafafa;
  padding:8px;
  margin-top:8px
}
.result-box textarea{
  height:40px;
  font-weight:bold
}
button{
  padding:6px 12px;
  margin-top:8px;
  cursor:pointer
}
</style>
</head>

<body>
<div class="box">

<h3>Input Angka 2 Digit</h3>
<textarea id="input" placeholder="contoh: 00*01*02*03"></textarea>

<button onclick="proses()">Proses</button>

<h4>Hasil (Sisa Angka)</h4>
<div id="hasil"></div>

</div>

<script>
function proses(){
  const input=document.getElementById("input").value.trim()
  const hasil=document.getElementById("hasil")
  hasil.innerHTML=""

  // ambil input valid
  let inputNums=input.split("*")
    .map(x=>x.trim())
    .filter(x=>/^\d{2}$/.test(x))

  // buat set input
  let inputSet=new Set(inputNums)

  // cari sisa 00–99
  let sisa=[]
  for(let i=0;i<100;i++){
    let n=i.toString().padStart(2,"0")
    if(!inputSet.has(n)) sisa.push(n)
  }

  // acak
  sisa.sort(()=>Math.random()-0.5)

  // tampilkan max 10 per baris
  for(let i=0;i<sisa.length;i+=10){
    let slice=sisa.slice(i,i+10).join("*")
    let div=document.createElement("div")
    div.className="result-box"
    div.innerHTML=`<textarea readonly>${slice}</textarea>`
    hasil.appendChild(div)
  }
}
</script>

</body>
</html>

