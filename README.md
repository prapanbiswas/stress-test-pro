# ☢️ ULTIMATE Browser Stress Test

**The Ultimate Browser Meltdown** is a comprehensive, multi-faceted browser stress testing suite designed to push modern web browsers to their absolute limits through multiple concurrent stressors targeting different subsystems.

This tool demonstrates the performance characteristics of various browser technologies including WebGL shaders, JavaScript computation, Web Workers, Web Audio API, DOM manipulation, and memory allocation.

## 🚀 Features

### 🎯 Multi-Stressor Architecture
Unlike simple stress tests, this system allows you to enable multiple concurrent stressors, each targeting different browser subsystems:

#### **Geometry Stressors**
- **Multi-Sphere**: Renders multiple high-density spheres simultaneously (up to millions of vertices)
- **Torus Knot**: Complex mathematical geometry with twisted tube topology
- **Icosahedron**: Detailed icosahedral geometry with wireframe rendering
- **CPU Deform**: CPU-bound vertex deformation (intentionally slow)
- **Morph Targets**: Dynamic geometry morphing between shapes
- **Adjustable Density**: Scale geometry from 100 to 500 segments

#### **Particle Systems**
- **GPU Particles**: Hardware-accelerated particle rendering with thousands of particles
- **CPU Particles**: JavaScript-calculated particle physics (extremely CPU-intensive)
- **Particle Trails**: Particle systems with motion trail effects
- **Configurable Count**: 1,000 to 100,000 particles per system

#### **Physics Simulation**
- **Verlet Cloth**: Real-time cloth simulation using Verlet integration
- **Soft Body**: Jelly-like deformable mesh physics
- **Collision Detection**: Physics-based collision between objects

#### **Compute & Web Workers**
- **Web Workers**: Multi-threaded computation offloading
- **Worker Pool**: Spawns multiple workers for parallel processing
- **Configurable Count**: 1 to 16 concurrent workers
- **Heavy Computation**: Stress tests with Fibonacci calculations

#### **Shaders & Visual Effects**
- **Complex Shaders**: Multi-layered noise functions (FBM, Perlin)
- **Post-Processing**: Full-screen shader effects
- **Bloom**: Glowing light bloom effect
- **Chromatic Aberration**: RGB color separation effect

#### **Audio Stress Test**
- **Oscillator Bank**: Multiple concurrent audio oscillators
- **Audio Analysis**: Real-time FFT spectrum analysis
- **Configurable Count**: 10 to 500 simultaneous audio nodes

#### **Memory & DOM Stressors**
- **Memory Allocation**: Rapid buffer allocation/deallocation cycles
- **DOM Thrashing**: Continuous DOM reads/writes causing layout thrashing
- **Canvas 2D**: Additional 2D canvas stress test

### 🎮 Preset Configurations
- **🟡 LAGGY**: Heavy load with GPU-accelerated stressors (safe for most devices)
- **🔴 FREEZE**: Extreme load with CPU-bound calculations (expect lag)
- **💀 CRASH**: Maximum stress - all stressors enabled (DANGER - may crash browser)

### 📊 Real-Time Performance Monitoring
- **FPS Counter**: Frames per second
- **Frame Time**: Time per frame in milliseconds
- **JS Time**: JavaScript execution time per frame
- **Vertex Count**: Total number of vertices being rendered
- **Draw Calls**: Number of WebGL draw calls
- **Web Workers**: Number of active workers
- **Audio Nodes**: Number of active audio nodes
- **Memory Usage**: JavaScript heap size (Chrome only)

### 🛑 Safety Features
- **Emergency Stop**: Instantly disables all stressors
- **Progressive Loading**: Stressors must be manually enabled
- **Warning System**: Alerts when stress level is dangerous
- **Load Bar**: Visual indicator of total system load

## 🛠️ Installation & Usage

This is a **zero-dependency** project. You do not need `npm`, `node`, or a build server.

### Basic Usage
1. Download the `index.html` file
2. Open in any modern web browser (Chrome, Edge, Safari, Firefox)
3. Toggle individual stressors on/off using the control panel
4. Use sliders to adjust intensity of each stressor
5. Try presets for different stress levels

### Advanced Usage
- Combine multiple stressors for maximum chaos
- Adjust geometry density and particle counts independently
- Use presets as starting points, then customize
- Monitor performance metrics to identify bottlenecks

## 🎯 How Each Stressor Works

### Geometry Stressors
**CPU Deform Mode**: Forces the browser's main thread to calculate trigonometry (`Math.sin`, `Math.cos`) for every vertex, every frame. This blocks the UI and demonstrates JavaScript's single-threaded limitation.

**GPU Mode**: Uses WebGL Vertex Shaders to perform the same calculations in parallel across GPU cores. The CPU remains idle while the animation stays smooth.

### Particle Systems
**GPU Particles**: Uses Three.js `PointsMaterial` with GPU-based transformation for smooth rendering of thousands of particles.

**CPU Particles**: Calculates particle physics in JavaScript, updating positions, velocities, and colors for every particle every frame. Extremely CPU-intensive.

### Physics Simulation
**Verlet Cloth**: Simulates cloth physics by calculating forces between connected points using Verlet integration, a position-based physics method.

**Soft Body**: Uses spring-mass systems to create jelly-like deformation effects by applying forces to mesh vertices.

### Web Workers
**Multi-Threading**: Offloads computation from the main thread to worker threads, preventing UI blocking and utilizing multiple CPU cores.

**Worker Pool**: Creates multiple workers that perform heavy calculations simultaneously, demonstrating parallel processing capabilities.

### Audio Processing
**Oscillator Bank**: Creates multiple audio oscillators with different waveforms (sine, square, sawtooth, triangle) that modulate in real-time, stressing the Web Audio API.

