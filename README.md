# Plant Monitoring System

## Introduction

Our project, the Plant Monitoring System, is a smart IoT solution that helps take care of plants by monitoring their environment. It collects data like soil moisture using sensors and sends it to the cloud, where we can visualize it in real time through a user-friendly dashboard.

Let's see how this project was implemented step by step.

## Benifits
1. **Real-Time Monitoring:** Alerts for dry or wet soil conditions.
2. **Water Conservation:** Reduces overwatering or underwatering and promotes efficient use of resources.
3. **Ease of Use:** Accessible through a user-friendly interface.
4. **Scalability:** Can be expanded to monitor additional environmental factors like temperature and humidity.
5. **24/7 Uptime:** Services managed by PM2 and Nginx ensure continuous operation.



## 1. Resource Alloction

### 1.1. Resources ###

1. Hardware Resources

Raspberry Pi Pico W: Acts as the IoT device for data collection and transmission.

Soil Moisture Sensor: Collects environmental data.

2. Cloud Resources

Ubuntu 24.04 VPS: Hosts backend services, database, and the web server.

Node.js 23: Backend runtime for data processing.

InfluxDB v2.7.10: Time-series database for storing IoT data.

Nginx v1.24.0: Handles HTTP traffic and serves the dashboard.

### 1.2. Cost ###

1. Raspberry Pi Pico W : 52 Euro
2. Moisture Sensor : 10 Euro
3. All software (MicroPython, Node.js, InfluxDB, React, Nginx) is open-source and free.

Total Project cost around 62 Euro.

## 2. Embeded Device Setup
The Raspberry Pi Pico W is programmed with MicroPython to collect soil moisture data from a connected sensor.

The soil moisture sensor is connected to the ADC pin (26 pin) of the Pico W, while power and ground are wired to the 3.3V and GND pins, respectively.

A MicroPython script on the device reads the soil moisture levels and sends them to a backend server using HTTP POST requests.

## 3. Cloud Service(VPS) ##

Before the project, we installed Cloud Service(VPS) and loaded with the latest versions of the softwares for the IoT Pipeline.

1. Backend runtime e.g., NodeJS 23
2. Database e.g., InfluxDB v2.7.10
3. HTTP Web server e.g., Nginx v1.24.0
4. Other services

## 4. Cloud Service Configuration

1. Connectivity

Firewall Configuration: Public ports 80 (HTTP) and 443 (HTTPS) are open.

Routing: Traffic is correctly routed to the backend server.

2. Database Setup

InfluxDB is configured with appropriate retention policies and security.

Data can be queried by backend and visualization services seamlessly.

3. Backend Configuration

Node.js is configured to listen for data from the embedded device.

Incoming data is logged, sanitized, and written to InfluxDB.

## 5. Backend Development ##
**General Data Flow:**

Sensor → Backend → Database → Frontend

**Process Flow:**
1. Receive soil moisture data from the Raspberry Pi Pico W.
2. Store the data in a time-series database (InfluxDB).
3. Provide APIs for the frontend to display real-time and historical data.
4. Trigger alerts for abnormal moisture levels.

**Decide Key Tools and Technologies:**
1. Node.js (Backend server runtime).
2. Express.js (Framework for handling HTTP requests).
3. InfluxDB (Database for time-series data).
4. Nginx (For reverse proxy and static file hosting).
5. Docker (Optional for deployment and scaling).
   
**Backend Development Process**

Step 1: Set Up the Project

1. Install Node.js and create a project folder.
2. Install required dependencies.
3. Set up the file structure.

Step 2: Use Express.js to set up a basic server

step 3: Set up InfluxDB to store the soil moisture data
1. Install InfluxDB on our server.
2. Create a bucket and an organization.

Step 4: Add APIs for Frontend


The backend acts as a bridge between InfluxDB and the frontend dashboard.
We developed APIs using Node.js and Express.js that allow the frontend to fetch both real-time and historical data stored in InfluxDB.
This ensures that the user interface can visualize the data efficiently, using graphs and dashboards.

## 6. User Interface ##
A web-based dashboard provides real-time insights into the soil moisture levels. It is built using:

React: Ensures responsiveness and interactivity.

Chart.js: Displays dynamic graphs for real-time and historical data visualization.

Tailwind CSS: Enhances the UI with modern and intuitive design.

In our UI displays:

1. Real-Time Soil Moisture with Percentage.
2. Historical data for the past hour.
3. Alerts for low or high moisture levels.

The soil moisture level can be displayed as a percentage or visualized using a graph in the user interface. To make it intuitive, color-coded indicators are used: red for low moisture levels, green for medium levels, and blue for high levels.
