# Autonomous IoT Smart Bin: Embedded C++ & Cloud Architecture

An end-to-end IoT solution that bridges physical hardware with real-time cloud infrastructure. Built with C++ on an ESP8266, this project focuses on robust sensor data processing, fault tolerance, and optimized cloud communication.

## Engineering Highlights

While reading an ultrasonic sensor is trivial, building a reliable, autonomous system is not. This project implements several advanced embedded software concepts:

* **Algorithmic Signal Smoothing:** Ultrasonic sensors (HC-SR04) often return noisy or anomalous data. I implemented a custom `getAverageDistance()` function that acts as a low-pass filter, rejecting outliers (measurements deviating >20% from the baseline) to ensure absolute data accuracy.
* **Dynamic Auto-Calibration:** Upon boot, the system dynamically measures and calibrates its total depth (`initDistance`), making the codebase hardware-agnostic and adaptable to any bin size without hardcoding values.
* **Bandwidth & Power Optimization:** Instead of continuously blasting data to the cloud, the system uses delta-based updates. It pushes JSON payloads to Firebase only if the fill level changes significantly (≥5%), or upon a defined timeout, drastically reducing API calls.
* **Two-Way Asynchronous Communication:** * **Upstream:** Pushes real-time fill percentages, lid-open counters, and timestamp data to Firebase.
  * **Downstream:** Listens for remote commands (e.g., "MEASURE" via web dashboard) to trigger on-demand hardware interruptions.
* **Secure Webhooks:** Utilizes `WiFiClientSecure` to trigger Google Apps Script APIs for automated email notifications when critical capacity (80%) is reached.

##  Tech Stack
* **Hardware:** ESP8266 Microcontroller, HC-SR04 Ultrasonic Sensor.
* **Language:**  C++
* **Cloud & DB:** Google Firebase (Realtime Database), JSON Data Structuring.
* **Networking:** 802.11 Wi-Fi, Secure HTTP (HTTPS) Requests, Webhooks.

##  About the Developer
I am Kaan Degirmenci, a Computer Science student with a strong passion for System Architecture. This project showcases my ability to write clean, memory-efficient C++ code for low-level hardware while seamlessly integrating it into high-level cloud architectures.
