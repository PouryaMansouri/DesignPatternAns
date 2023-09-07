Q 1: Singleton Pattern - Configuration

```python
class Configuration:
    __instance = None

    @staticmethod
    def get_instance():
        if Configuration.__instance is None:
            Configuration()
        return Configuration.__instance

    def __init__(self):
        if Configuration.__instance is not None:
            raise Exception("Singleton class cannot be instantiated more than once.")
        else:
            Configuration.__instance = self
        self.config_settings = {}

    def set_config_setting(self, key, value):
        self.config_settings[key] = value

    def get_config_setting(self, key):
        return self.config_settings.get(key, None)
```

Q 2: Factory Pattern - Animal Factory

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

    @abstractmethod
    def eat(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

    def eat(self):
        return "Eating bones"

class Cat(Animal):
    def speak(self):
        return "Meow!"

    def eat(self):
        return "Eating fish"

class Lion(Animal):
    def speak(self):
        return "Roar!"

    def eat(self):
        return "Eating meat"

class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()
        elif animal_type == "lion":
            return Lion()
        else:
            raise ValueError("Invalid animal type")
```

Q 3: Decorator Pattern - Authentication Decorator

```python
def authentication_decorator(func):
    def wrapper(request):
        token = request.headers.get("Authorization")
        if token == "valid_token":
            return func(request)
        else:
            return "Authentication failed"
    return wrapper

@authentication_decorator
def sample_view(request):
    return "Authenticated view"

# Sample usage
valid_request = {"headers": {"Authorization": "valid_token"}}
invalid_request = {"headers": {"Authorization": "invalid_token"}}

print(sample_view(valid_request))  # Output: Authenticated view
print(sample_view(invalid_request))  # Output: Authentication failed
```

Q 4: Observer Pattern - Weather Station

```python
class WeatherStation:
    def __init__(self):
        self.observers = []
        self.temperature = 0
        self.humidity = 0

    def register_observer(self, observer):
        self.observers.append(observer)

    def unregister_observer(self, observer):
        self.observers.remove(observer)

    def notify_observers(self):
        for observer in self.observers:
            observer.update(self.temperature, self.humidity)

    def set_measurements(self, temperature, humidity):
        self.temperature = temperature
        self.humidity = humidity
        self.notify_observers()

class TemperatureDisplay:
    def update(self, temperature, humidity):
        print(f"Temperature updated: {temperature}°C")

class HumidityDisplay:
    def update(self, temperature, humidity):
        print(f"Humidity updated: {humidity}%")

# Sample usage
weather_station = WeatherStation()

temperature_display = TemperatureDisplay()
humidity_display = HumidityDisplay()

weather_station.register_observer(temperature_display)
weather_station.register_observer(humidity_display)

weather_station.set_measurements(25, 60)
# Output:
# Temperature updated: 25°C
# Humidity updated: 60%
```
