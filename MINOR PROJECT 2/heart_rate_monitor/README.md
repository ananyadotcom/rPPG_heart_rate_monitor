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

You can install the dependencies using pip:

```bash
pip install opencv-python mediapipe numpy scipy
```

## Usage

1. Clone this repository.
2. Navigate to the `heart_rate_monitor` directory:
   ```bash
   cd heart_rate_monitor
   ```
3. Run the application:
   ```bash
   python main.py
   ```
4. Look straight into the camera in a well-lit room. Ensure your face is clearly visible and try to keep still.
5. The application will track your face, extract signals, and after a short buffer period, display your estimated heart rate (BPM) along with a confidence level.
6. Press the **'q'** key to quit the application.

## How it Works

The application operates on the principle of remote photoplethysmography (rPPG):
1. **Face Detection:** It detects the user's face and isolates specific skin regions (forehead and cheeks).
2. **Signal Extraction:** It tracks the average pixel intensity over time in the ROI bounding boxes. These values correspond to subtle skin color changes synchronized with the cardiac cycle.
3. **Filtering:** The raw signal is noisy, so a Butterworth bandpass filter is applied to isolate frequencies that correspond to a normal human heart rate (typically 0.8 Hz to 3.5 Hz).
4. **Estimation:** The filtered signal is analyzed using FFT and peak detection to determine the dominant frequency, which is then converted into Beats Per Minute (BPM).
