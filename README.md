# 🎮 Virtual Steering Wheel — MediaPipe + Python

A computer-vision based virtual steering wheel that allows you to control keyboard-based games using hand gestures through a webcam.

This project uses **Python, MediaPipe, OpenCV, NumPy, and pynput** to detect two hands, determine their position and gesture, and convert those gestures into keyboard inputs.

No physical steering wheel or controller is required.

---

## 🚗 How It Works

The program uses your webcam to track both hands.

Place your hands in front of the camera as if you are holding a steering wheel.

The position and angle of your hands determine the steering direction, while the hand gestures determine acceleration and braking.

### Basic Controls

- 👊 Both hands closed → Accelerate
- 🖐 Both hands open → Brake
- ↔️ Hands tilted left or right → Steer
- 👊🖐 One fist + one open hand → Neutral
- ❌ No hands detected → Release all keys

The program sends keyboard inputs using the `pynput` library.

---

## 🎮 Gesture Controls

| Hand Gesture | Action | Keyboard Input |
|---|---|---|
| 👊 Both fists, hands level | Accelerate | ↑ Up |
| 👊 Both fists, tilted left | Accelerate + steer left | ↑ + ← |
| 👊 Both fists, tilted right | Accelerate + steer right | ↑ + → |
| 🖐 Both hands open, level | Brake | ↓ Down |
| 🖐 Both hands open, tilted left | Brake + steer left | ↓ + ← |
| 🖐 Both hands open, tilted right | Brake + steer right | ↓ + → |
| 👊🖐 One fist + one open hand | Neutral | No throttle/brake |
| ❌ No hands visible | Release controls | All keys released |

> **Note:** Steering works independently from acceleration and braking. This means you can steer while accelerating or braking.

---

## ✨ Features

- Real-time webcam hand tracking
- Detection of up to two hands
- Fist detection
- Open-hand detection
- Gesture-based acceleration and braking
- Gesture-based left/right steering
- Steering angle calculation
- Steering dead zone
- Steering release zone
- Adjustable steering sensitivity
- Keyboard control using `pynput`
- Real-time FPS display
- On-screen virtual steering wheel
- On-screen status information
- Grace period when hands temporarily disappear
- Automatic MediaPipe hand model download
- Automatic camera backend selection based on operating system

---

## 💻 Requirements

### Hardware

- A computer
- Webcam
- Internet connection for the first run if the MediaPipe hand model is not already downloaded

### Software

- Python
- Webcam access enabled for the application
- Required Python packages listed in `requirements.txt`

This project was developed and tested in a Windows environment with Python 3.14.

---

## 📦 Installation

### 1. Clone the repository

Clone the project from GitHub or download the repository as a ZIP file.

After downloading, open PowerShell or Terminal inside the project folder.

### 2. Install the required packages

Run:

```bash
pip install -r requirements.txt
```

The project requires:

```text
mediapipe
opencv-python
numpy
pynput
```

---

## 📄 Requirements

The `requirements.txt` file contains the Python dependencies used by the project.

Example:

```text
mediapipe==0.10.35
opencv-python==5.0.0.93
pynput==1.8.2
numpy==2.5.1
```

The versions above represent the environment used to test the current project.

---

## ▶️ Run the Project

Open PowerShell or Terminal in the project folder.

On Windows, run:

```bash
python steering_wheel.py
```

On systems where `python3` is used, run:

```bash
python3 steering_wheel.py
```

When the program starts, it will:

1. Check whether the MediaPipe hand model exists.
2. Download the model automatically if it is missing.
3. Open the webcam.
4. Detect up to two hands.
5. Calculate the steering angle.
6. Detect hand gestures.
7. Send keyboard inputs according to the detected gestures.
8. Display the virtual steering wheel and status information.

---

## 📥 MediaPipe Hand Model

The project uses the MediaPipe Hand Landmarker model.

The required model file is:

```text
hand_landmarker.task
```

If the file does not exist, the program automatically downloads it when the application starts.

You therefore do not need to manually download the model before running the program.

An internet connection is required the first time the model needs to be downloaded.

---

## 🪟 Windows Camera Setup

The current program automatically selects the appropriate camera backend based on the operating system.

No manual camera backend configuration is normally required.

The default camera index is:

```python
CAMERA_INDEX = 0
```

This means the program first tries to use the default webcam.

If the camera does not open, you can try another camera index:

```python
CAMERA_INDEX = 1
```

or:

```python
CAMERA_INDEX = 2
```

After changing the value, save the file and run the program again:

```bash
python steering_wheel.py
```

### Camera Permission

Make sure your operating system allows Python to access the webcam.

If Windows asks for camera permission, allow camera access.

Also close other applications that may already be using the webcam.

---

## ⚙️ Configuration

The main configuration settings are located near the beginning of:

```text
steering_wheel.py
```

Current settings include:

| Setting | Default | Purpose |
|---|---:|---|
| `CAMERA_INDEX` | `0` | Selects the webcam |
| `DEAD_ZONE_DEG` | `12` | Ignores small steering movements around the center |
| `RELEASE_ZONE_DEG` | `6` | Angle used to release steering |
| `SOFT_ZONE_DEG` | `25` | Controls the steering sensitivity range |
| `FLIP_CAMERA` | `False` | Controls horizontal camera flipping |
| `SHOW_ANGLE` | `True` | Displays the steering angle |
| `MIN_DETECTION_CONF` | `0.7` | Minimum hand detection confidence |
| `MIN_TRACKING_CONF` | `0.5` | Minimum hand tracking confidence |
| `GRACE_FRAMES` | `8` | Frames allowed before releasing controls when hands disappear |
| `OPEN_FINGER_THRESH` | `3` | Number of detected open fingers required for an open-hand gesture |

