---
title: Week 7 
published_at: 2024-5
snippet: Week 7
disable_html_sanitization: true

---

Hello, world

# Asci cam combine with week 5 glitch

<canvas id="glitch_self_portrait"></canvas>
<script src="/scripts/glitch.js"></script>

# LOL
<div id="ascii_div"></div>
<canvas id="glitch_self_portrait" style="display:none;"></canvas>

<script type="module">
    const cnv = document.getElementById(`glitch_self_portrait`);
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;

    const ctx = cnv.getContext(`2d`);
    let img_data;

    const draw = i => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

    const img = new Image();
    img.onload = () => {
        cnv.height = cnv.width * (img.height / img.width);
        draw(img);
        img_data = cnv.toDataURL("image/jpeg");
        add_glitch();
    };
    img.src = `/images/creepy.jpg`;

    const rand_int = max => Math.floor(Math.random() * max);

    const glitchify = (data, chunk_max, repeats) => {
        const chunk_size = rand_int(chunk_max / 4) * 4;
        const i = rand_int(data.length - 24 - chunk_size) + 24;
        const front = data.slice(0, i);
        const back = data.slice(i + chunk_size);
        const result = front + back;
        return repeats === 0 ? result : glitchify(result, chunk_max, repeats - 1);
    };

    const glitch_arr = [];

    const add_glitch = () => {
        const i = new Image();
        i.onload = () => {
            glitch_arr.push(i);
            if (glitch_arr.length < 12) add_glitch();
            else draw_frame();
        };
        i.src = glitchify(img_data, 96, 6);
    };

    let is_glitching = false;
    let glitch_i = 0;

    const ascii_div = document.getElementById(`ascii_div`);
    ascii_div.style.fontFamily = `monospace`;
    ascii_div.style.textAlign = `center`;

    const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙";

    const draw_frame = () => {
        const imageToDraw = is_glitching ? glitch_arr[glitch_i] : img;
        draw(imageToDraw);

        // Convert canvas to ASCII
        const pixels = ctx.getImageData(0, 0, cnv.width, cnv.height).data;
        let ascii_img = ``;
        for (let y = 0; y < cnv.height; y += 2) {
            for (let x = 0; x < cnv.width; x++) {
                const i = (y * cnv.width + x) * 4;
                const r = pixels[i], g = pixels[i + 1], b = pixels[i + 2];
                const br = (r * g * b / 16581376) ** 0.1;
                const char_i = Math.floor(br * chars.length);
                ascii_img += chars[char_i];
            }
            ascii_img += `\n`;
        }
        ascii_div.innerText = ascii_img;

        if (Math.random() < (is_glitching ? 0.05 : 0.02)) {
            glitch_i = rand_int(glitch_arr.length);
            is_glitching = !is_glitching;
        }

        requestAnimationFrame(draw_frame);
    };

    img.src = `/images/creepy.jpg`; // Ensure this path is correct and the image exists
</script>



## Why does combining ideas / libraries seem to make things more aesthetically chaotic?  
Combining ideas and or libraries will increase the nonlinearity directions of the work. In effective complexity, even though it consists of randomness, there are typically some limits to keep things from getting too chaotic and ensure the non-random components remain visible. However when combining ideas and libraries, the limit factor does not proportionally expand to keep up with the new variations. Furthermore, when presented with multiple ideas simultaneously, especially if they are complex or unfamiliar, the cognitive load increases therefore make the visual having more weight and harder to handle, therefore maximizing the discord in communicating the idea effiecently. This complexity can also make it tougher to communicate clearly, which might lead to misunderstandings or confusion, adding to the overall sense of chaos.