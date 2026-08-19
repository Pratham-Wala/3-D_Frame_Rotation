# Rigid Body Rotation Visualizer

An interactive 3D tool for visualizing rigid body rotations. It renders two coordinate frames — a fixed reference frame and a rotatable body frame — and updates a live rotation matrix (plus quaternion and axis-angle) readout in real time as you adjust the rotation.

https://pratham-wala.github.io/3-D_Frame_Rotation/


## What it shows

- **Reference frame F** — dim, static axes at the origin. This is the fixed world frame.
- **Body frame B** — bright axes plus a wireframe box representing a rigid body. This frame rotates as you move the sliders.
- **Rotation matrix R** — the live 3×3 matrix such that `v_F = R · v_B`, i.e. it maps a vector's coordinates in the body frame to its coordinates in the reference frame. The columns of R are the body's x, y, z axes expressed in the reference frame.
- **Quaternion, axis-angle, and det(R)** — alternate representations of the same rotation, shown alongside the matrix. `det(R)` stays at 1.000 as a running check that R remains a proper orthonormal rotation matrix.

## Controls

| Control | Effect |
|---|---|
| α, β, γ sliders | Rotation angles (degrees) about the body's x, y, z axes |
| Euler sequence chips | Choose the intrinsic rotation order (XYZ, ZYX, ZXZ, XZX, YXY, ZYZ) used to compose α, β, γ into a single rotation |
| Reset | Returns all angles to zero (identity rotation) |
| Animate | Continuously sweeps the angles so you can watch the frame and matrix evolve over time |
| Drag / scroll on the 3D view | Orbit and zoom the camera |

Rotation order matters: composing the same three angles in a different sequence produces a different final orientation. Switching the Euler sequence chip with the sliders held fixed is a quick way to see this (non-commutativity of 3D rotations) in action.

## Running it

No build step or dependencies to install — it's a single self-contained HTML file. Three.js is loaded from a CDN at runtime.

- **Locally:** clone the repo and open `index.html` in any modern browser.
- **Online:** use the GitHub Pages link above.

## Implementation notes

- Built with [Three.js](https://threejs.org/) (r128) for the 3D scene, rendered on an HTML5 canvas.
- Camera orbit/zoom is a small hand-rolled controller (no external OrbitControls dependency).
- Rotations are computed from Euler angles via `THREE.Euler` with a selectable intrinsic axis order, converted to a quaternion and then to a rotation matrix each frame.
- The displayed matrix, quaternion, axis-angle, and determinant are all recomputed live from the same underlying quaternion, so they stay mutually consistent.

## License

MIT (or your preferred license — update as needed).
