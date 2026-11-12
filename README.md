# 🎬 Camera, Code, Action! — GDSC Computer Vision Workshop

Turn your index finger into a paintbrush. This workshop uses **Google MediaPipe Hand Landmarker** to track a hand in a video, then draws wherever the fingertip goes. We call it the AirCanvas.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Aarsh-collab/camera-code-action/blob/main/Camera_Code_Action_Instructor.ipynb)

## What you'll learn

- How a computer "sees" a hand: MediaPipe's **21 hand landmarks** and how they connect
- Running a pretrained model on video frames (`VIDEO` running mode, timestamps)
- Turning normalized landmark coordinates into pixel positions
- Building a drawing app on top of tracking: smoothing, pinch-to-draw, and lifting the pen when tracking is lost
- Exporting results as shareable MP4 videos

No prior computer vision experience is needed. Basic Python helps.

## Quick start (Google Colab, recommended)

1. Click the **Open in Colab** badge above.
2. A standard **CPU** runtime is enough. You don't need a GPU.
3. Choose **Runtime → Run all**.
4. In Section 3, upload a short MP4 of your hand (see [Recording your own video](#recording-your-own-video)).
5. Your results appear in Section 9 and are saved in the `outputs/` folder:
   - `air_drawing_A_tracking.mp4`: the landmarks, the skeleton, and the highlighted fingertip
   - `air_drawing_B_canvas.mp4`: the AirCanvas drawing
   - `air_drawing_C_combined.mp4`: both videos side by side
   - `air_drawing_final_drawing.png`: the finished drawing

The setup cell installs `mediapipe==1.1.1` with `--no-deps`, which keeps Colab's own OpenCV and NumPy in place, so you won't have to restart the runtime. It also downloads the `hand_landmarker.task` model from Google.

> **Tip:** To skip the upload step, paste a direct link to an MP4 into `SAMPLE_VIDEO_URL` in Section 3.

## Running locally

Tested with Python 3.12. FFmpeg must be on your `PATH`.

```bash
git clone https://github.com/Aarsh-collab/camera-code-action.git
cd camera-code-action
python -m venv .venv && source .venv/bin/activate
pip install --no-deps mediapipe==1.1.1
pip install -r requirements.txt jupyter
jupyter notebook Camera_Code_Action_Instructor.ipynb
```

## What's in the repo

| Path | What it is |
|---|---|
| `Camera_Code_Action_Instructor.ipynb` | The complete workshop notebook, with all code working |
| `requirements.txt` | Tested dependency versions for local runs |

## Notebook outline

1. Introduction
2. Setup
3. Load the Video
4. Understanding MediaPipe (21 landmarks, `HAND_CONNECTIONS`)
5. Initialize HandLandmarker (`VIDEO` mode)
6. Detect Hand Landmarks (`detect_for_video`)
7. Extract Finger Coordinates
8. AirCanvas (continuous or pinch-to-draw, smoothing, pen-lift)
9. Generate Results (H.264 MP4s)
10. Experimentation
11. Optional Challenges (rainbow brush, two hands, AR ink, and more)

MediaPipe runs once per video. Every drawing experiment after that reuses the stored landmarks, so it re-renders in seconds.

## Recording your own video

- 10–15 seconds, one hand, index finger extended
- Keep the whole hand in view, with good lighting and a plain background
- Move steadily and trace something recognizable: a star, a heart, your initials

Any resolution or orientation works. Frames are downscaled so the longest side is 640 px.

## Credits

Built for a Google Developer Student Club (GDSC) workshop. Hand tracking is powered by [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker).
