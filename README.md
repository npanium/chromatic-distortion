# Chromatic Text Distortion

A WebGL shader effect that renders text with animated chromatic aberration and noise-based distortion. Based on a Shadertoy-style GLSL fragment shader.

## Features

- Real-time text rendering with customizable input
- Chromatic aberration (RGB channel separation)
- Multiple procedural noise types for distortion
- Custom image upload for displacement maps
- Fully adjustable parameters via sliders
- Mobile-friendly collapsible controls

## Controls

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Text** | The text to render | Distort |
| **Font** | Typeface selection | Georgia |
| **Noise Type** | Displacement pattern | Turbulence |
| **Distortion Strength** | How much the noise displaces the text | 0.06 |
| **Chromatic Spread** | RGB channel separation amount | 0.01 |
| **Noise Scale** | Frequency/zoom of the noise pattern | 0.75 |
| **Animation Speed** | How fast the distortion scrolls | 0.07 |
| **Edge Softness** | Blur/sharpness of text edges | 0.032 |
| **Direction** | Angle of distortion movement (degrees) | 215° |

## Noise Types

- **White Noise** — Random static
- **Perlin-like** — Smooth coherent noise
- **Simplex-like** — Multi-octave smooth noise
- **Worley/Cellular** — Organic cell-based patterns
- **FBM (Fractal)** — Fractal Brownian motion, layered detail
- **Turbulence** — Absolute value of FBM, chaotic look
- **Ridged** — Inverted ridges, mountain-like
- **Gradient** — Simple diagonal gradient
- **Stripes** — Sine wave stripes
- **Checker** — Checkerboard pattern
- **Custom Image** — Upload your own displacement map

## How It Works

The shader samples a noise texture to distort UV coordinates differently for each RGB channel. This creates the chromatic aberration effect where red, green, and blue separate at the edges. The noise scrolls over time in a configurable direction, creating the animated liquid distortion.

```glsl
// Core distortion logic
vec2 noiseUV = uv * scale - direction * time * speed;
float noise = texture(noiseTexture, noiseUV + offset).r;
vec2 distortedUV = uv - smoothstep(0.01, 2.0, noise) * strength;
```

## Color Scheme

- Text: `#30302b` (dark olive)
- Background: `#ffffe3` (warm cream)

## Usage

Open `chromatic-text.html` in any modern browser. No build step or dependencies required.

## Browser Support

Requires WebGL support. Works in all modern browsers (Chrome, Firefox, Safari, Edge).
