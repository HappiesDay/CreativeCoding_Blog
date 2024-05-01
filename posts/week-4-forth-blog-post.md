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
Please welcome my broccoli

<br>

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
cnv.height = innerHeight/1.5

const ctx = cnv.getContext('2d')

// Drawing setup
ctx.fillStyle = '#A6B8A5'
ctx.strokeStyle = '#A6B8A5'
ctx.lineWidth = 30
ctx.lineCap = 'round'
ctx.save()
ctx.translate(0,cnv.height/2)
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
    if (level > 7) {
        ctx.strokeStyle = '#02590F'; // New stroke color
    }
    else {
      ctx.strokeStyle = '#A6B8A5'
    }
   ctx.beginPath()
   ctx.moveTo(0,0)
   ctx.lineTo(size,0)
   ctx.stroke()

   ctx.save()
   ctx.translate(size/2,0)
   ctx.rotate(spread)
   ctx.scale(scale, scale)
   drawBranch(level + 1)
   ctx.strokeStyle = '#02590F'
   ctx.restore()

   ctx.save()
   ctx.translate(size/2,0)
   ctx.rotate(-spread)
   ctx.scale(scale, scale)
   drawBranch(level + 1)
   ctx.restore()

  
}
drawBranch(0)

})

</script>

```
<canvas id='fractal_broccoli'></canvas>
<script>
// Default setup

document.body.style.margin = 0;


window.addEventListener('load', function()
{
const cnv = document.getElementById('fractal_broccoli')
cnv.width = innerWidth
cnv.height = innerHeight/2

const ctx = cnv.getContext('2d')

// Drawing setup
ctx.fillStyle = '#A6B8A5'
ctx.strokeStyle = 'black'
ctx.lineWidth = 30
ctx.lineCap = 'round'
ctx.save()
ctx.translate(0,cnv.height/2)
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

})

</script>

```


<br>

When doing this fractal, my main takeaway is how the canvas context API was applied in this work. 
Firstly the basic foundation to draw the stroke consist of [these 4](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo)

```
ctx.beginPath()
   ctx.moveTo(x,y)
   ctx.lineTo(x,y)
   ctx.stroke()

```
<br>

These 4 are essential to create a stroke and can be used for more advance polygons but here i only need the thick strokes so I only need one ctx.lineTo. The combination of the 4 feels like a vector drawing programm like Adobe Illustrator where *beginPath* is when you click the pen icon, *moveTo* is when you click on the canvas and it shows a dot, *lineTo* is when you dragged the mouse and a dynamic line that follows your cursor and *ctx.Stroke* is when you click again to settle the line. However in this work I don't utilise the x and y position as much since most of it are done via the ctx.translate in  which requires less calculations and relies on ctx.save and ctx.restore more.

```
   ctx.save()
   ctx.translate(x,y)
   ctx.rotate(r) //r as in Radiant, max is ~3.14
   ctx.scale(s1, s2)
   drawBranch(level + 1) //recursion with condition
   ctx.restore()

```

<br>

In here is where the iteration occur with the use of recursion by calling itself within the function, however in here I set a level condition so the function doesn't loop infinitly and I also use level to change the color of the end bits of the broccoli. This broccoli is absense of randomness since I like how the branches symmertically bloom better.
By the use of recursion, we can introduce intricate patterns, complex textures but dynamic. It achieves a share similiar attribute with loops which maximize the visual therefore enhanced the chaos. Moreover, recursion can generate unbounded iterations growth in data structures or processes, potentially crashing, which fits the A2 post-digital theme and unpredictable outcomes.

<br>

<br>