# Geomotion
Geomotion is an Android application designed to detect and classify road anomalies such as potholes, road cracks, and bumps using data collected from smartphone sensors. The app implements a classification model developed as part of the developers' Thesis research.

# Requirements
1. A smartphone compatible with [SensorLogger](https://github.com/tszheichoi/awesome-sensor-logger), as the app leverages data from the device’s accelerometer, gyroscope, and GPS sensors
1. Active internet connection for Google Maps API (optional; coordinates will still display even if the map is unavailable due to API token expiration)

# Features
1. Detects and classifies road anomalies
   - potholes
   - road cracks
   - road bumps
1. Geotags detected anomalies on Google Maps (if API token is valid)
1. Displays coordinates of detected anomalies even without map availability

# How to run
1. Launch SensorLogger on your smartphone
1. Tap the gear icon to open settings
1. Select Data Streaming
1. Enable HTTP Push by toggling the button
1. Set the Push URL to your smartphone's Wi-Fi IP address, using port `8000` and the endpoint `/data`.
   - Example: `http://192.168.x.x:8000/data`
   - Replace `127.0.x.x` with your actual IP address
1. Launch Geomotion
1. Press Check Status; you should see a popup saying:
   - `"SensorLogger Status: No data received yet"` (this is expected since SensorLogger is still inactive)
1. Return to SensorLogger’s settings and tap Test Push to verify connection. A "Got Status: 200" response indicates success
1. Go back to SensorLogger’s home screen and make sure both Accelerometer and Gyroscope sensors are enabled.
1. Enable your smartphone’s Location Services.
1. In SensorLogger, press Start Recording.
1. Switch back to Geomotion and press Start Recording to begin anomaly detection.

# Limitations

Field testing revealed two significant challenges affecting its system performance:

### Over-Classification of Segments as Potholes  
The model exhibited a tendency to overclassify road segments as potholes. This indicates that the decision boundary of the classifier is particularly sensitive to features associated with potholes. This observation is consistent with the error analysis of the research, where pothole misclassification rates were notably higher compared to other anomaly classes.

### Windowing and Segmentation Limitations  
The application uses fixed-duration windows of size 50 for feature extraction during field testing. This static windowing approach led to inconsistent results: shorter windows fragmented large anomalies, while longer windows lacked sufficient context for smaller anomalies. Future developers working on this repository may consider adjusting the window size, which can be modified in the HomeFragment class.

### Proposed Refinements  
To address these limitations, we propose the following enhancements:  
- Implement adaptive sliding windows with overlap to better capture full anomaly signatures under varying road conditions.  
- Develop an improved classification model to increase the reliability of pothole detection.  
- Employ event-triggered segmentation (e.g., based on acceleration thresholds) to focus processing on suspected anomaly events.

Future work should prioritize field validation of these refinements to improve the system’s alignment with real-world road conditions and performance expectations.

# Proponents
  - Developers: Mary Erika Culala and Gleezell Uy
  - Thesis Adviser: Clement Ong

# Technologies used
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=java&logoColor=white)
![AndroidStudio](https://img.shields.io/badge/Android%20Studio-3DDC84.svg?style=for-the-badge&logo=Android-Studio&logoColor=white)
