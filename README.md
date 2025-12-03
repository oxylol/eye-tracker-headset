# Open Source Gaze Tracker

**Status:** Design & Specification Phase

## Project Abstract
This repository contains the design files and software architecture for a custom head-mounted eye tracker. The project aims to replicate professional gaze-mapping functionality by synchronizing a high-speed infrared camera (eye) with a wide-angle scene camera.

The system runs on a **Raspberry Pi Compute Module 4** processing dual video streams to calculate a real-time gaze vector.

## Hardware Specifications

The system is built on the **Waveshare Mini Base Board (A)**, utilizing its dual CSI capability to interface with both cameras simultaneously without adapters.

### Bill of Materials

| Component | Part Name | Price (Est.) | Purpose |
| :--- | :--- | :--- | :--- |
| **Compute Module** | [Raspberry Pi CM4 (2GB RAM, WiFi)](https://www.waveshare.com/compute-module-4.htm?sku=18789) | €49.91 | 2GB is sufficient for headless (SSH) operation. "Lite" uses SD card. |
| **Carrier Board** | [Waveshare Mini Base Board (A)](https://www.waveshare.com/CM4-IO-BASE-A.htm) | €16.34 | Compact breakout with 2x Standard CSI-2 ports. |
| **Eye Camera** | [Arducam OV9281 Global Shutter](https://www.welectron.com/Arducam-B0165-OV9281-1MP-Global-Shutter-Monochrome-NoIR-Camera-Module-with-M12-Mount-lens-for-Raspberry-Pi-4-3B-3) | €47.90 | 120FPS Monochrome capture of the pupil (NoIR). |
| **World Camera** | [Waveshare RPi Camera (D)](https://www.waveshare.com/rpi-camera-d.htm) | €12.04 | Wide-angle OV5647 sensor for scene recording. |
| **Cooling** | [CM4 Aluminum Heatsink](https://www.waveshare.com/cm4-heatsink.htm) | €3.00 | Essential for cooling the CPU during video encoding. |
| **Lighting** | [850nm IR LEDs x3](https://www.electrokit.com/led-ir-tshg5410-5mm-850nm-55mw-36gr) | €0.99 | Illuminates the eye for the OV9281 sensor. |
| **Mounting** | Custom 3D Printed Frame | N/A | Chassis to attach cameras to safety glasses. |

*A full parts list can be found in `BOM.csv`. I will be manufacturing the mount on my personal 3D printer, so no outsourcing costs are required.*

 ## Software Architecture

The device operates in "Headless Mode" to conserve RAM.

1.  **OS:** Raspberry Pi OS Lite (64-bit).
2.  **Access:** SSH over WiFi (VS Code Remote Development).
3.  **Video Pipeline:**
    * **Stream 1 (Eye):** OV9281 capturing 640x400 @ 120fps (Global Shutter).
    * **Stream 2 (World):** OV5647 capturing 1280x720 @ 30fps.
4.  **Algorithm:**
    * Python/OpenCV script performs pupil centroid detection on the Stream 1 (IR) feed.
    * Coordinate transformation maps the centroid to Stream 2 (World) pixels.

## Repository Structure

* `/hardware` - CAD files (.step/.stl) for the custom headset mount.
* `/src` - Python scripts for multi-camera initialization and testing.

## Development Roadmap

* [ ] **Phase 1:** Procurement of Hardware.
* [ ] **Phase 2:** SSH Setup and dual-camera test script.
* [ ] **Phase 3:** 3D Modeling.
* [ ] **Phase 4:** Developing the pupil tracking algorithm.