### Memory Stress
**Allocation Cycles**: Rapidly allocates and deallocates large ArrayBuffers and Float32Arrays, creating memory pressure and garbage collection load.

### DOM Thrashing
**Layout Thrashing**: Forces continuous layout recalculation by interleaving DOM reads (getting element dimensions) and writes (changing styles), which is extremely expensive.

## 📈 Performance Characteristics

### Expected Results by Mode

| Stress Level | FPS (High-End) | FPS (Mid-Range) | FPS (Mobile) |
|:------------|:---------------|:-----------------|:--------------|
| **Laggy** | 30-45 | 15-25 | 5-10 |
| **Freeze** | 10-20 | 3-10 | 1-3 |
| **Crash** | 0-5 | 0-2 | Likely crash |

### Key Performance Bottlenecks

1. **CPU Deform**: Single-threaded JavaScript computation
2. **CPU Particles**: Physics calculations for thousands of particles
3. **DOM Thrashing**: Forced layout recalculations
4. **Memory Alloc**: Garbage collection pressure
5. **Soft Body Physics**: Spring-mass system calculations

## ⚠️ Warnings

### High Settings Warning
- **Mobile Devices**: Extreme stress tests can overheat devices and drain battery rapidly
- **Low-End Laptops**: Maximum settings may cause the browser tab to freeze or crash
- **Work Computers**: May trigger antivirus or system monitoring due to high resource usage

### Browser-Specific Notes
- **Chrome**: Full memory monitoring available
- **Firefox/Safari**: Some performance APIs may be restricted
- **Mobile**: Gyroscope requires HTTPS or localhost

### Device Safety
- Do not run "CRASH" preset on devices with limited cooling
- Reduce stressors if you notice the device becoming hot
- The "EMERGENCY STOP" button will immediately halt all stress tests

## 🧠 Technical Details

### Architecture
The application uses a modular stressor system where each stressor is an independent class:
- `GeometryStressor`: Manages multi-object geometry systems
- `ParticleStressor`: Handles CPU and GPU particle systems
- `PhysicsStressor`: Implements cloth and soft-body physics
- `WorkerStressor`: Manages Web Worker pool and task distribution
- `AudioStressor`: Controls Web Audio API oscillators
- `MemoryStressor`: Handles buffer allocation/deallocation
- `DOMStressor`: Manages DOM and Canvas 2D stress tests

### Shader Technology
- **FBM (Fractal Brownian Motion)**: Multi-octave noise for organic displacement
- **Simplex Noise**: Efficient 3D noise function
- **Custom Vertex Shaders**: Real-time geometry deformation
- **Fragment Shaders**: Dynamic coloring based on displacement
- **Post-Processing**: Full-screen shader effects

### Performance Optimization Techniques Used
- **Object Pooling**: Reuse objects instead of creating/destroying
- **Instanced Rendering**: Efficient multi-object rendering
- **Typed Arrays**: Use Float32Array for high-performance numerical data
- **requestAnimationFrame**: Synchronized with browser refresh rate
- **Web Workers**: Parallel computation off main thread

## 🕹️ Controls

| Control | Description |
|:--------|:------------|
| **Toggle Buttons** | Enable/disable individual stressors |
| **Sliders** | Adjust intensity (density, count, workers, etc.) |
| **Presets** | Quick configuration for different stress levels |
| **Rotate/Zoom** | Drag to rotate camera, scroll to zoom |
| **Emergency Stop** | Instantly disable all stressors |
| **Mouse Position** | Affects deformation pattern (desktop) |
| **Device Tilt** | Affects deformation pattern (mobile) |

## 📊 Benchmarking Tips

### To Benchmark Your Device
1. Start with no stressors enabled (baseline)
2. Enable stressors one by one, noting FPS drop for each
3. Try the "LAGGY" preset for a moderate stress test
4. Record vertex count vs FPS to find your device's limit
5. Use CPU Deform mode to test single-threaded performance

### Identifying Bottlenecks
- **If FPS drops with geometry stressors**: GPU bottleneck
- **If FPS drops with CPU Deform**: CPU single-thread bottleneck
- **If FPS drops with DOM thrashing**: Layout engine bottleneck
- **If memory usage climbs rapidly**: Garbage collection bottleneck
- **If UI becomes unresponsive**: Main thread blocking

## 🎓 Educational Value

This tool demonstrates several important web development concepts:

1. **CPU vs GPU Computation**: Understanding when to use shaders vs JavaScript
2. **Single-Threaded JavaScript**: Why main thread blocking matters
3. **Web Workers**: How to offload computation
4. **DOM Performance**: Why layout thrashing is expensive
5. **Memory Management**: Garbage collection impact on performance
6. **Parallel Processing**: GPU vs multi-threaded CPU
7. **Audio API**: Real-time audio synthesis capabilities
8. **Browser Limits**: Understanding performance ceilings

## 📄 License

Open Source. Feel free to use this code for benchmarking, educational purposes, or stress testing web applications.

## 🤝 Contributing

This is a demonstration project. Feel free to fork and experiment with additional stressors:
- WebRTC stress testing
- IndexedDB operations
- WebGL compute shaders (WebGPU)
- WebAssembly heavy computation
- Service worker stress tests
- WebGL context loss handling

## 🐛 Known Limitations

- `performance.memory` is Chrome-only
- SharedArrayBuffer requires COOP/COEP headers
- WebGPU is experimental (WebGL2 fallback used)
- Some mobile browsers limit worker count
- Audio autoplay policies may require user interaction

---

**Remember: This tool is designed to stress test browsers. Use responsibly and always have the Emergency Stop button ready!** ☢️
