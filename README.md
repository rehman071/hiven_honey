# HIVEN — Raw Honey

A single-page, full-screen interactive product story for **HIVEN**, a fictional raw-honey brand. A single jar of honey remains pinned on screen throughout the entire experience while four distinct editorial scenes transition seamlessly around it—built with zero frameworks and zero native scrolling.

![HTML5](https://img.shields.io/badge/HTML5-Single%20File-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-Responsive%20Dual--Unit-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla%20ES6-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

---

## Experience Overview

Every mouse wheel flick, trackpad gesture, touch swipe, or arrow key triggers one complete, time-based transition between four scenes using custom cubic-bezier motion curves:

| Scene | Name | Visual & Motion Breakdown |
| :--- | :--- | :--- |
| **0** | **Misty Lake Hero** | Opens with a 1.6 s rising reveal of the misty lake, basalt rock, and jar. Features a seamless dual-video crossfade water loop and a DOM-measured `Playfair Display` wordmark framed behind the jar. |
| **1** | **Ingredients Ring** | The lake fades and subtly zooms into warm cream (`#FAF4EC`) while the jar enlarges and anchors at the bottom edge. Five macro ingredient circles (**Wild Acacia**, **Lavender**, **Honeycomb**, **Bee Pollen**, **Bee Resin**) scale in around an arch. |
| **2** | **Benefits & Presentation** | A warm beige panel (`#F2E6D3`) rises with an open palm that catches the jar behind the fingers. Three benefit rows (**Clean Energy**, **Soothes Throat**, **Raw & Unfiltered**) glide in staggered from the right. |
| **3** | **Dark Kitchen Finale** | The hand exits left while the jar follows a continuous per-axis Bezier curve onto a wooden pedestal in a dusk terracotta kitchen (`#2B1F14`). Navigation adapts to light typography as the tagline and **Discover** pill appear. |

---

## Key Technical Features

- **In-Browser Cutout Refinement:** Loads transparent product and hand assets via CORS onto an offscreen `<canvas>`, crops to exact bounding boxes, applies two 4-neighbour minimum alpha-erosion passes plus a weighted feather pass to eliminate matte halos, and exports clean WebP blobs with automatic raw-URL fallback.
- **Dual-Unit Responsive Scaling:** Recomputes both a cover plate unit (`s`) and a contain UI unit (`c`) relative to a `1440×900` reference frame on every resize, paired with a dedicated portrait layout (`vw/vh < 0.9`) engineered for viewports from `320×568` to `2560×1440`.
- **Custom Channel Motion Engine:** Drives every transform and opacity via `requestAnimationFrame` using fitted cubic-bezier curves (`EJ`, `EP`, `EF`, `EY`). Mid-transition inputs smoothly interrupt from live channel values, and the Scene 2 → 3 jar move uses independent per-axis durations (`700 ms` X, `1600 ms` Y, `1600 ms` width) for a continuous curved arc.
- **Stepped Input Controller:** Filters trackpad inertia via gap and delta-spike detection, enforces a `1000 ms` transition lock so scenes are never accidentally skipped, and supports mouse wheel, touch swipes, keyboard navigation, and direct navbar jumps.
- **Seamless Video Crossfade Loop:** Alternates two muted, inline `<video>` elements with a `600 ms` crossfade and automatically pauses playback when the hero scene is hidden.
- **Accessibility:** Respects `prefers-reduced-motion` by keeping the hero plate static and snapping scene transitions instantly while preserving full navigation.

---

## Controls & Testing API

### User Controls
- **Scroll / Trackpad:** Flick up or down to step one scene at a time.
- **Touch:** Swipe vertically (greater than `40px`) to step between scenes.
- **Keyboard:** `ArrowDown`, `PageDown`, or `Space` (next) · `ArrowUp` or `PageUp` (previous) · `Home` (Scene 0) · `End` (Scene 3).
- **Navigation Bar:** `Home` → 0 · `Products` → 1 · `About` / `Reviews` → 2 · `Contact` → 3.

### Developer Console Hook
The page exposes a global helper on `window.hiven` for quick scene inspection and automated testing:

```js
// Jump smoothly to Scene 2
window.hiven.go(2);

// Snap immediately to Scene 3 without animation
window.hiven.go(3, true);

// Read the current scene index (0–3)
console.log(window.hiven.state);
```

---

## Design System

- **Typography:** `Playfair Display` (wordmark, benefit headings, finale tagline) and `Outfit` (navigation, ingredient labels, body copy, CTA) via Google Fonts.
- **Color Palette:**
  - Cream Canvas: `#FAF4EC`
  - Hero Haze Fill: `#FBF4E9`
  - Benefits Panel: `#F2E6D3`
  - Honey Accent: `#C79A67`
  - Primary Ink: `#2A2118`
  - Secondary Copy: `#4A3D30`
  - Dusk Kitchen: `#2B1F14`
  - Light Surface Text: `#F6EEE2`

---

## Running Locally

Because the entire project lives in a single self-contained HTML file with no build step, you can run it immediately:

```bash
# Clone the repository
git clone [https://github.com/](https://github.com/)<your-username>/<your-repo-name>.git
cd <your-repo-name>

# Serve locally (recommended for smooth media & CORS handling)
npx serve .
```

Or simply open `index.html` directly in any modern browser.

---

## Project Structure

```text
.
├── index.html   # Complete markup, dual-unit CSS, canvas cutout pipeline, and motion engine
└── README.md    # Project documentation
```

---

## License

This project is open-source and available under the [MIT License](LICENSE).
