---
title: Week 4 Fractal and Recursion 
published_at: 2024-3
snippet: Week 4
disable_html_sanitization: true

---

Hello, world


# Fractal 
## What is fractal aesthetic?

Fractal aesthetics can be easily understood without an explanation of mathematics. They feature "self-similarity," repetitive and detailed patterns. The defining attribute is high complexity, as the visual continues, creating mini versions of itself that reappear and scale down all the data (Mandelbrot 1983), rendering it a densely related visual. <br>
Fractals, born from recursion's embrace in computation and mathematic is chaotic by nature as it fits 3 of Ngai desciption on the zanni aesthetic: performative, execessive and mimicry. 
Mirroring the recursive nature of fractals' self-replicating patterns and through their dynamic and self iterating attribute of recusion, fractals encapsulate the essence of chaos, exaggerated gestures to draw us into their mesmerizing world of complexity.<br>
[Wiki Fractal (More on the mathematic history)](https://en.wikipedia.org/wiki/Fractal) <br>


Geometry and symmetrical present us it's crowded chaotic order with [Sierpiński triangle](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle) or [Gosper curve](https://en.wikipedia.org/wiki/Fractal_curve) while its nature counterpart bring about the fancy irregularity in simple objects such as seashell, snowflake and brocolli.

<br>

## My attempt at Broccoli Fractal
I follow [this tutorial](https://www.youtube.com/watch?v=dQKYao-daYw&t=1693s) by Frank laboratory
<br>
<canvas id='fractal_broccoli'></canvas>
<script>
// Default setup

document.body.style.margin = 0;


window.addEventListener('load', function()
{
const cnv = document.getElementById('fractal_broccoli')
cnv.width = innerWidth
cnv.height = innerHeight

const ctx = cnv.getContext('2d')

// Drawing setup
ctx.fillStyle = '#A6B8A5'
ctx.strokeStyle = 'black'
ctx.lineWidth = 30
ctx.lineCap = 'round'
ctx.save()
ctx.translate(cnv.width/3,cnv.height/2)
ctx.scale(1,1)
ctx.rotate(0)


let size = 200
let sides = 2
let maxLevel = 10
let scale = 0.7
let spread = 0.5 //radiant unit, max is 3.14
let branhces = 2


function drawBranch(level)
{
   if (level> maxLevel) return
   ctx.beginPath()
   ctx.moveTo(0,0)
   ctx.lineTo(size,0)
   ctx.stroke()

   ctx.save()
   ctx.translate(size/2,0)
   ctx.rotate(spread)
   ctx.scale(scale, scale)
   drawBranch(level + 1)
   ctx.restore()

   ctx.save()
   ctx.translate(size/2,0)
   ctx.rotate(-spread)
   ctx.scale(scale, scale)
   drawBranch(level + 1)
   ctx.restore()

}
drawBranch(0)

// for (let i = 0; i < sides; i++)
// {  
// console.log('hekki')



// ctx.fillRect (50,50,100,100)
// ctx.beginPath()
// ctx.moveTo(0,0)
// ctx.lineTo(size,0)
// console.log('0')
// ctx.stroke()
// ctx.restore()
// }
})

</script>

<br>
With coherent aesthetic frame, we can bypass some originality novelty, refrains its unexpectability to certain mood and style. This approach effective gives it an inherent foundation and composition that can be built upon. The redundancy is not just tolerated but is a key feature of the aesthetic, contributing to the overall experience in a soothing and comforting respond. 


<br>
