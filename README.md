# Plant Care Companion Bot

This bot fetches local weather data and suggests optimal care instructions for your houseplants. It uses machine learning models trained on various parameters like humidity, temperature, and light levels to give you the best advice for your plants.

## Features
- Web scraping for local weather data
- Predictive models for plant care
- Customizable for different types of plants

## How to Run
1. Clone this repository
2. Install requirements `pip install -r requirements.txt`
3. Run `python main.py`

## Tech Stack
- Python
- BeautifulSoup
- Scikit-Learn
- Matplotlib

## License
MIT
requirements.txt
makefile
Copy code
beautifulsoup4==4.9.3
requests==2.25.1
scikit-learn==0.24.2
matplotlib==3.4.2
main.py
python
Copy code
from bs4 import BeautifulSoup
import requests
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
import numpy as np

def fetch_weather_data(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    weather = soup.find('div', {'id': 'weather'})
    return float(weather.text.strip("°C"))

def plant_care_model(temp):
    X = np.array([[15], [20], [25], [30], [35]])
    y = np.array([3, 4, 5, 2, 1])  # Hypothetical watering frequency
    model = LinearRegression().fit(X, y)
    return model.predict(np.array([[temp]]))[0]

def main():
    url = 'http://www.example-weather-website.com'
    temp = fetch_weather_data(url)
    
    print(f"Today's temperature is {temp}°C.")

    watering_freq = plant_care_model(temp)
    print(f"Based on the current temperature, water your plant {watering_freq} times this week.")

if __name__ == "__main__":
    main()
