---
title: Week 12 A3
published_at: 2024-2
snippet: Week 12
disable_html_sanitization: true

---

Hello, world

## Code developement
I was really inspired by the product [PureRef](https://www.pureref.com/) application infinite canvas. Following the [code](https://github.com/TomHumphries/InfiniteCanvasWhiteboard) provide by Tom Humphries, I manage to understand on the logic. <br>
What I want to achieve have 4 main parts: the drawing, the resize canvas so it appear infinite, the calculating of the coordinate and the panning, zooming, scrolling, dragging based on the coordinate. 

<br>

This is Tom Humpries code:

```
  // get our canvas element
        const canvas = document.getElementById("canvas");
        const context = canvas.getContext("2d");

        // disable right clicking
        document.oncontextmenu = function () {
            return false;
        }

        // list of all strokes drawn
        const drawings = [];

        // coordinates of our cursor
        let cursorX;
        let cursorY;
        let prevCursorX;
        let prevCursorY;

        // distance from origin
        let offsetX = 0;
        let offsetY = 0;

        // zoom amount
        let scale = 1;

        // convert coordinates
        function toScreenX(xTrue) {
            return (xTrue + offsetX) * scale;
        }
        function toScreenY(yTrue) {
            return (yTrue + offsetY) * scale;
        }
        function toTrueX(xScreen) {
            return (xScreen / scale) - offsetX;
        }
        function toTrueY(yScreen) {
            return (yScreen / scale) - offsetY;
        }
        function trueHeight() {
            return canvas.clientHeight / scale;
        }
        function trueWidth() {
            return canvas.clientWidth / scale;
        }

        function redrawCanvas() {
            // set the canvas to the size of the window
            canvas.width = document.body.clientWidth;
            canvas.height = document.body.clientHeight;

            context.fillStyle = '#fff';
            context.fillRect(0, 0, canvas.width, canvas.height);
            for (let i = 0; i < drawings.length; i++) {
                const line = drawings[i];
                drawLine(toScreenX(line.x0), toScreenY(line.y0), toScreenX(line.x1), toScreenY(line.y1));
            }
        }
        redrawCanvas();

        // if the window changes size, redraw the canvas
        window.addEventListener("resize", (event) => {
            redrawCanvas();
        });

        // Mouse Event Handlers
        canvas.addEventListener('mousedown', onMouseDown);
        canvas.addEventListener('mouseup', onMouseUp, false);
        canvas.addEventListener('mouseout', onMouseUp, false);
        canvas.addEventListener('mousemove', onMouseMove, false);
        canvas.addEventListener('wheel', onMouseWheel, false);

        // mouse functions
        let leftMouseDown = false;
        let rightMouseDown = false;
        function onMouseDown(event) {

            // detect left clicks
            if (event.button == 0) {
                leftMouseDown = true;
                rightMouseDown = false;
            }
            // detect right clicks
            if (event.button == 2) {
                rightMouseDown = true;
                leftMouseDown = false;
            }

            // update the cursor coordinates
            cursorX = event.pageX;
            cursorY = event.pageY;
            prevCursorX = event.pageX;
            prevCursorY = event.pageY;
        }
        function onMouseMove(event) {
            // get mouse position
            cursorX = event.pageX;
            cursorY = event.pageY;
            const scaledX = toTrueX(cursorX);
            const scaledY = toTrueY(cursorY);
            const prevScaledX = toTrueX(prevCursorX);
            const prevScaledY = toTrueY(prevCursorY);

            if (leftMouseDown) {
                // add the line to our drawing history
                drawings.push({
                    x0: prevScaledX,
                    y0: prevScaledY,
                    x1: scaledX,
                    y1: scaledY
                })
                // draw a line
                drawLine(prevCursorX, prevCursorY, cursorX, cursorY);
            }
            if (rightMouseDown) {
                // move the screen
                offsetX += (cursorX - prevCursorX) / scale;
                offsetY += (cursorY - prevCursorY) / scale;
                redrawCanvas();
            }
            prevCursorX = cursorX;
            prevCursorY = cursorY;
        }
        function onMouseUp() {
            leftMouseDown = false;
            rightMouseDown = false;
        }
        function onMouseWheel(event) {
            const deltaY = event.deltaY;
            const scaleAmount = -deltaY / 500;
            scale = scale * (1 + scaleAmount);

            // zoom the page based on where the cursor is
            var distX = event.pageX / canvas.clientWidth;
            var distY = event.pageY / canvas.clientHeight;

            // calculate how much we need to zoom
            const unitsZoomedX = trueWidth() * scaleAmount;
            const unitsZoomedY = trueHeight() * scaleAmount;

            const unitsAddLeft = unitsZoomedX * distX;
            const unitsAddTop = unitsZoomedY * distY;

            offsetX -= unitsAddLeft;
            offsetY -= unitsAddTop;

            redrawCanvas();
        }
        function drawLine(x0, y0, x1, y1) {
            context.beginPath();
            context.moveTo(x0, y0);
            context.lineTo(x1, y1);
            context.strokeStyle = '#000';
            context.lineWidth = 2;
            context.stroke();
        }
```
The code already have all 4 base thing I want, and it was my job to figure out how to apply the code to a div that have an audio element so the element can be panned, zoomed and dragged. However it took me quite a long time to figure out how to put an audio along with the canvas. 

## Final product
Left click to drag or draw. <br>
Middle click to pan. <br> 
Right click to move canvas. <br>
Scrollwheel to zoom. <br>

<br>

<iframe width="100%" height=1200px src="https://happiesday-a3-interest-56.deno.dev/"></iframe>

<br>

<br>