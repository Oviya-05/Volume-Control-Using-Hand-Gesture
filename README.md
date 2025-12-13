# Volume-Control-Using-Hand-Gesture
Real-time system for touchless volume control. It utilizes MediaPipe and OpenCV to detect hand gestures (index-thumb distance) and maps the spatial relationship directly to system audio via pycaw. Provides an elegant, highly responsive alternative to physical controls.

# Key Technologies Used
<img width="596" height="241" alt="image" src="https://github.com/user-attachments/assets/e14462c0-deb3-40be-beac-670ef56f9bb2" />

## How It Works
### 1. Webcam Acquisition
  The application captures live video feed from a webcam using OpenCV. Each frame is processed in real time to detect the user’s hand. 
  
### 2. Hand Detection and Landmark Extraction
  
  MediaPipe’s hand tracking model detects and tracks up to 21 key hand landmarks (fingertips and joints) in each frame. These landmarks provide precise (x, y) coordinates of hand features. 
    
### 3. Gesture Interpretation
  
  The core gesture used for volume control is the relative distance between the thumb tip and the index fingertip:
  
    Larger distance → Increase volume
      
    Smaller distance → Decrease volume
  
  A continuous mapping function interpolates this distance to the system audio volume range. 
  
### 4. Volume Mapping and Control
  
  Using the pycaw library, the system translates the computed gesture-based value into an actual system volume level. Continuous adjustments ensure smooth volume transitions. 
   
### 5. Visual Feedback (Optional)
  
  Many implementations draw the hand landmarks, connecting line between fingers, and a dynamically updating volume bar on the webcam window so that the user can see gesture detection and volume state in real time. 


## Functional Workflow (Step-by-Step)

  * Initialize Webcam Feed
  
    Start video capture from the default or specified camera.
  
  * Detect and Track Hand
  
    Employ MediaPipe Hands to locate and track hand landmarks.
  
  * Compute Finger Distance
  
    Extract coordinates for the thumb tip and index fingertip.
    
    Calculate Euclidean distance between these points.
  
  * Map Distance to Volume
  
    Normalize the gesture distance to the system volume range.
    
    Use linear interpolation to obtain the equivalent volume level.
  
  * Apply Audio Control
  
    Set system volume through the audio control interface (pycaw).
    
    Provide UI Feedback
  
    Display volume value and live hand tracking visuals on the screen.
  
  * Strengths and Features
  
    Touchless Interaction: Eliminates the need for physical buttons for volume control.

