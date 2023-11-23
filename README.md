# Python-Mini-Project

import requests 
import random

# Currency Converter
def currency_converter():
    base_currency = input("Enter the base currency: ").upper()
    target_currency = input("Enter the target currency: ").upper()
    amount = float(input(f"Enter the amount in {base_currency}: "))

    url = f"https://api.exchangerate-api.com/v4/latest/{base_currency}"
    response = requests.get(url)
    data = response.json()
    rate = data['rates'].get(target_currency)

    if rate:
        converted_amount = amount * rate
        print(f"{amount} {base_currency} is equal to {converted_amount} {target_currency}")
    else:
        print("Invalid currency codes or conversion rate not found.")

# URL Shortener
def url_shortener():
    access_token = "YOUR_BITLY_ACCESS_TOKEN"
    long_url = input("Enter the long URL to shorten: ")

    api_url = f"https://api-ssl.bitly.com/v4/shorten"
    headers = {
        "Authorization": f"Bearer {access_token}",
        "Content-Type": "application/json"
    }
    data = {
        "long_url": long_url
    }

    response = requests.post(api_url, headers=headers, json=data)
    shortened_url = response.json().get("link")

    if shortened_url:
        print(f"Shortened URL: {shortened_url}")
    else:
        print("Failed to shorten the URL.")

# Weather App
def weather_app():
    api_key = "YOUR_OPENWEATHERMAP_API_KEY"
    city = input("Enter the city: ")
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    
    response = requests.get(url)
    data = response.json()

    if data["cod"] == 200:
        weather = data["weather"][0]["description"]
        temperature = data["main"]["temp"]
        print(f"Weather in {city}: {weather}")
        print(f"Temperature: {temperature}°C")
    else:
        print("City not found or API request failed.")

# Number Guessing Game
def number_guessing_game():
    lower_limit = 1
    upper_limit = 100
    secret_number = random.randint(lower_limit, upper_limit)
    attempts = 0

    print(f"Guess the number between {lower_limit} and {upper_limit}.")

    while True:
        guess = int(input("Enter your guess: "))
        attempts += 1

        if guess < secret_number:
            print("Too low. Try again.")
        elif guess > secret_number:
            print("Too high. Try again.")
        else:
            print(f"Congratulations! You guessed the number {secret_number} in {attempts} attempts.")
            break

# Main program loop
while True:
    print("\nChoose an option:")
    print("1. Currency Converter")
    print("2. URL Shortener")
    print("3. Weather App")
    print("4. Number Guessing Game")
    print("5. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        currency_converter()
    elif choice == "2":
        url_shortener()
    elif choice == "3":
        weather_app()
    elif choice == "4":
        number_guessing_game()
    elif choice == "5":
        print("Exiting the program. Goodbye!")
        break
    else:
        print("Invalid choice. Please select a valid option.")
