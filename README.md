Bike Tracks Multi-Sensory Application
=====================================

[Learn about this example app](ARTICLE.md)

## Setup

* Download this repo (either via a `git clone` or via the zip download)

* Salesforce
    1. [Create a Developer Edition](developer.salesforce.com/signup)
    1. Deploy the metadata to Salesforce by running the following in this project's root dir:
        Mac & Linux:
            SALESFORCE_USERNAME=your@username.com SALESFORCE_PASSWORD=yourPasswordAndAccessToken ./activator force:deploy
        Windows:
            SALESFORCE_USERNAME=your@username.com SALESFORCE_PASSWORD=yourPasswordAndAccessToken activator force:deploy
    1. On Salesforce in the `Rental Bike` tab, create a new example Rental Bike and keep track of it's ID for later use
    1. [Create a new Connected App](https://login.salesforce.com/app/mgmt/forceconnectedapps/forceAppEdit.apexp)
           1. Check `Enable OAuth Settings`
           1. Set the `Callback URL` to `http://localhost:9000/`
           1. In `Available OAuth Scopes` select `Full access (full)` and click `Add`
           1. Save the new Connected App and keep track of the Consumer Key & Consumer Secret for later use

* Raspberry Pi
    1. Obtain a Raspberry Pi (1 or 2)
    1. [Obtain the Adafruit Ultimate GPS Breakout Sensor](https://www.adafruit.com/product/746) (requires soldering) or [Flora Wearable Ultimate GPS](https://www.adafruit.com/products/1059) (can be used with alligator clips)
    1. Follow the [setup instructions](https://learn.adafruit.com/adafruit-ultimate-gps-on-the-raspberry-pi/introduction) to get the GPS working with the Raspberry Pi
    1. Setup the tracker app on the Raspberry Pi
        1. Copy the `raspberrypi/tracker.py` file to the device
        1. In the file update the rental bike id's value with the one your created

## Local Development

1. From your project's root directory, create a new `conf/local.conf` file containing:
        salesforce.consumer.key="YOUR CONSUMER KEY"
        salesforce.consumer.secret="YOUR CONSUMER SECRET"
        salesforce.username="YOUR USERNAME"
        salesforce.password="YOUR PASSWORD AND ACCESS TOKEN"
1. Start the local server:
    Mac & Linux:
        ./activator ~run
    Windows:
        activator ~run
1. Optionally send a test location using CURL:
        curl -d "bike_rental_id=YOUR_RENTAL_BIKE_ID&lat=38.869903333&lon=-106.98946" http://localhost:9000/
1. Setup the tracker app on the Raspberry Pi
    1. Make sure the device is connected to the same network as your machine
    1. Update the web connection info in the `tracker.py` on your device by changing the `conn = ...` line to the following (replacing the IP with you machine's local IP):
            httplib.HTTPConnection("192.168.0.5", 9000)
    1. Run the tracker script:
            python tracker.py


## Deploy on Heroku

1. [![Deploy on Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)
1. Setup the tracker app on the Raspberry Pi
    1. Make sure the device is connected to the same network as your machine
    1. Update the web connection info in the `tracker.py` on your device by changing the `conn = ...` line to the following (replacing the IP with you machine's local IP):
            httplib.HTTPConnection("yournewapp.herokuapp.com")
    1. Run the tracker script:
            python tracker.py