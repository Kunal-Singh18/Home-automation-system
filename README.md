<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Home Automation System - README</title>
</head>
<body>

<h1>Home Automation System</h1>

<p>This project is a home automation system developed using a Raspberry Pi. The system is designed to automate control over household appliances like bulbs and fans, as well as monitor the environment through sensors such as PIR and gas sensors.</p>

<h2>Features</h2>
<ul>
  <li>Automated control of lights and fans based on sensor inputs.</li>
  <li>Fire detection through gas sensors, which triggers an alarm and sends an SMS alert.</li>
  <li>Motion detection using a PIR sensor to control appliances.</li>
  <li>Temperature and light intensity monitoring to adjust fan speed and lighting accordingly.</li>
</ul>

<h2>Python Scripts</h2>

<h3>main.py</h3>
<p>This is the main Python script that controls the home automation system. It handles sensor input and outputs to actuators (bulbs, fans, buzzer). The code is written using the <code>RPi.GPIO</code> library for Raspberry Pi and communicates with external devices using SPI.</p>

<pre>
import spidev
import time
import RPi.GPIO as GPIO
import pio
import Ports

GPIO.setmode(GPIO.BOARD)

# Code for initializing GPIO pins, SPI, and sensors
# PIR sensor, gas sensor, LCD display, temperature sensor, and fan/motor control.
# The code handles automation based on sensor inputs.
</pre>

<h3>showlog.py</h3>
<p>The <code>showlog.py</code> script reads and displays incoming contents of the server log. This is useful for monitoring activities like sensor inputs or appliance status in real time.</p>

<pre>
import os, time, sys, select
pipe_name = '/tmp/server.log'

def readlog():
    pipein = open(pipe_name, 'r')
    while not heardEnter():
        line = pipein.readline()
        if line != "":
           print(line[:-1])
        if line.startswith("***ENDS"):
           break
    pipein.close()

def heardEnter():
    i,o,e = select.select([sys.stdin],[],[],0)
    for s in i:
        if s == sys.stdin:
            input = sys.stdin.readline()
            return True
    return False

if os.path.exists(pipe_name):
   os.remove(pipe_name)
os.mkfifo(pipe_name)
readlog()
os.remove(pipe_name)
</pre>

<h2>Prerequisites</h2>
<ul>
  <li>Python 3.x</li>
  <li>Raspberry Pi (with RPi.GPIO and spidev libraries)</li>
  <li>SPI-enabled devices (e.g., LCD, sensors)</li>
</ul>

<h2>Installation</h2>
<p>To install the required dependencies, run the following command:</p>

<pre>
sudo apt-get install python3-rpi.gpio python3-spidev
</pre>

<p>Ensure the following libraries are installed:</p>
<ul>
  <li>PIR sensor library</li>
  <li>Gas sensor library</li>
</ul>

<h2>Usage</h2>
<p>Run the <code>main.py</code> script to start the automation system:</p>

<pre>
python3 main.py
</pre>

<p>To view the server log in real-time, run the <code>showlog.py</code> script:</p>

<pre>
python3 showlog.py
</pre>

<h2>License</h2>
<p>This project is licensed under the MIT License.</p>

</body>
</html>