---

## 🎯 Steering System

The program calculates the angle between the detected hand positions to determine the steering direction.

### Steering

When the hands are tilted:

```text
Tilt Left  → ← Left Arrow
Tilt Right → → Right Arrow
```

A dead zone is used around the center to prevent small hand movements from causing unwanted steering.

The current steering settings are:

```python
DEAD_ZONE_DEG = 12
RELEASE_ZONE_DEG = 6
SOFT_ZONE_DEG = 25
```

This helps make the steering more stable and reduces unwanted key presses.

---

## ✋ Hand Gesture Detection

The program detects the state of both hands.

### Both Fists

When both hands are detected as fists:

```text
ACCEL
```

The program presses:

```text
↑ Up
```

### Both Hands Open

When both hands are detected as open:

```text
BRAKE
```

The program presses:

```text
↓ Down
```

### One Fist + One Open Hand

When one hand is closed and the other is open:

```text
NEUTRAL
```

No acceleration or braking key is pressed.

Steering can still operate independently.

---

## 🛡️ Grace Period

Sometimes a hand may temporarily disappear from the camera.

To prevent controls from immediately changing because of a single missed frame, the program uses:

```python
GRACE_FRAMES = 8
```

After the allowed number of frames without detecting the hands, the program releases the keyboard controls.

This helps prevent keys from remaining pressed if the hands temporarily leave the camera view.

---

## 🖥️ On-Screen Display

The program provides a real-time interface showing information such as:

- Steering direction
- Steering angle
- Steering strength
- Acceleration status
- Braking status
- Left-hand status
- Right-hand status
- FPS
- Hand connection status
- Virtual steering wheel

This makes it easier to understand what the program is detecting while testing the controller.

---

## ⌨️ Keyboard Controls

The controller uses the following keyboard keys:

| Action | Keyboard Key |
|---|---|
| Accelerate | ↑ Up |
| Brake | ↓ Down |
| Steer Left | ← Left |
| Steer Right | → Right |

The keys are controlled automatically by `pynput`.

You do not need to press these keys manually while the program is running.

---

## 🛑 Stop the Program

To stop the program, focus on the camera window and press:

```text
Q
```

or:

```text
Esc
```

When the program exits, it releases the keyboard controls and closes the camera and application windows.

---

## 🎮 Using the Controller With Games

This project is designed for games or applications that accept keyboard controls.

The controller generates:

```text
↑ Up
↓ Down
← Left
→ Right
```

Therefore, it can be used with games that support these keyboard inputs.

### Google Chrome Dinosaur Game

The Chrome Dinosaur game is useful for testing the acceleration/jump-related input, but it does not use left/right steering controls.

The Dino game mainly uses:

```text
↑ Up / Space → Jump
↓ Down       → Duck
```

Therefore, it cannot demonstrate the complete left/right steering functionality of this project.

For testing the complete virtual steering wheel, use a game that supports:

```text
↑ ↓ ← →
```

---

## 🔧 Troubleshooting

### Camera does not open

First try:

```python
CAMERA_INDEX = 0
```

If that does not work, try:

```python
CAMERA_INDEX = 1
```

or:

```python
CAMERA_INDEX = 2
```

Also make sure another application is not using the webcam.

---

### Steering direction is reversed

Check:

```python
FLIP_CAMERA = False
```

The camera flipping setting can be changed if the displayed camera orientation does not match the desired control direction.

---

### Hands are not detected

Try the following:

- Improve the lighting.
- Keep both hands inside the camera frame.
- Avoid covering your hands.
- Move your hands closer to the camera.
- Make sure the webcam image is clear.
- Avoid very dark environments.

---

### Brake is not detected

The program uses:

```python
OPEN_FINGER_THRESH = 3
```

This means the open-hand detection depends on detecting enough open fingers.

Make sure your fingers are clearly visible to the camera.

---

### Brake triggers too easily

You can increase:

```python
OPEN_FINGER_THRESH
```

to make the open-hand detection more restrictive.

---

### Keys remain active briefly

The program uses:

```python
GRACE_FRAMES = 8
```

This provides a short grace period when hands temporarily disappear.

The value can be adjusted if needed.

---

### Low FPS

If the program is running slowly:

- Close unnecessary applications.
- Close other programs using the webcam.
- Make sure your computer is not under heavy load.
- Use a well-lit environment.
- Check the FPS displayed in the program window.

---

### MediaPipe model is missing

Make sure your computer has an internet connection during the first run.

The program will automatically download:

```text
hand_landmarker.task
```

if it is not already available.

---

## 📁 Project Structure

```text
virtual-steering-wheel/
│
├── README.md
├── requirements.txt
└── steering_wheel.py
```

The program may also download:

```text
hand_landmarker.task
```

when the model is required.

---

## 🧠 Technologies Used

### Python

Main programming language used to build the application.

### MediaPipe

Used for real-time hand detection and hand landmark tracking.

### OpenCV

Used for webcam access, image processing, and the on-screen interface.

### NumPy

Used for numerical calculations.

### pynput

Used to generate keyboard inputs from the detected hand gestures.

---

## 🚀 Possible Future Improvements

Future versions could include:

- Adjustable steering sensitivity from the interface
- Custom keyboard mappings
- Additional hand gestures
- Better gesture stability
- Improved calibration
- More game-control options
- Improved visual interface
- Controller configuration profiles
- Recording and demonstration mode

---

## 📜 License

This project is provided for learning, experimentation, and personal use.
