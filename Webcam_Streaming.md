# Raspberry Pi Webcam Streaming

This guide explains how to set up a USB webcam on a Raspberry Pi and stream the video over the internet using MJPG-Streamer.

## **1. Connect and Verify Your Webcam**
1. Plug your USB webcam into the Raspberry Pi.
2. Check if the webcam is detected by running:
   ```bash
   ls /dev/video*
   ```
   If you see `/dev/video0`, your webcam is recognized.

---

## **2. Install Required Packages**
Update your package list and install dependencies:
```bash
sudo apt update
sudo apt install git cmake libjpeg62-turbo-dev imagemagick libv4l-dev -y
```

---

## **3. Install and Configure MJPG-Streamer**
1. Clone the MJPG-Streamer repository:
   ```bash
   git clone https://github.com/jacksonliam/mjpg-streamer.git
   ```
2. Navigate to the directory:
   ```bash
   cd mjpg-streamer/mjpg-streamer-experimental
   ```
3. Build MJPG-Streamer:
   ```bash
   make clean
   make
   ```
4. Start streaming from your webcam:
   ```bash
   ./mjpg_streamer -i "./input_uvc.so -d /dev/video0 -r 640x480 -f 30" -o "./output_http.so -w ./www"
   ```

---

## **4. Access the Webcam Stream**
Find your Raspberry Pi's local IP:
```bash
hostname -I
```
Open your browser and go to:
```
http://<RaspberryPi-IP>:8080/?action=stream
```

---

## **5. Share the Stream Over the Internet**

### **Port Forwarding (Less Secure)**
1. Log in to your router and forward port `8080` to your Raspberry Pi’s IP address.
2. Find your public IP:
   ```bash
   curl ifconfig.me
   ```
3. Access the stream at:
   ```
   http://<your-public-IP>:8080/?action=stream
   ```

---


