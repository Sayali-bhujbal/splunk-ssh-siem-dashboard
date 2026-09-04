# Splunk-siem-dashboard
## SIEM dashboard built in Splunk to monitor SSH login activity

A custom-built Splunk SIEM dashboard designed to monitor, visualize, and analyze SSH login activity, detect failed login attempts, and identify suspicious or unauthorized access patterns in real time. Developed using Splunk's Search Processing Language (SPL) to query, correlate, and present security log data through interactive dashboard panels.
## 🛠️ Features
- 📊 Real-Time Monitoring — Continuously tracks and displays security events as they happen.
- 🔍 Threat Detection — Identifies suspicious activity like failed logins or unusual traffic.
- 📁 Centralized Log Collection — Gathers logs from multiple sources into one dashboard.
- 🚨 Alerting — Sends real-time alerts when a security threat is detected.
- 📈 Data Visualization — Displays logs and events through charts, graphs, and tables for easy analysis.

# Objective

## Lab Set up
- Task0: Splunk main interface
- Splunk Dashboard creation
- Setting up Time Range
- Add Time Range Button
- Click on Add Input
- Select Time and click on pencil icon
- Set Label to Time Range and Token time_range
- Again Add Input
- Select Submit
- Note: For all future panel, set the time to time_range for consistency.
  
<img width="1917" height="1020" alt="Screenshot 2026-09-03 151437" src="https://github.com/user-attachments/assets/f8bf565b-eb83-42cf-a086-4fdcb5f38791" />

<img width="1917" height="872" alt="Screenshot 2026-09-03 152020" src="https://github.com/user-attachments/assets/2d84d038-9f29-49ff-89d2-781ef8621f96" />

<img width="1917" height="877" alt="Screenshot 2026-09-03 152913" src="https://github.com/user-attachments/assets/dc6f8cf4-6bb4-4a26-88bc-f2cf4837ea04" />

<img width="1917" height="872" alt="Screenshot 2026-09-03 153420" src="https://github.com/user-attachments/assets/05de2add-d861-4c81-93b0-59afb838fa17" />

<img width="1917" height="865" alt="Screenshot 2026-09-03 153453" src="https://github.com/user-attachments/assets/ce47bdc9-913c-4fee-8178-d1ea65541722" />

<img width="1917" height="862" alt="Screenshot 2026-09-03 153615" src="https://github.com/user-attachments/assets/67e5cf06-1d1d-4ecb-98e5-ac658dac8a13" />

# Task1: Authentication Overview Panels
## Goal: Give a quick summary of SSH activity.
### 1. Total SSH Events
- Click on Add Panel

- Under New, choose Single Value

- Use Shared Time Picker time_range

- Set Content Title to "Total SSH Events"

- Enter the Search String as below

  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"|stats count as "Total SSH Events"

#### Lab image  
<img width="1917" height="870" alt="Screenshot 2026-09-03 153905" src="https://github.com/user-attachments/assets/aa4ffb33-5569-491a-b3dc-a0ed556cdb51" />

### 2.Successful Logins
- Click on Add Panel

- Under New, choose Single Value

- Use Shared Time Picker time_range

- Set Content Title to "Successful Logins"

- Enter the Search String as below:

  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Successful SSH Login"|stats count as "Successful  Login"

#### Lab image 
<img width="1917" height="871" alt="Screenshot 2026-09-03 154250" src="https://github.com/user-attachments/assets/938454ba-0c20-4d71-9223-6d4400fac002" />

### 3. Failed Logins
- Click on Add Panel
  
- Under New, choose Single Value
  
- Use Shared Time Picker time_range
  
- Set Content Title to "Failed Logins"
  
- Enter the Search String as below:
  
  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Failed SSH Login"|stats count as "Failed Login"

  #### Lab image
  <img width="1917" height="875" alt="Screenshot 2026-09-03 154408" src="https://github.com/user-attachments/assets/6cfc8ffc-df9a-4dd3-bb7a-0b24cc9adf07" />
  
### 4. Connection without Authentication
- Click on Add Panel

- Under New, choose Single Value

- Use Shared Time Picker time_range

- Set Content Title to "Invalid User Attempts"

- Enter the Search String as below:

  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Connection without Authentication"|stats count as "Connection without Authentication"

  #### Lab image
  <img width="1917" height="872" alt="Screenshot 2026-09-03 155149" src="https://github.com/user-attachments/assets/c4135db8-152b-4e50-b3d8-fc383c49a644" />

# Task2: Login Activity Trends
## Goal: Visualize login behaviour over time and detect spikes.
# 1. Failed Logins by username
- Click on Add Panel

- Under New, choose Bar Chart

- Use Shared Time Picker time_range

- Set Content Title to "Failed Logins by username"

- Enter the Search String as below:
  
  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Failed SSH Login"|top username

 #### Lab image
 <img width="1917" height="871" alt="Screenshot 2026-09-03 155640" src="https://github.com/user-attachments/assets/f96c60cb-9501-47c6-96d0-dcb9cefdb373" />

# 2. Possible Brute Force
- Click on Add Panel

- Under New, choose Statistics Table

- Use Shared Time Picker time_range

- Set Content Title to Possible Brute Force by IP Address

- Enter the Search String as below:
  
  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Multiple Failed Authentication Attempts"|top id.orig_h
  
  #### Lab image
  <img width="1917" height="875" alt="Screenshot 2026-09-04 081105" src="https://github.com/user-attachments/assets/245ac207-7d17-444c-bf68-ca498814d67c" />

# Task3: Visualizing Brute Force attack in geo-location
## Goal: Visualizing Brute Force attack with geo-location
- Click on Add Panel

- Under New, choose Choropleth Map

- Use Shared Time Picker time_range

- Set Content Title to Brute Force attack with geo-location

- Enter the Search String as below:
  
  source="ssh_logs_new.json" host="LAPTOP-5DCNBVQ7" sourcetype="_json"event_type="Multiple Failed Authentication Attempts"|table id.orig_h|iplocation id.orig_h| stats   count by Country|geom geo_countries featureIdfield="Country"

  #### Lab image
  <img width="1917" height="863" alt="Screenshot 2026-09-03 160513" src="https://github.com/user-attachments/assets/f1ece44d-e797-4f66-93e5-5468d833b034" />

## Overview of all Dashboard Image
<img width="1917" height="927" alt="Screenshot 2026-09-03 162811" src="https://github.com/user-attachments/assets/ccdbb767-e316-403b-8f23-c96350abdf63" />

  



  



  

