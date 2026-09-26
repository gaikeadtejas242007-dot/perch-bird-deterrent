# Perch — Bird Detection & Deterrent

A browser-based bird monitor that analyzes a live camera feed with COCO-SSD / TensorFlow.js and optionally plays an audio file you choose while birds are detected.

## Run locally

1. Unzip the package.
2. Open a terminal in the `bird-deterrent` folder.
3. Run a local static server:

   ```bash
   python3 -m http.server 5173
   ```

   Or use any static web server. A secure context is required for camera access: `http://localhost` is allowed by browsers; remote deployments need HTTPS.

4. Open [http://localhost:5173](http://localhost:5173) in a current browser.
5. Choose an audio file if you want a deterrent, then click **Start detection** and allow camera access.
6. Turn on **Auto deterrent**. If your browser asks, click **Enable audio for automatic playback** once.

The first start needs an internet connection to load TensorFlow.js, COCO-SSD, and the model weights. Detection thereafter runs in the browser. No frames are uploaded.

## Features

- Live camera preview with COCO-SSD bird-class detection, confidence labels, and bounding boxes.
- Adjustable confidence threshold, detection pace, and missed-frame persistence.
- User-selected local audio, manual play/pause/stop, volume, and optional automatic playback.
- Debounced detection sessions, including dates, duration, bird peak, max/average confidence, and audio name.
- Local history summaries and settings saved in browser `localStorage`; camera frames and uploaded audio are not stored.
- Responsive layout designed for phone and desktop screens.

## Browser and privacy notes

- Camera access is requested only after **Start detection**. Audio capture is never requested.
- The camera stream is processed in-browser using TensorFlow.js; the app has no backend and does not record or transmit camera frames.
- The selected audio file is held in a temporary browser object URL while the page is open. It is not uploaded or persisted.
- Detection history and preferences remain in that browser's local storage. Clearing browser storage removes them.
- To play sound automatically, browsers may require a user gesture. Selecting a file and using **Enable audio** primes playback; if playback is still blocked, follow the browser prompt and enable audio manually.
- COCO-SSD recognizes the standard COCO object classes, including `bird`. Results depend on camera angle, lighting, distance, and model confidence.

## Included files

- `index.html` — interface and browser AI dependency loading
- `style.css` — responsive interface
- `script.js` — camera, detection loop, audio, settings, and local history

This static app intentionally needs no API key, database account, server backend, or package installation.