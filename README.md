# GAZESCOPE - AR eye tracker

On-device AR eye tracking and Privacy Shield for the browser. Camera frames never
leave the device: all face, iris and head-pose processing runs locally in WebAssembly
(MediaPipe Face Mesh with iris refinement, vendored under `mediapipe/` - no CDN, no
server, no account).

## Features
- 9-point calibration (~20s) + ridge-regression gaze model, accuracy readout in px
- Live AR overlay: mirrored camera, face mesh, eye contours, iris rings, gaze rays, smoothed gaze dot with trail (One Euro filter)
- Session heatmap, CSV/JSON export, optional AES-GCM encryption of saved data (passphrase, PBKDF2 250k)
- Privacy Shield: head-pose yaw/pitch watch; turn away past your comfort angle (2-30 deg, default 15) and the page blurs behind a gradient. Look back to clear, Esc to dismiss. Protects this page only.
- Practice mode (mouse) for trying the flow without a camera
- Humanized camera-permission states

## Verify
Open `?selftest=1` on the deployed URL: checks local model load, 478-landmark + iris
detection on a bundled still, regression sanity, AES-GCM roundtrip, and that every
loaded resource is same-origin.

`?demo=image` runs real detection on the bundled still photo with a synthetic gaze dot.

## Run locally
Any static server: `python3 -m http.server` then open http://localhost:8000
(camera requires localhost or HTTPS).
