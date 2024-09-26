
# 1-Up Workshop: Animating with HTML Canvas and JavaScript

## Purpose
In this workshop, we’ll explore basic animation using the HTML `<canvas>` element and JavaScript. We'll focus on the essential methods for drawing and updating visuals on the canvas.

---

## 1. Setting Up the Canvas

We use the `<canvas>` element in HTML as a drawing area. To interact with it using JavaScript, we get its **2D rendering context**, which provides methods to draw shapes and objects.

### Key Methods:
- `getContext('2d')`: Initializes a 2D drawing context, which gives us access to canvas drawing methods.

### Code:
```javascript
const canvas = document.getElementById('animationCanvas');
const ctx = canvas.getContext('2d');
```

This sets up the canvas and makes it full screen:

```javascript
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

> **Why?** `getContext('2d')` allows us to draw 2D shapes and animations on the canvas. The canvas size matches the window to create a full-screen animation environment.

---

## 2. Drawing Shapes

We use the `arc()` method to draw a circle (representing a circle) on the canvas.

### Key Method:
- `ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise)`: Draws an arc (circle). 
  - `x`, `y`: Center of the circle.
  - `radius`: Radius of the circle.
  - `startAngle`: Starting point in radians (0 = right side of circle).
  - `endAngle`: End point in radians (`2 * Math.PI` for a full circle).
  - `anticlockwise`: Draw direction (`false` for clockwise).

### Code Example:
```javascript
ctx.beginPath();  // Start a new path (new shape)
ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);  // Draw a circle
ctx.fillStyle = this.color;  // Set the fill color
ctx.fill();  // Fill the shape
ctx.closePath();  // Close the drawing path
```

> **Why?** `arc()` is essential for drawing circular shapes, and `fill()` fills the shape with a color. These are key to visualizing the circles.

---

## 3. Clearing the Canvas

To animate, we need to clear the previous frame before drawing the updated positions of the circles.

### Key Method:
- `ctx.clearRect(x, y, width, height)`: Clears the specified rectangular area. In animation, we typically clear the entire canvas (`0, 0, canvas.width, canvas.height`).

### Code:
```javascript
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

> **Why?** Without clearing the canvas, the circles would leave a trail as they move. This method removes the old frame before drawing the new one.

---

## 4. Animation Loop

For continuous animation, we use `requestAnimationFrame()`, which tells the browser to call a specified function before the next repaint (usually 60 frames per second).

### Key Method:
- `requestAnimationFrame(callback)`: Schedules the `callback` function to be executed before the next repaint, ensuring smooth animation.

### Code:
```javascript
function animate() {
  requestAnimationFrame(animate);  // Loop the animation
  ctx.clearRect(0, 0, canvas.width, canvas.height);  // Clear the canvas
  circles.forEach(circle => circle.update());  // Update and redraw each circle
}
animate();  // Start the animation loop
```

> **Why?** `requestAnimationFrame()` is a key function for creating smooth, efficient animations. It uses the browser’s refresh rate, making it better than `setInterval()` for performance.

---

## 5. Circle Movement and Collision Detection

To animate the circles, we update their positions based on their velocity and handle collisions with the edges of the canvas.

### Key Concept:
- **Velocity**: Change in position per frame. We add velocity values (`dx`, `dy`) to the circle’s position (`x`, `y`) to create movement.
- **Edge Detection**: To make the circle "bounce," we reverse the velocity when the circle hits a canvas edge (left, right, top, bottom).

### Code:
```javascript
if (this.x + this.radius > canvas.width || this.x - this.radius < 0) {
  this.dx = -this.dx;  // Reverse horizontal direction
}
if (this.y + this.radius > canvas.height || this.y - this.radius < 0) {
  this.dy = -this.dy;  // Reverse vertical direction
}
this.x += this.dx;  // Update horizontal position
this.y += this.dy;  // Update vertical position
```

> **Why?** By adding velocity to the position, we move the circle. Collision detection ensures the circle "bounces" when it hits the canvas edges by reversing its velocity.

---

## Summary of Key Functions and Methods

- `getContext('2d')`: Initializes the 2D drawing context.
- `ctx.arc()`: Draws a circle on the canvas.
- `ctx.fill()`: Fills a shape with color.
- `ctx.clearRect()`: Clears part or all of the canvas.
- `requestAnimationFrame()`: Creates smooth animations by synchronizing with the browser’s refresh rate.

---

## Putting It All Together

The final animation combines these concepts:
1. We draw the circles using `arc()`.
2. We clear the canvas each frame using `clearRect()`.
3. We update the circle’s position based on velocity.
4. We handle edge collisions by reversing velocity.
5. The animation runs continuously using `requestAnimationFrame()`.

---

### Additional Exercises
- **Add Gravity**: Try modifying the `dy` value to simulate gravity.
- **Speed Variation**: Increase or decrease the circle velocities dynamically during the animation.

