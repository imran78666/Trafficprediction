```python
import requests
import joblib
import smtplib
from email.mime.text import MIMEText

# ---------------- Step 1: Get Location Coordinates ----------------
def get_lat_lon(area, city):
    url = f"https://geocode.maps.co/search?q={area},{city}&api_key=67ab21aa63f4d508193346tcs5f87a3"
    response = requests.get(url).json()
    
    if response and isinstance(response, list):
        return float(response[0]["lat"]), float(response[0]["lon"])
    else:
        print("❌ Failed to get location data.")
        return None, None

# ---------------- Step 2: Fetch Live Traffic Data ----------------
def get_live_traffic_data(lat, lon):
    return 0.5  # Replace with real API if needed

# ---------------- Step 3: Predict Accident Risk ----------------
def predict_accident_risk(features):
    model = joblib.load("random_forest.pkl")  # Load trained model
    prediction = model.predict([features])
    return "High Risk" if prediction[0] == 1 else "Low Risk"

# ---------------- Step 4: Send Email Alerts ----------------
def send_email_alert(email, area, city):
    sender_email = "munnaimran50@gmail.com"
    sender_password = "bssd xxst kfxg daht"
      # Use App Password for security
    subject = "🚨 Accident Risk Alert!"
    body = f"⚠️ High accident risk detected at {area}, {city}. Drive safely! 🚗💨"
    
    msg = MIMEText(body)
    msg["Subject"] = subject
    msg["From"] = sender_email
    msg["To"] = email

    try:
        server = smtplib.SMTP("smtp.gmail.com", 587)
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, email, msg.as_string())
        server.quit()
        print("✅ Email alert sent!")
    except Exception as e:
        print(f"❌ Email sending failed: {e}")

# ---------------- Step 5: Main Function to Check Accident Risk ----------------
def check_accident_risk():
    area = input("Enter area name: ")
    city = input("Enter city name: ")
    email = input("Enter your email: ")
    
    lat, lon = get_lat_lon(area, city)
    if lat and lon:
        traffic_data = get_live_traffic_data(lat, lon)
        features = [18, 3, 2, traffic_data, 1]  # Example input features
        risk = predict_accident_risk(features)
        
        print(f"🚦 Accident Risk: {risk}")
        
        if risk == "High Risk":
            send_email_alert(email, area, city)
    else:
        print("❌ Could not fetch location data.")

# ---------------- Step 6: Run the Function ----------------
check_accident_risk()

```

    Enter area name:  jagannaickpur
    Enter city name:  kakinada
    Enter your email:  munnaimran50@gmail.com
    

    🚦 Accident Risk: High Risk
    ✅ Email alert sent!
    


```python

```
