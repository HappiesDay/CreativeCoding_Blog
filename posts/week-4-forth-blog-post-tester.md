---
title: Week 11 Fractal and Recursion 
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

<canvas id='fractal_tree_0'></canvas>

<script type='module'>

    // get and format canvas
const cnv = document.getElementById ('fractal_tree_0')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16

    // get canvas context
    const ctx = cnv.getContext ('2d')

    // this is the recursive function that will draw the tree
    // it accepts three arguments:
    // base: vector describing the starting position
    // stem: vector describing the new line
    // generation: integer limiting the number of recursions
    function tree (base, stem, generation) {

        // start with the base position
        // we want to tranform it, so we make a copy
        const end = base.clone ()

        // add the stem to the start position
        end.add (stem)

        // draw the line from the start point
        // to the end point
        ctx.beginPath ()
        ctx.moveTo (base.x, base.y)
        ctx.lineTo (end.x, end.y)
        ctx.stroke ()

        // if generations is still positive
        if (generation > 0) {

            // clone the stem
            const L_stem = stem.clone ()

            // rotate it anti-clockwise
            L_stem.rotate (-TAU / 7)

            // reduce the length
            L_stem.mult (0.6)

            // clone the stem again
            const R_stem = stem.clone ()

            // rotate this one clockwise
            R_stem.rotate (TAU / 7)

            // reduce its length
            R_stem.mult (0.6)

            // decrease generation by 1
            const next_gen = generation - 1

            // recursively call tree twice, 
            // with end as the new base
            // L_stem & R_stem as the new stems
            // and next_gen as the new generation
            tree (end, L_stem, next_gen)
            tree (end, R_stem, next_gen)
        }
    }
   const Vector
    // new vector defining the starting point of our tree
    const seed = new Vector (cnv.width / 2, cnv.height)

    // new vector defining the first stem
    // ie. 150 pixels straight up
    const shoot = new Vector (0, -150)

    // pass seed in as the base argument
    // shoot as the stem argument
    // and 7, denoting that we want 7 recursions
    tree (seed, shoot, 7)
</script>