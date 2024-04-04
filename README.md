import requests
import sys

def get_weather(api_key, city):
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        temp = data['main']['temp']
        weather = data['weather'][0]['description']
        print(f"Weather in {city}: {weather}, Temperature: {temp}°C")
    else:
        print("Error fetching weather data. Please check the city name or your API key.")

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: python weathercli.py [API_KEY] [CITY_NAME]")
        sys.exit(1)
    api_key = sys.argv[1]
    city = sys.argv[2]
    get_weather(api_key, city)
