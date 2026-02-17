# ☢️ Browser Meltdown: CPU vs GPU Stress Test

**Browser Meltdown** is a single-file 3D visualization tool designed to benchmark and demonstrate the massive performance gap between **CPU-bound JavaScript execution** and **GPU-accelerated WebGL Shaders**.

It renders a high-density sphere (up to 250,000 vertices) that deforms in real-time based on user input (Gyroscope or Mouse).

### [Live Demo](#) ## 🚀 Features

* **Dual Processing Modes:**
    * **🔥 CPU Mode (Torture Test):** Forces the browser's Main Thread to calculate 3D trigonometry and color interpolation for every single vertex, every single frame. Excellent for testing JavaScript engine limits and single-core performance.
    * **⚡ GPU Mode (Shader Accelerated):** Offloads all mathematics to the Vertex Shader. Demonstrates the parallel processing power of modern graphics cards, maintaining 60 FPS even at maximum geometry density.
* **Dynamic Heatmap:** Real-time color visualization where vertex color changes based on displacement height (Red = High, Blue = Low).
* **Device Interaction:**
    * **Mobile:** Uses the **Gyroscope** to warp the sphere as you tilt your phone.
    * **Desktop:** Uses the **Mouse** position to direct the wave distortion.
* **Adjustable Load:** A "Meltdown Factor" slider lets you increase the geometry density from ~10k to ~250k vertices dynamically.

## 🛠️ Installation & Usage

This is a **zero-dependency** project. You do not need `npm`, `node`, or a build server.

1.  Download the `sphere-meltdown.html` file.
2.  Open the file in any modern web browser (Chrome, Edge, Safari, Firefox).
3.  **Mobile Users:** For the Gyroscope to work, the file usually needs to be served over **HTTPS** or `localhost`. If opening directly as a file (`file://`), some browsers block sensor access.

## 🕹️ Controls

| Control | Description |
| :--- | :--- |
| **CPU Button** | Switches to JavaScript-based calculation (expect lag). |
| **GPU Button** | Switches to WebGL Shader calculation (smooth). |
| **Slider** | Adjusts the mesh density. **Warning:** Max setting is heavy. |
| **Rotate/Zoom** | Drag to rotate the camera, scroll to zoom (OrbitControls). |

## 🧠 Technical Explanation

This tool visualizes the "Glass Ceiling" of Client-Side Rendering.

### The CPU Bottleneck (CPU Mode)
In this mode, the application runs a `for` loop in JavaScript for every vertex ($250,000$ times per frame).
1.  **Calculation:** It computes `Math.sin()` and `Math.cos()` for X, Y, and Z axes.
2.  **Data Transfer:** It must upload the entire new array of positions to the GPU memory using `geometry.attributes.position.needsUpdate = true`.
* **Result:** The Main Thread gets blocked. The UI becomes unresponsive, and FPS drops drastically because JavaScript is single-threaded.

### The GPU Solution (GPU Mode)
In this mode, JavaScript does almost nothing.
1.  **Uniforms:** JS sends just **two variables** (Time and Input Vector) to the GPU.
2.  **Parallelism:** The GPU's Vertex Shader executes the math for all 250,000 vertices simultaneously.
* **Result:** The CPU remains idle (0% load), leaving the browser responsive while the animation remains silky smooth.

## ⚠️ Warning

**High Settings Warning:** Setting the density slider to the maximum (500) while in **CPU Mode** on a mobile device or low-end laptop may cause the browser tab to **freeze** or crash completely. This is the intended behavior of the stress test.

## 📄 License

Open Source. Feel free to use this code for benchmarking, educational purposes, or just to warm up your phone in the winter.

