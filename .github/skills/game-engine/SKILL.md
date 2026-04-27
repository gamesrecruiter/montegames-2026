---
name: game-engine
description: 'Expert skill for building web-based game engines and games using HTML5, Canvas, WebGL, and JavaScript. Use when asked to create games, build game engines, implement game physics, handle collision detection, set up game loops, manage sprites, add game controls, or work with 2D/3D rendering. Covers requestAnimationFrame loops, Canvas 2D API, Web Audio API for synthesized sound effects, and performance optimization for real-time rendering.'
---

# Game Engine Skill

Build web-based games and game engines using HTML5 Canvas, WebGL, and JavaScript. This skill includes step-by-step workflows for 2D and 3D game development.

## When to Use This Skill

- Building a game engine or game from scratch using web technologies
- Implementing game loops, physics, collision detection, or rendering
- Working with HTML5 Canvas, WebGL, or SVG for game graphics
- Adding game controls (keyboard, mouse, touch, gamepad)
- Creating 2D platformers, breakout-style games, maze games, or 3D experiences
- Working with tilemaps, sprites, or animations
- Adding audio to web games via Web Audio API
- Optimizing game performance

## Core Concepts

### Game Loop

Every game engine revolves around the game loop — a continuous cycle of:

1. **Process Input** - Read keyboard, mouse, touch, or gamepad input
2. **Update State** - Update game object positions, physics, AI, and logic
3. **Render** - Draw the current game state to the screen

Use `requestAnimationFrame` for smooth, browser-optimized rendering.

```js
function gameLoop(timestamp) {
  const deltaTime = timestamp - lastTime;
  lastTime = timestamp;

  processInput();
  update(deltaTime);
  render();

  requestAnimationFrame(gameLoop);
}
requestAnimationFrame(gameLoop);
```

### Rendering

- **Canvas 2D** - Best for 2D games, sprite-based rendering, and tilemaps
- **WebGL** - Hardware-accelerated 3D and advanced 2D rendering
- **SVG** - Vector-based graphics, good for UI elements
- **CSS** - Useful for DOM-based game elements and transitions

### Physics and Collision Detection

- **2D Collision Detection** - AABB, circle, and SAT-based collision
- **Velocity and Acceleration** - Basic Newtonian physics for movement
- **Gravity** - Constant downward acceleration for platformers

### Controls

- **Keyboard** - Arrow keys, WASD, and custom key bindings
- **Mouse** - Click, move, and pointer lock for FPS-style controls
- **Touch** - Mobile touch events and virtual joysticks
- **Gamepad** - Gamepad API for controller support

### Audio

- **Web Audio API** - Programmatic sound generation and spatial audio
- **HTML5 Audio** - Simple audio playback for music and sound effects

```js
// Synthesized sound effect with Web Audio API
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
const osc = audioCtx.createOscillator();
const gain = audioCtx.createGain();
osc.connect(gain);
gain.connect(audioCtx.destination);
osc.type = 'sine';
osc.frequency.setValueAtTime(800, audioCtx.currentTime);
osc.frequency.exponentialRampToValueAtTime(400, audioCtx.currentTime + 0.08);
gain.gain.setValueAtTime(0.06, audioCtx.currentTime);
gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.1);
osc.start(audioCtx.currentTime);
osc.stop(audioCtx.currentTime + 0.1);
```

## Step-by-Step Workflows

### Creating a Basic 2D Game

1. Set up an HTML file with a `<canvas>` element
2. Get the 2D rendering context
3. Implement the game loop using `requestAnimationFrame`
4. Create game objects with position, velocity, and size properties
5. Handle keyboard/mouse input for player control
6. Implement collision detection between game objects
7. Add scoring, lives, and win/lose conditions
8. Add sound effects and music

### Canvas Particle System

1. Create particle array with position, velocity, radius, alpha
2. Use `requestAnimationFrame` for animation loop
3. Clear canvas each frame with `ctx.clearRect()`
4. Update particle positions based on velocity
5. Draw particles with `ctx.arc()` and `ctx.fill()`
6. Optionally draw connection lines between nearby particles
7. Pause rendering when `document.hidden` is true
8. Target < 2ms/frame for performance

## Performance Optimization

- Use `requestAnimationFrame` instead of `setInterval`
- Pause animation when tab is hidden (`document.hidden`)
- Use object pooling instead of creating/destroying particles
- Minimize canvas state changes (batch similar draw calls)
- Use `will-change: transform` sparingly on DOM elements
- Profile with browser DevTools Performance tab
- Target < 2ms/frame for canvas rendering

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Canvas is blank | Check that you are calling drawing methods after getting the context and inside the game loop |
| Game runs at different speeds | Use delta time in update calculations instead of fixed values |
| Collision detection is inconsistent | Use continuous collision detection or reduce time steps |
| Audio does not play | Browsers require user interaction before playing audio; trigger playback from a click handler |
| Performance is poor | Profile with browser dev tools, reduce draw calls, use object pooling |
| Touch controls are unresponsive | Prevent default touch behavior and handle touch events separately from mouse events |
