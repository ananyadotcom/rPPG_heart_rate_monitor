# Three-ROI Heart Rate Monitor

A real-time, non-contact heart rate monitoring application using regular webcams. This project uses computer vision and signal processing techniques (such as rPPG - remote photoplethysmography) to estimate a user's heart rate by analyzing slight color variations in their facial skin caused by blood flow.

## Features

- **Real-Time Processing:** Captures video feed from your webcam to estimate heart rate instantly.
- **Advanced Face Tracking:** Utilizes MediaPipe Face Mesh to accurately track facial landmarks.
- **Three-ROI System:** Enhances accuracy by extracting and combining signals from three Regions of Interest (ROIs): the forehead and both cheeks.
- **Robust Signal Processing:**
  - Dynamic ROI quality assessment and weighting.
  - Signal noise reduction using Butterworth bandpass filtering.
  - Heart rate calculation using both Fast Fourier Transform (FFT) and Peak Detection.
  - Signal-to-Noise Ratio (SNR) tracking to provide a confidence metric.
- **Live Visualization:** Displays live graphs for raw signals, filtered signals, and frequency spectrums directly on the application window.

## Project Structure

- `heart_rate_monitor/`
  - `main.py`: The entry point of the application. Integrates all components and runs the main video loop.
  - `video_processor.py`: Handles webcam initialization, frame capturing, and facial landmark detection using MediaPipe.
  - `roi_manager.py`: Responsible for extracting and managing the different facial Regions of Interest.
  - `signal_processor.py`: Contains the core logic for filtering the raw color signals and estimating the heart rate (BPM).
  - `visualization.py`: Manages the on-screen display, rendering graphs, text, and bounding boxes over the camera feed.
  - `config.py`: Stores configuration parameters and constants used across the application.
  - `utils.py`: Helper functions for signal processing and math operations.

## Requirements

Ensure you have Python 3.7+ installed. The following libraries are required:

- OpenCV (`opencv-python`)
- MediaPipe (`mediapipe`)
- NumPy (`numpy`)
- SciPy (`scipy`)


