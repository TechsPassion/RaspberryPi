# Create a systemd Service File

This guide explains how to run apps automatically when your Raspberry Pi starts up using MJPG-Streamer as an example

## **1. Create a Service File**
1. Create a "unit file" that tells systemd what to do.
2. Open a new file in the systemd directory using a text editor like nano:
   ```bash
   sudo nano /etc/systemd/system/mjpg-streamer.service
   ```

---

## **2. Add the Service Configuration**
Copy and paste the following configuration into the file.

Important: You must change the WorkingDirectory and ExecStart paths to match the location of your mjpg-streamer installation.
```bash
[Unit]
Description=MJPG-Streamer - USB Camera Stream
After=network.target

[Service]
# Replace 'pi' with the user you want to run the service as
User=pi

# !!! CHANGE THIS !!! 
# Set this to the directory where mjpg_streamer is located
WorkingDirectory=/home/pi/mjpg-streamer/mjpg-streamer-experimental

# !!! CHANGE THIS if your path is different !!! 
# This is the command to start the streamer
ExecStart=/home/pi/mjpg-streamer/mjpg_streamer -i "./input_uvc.so -d /dev/video0 -r 640x480 -f 30" -o "./output_http.so -w ./www"

# Restart the service if it crashes
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
Press Ctrl+X, then Y, then Enter to save and exit nano.
---

## **3. Enable and Start the Service**
1. Now, tell systemd to recognize and enable your new service to run on boot:
   ```bash
   # Reload systemd to recognize the new file
   sudo systemctl daemon-reload
   
   # Enable the service to start on boot
   sudo systemctl enable mjpg-streamer.service
   ```
2. You can start the service immediately without rebooting to test it:
   ```bash
   sudo systemctl start mjpg-streamer.service
   ```
3. Your stream should now be running. It will also start automatically every time you reboot your Pi.

Useful Commands:

Check the status: sudo systemctl status mjpg-streamer.service

Stop the service: sudo systemctl stop mjpg-streamer.service

Start the service: sudo systemctl start mjpg-streamer.service
   
