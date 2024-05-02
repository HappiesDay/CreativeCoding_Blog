---
title: Week 6 Three Js and C2
published_at: 2024-4
snippet: Week 5
disable_html_sanitization: true

---

Hello, world

<style>
@font-face {
    font-family: GOSTAi;
    src: url("https://cywarr.github.io/small-shop/GOSTtypeAitalic.ttf") format("truetype");
}
body{
  overflow: hidden;
  margin: 0;
  background-color: #face8d;
}

#cnv{
  position: absolute;
  top: calc(50% - 410px);
  left: calc(50% - 410px);
  border: 10px solid #800000;
  border-radius: 20px;
}

.writing{
  position: absolute;
  font-family: GOSTAi;
  -webkit-text-fill-color: aquamarine;
  pointer-events: none;
}

.unselectable {
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

#idWire{
  top:calc(50% - 390px);
  left:calc(50% - 390px);
  font-size: 80px;
  -webkit-text-stroke: 2px darkgreen;
}

#idRev{
  bottom: calc(50% - 390px);
  right: calc(50% - 390px);
  font-size: 40px;
  -webkit-text-stroke: 1px darkgreen;
}
</style>

# Three js
<canvas id="cnv" width="800" height="800"></canvas>
<div class="writing unselectable" id="idWire">Wire Boxes</div>
<div class="writing unselectable" id="idRev">Rev0.1</div>
<script async src="https://ga.jspm.io/npm:es-module-shims@1.5.1/dist/es-module-shims.js" crossorigin="anonymous"></script>
<script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@0.149.0/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@0.149.0/examples/jsm/"
    }
  }
</script>