# idotmatrix-homeassistant
Home Assistant iDotMatrix Display Integration

This repository provides a solution for integrating the iDotMatrix display into Home Assistant via MQTT. This setup allows you to control the iDotMatrix display, upload GIFs, and manage brightness using MQTT automations within Home Assistant.
It's build on derkalle4's project https://github.com/derkalle4/python3-idotmatrix-library

Features

    Display Control: Turn the display on or off via MQTT messages.
    GIF Upload: Upload and display GIFs on the iDotMatrix display from Home Assistant.
    Brightness Control: Adjust the display brightness via MQTT messages.

Requirements

    Home Assistant installed and running.
    Python 3.x with a virtual environment set up.
    iDotMatrix Display and its Bluetooth connection available.
    MQTT Broker set up and connected with Home Assistant.
    Git installed for cloning the repository.

Installation
1. Clone the Repository

bash

git clone https://github.com/YOUR_USERNAME/homeassistant-idotmatrix-display.git
cd homeassistant-idotmatrix-display

2. Set Up Python Environment

    Create and activate a Python virtual environment:

    bash

python3 -m venv venv
source venv/bin/activate

Install the necessary Python dependencies:

bash

    pip install -r requirements.txt

3. Configure MQTT in Home Assistant

Ensure that your MQTT broker is set up and configured within Home Assistant. You can do this by adding the following to your configuration.yaml:

yaml

mqtt:
  broker: 192.168.x.x
  username: mqtt_user
  password: test

4. Edit the idotmatrix_service.py Script

Update the idotmatrix_service.py file with your iDotMatrix display’s Bluetooth address and MQTT broker information.

python

MQTT_BROKER = "192.168.x.x"  # Your MQTT broker IP address
MQTT_USERNAME = "mqtt_user"   # Your MQTT username
MQTT_PASSWORD = "test"        # Your MQTT password

5. Automate the Script on System Boot

Follow one of the methods below to automate starting the display service on system boot:
Method 1: Add to rc.local

bash

sudo nano /etc/rc.local

Add the following before the exit 0 line:

bash

/homeassistant-idotmatrix-display/run.sh &

Method 2: Use Cron Job

    Edit cron jobs:

    bash

sudo crontab -e

Add the following line:

bash

    @reboot /homeassistant-idotmatrix-display/run.sh &

6. Running the Script

You can manually start the service using:

bash

./run.sh

Usage

Once everything is set up and running, you can control the display using MQTT messages.
Turning Display On/Off

To control the display power, send a JSON payload to the display/control topic:

json

{
  "state": "on"
}

Uploading a GIF

To upload a GIF to the display, send a JSON payload to the display/gif topic:

json

{
  "filename": "your_gif.gif"
}

Ensure that the GIF file exists in the /homeassistant/images/ directory.
Adjusting Brightness

To adjust the brightness, send a JSON payload to the display/control topic:

json

{
  "brightness": 75
}

Directory Structure

bash

.
├── idotmatrix_service.py       # Main script that handles MQTT messages and controls the iDotMatrix display
├── run.sh                      # Script to run the idotmatrix service
├── requirements.txt            # Python dependencies
└── images/                     # Directory to store your GIFs

Credits

    iDotMatrix Library: Integration with the iDotMatrix display is powered by the idotmatrix library https://github.com/derkalle4/python3-idotmatrix-library
    Paho-MQTT: MQTT communication is managed through the Paho-MQTT library.

Make sure to respect the licenses of the iDotMatrix library and other third-party tools used in this repository.
