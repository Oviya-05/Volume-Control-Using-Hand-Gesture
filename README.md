# AirVolume: Volume_Control_Using_Hand_Gesture

**Team Members:** Oviya K P, Girija, Muhammad Rashad, Dhanush
**Mentor:** Dr. D. Bhanu Prakash
**Platform:** Infosys Springboard

---
## Project Overview

<img width="1376" height="897" alt="image" src="https://github.com/user-attachments/assets/3276725b-aea2-4409-a7f3-6c8f1f715f57" />


<div style="text-align: justify">
  
AirVolume is a Human-Computer Interaction (HCI) application designed to translate physical hand gestures into real-time digital system commands. By leveraging a standard webcam and the Windows Core Audio APIs, this project eliminates the need for physical peripherals, offering a touchless and intuitive control mechanism. The system utilizes a computer vision pipeline to detect hand landmarks and interfaces directly with the operating system to adjust master volume levels.
</div>

---
## 1. Development Methodology: Adaptive Agile Framework
<div style="text-align: justify">
To manage the multifaceted nature of the AirVolume system, the team utilized an Agile-Iterative methodology. This approach allowed for the concurrent development of three critical modules: the Computer Vision Pipeline, the Dynamic UI Layer, and the Core Audio Interface.
</div>

### 1.1 Iterative Lifecycle
The project progressed through three high-impact phases:
- **Phase 1**: Environment Orchestration: Establishing the cross-platform dependency matrix (OpenCV, MediaPipe, Kivy, and Pycaw).
- **Phase 2:** Core Logic Synthesis: Engineering the vector-based gesture recognition engine and the signal smoothing algorithms.
- **Phase 3:** System Validation: Stress-testing the Windows Core Audio API integration and optimizing the real-time UI frame rate.

### 1.2 Cross-Functional Synchronization
<div style="text-align: justify">
We bridged the gap between backend execution and frontend visualization. By implementing a Function Trace Debugger within the Kivy dashboard, the team ensured that real-time backend logs (e.g., device switching, lock states) were mirrored instantaneously for the user.
  
---
## 2. System Architecture:
The application operates on a linear, low-latency pipeline defined by three distinct stages: Acquisition, Cognition, and Execution.

<img width="816" height="452" alt="image" src="https://github.com/user-attachments/assets/2d108532-200d-4e54-bb23-f55d0508edc6" />

### 2.1 Image Acquisition 
- **Ingestion:** The system initializes a high-speed stream via cv2.VideoCapture(0).
- **Geometric Normalization:** Frames undergo a horizontal flip transformation (cv2.flip) to provide a naturalistic mirror interface for the user.
- **Stack:** OpenCV for vision processing and NumPy for high-performance matrix manipulation.

### 2.2 Gesture Recognition:
The system leverages Google’s MediaPipe framework for real-time hand-mesh reconstruction, but adds a custom mathematical layer for gesture interpretation.
- **Spatial Mapping:** Identification of 21 localized hand landmarks.
- **Vector Geometry:** To ensure depth-robustness, we transitioned away from distance-based measurements. Instead, we calculate the angular relationship between the Wrist (Point 0), Thumb Tip (Point 4), and Index Tip (Point 8).
- **Scale Invariance:** By utilizing the dot product formula to derive angles, the system remains accurate regardless of the user’s distance from the lens.

<div align="center">
 <img width="216" height="56" alt="image" src="https://github.com/user-attachments/assets/0eb5cdad-3112-4559-9550-08c4f614680a" />
</div>


### 2.3 System Interfacing 
- **Audio Endpoint Management:** Using the Pycaw library, the system communicates with Windows Core Audio APIs.
- **COM Implementation:** The backend initializes a Component Object Model (COM) interface to gain direct, granular control over the system's default render and capture devices.

