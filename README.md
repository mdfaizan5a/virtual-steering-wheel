Sure 👍 Here is the **complete fixed README in Markdown code format**, so you can directly copy-paste it into `README.md`:

````markdown
# 🎮 Virtual Steering Wheel — MediaPipe + Python

Control a car game using your hands as a virtual steering wheel — no physical steering wheel required.

The project uses your **webcam, MediaPipe, OpenCV, and Python** to detect both hands and convert hand gestures into keyboard controls.

---

## 🚗 How It Works

Place both hands in front of your webcam as if you are holding a steering wheel.

- 👊 **Both fists** → Accelerate
- 🖐 **Both hands open** → Brake
- ↔️ **Tilt both hands** → Steer left or right
- 👊🖐 **One fist + one open hand** → Neutral
- ❌ **No hands detected** → Release all keys

The controller sends keyboard inputs using `pynput`.

---

## 🎮 Gestures

| Gesture | Action | Keyboard |
|---|---|---|
| 👊 Both fists, hands level | Accelerate | ↑ UP |
| 👊 Both fists, tilt LEFT | Accelerate + steer left | ↑ + ← |
| 👊 Both fists, tilt RIGHT | Accelerate + steer right | ↑ + → |
| 🖐 Both hands open, level | Brake | ↓ DOWN |
| 🖐 Both hands open, tilt LEFT | Brake + steer left | ↓ + ← |
| 🖐 Both hands open, tilt RIGHT | Brake + steer right | ↓ + → |
| 👊🖐 One fist + one open hand | Neutral | — |
| ❌ No hands visible | Release all keys | — |

> **Tip:** Steering works independently from acceleration and braking, so you can steer while accelerating or braking.

---

## ✨ Features

- 🎥 Real-time webcam hand tracking
- ✋ Detects up to two hands
- 👊 Fist detection for acceleration
- 🖐 Open-hand detection for braking
- ↔️ Gesture-based left/right steering
- 🎮 Sends keyboard controls using `pynput`
- 📐 Steering angle detection
- 🎯 Dead-zone to reduce unwanted steering
- 🛡️ Grace period when hands temporarily disappear
- 📊 Real-time FPS display
- 🖥️ On-screen steering wheel and HUD
- 📥 Automatically downloads the MediaPipe hand model
- 🪟 Windows camera support

---

## 💻 Requirements

### Hardware

- Webcam
- Computer with Python support

### Software

- Python 3.9+
- Internet connection for the first run if the MediaPipe hand model is not already downloaded

---

## 📦 Install Dependencies

Open PowerShell or Terminal in the project folder and run:

```bash
pip install mediapipe opencv-python numpy pynput
````

---

## ▶️ Run the Project

### Windows

```bash
python steering_wheel.py
```

### macOS / Linux

```bash
python3 steering_wheel.py
```

On the first run, the program automatically downloads:

```text
hand_landmarker.task
```

The model is downloaded only if it is not already present.

---

## 🪟 Windows Setup

The program automatically selects the camera backend based on your operating system.

No manual backend change is required.

The default camera setting is:

```python
CAMERA_INDEX = 0
```

If your webcam does not open, try:

```python
CAMERA_INDEX = 1
```

or:

```python
CAMERA_INDEX = 2
```

Then run the program again.

### Windows Camera Permission

If Windows asks whether Python can access your camera, select **Allow**.

---

## ⚙️ Configuration

The main settings are located near the top of `steering_wheel.py`.

| Setting              | Default | Description                                       |
| -------------------- | ------: | ------------------------------------------------- |
| `CAMERA_INDEX`       |     `0` | Webcam index                                      |
| `DEAD_ZONE_DEG`      |    `12` | Steering angle ignored around the center          |
| `RELEASE_ZONE_DEG`   |     `6` | Angle used to release steering                    |
| `SOFT_ZONE_DEG`      |    `25` | Controls steering strength                        |
| `FLIP_CAMERA`        | `False` | Controls horizontal camera mirroring              |
| `SHOW_ANGLE`         |  `True` | Shows steering angle on screen                    |
| `MIN_DETECTION_CONF` |   `0.7` | Minimum hand detection confidence                 |
| `MIN_TRACKING_CONF`  |   `0.5` | Minimum hand tracking confidence                  |
| `GRACE_FRAMES`       |     `8` | Frames before releasing keys when hands disappear |
| `OPEN_FINGER_THRESH` |     `3` | Fingers required to detect an open hand           |

---

## 🖥️ On-Screen Display

The program displays:

* Current steering direction
* Steering angle
* Steering strength
* Acceleration / braking status
* Left-hand status
* Right-hand status
* FPS
* Hand connection
* Virtual steering wheel

---

## ⌨️ Controls

The program sends these keyboard keys:

| Gesture     | Key     |
| ----------- | ------- |
| Accelerate  | ↑ Up    |
| Brake       | ↓ Down  |
| Steer Left  | ← Left  |
| Steer Right | → Right |

### Quit

Press:

```text
Q
```

or:

```text
Esc
```

in the camera window to stop the program.

The program releases all held keys before exiting.

---

## 🎮 Compatible Games

This controller is designed for games that use keyboard arrow keys.

Examples include:

* Racing games using ↑ ↓ ← →
* Trackmania
* TORCS
* Hill Climb Racing browser versions
* Other browser or PC games with arrow-key controls

### Google Chrome Dinosaur Game

The Chrome Dinosaur game mainly uses:

* `Space` / `↑` for jumping
* `↓` for ducking

It does **not** use left/right steering.

Therefore, Dino can demonstrate the **UP/DOWN controls**, but a racing game using all four arrow keys is better for testing the complete virtual steering wheel.

---

## 🔧 Troubleshooting

| Problem                        | Possible Fix                                                          |
| ------------------------------ | --------------------------------------------------------------------- |
| Camera does not open           | Try `CAMERA_INDEX = 0`, `1`, or `2`                                   |
| Steering direction is reversed | Try changing `FLIP_CAMERA`                                            |
| Hands are not detected         | Improve lighting and keep both hands visible                          |
| Brake does not trigger         | Open your fingers clearly; at least 3 fingers must be detected        |
| Brake triggers too easily      | Increase `OPEN_FINGER_THRESH`                                         |
| Keys remain active briefly     | The controller waits for `GRACE_FRAMES` before releasing keys         |
| Low FPS                        | Close other camera-using applications or reduce camera resolution     |
| MediaPipe model missing        | Run the program with an internet connection so the model can download |

---

## 📁 Project Structure

```text
virtual-steering-wheel/
│
├── README.md
├── requirements.txt
└── steering_wheel.py
```

The program may also create/download:

```text
hand_landmarker.task
```

when it is needed.

---

## 🧠 Technologies Used

* **Python**
* **MediaPipe**
* **OpenCV**
* **NumPy**
* **pynput**

---

## 🚀 Future Improvements

Possible future improvements include:

* Better hand detection stability
* Adjustable steering sensitivity
* More configurable gestures
* Support for additional game controls
* Improved UI
* Recording/demo mode
* Better calibration
* Custom key mapping

---

## 📜 License

This project is available for learning and experimentation.

```

**Bas `README.md` ka pura old content replace karke ye paste kar do.** ✅
```
