# Accident Risk Prediction System

## Overview
This Python-based project predicts accident risk for a given location based on live traffic data and predefined features. If a high risk is detected, the system sends an email alert to the user.

## Features
- Fetches latitude and longitude of a location using a geolocation API.
- Simulates live traffic data retrieval.
- Predicts accident risk using a pre-trained Random Forest model.
- Sends an email alert in case of high risk.

## Requirements
Ensure you have the following installed:
- Python 3.x
- Required libraries:
  ```bash
  pip install requests joblib smtplib
  ```

## Setup & Usage
1. Clone this repository or copy the script.
2. Replace `random_forest.pkl` with your trained model file.
3. Update the `api_key` in `get_lat_lon()` with a valid geolocation API key.
4. Use an App Password instead of a raw password in `send_email_alert()` for better security.
5. Run the script:
   ```bash
   python script_name.py
   ```
6. Enter the area, city, and email when prompted.
7. If a high accident risk is detected, an email alert is sent.

## Code Breakdown
- **get_lat_lon(area, city)**: Fetches latitude and longitude using an external API.
- **get_live_traffic_data(lat, lon)**: Simulates traffic data retrieval (replace with a real API if needed).
- **predict_accident_risk(features)**: Loads a trained model and predicts accident risk.
- **send_email_alert(email, area, city)**: Sends an email alert if a high risk is detected.
- **check_accident_risk()**: Main function that integrates all steps and prompts user input.

## Security Considerations
- Use environment variables for sensitive information like email credentials.
- Never hardcode passwords; use an App Password for Gmail.
- Ensure the API key used for geolocation is valid and secure.

## Future Enhancements
- Integrate real-time traffic data from Google Maps API.
- Improve feature extraction for better prediction accuracy.
- Implement SMS alerts using Twilio.

## License
This project is for educational purposes. Modify and use it at your own risk!

