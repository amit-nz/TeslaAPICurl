# TeslaAPICurl
Using cURL to interact with Tesla's API to get info about a vehicle.

Useful Resources: 
1. https://medium.com/@jhuang5132/a-beginners-guide-to-the-unofficial-tesla-api-a5b3edfe1467
2. https://www.teslaapi.io/

Don't trust various websites/apps to generate your API key? Do it yourself with curl.

# Generate Access Key
Update values **-F "email=john@smith.com"** and **-F "password=1234"** with your my.teslamotors.com credentials

```
curl -X POST -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" -F "grant_type=password" -F "client_id=81527cff06843c8634fdc09e8ac0abefb46ac849f38fe1e431c2ef2106796384" -F "client_secret=c7257eb71a564034f9419ee651c7d0e5f7aa6bfbd18bafb5c5c033b093bb2fa3" -F "email=john@smith.com" -F "password=1234" "https://owner-api.teslamotors.com/oauth/token"
```


This will generate an access token like below. The relevant part is the alphanumeric string after `access_token":`

```
{"access_token":"1234","token_type":"bearer","expires_in":3888000,"refresh_token":"4568","created_at":1573431375}% 
```

# Get List of Vehicles
```
curl --request GET --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles'
```


# Get info re vehicle 

If you don't get a valid response, then it is likely that the car is in a deep sleep state. These commands will not automatically wake the car. To wake the car, see "Wake" below

(replace NNNNNNNN with vehicle ID from prev call) 
```
curl --request GET --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles/NNNNNNNNNNNNNNN/vehicle_data'
```

# Wake Car
curl --request POST --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles/NNNNNNNNNNNNNNN/wake_up`

# Honk Horn
```
curl --request POST --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles/NNNNNNNNNNNNNNN/command/honk_horn'
```

# Get charge state
Information on the state of charge in the battery and its various settings.

```
curl --request GET --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles/NNNNNNNNNNNNNNN/data_request/charge_state'
```

# Get drive state (current speed, heading, location etc)
Returns the driving and position state of the vehicle.

```
curl --request GET --header 'Authorization: Bearer 1234' 'https://owner-api.teslamotors.com/api/1/vehicles/NNNNNNNNNNNNNNN/data_request/drive_state'
```