---
## 3.Technical Implementation
### 3.1 Responsive UI Engineering (Kivy)
The dashboard was designed for high-fidelity feedback and aesthetic appeal.
- **Component Design:** Implementation of the CurvedNeonBox widget for a modern "Glow-UI" feel.
- **Real-Time Analytics:** The interface renders live metrics including Vector Angle, Volume Percentage, and a dynamic Gain Level bar.
- **Concurrency Management:** To prevent UI blocking, we utilized Clock.schedule_interval to decouple video processing from the main interface thread, maintaining a consistent 30 FPS.
  <img width="1381" height="893" alt="image" src="https://github.com/user-attachments/assets/e138954a-d8c3-426d-95e0-485ecb7d8e60" />


  
### 3.2 Signal Processing & Smoothing
To mitigate "jitter"—unintentional volume fluctuations caused by minor hand tremors—we implemented an **Exponential Moving Average (EMA) algorithm:**
<div align="center">
<img width="377" height="44" alt="image" src="https://github.com/user-attachments/assets/9fbed76c-2eb0-4ecc-9564-f0f51a449790" />
</div>

- **Impact**: This result is a fluid, high-end user experience where volume transitions feel intentional and professional.
  
### 3.3 Target-Specific Audio Routing
Unlike standard volume controllers, our code allows for **Application-Specific Control**. By iterating through active audio sessions, the system can target specific processes like chrome.exe or Discord.exe without affecting the global system volume.

---
## 4. Challenges & Solutions
| Challenge | Impact | Solution |
| :--- | :--- | :--- |
| **Z-Axis Variance** | Distance from camera caused volume "drift." | Replaced Euclidean distance with Angular Vector Logic. |
| **Interface Latency** | Heavy math calculations slowed the UI. | Optimized the update loop and implemented Kivy Clock scheduling. |
| **Hand Ambiguity** | Left hand movements accidentally triggered volume. | Implemented Zonal Logic (Left Zone for Locking, Right Zone for Volume). |

---
## 5. Milestone Outcomes & Insights

### **Milestone 1: Computer Vision Fundamentals**
- **Numerical Perception:** Established the foundational concept that digital images are processed as multi-dimensional numerical grids, where every pixel corresponds to an intensity value within a NumPy matrix.
- **Matrix Manipulation:** Gained the ability to treat video frames as live data structures, allowing for real-time mathematical operations on the underlying image arrays.

### **Milestone 2: Spatial Mapping & OpenCV Proficiency**
- **API Mastery:** Developed technical fluency in OpenCV basics, specifically managing the lifecycle of image data through ingestion (cv2.imread), real-time rendering (cv2.imshow), and frame transformation.

- **Coordinate Logic:** Internalized the Top-Left Origin (0,0) coordinate system. Mastering this spatial orientation was critical for aligning physical hand movements with digital screen coordinates.

### **Milestone 3: Deep Learning Concepts**
- We explored how Convolutional Neural Networks (CNNs) emulate biological neurons to process visual data
- We learned that traditional linear layers are insufficient for vision; [cite_start]Activation Functions are required to introduce non-linearity and "unlock" the network's ability to learn complex shapes

### **Milestone 4: System Integration**
- We learned that Windows uses Audio Endpoints to abstract hardware devices *We discovered that Pycaw acts as a Pythonic wrapper, hiding the complexity of low-level C++ COM pointers and allowing us to control system volume with high-level commands

---
## 6.Future Scope & Roadmap
To advance the AirVolume pipeline, the following strategic enhancements are prioritized:

### **Advanced Gesture Logic**
- **Motion Tracking:** Implementing LSTM/GRU networks to recognize dynamic gestures like swipes or circular motions.
- **Voice Fusion:** Adding multi-modal confirmation to prevent accidental triggers in busy environments.
### **Robustness & Security**
- **Hand Biometrics:** Restricting control to authorized users based on unique hand-geometry signatures.
- **Synthetic Training:** Using Generative AI to improve landmark detection in low-light or high-glare conditions.
### **Accessibility & Navigation**
- **Adaptive Input:** Auto-calibrating sensitivity for users with limited ranges of motion.
- **Virtual Mouse:** Expanding gestures to control system-wide scrolling and window management.
### **Cross-Platform Expansion**
- **OS Portability**: Transitioning to agnostic libraries for macOS and Linux compatibility.
- **Mobile Edge:** Optimizing the pipeline for Android/iOS smart-home integration.

---
