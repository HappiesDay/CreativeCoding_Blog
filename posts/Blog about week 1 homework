let angle = 0;
function setup() {
  createCanvas(innerWidth, innerHeight);
  ellipseMode(CENTER)
  rectMode(CENTER)
  noStroke()
  console. log("Set up works")
  angleMode(DEGREES)
  
}
function draw(){
//  background(220) DONT UNDERSTAND WHY A BACKGROUND IS A MUST HERE 
  // Calculate the difference between the mouse position and the center of     the canvas

  let deltaX = mouseX - width / 2;
  let deltaY = mouseY - height / 2;

  // Calculate the angle between the line from the center to the mouse position and the         horizontal axis

  // circle(innerWidth/2,innerHeight/2 , innerWidth/2) 

  translate(width/2, height/2)
  rotate(angle)
  fill('green');
  rect(0,0, 52, 52);
  angle = atan2(deltaY, deltaX);
  console. log("Rotate base on mouse works")  

}


//Steps: Create a circle in the middle, then create a gradient background, then make the gradient follow the mouse cursor value

//REF: https://editor.p5js.org/Antman/sketches/BLMo8XfS https://p5js.org/reference/#/p5/angleMode https://p5js.org/reference/#/p5/rotate https://p5js.org/reference/#/p5/lerpColor 