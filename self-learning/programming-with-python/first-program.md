# Our First Program

Most beginner's tutorials on Python - or any programming language for that matter - start with the so called Hello World example. All the program does is print the two words "Hello World" to a console. That's pretty boring and does not really entice anyone to continue.

Not this tutorial! The code below is our first program. For a first program, it looks already quite complicated. And that's true - but it also does something useful: It tells us the current temperature in our city and gives us advice on whether we should go out or not \(and whether to pack an umbrella\).

{% code title="first\_program.py" %}
```python
import requests
import json

# Thanks to OpenWeather Map - https://openweathermap.org/
response = requests.get('https://api.openweathermap.org/data/2.5/weather?q=Osnabrück&units=metric&appid=259f0b9a44cfc5cd08793bab9d6e076e')

weather = json.loads(response.content)
current_temperature = weather.get('main').get('temp')
weather_code = str(weather.get('weather')[0].get('id'))

print('The current temperature in Osnabrück is %s °C!' % (current_temperature))

# Weahter codes see here: https://openweathermap.org/weather-conditions

if weather_code.startswith('2'):
    print("There is a thunderstorm going on, stay in!")
elif weather_code.startswith('3'):
    print("It's drizzling - check if you need an umbrella!")
elif weather_code.startswith('5'):
    print("It's raining, pack an umbrella!")
elif weather_code.startswith('6'):
    print("It's freaking snowing outside!")
elif weather_code == '800':
    print("Clear sky and sun - have fun!")
elif weather_code.startswith('8'):
    print("Dry, but cloudy!")
```
{% endcode %}

