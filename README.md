*If you have a question, please just open a dialog in the “issue” section so others can benefit from the discussion.*

*This project is interested in collaborating with the integration of the Zigbee2mqtt NodeJS API* https://www.npmjs.com/package/zigbee2mqtt 

### Preamble:
Even if you don't require Home Assistant, Telegram, or ESPHome integration, this framework provides essential features such as UDP communications, a debugging website, timer functions, logging, notifications, a service installer, and straightforward management of both volatile and non-volatile memory storage.

### General Concept of ThingWerks:
ThingWerks is an ultra-lightweight IoT Automation Framework for NodeJS, intended to enable users to swiftly create automation scripts in NodeJS. Tailored for both industrial and home automation projects, its primary goal is to expedite the setup of a basic automation system.

Ready made industrial TW-Client automations will be included here in this repo such as PumperPro

### Design Principals:
TW-Core maintains all of the communication, management and system functions. The TW-Client contains just the bare minimum code to communicate with the Core and is the intended location to put your automation(s) code. It has been designed this way to increase reliability, simplicity and streamline the deployment of future enhancements. 

### Relationship with Home Assistant:
This framework utilizes Home Assistant's robust GUI, smartphone app, and monitoring capabilities for NodeJS automations, offering a more reliable, flexible, and responsive approach than relying on Home Assistant for complex tasks. Coding basic logic in JavaScript is argued to be simpler than using the GUI or YAML.

While Home Assistant excels in certain scenarios, it is unsuitable for industrial applications, where malfunctions can cause costly equipment damage. Managing data within Home Assistant is challenging, with slow responsiveness to inputs and significant lag. Despite these challenges, Home Assistant serves well as a monitoring and control mechanism within the framework.

In more complex environments with multiple sensors and outputs, Home Assistant falls short. NodeJS proves more suitable, handling intricacies with reliability and efficiency.

### Compactness and Resource Efficiency (TW together with HA Core):

The TW IoT with Home Assistant (HA) solution is highly compact and resource-efficient, especially with Home Assistant Core, which operates stably with just 500MB of RAM—unlike Home Assistant Supervised. During testing, Home Assistant Supervised consistently crashed with 1GB of RAM. The ESP Home web interface easily installs alongside HA Core, creating an efficient platform for modest IoT devices with 1GB of RAM.

A key point is the remarkable responsiveness of the HA Core API, averaging 2-5ms with no timeouts. In contrast, Home Assistant Supervised can exhibit latency exceeding 100ms, occasionally becoming completely unreachable or crashing, likely due to resource-intensive background updates. Thus, using Home Assistant Supervised for reliable, time-critical operations is strongly advised against.
It's worth mentioning that the TW IoT with Home Assistant (HA) solution is highly compact and resource-efficient, particularly when running Home Assistant Core. A mere 500MB of RAM is sufficient for stable operation—an aspect not applicable to Home Assistant Supervised. During testing, while executing all automations, Home Assistant Supervised consistently crashed with just 1GB of RAM. The ESP Home web interface seamlessly installs alongside HA Core, creating a tiny yet efficient platform that performs exceptionally well on modest IoT devices with a mere 1GB of RAM.

### General Features
* Has very stable power and network loss recovery 
* Functions as an ESPHome subscriber
* Supports Telegram for monitoring and remote control
* Has web-based debugger for your automation
* Has a nice and easy to use logging function
* Has SystemD service creator

### Home Assistant Features
* TW IoT completely removes all need for automation logic and control in Home Assistant
* This framework is immune to network interruptions with HA
* Has full support for HA Websocket API
* System keeps track of HA latency and availability and notifies you if something is wrong
* Adds industrial level reliability to Home Assistant
* Gives Home Assistant full support of automation with NodeJS
* Can be used as a relay agent for Home Assistant
* Can synchronize two separate Home Assistants
