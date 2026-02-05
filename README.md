# 🪄 Invisibility Cloak - Harry Potter Magic with OpenCV

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-4.5+-green?style=for-the-badge&logo=opencv)
![NumPy](https://img.shields.io/badge/NumPy-Latest-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**Invisibility Cloak** recreates Harry Potter's magical invisibility cloak using computer vision! Wear any navy blue cloth and watch yourself disappear in real-time through your webcam. Pure OpenCV magic - no green screen required!

## ✨ Features

🎥 **Real-time Processing** - Instant invisibility effect through your webcam

🔵 **Navy Blue Detection** - Uses HSV color space for accurate cloth tracking

🪄 **Background Replacement** - Seamlessly replaces blue areas with captured background

🔄 **Mirror Mode** - Flipped display for natural interaction

🧹 **Noise Reduction** - Morphological operations for clean masking

⚡ **Fast Performance** - 30+ FPS on most systems

🎯 **No Green Screen** - Works with any navy blue cloth

## 🎬 How It Works

```
Background Capture → Real-time Detection → Color Masking → Background Overlay → Invisibility!
```

1. **Background Capture** - Program captures clean background (without you)
2. **Blue Detection** - Detects navy blue cloth in HSV color space
3. **Mask Creation** - Creates binary mask of blue regions
4. **Noise Removal** - Cleans mask using morphological operations
5. **Background Overlay** - Replaces blue areas with saved background
6. **Real-time Display** - Shows final invisibility effect

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Webcam
- Navy blue cloth/fabric (the "cloak")
- Good lighting conditions

### Installation

1. **Install dependencies**
```bash
pip install opencv-python numpy
```

2. **Download the script**
```bash
# Download cloak.py or clone the repository
```

3. **Run the magic!**
```bash
python cloak.py
```

## 🎯 Usage Instructions

### Step-by-Step Guide

1. **Run the script**
```bash
python cloak.py
```

2. **Move away from camera**
   - You'll see: "Background capture... Please move away"
   - Step completely out of frame
   - Wait 2-3 seconds

3. **Grab your navy blue cloth**
   - Any navy blue fabric works (cloth, towel, shirt)
   - The bluer and more solid, the better

4. **Stand in front of camera**
   - Hold the blue cloth in front of you
   - Watch yourself disappear! 🪄

5. **Press 'q' to quit**
   - Exit the magical experience

## 🎨 Technical Details

### Color Detection (HSV)

```python
# Navy Blue HSV Range
lower_blue = np.array([100, 60, 30])   # Hue: 100-130 (Blue)
upper_blue = np.array([130, 255, 180])  # Saturation: 60-255
                                         # Value: 30-180
```

### Image Processing Pipeline

```python
1. Mirror Frame        # cv2.flip() for natural view
2. BGR → HSV          # Color space conversion
3. Color Mask         # cv2.inRange() for blue detection
4. Noise Removal      # Morphological opening & dilation
5. Inverse Mask       # cv2.bitwise_not()
6. Background Layer   # cv2.bitwise_and() with mask
7. Foreground Layer   # cv2.bitwise_and() with inverse mask
8. Final Composite    # cv2.add() to combine layers
```

## ⚙️ Customization

### Change Detection Color

**For Red Cloak:**
```python
# Red HSV range
lower_red = np.array([0, 120, 70])
upper_red = np.array([10, 255, 255])
```

**For Green Cloak:**
```python
# Green HSV range
lower_green = np.array([40, 40, 40])
upper_green = np.array([80, 255, 255])
```

**For Yellow Cloak:**
```python
# Yellow HSV range
lower_yellow = np.array([20, 100, 100])
upper_yellow = np.array([30, 255, 255])
```

### Adjust Sensitivity

```python
# More sensitive (detects lighter blues)
lower_blue = np.array([100, 40, 40])
upper_blue = np.array([130, 255, 200])

# Less sensitive (only dark blues)
lower_blue = np.array([100, 100, 50])
upper_blue = np.array([130, 255, 150])
```

### Change Noise Reduction

```python
# Larger kernel = more smoothing
kernel = np.ones((5,5), np.uint8)  # Smoother edges

# Smaller kernel = preserve detail
kernel = np.ones((2,2), np.uint8)  # More detailed
```

## 🎭 Best Practices

### For Best Results

✅ **Good Lighting**
- Bright, even lighting works best
- Avoid shadows on the blue cloth
- Natural daylight is ideal

✅ **Navy Blue Cloth**
- Solid, uniform blue color
- Larger cloth = more invisible area
- Avoid shiny or reflective materials

✅ **Clean Background**
- Simple, static background
- Avoid moving objects
- No blue items in background

✅ **Stable Camera**
- Keep camera steady
- Fixed position (tripod recommended)
- Avoid moving the webcam

### Common Issues

❌ **Flickering Effect**
- Adjust HSV ranges for your lighting
- Use larger kernel for noise reduction
- Ensure stable lighting conditions

❌ **Incomplete Invisibility**
- Make sure entire cloth is in frame
- Check HSV color ranges
- Use more saturated blue fabric

❌ **Background Leaking**
- Ensure you were out of frame during capture
- Recapture background if needed
- Avoid moving background objects

## 📊 Performance

- **FPS:** 30-60 (depends on webcam and CPU)
- **Resolution:** Webcam default (usually 640x480 or 1280x720)
- **Latency:** < 50ms
- **CPU Usage:** 15-30%
- **Memory:** ~100-200 MB

## 🔧 Troubleshooting

### Camera Not Opening
```python
# Try different camera index
cap = cv2.VideoCapture(1)  # or 2, 3, etc.
```

### Background Capture Failed
```python
# Increase capture frames
for i in range(60):  # More frames for stability
    ret, background = cap.read()
```

### Color Not Detected
```python
# Test HSV values interactively
hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
print(hsv[height//2, width//2])  # Print center pixel HSV
```

### Slow Performance
```python
# Reduce resolution
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
```

## 🎓 How It Actually Works

### The Science Behind the Magic

1. **Background Subtraction**
   - Captures background without you
   - Stores this "empty" scene

2. **Color Segmentation**
   - HSV is better than RGB for color detection
   - Blue cloth is detected by hue (100-130°)

3. **Binary Masking**
   - White = Blue cloth detected
   - Black = Everything else

4. **Morphological Operations**
   - Opening: Removes small noise
   - Dilation: Fills small holes

5. **Bitwise Operations**
   - Mask isolates blue regions
   - Inverse mask isolates non-blue regions
   - Combining layers creates final effect

### Mathematical Formula

```
Final Image = (Background ∩ Blue_Mask) + (Current_Frame ∩ ~Blue_Mask)

Where:
∩ = Bitwise AND operation
~ = Bitwise NOT operation
+ = Image addition
```

## 💡 Use Cases

- 🎬 **Film Effects** - DIY special effects for videos
- 🎓 **Education** - Teaching computer vision concepts
- 🎮 **Gaming** - Virtual background effects
- 📹 **Video Calls** - Fun background replacement
- 🎪 **Entertainment** - Magic tricks and performances
- 👨‍🏫 **STEM Demos** - Science fair projects

## 🚀 Advanced Features

### Add Recording

```python
# Add video recording
fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter('output.avi', fourcc, 20.0, (640,480))

# In the loop
out.write(final)

# After loop
out.release()
```

### Multiple Color Detection

```python
# Detect multiple colors
mask_blue = cv2.inRange(hsv, lower_blue, upper_blue)
mask_red = cv2.inRange(hsv, lower_red, upper_red)
mask = cv2.bitwise_or(mask_blue, mask_red)
```

### Dynamic Background Update

```python
# Press 'b' to recapture background
if cv2.waitKey(1) & 0xFF == ord('b'):
    background = frame.copy()
    print("Background updated!")
```

## 📚 Learning Resources

### Concepts Covered
- Color space conversion (BGR → HSV)
- Binary image masking
- Morphological operations
- Bitwise operations
- Real-time video processing

### Related OpenCV Functions
- `cv2.cvtColor()` - Color space conversion
- `cv2.inRange()` - Threshold-based masking
- `cv2.morphologyEx()` - Morphological operations
- `cv2.bitwise_and()` - Bitwise AND
- `cv2.bitwise_not()` - Bitwise NOT
- `cv2.add()` - Image addition

## 🎨 Project Extensions

Try adding these features:

- [ ] Multiple cloth color support
- [ ] Dynamic background recapture (press 'b')
- [ ] Save video output
- [ ] Adjustable HSV sliders (trackbars)
- [ ] Full-body invisibility
- [ ] Transparent effect (partial visibility)
- [ ] Multiple people support
- [ ] Green screen mode

## 🔐 System Requirements

### Minimum
- **OS:** Windows 7+, macOS 10.12+, Linux (Ubuntu 18.04+)
- **Python:** 3.8+
- **RAM:** 2 GB
- **Webcam:** 480p
- **CPU:** Dual-core 2.0 GHz

### Recommended
- **OS:** Windows 10+, macOS 12+, Linux (Ubuntu 20.04+)
- **Python:** 3.10+
- **RAM:** 4 GB+
- **Webcam:** 720p or 1080p
- **CPU:** Quad-core 2.5 GHz+

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- [OpenCV](https://opencv.org/) - Computer vision library
- [Harry Potter](https://www.wizardingworld.com/) - Inspiration for the magic!
- Computer vision community - For tutorials and resources

## 👨‍💻 Author

**Shubroto Das**
- GitHub: [@ShubrotoDas10](https://github.com/ShubrotoDas10)

## 🆘 Support

Having issues?
- Check the troubleshooting section
- Ensure webcam is working
- Verify all dependencies are installed
- Try different lighting conditions
- Use a more saturated blue cloth

## 🌟 Fun Facts

- 🎬 The same technique is used in Hollywood VFX (chroma keying)
- 🔵 Blue and green are used because they're furthest from human skin tones
- 🪄 This effect can work with any solid color, not just blue!
- 📺 Weather forecasters use this exact technique daily
- 🎮 Virtual backgrounds in Zoom use similar technology

## 📞 Quick Start Commands

```bash
# Install dependencies
pip install opencv-python numpy

# Run the magic
python cloak.py

# Quit
Press 'q' key
```

---

<div align="center">

**Become Invisible Like Harry Potter! 🪄**

*No wands required, just Python and a blue cloth!*

[Report Bug](https://github.com/ShubrotoDas10/InvisibilityCloak/issues) · [Request Feature](https://github.com/ShubrotoDas10/InvisibilityCloak/issues)

</div>
