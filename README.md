# WhatsApp Weather & AQI Bot

A simple Python bot that fetches current weather and Air Quality Index (AQI) for a city and sends the report to a WhatsApp number using `pywhatkit` and public APIs for weather and air quality.[1][2][3]

***

## Features

- Get current temperature, feels-like temperature, humidity, and weather description using the OpenWeather API.[2]
- Get real-time AQI for any city using the World Air Quality Index (WAQI) API.[3]
- Send the combined Weather + AQI report to any WhatsApp number via `pywhatkit`.[1]
- Choose between instant send or scheduling the message for a specific time.[4]

***

## Prerequisites

- Python 3.8+ installed on your system.  
- A web browser (e.g. Chrome) with WhatsApp Web already logged in.[5]
- OpenWeather API key (free account).[2]
- WAQI API token (free token).[3]

***

## Installation

1. Clone or download this repository:

```bash
git clone <YOUR_REPO_URL>
cd <YOUR_REPO_FOLDER>
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

Example `requirements.txt`:

```txt
requests
pywhatkit
```


***

## Configuration

Open `main.py` and set your API keys:

```python
OPENWEATHER_API_KEY = "YOUR_OPENWEATHER_KEY"
WAQI_TOKEN = "YOUR_WAQI_TOKEN"
```

- Get your OpenWeather API key from your account dashboard after signing up.[2]
- Get your WAQI token from the AQICN API token page.[3]

Make sure your phone number is entered with the country code when prompted, for example: `+91XXXXXXXXXX`.

***

## Usage

Run the bot:

```bash
python main.py
```

The script will:

1. Ask for the city name (e.g. `Delhi`).  
2. Ask for the WhatsApp number with country code (e.g. `+91XXXXXXXXXX`).  
3. Build a Weather + AQI summary message.  
4. Ask if you want to:
   - Send **now** (instant), or  
   - **Schedule** the message.

If you choose **schedule**, you will be asked for:

- Hour (24h) – e.g. `14` for 2 PM.  
- Minute – e.g. `30` for :30.  

A browser window will open with WhatsApp Web and the message will be sent automatically at the chosen time or instantly, depending on your selection.[4][5]

***

## How It Works

- Weather data is fetched from the OpenWeather **Current Weather Data** endpoint using the city name and your API key, with `units=metric` to get values in Celsius.[2]
- AQI data is fetched from the WAQI city feed endpoint (`/feed/{city}/?token=YOUR_WAQI_TOKEN`) and the numeric AQI value is mapped to a simple category (Good, Moderate, Poor, etc.).[3]
- The script constructs a formatted text message containing:
  - City  
  - Temperature + feels-like  
  - Weather description  
  - Humidity  
  - AQI value and category  
- The message is sent using `pywhatkit.sendwhatmsg_instantly` for instant send or `pywhatkit.sendwhatmsg` for scheduled send.[4][1]

***

## Notes

- Keep your system powered on, browser openable, and internet connected until the message is sent.[5]
- Make sure WhatsApp Web is logged in on the same browser that opens when the script runs.[1]
- If APIs return errors (invalid city, rate limit, wrong key/token), the script will print an error message instead of sending.[2][3]

[1](https://pypi.org/project/pywhatkit/)
[2](https://openweathermap.org/api)
[3](https://aqicn.org/api/)
[4](https://stackoverflow.com/questions/73279324/send-message-using-pywhatkit-instantly)
[5](https://github.com/Ankit404butfound/PyWhatKit/wiki/Sending-WhatsApp-Messages)
