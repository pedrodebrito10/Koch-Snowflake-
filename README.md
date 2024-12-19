let level = 0;
let colorOffset;
let colorlist = ['#e6194b', '#3cb44b', '#ffe119', '#4363d8', '#f58231', '#911eb4', '#46f0f0', '#f032e6', '#bcf60c', '#fabebe', '#008080', '#e6beff', '#9a6324', '#fffac8', '#800000', '#aaffc3', '#808000', '#ffd8b1', '#000075', '#808080', '#ffffff', '#000000'];

function setup() {
  createCanvas(600, 600);
  ellipseMode(RADIUS);
  noFill();
  noStroke();
  noLoop();  
  colorOffset = int(random(colorlist.length));
}

function draw() {
  background(220);
  translate(width/2, height/2);
  setFillForCurrentLevel();
  rCircle(-width/4, width/2);  // Draw the left side
  rCircle(width/4, width/2);   // Draw the right side
}

function setFillForCurrentLevel() {
  fill(colorlist[(level + colorOffset) % colorlist.length]);
}

function rCircle(x, d) {
  level++;
  const r = d / 2;
  if (r > 2) {  // Base case: stop when the diameter gets too small
    push();
    translate(x, 0);
    circle(0, 0, r);  // Draw the current circle
    const d1 = random(0.3, 0.7) * d;  // Split diameter randomly
    const d2 = d - d1;  // Remaining part of the diameter
    const r1 = d1 / 2;  // Radius of the first smaller circle
    const r2 = d2 / 2;  // Radius of the second smaller circle
    const x1 = -r + r1;  // Position of the left circle
    const x2 = x1 + r1 + r2;  // Position of the right circle
    rotate(random(TWO_PI));  // Rotate to add variation
    setFillForCurrentLevel();  // Set color for the current level
    rCircle(x1, d1);  // Recursively draw the left smaller circle
    rCircle(x2, d2);  // Recursively draw the right smaller circle
    pop();
  }
  level--;
}




FULL EXPLINATION
Setup Function:

createCanvas(600, 600): This Creates the canvas where I draw tbe Koch Snowflake. 
ellipseMode(RADIUS): This makes sures that the circles are drawn from their radius.
noLoop(): Prevents continuous drawing so we only draw once.
draw Function:

translate(width/2, height/2): This moves the origin to the center so the snowflake grows around the center
Calls rCircle(-width/4, width/2) and rCircle(width/4, width/2) to draw the left and right parts.
rCircle(x, d):

level++: Increases the recursion depth.
r = d / 2: The radius of the circle is half the diameter.
Base case: Stops the recursion when the diameter is too small (r > 2).
Drawing logic: this draws cirbles and splits them into smaller circles
Coloring: Uses colorOffset to cycle through colors to make the snowflake colorful at each recursion level.
Rotate and translate: Adds variation to the shapes and positions to create the snowflake effect.
