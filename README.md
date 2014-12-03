API Documentation
=================

A limited set of API end points have been exposed for integration.  We are
looking for new and more comprehensive ways to integrate Resy into your
application so <a href="mailto:api@resy.com">email us</a> if you need any help
or need more functionality from our API.

HTTP Response Codes
-------------------

### 400

    A bad request was made because of a data validation error.  Either a
    required parameter is missing or failed a custom software validation
    check.

    {
        "message": "[text]"
    }

    or

    {
        "status": 400,
        "message": Invalid data received.",
        "data": {
            "[field name 1]": "[validation failure 1]",
            "[field name 2]": "[validation failure 2]",
            ...
            "[field name N]": "[validation failure N]"
        }
    }

### 401

    The user could not be authenticated.

    {
        "status": 401,
        "message": "Unauthorized"
    }

### 402

    The user has not provided payment methods.

    {
        "status": 402,
        "message": "Payment Required"
    }

### 403

    The request is forbidden most likely because something has gone wrong.

    {
        "status": 403,
        "message": "[message]"
    }

### 404

    The object being requested could not be found.

    {
        "status": 404,
        "message": "Not Found"
    }

### 409

    The user's account does not exist or has been deactivated.  The user's
    Resy data should be wiped from the requesting device and the user should be
    logged out.

    {
        "status": 409,
        "message": "Conflict"
    }

Standard Parameters
-------------------

### auth_token

    The token representing the user's credentials.  Depending on the end
    point, this parameter may or may not be required.  This parameter
    encompasses both a registered user's and a guest user's credentials.

### day

    A day value represented as YYYY-mm-dd.

### resy_token

    The token that encapsulates all of the data required to identify a specific
    reservation.

### time_slot

    A time value represented as HH24:ii:00.

### x

    The longitude of the requestor's location.

### y

    The latitude of the requestor's location.

End Points
----------

# /2/reservation/find

### GET

    Gets all of the available reservations based on the user's criteria.

    +-------------------------------------------------------------------------+
    | Parameter Name    | Req (Y/N) | Details                                 |
    |-------------------|-----------|-----------------------------------------|
    | x                 |     Y     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | y                 |     Y     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | day               |     Y     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | num_seats         |     Y     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | auth_token        |     N     | If a request is being executed on       |
    |                   |           | behalf of an existing user, a value     |
    |                   |           | should be provided.                     |
    |-------------------|-----------|-----------------------------------------|
    | time_slot         |     N     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | venue_id          |     N     |                                         |
    |-------------------|-----------|-----------------------------------------|
    | location_id       |     N     |                                         |
    +-------------------------------------------------------------------------+

    +-------------------------------------------------------------------------+
    | Response Code | Details                                                 |
    |---------------|---------------------------------------------------------|
    | 200           |                                                         |
    |---------------|---------------------------------------------------------|
    | 400           |                                                         |
    |---------------|---------------------------------------------------------|
    | 401           |                                                         |
    +-------------------------------------------------------------------------+

    +-------------------------------------------------------------------------+
    | Response                                                                |
    +-------------------------------------------------------------------------+
    | {                                                                       |
    |   "guest_token": "4DINNDl4T_y7DN3WzUbclOV4ycCnKIUEDpggyZPwIQ70Wdqo...", |
    |   "location": {                                                         |
    |       "display": "nyc",                                                 |
    |       "distance": 1.3034779534716734,                                   |
    |       "id": "ny",                                                       |
    |       "is_active": 1,                                                   |
    |       "latitude": 40.7643304,                                           |
    |       "longitude": -73.9772046,                                         |
    |       "radius": 15                                                      |
    |   },                                                                    |
    |   "results": [                                                          |
    |       {                                                                 |
    |           "auction": {                                                  |
    |               "bid_increase_amount": null,                              |
    |               "buy_now_price": null,                                    |
    |               "max_bid": null                                           |
    |           },                                                            |
    |           "distance": 0.005240127936334476,                             |
    |           "lock_token": "qW2B8sxTOOIHRJMEio7cVyT38_3tJR0p0DerWknpN...", |
    |           "specs": {                                                    |
    |               "config_type": "Communal",                                |
    |               "config_type_color": "5DA4D0",                            |
    |               "config_type_font_color": "FFFFFF",                       |
    |               "config_type_id": 2,                                      |
    |               "day": "2014-08-17",                                      |
    |               "disable_cancellations": 0,                               |
    |               "disable_changes": 0,                                     |
    |               "disable_comps": 0,                                       |
    |               "features": [                                             |
    |                   "Gotham Bar & Grill donates 100% of proceeds from..." |
    |               ],                                                        |
    |               "menu_items": [                                           |
    |                   "Aged Clawhammer Farms Ribeye",                       |
    |                   "Chickpea & Quinoa Cake"                              |
    |               ],                                                        |
    |               "num_seats": 2,                                           |
    |               "price_per_seat": "50.00",                                |
    |               "purchase_type_id": 2,                                    |
    |               "service_type_id": 2,                                     |
    |               "table_config_id": 1,                                     |
    |               "table_ids": [                                            |
    |                   "1"                                                   |
    |               ],                                                        |
    |               "time_slot": "19:30:00",                                  |
    |               "when": "2014-08-17 23:30:00"                             |
    |           },                                                            |
    |           "ticketing": {                                                |
    |               "config_type": "event",                                   |
    |               "config_type_id": 1,                                      |
    |               "max_seats": 100,                                         |
    |               "num_seats_booked": 23                                    |
    |           },                                                            |
    |           "travel_time": {                                              |
    |               "driving": 1,                                             |
    |               "walking": 1                                              |
    |           },                                                            |
    |           "venue": {                                                    |
    |               "about": "Because Mike got to create this test venue...", |
    |               "address_1": "315 Park Avenue",                           |
    |               "address_2": null,                                        |
    |               "city": "New York",                                       |
    |               "cross_street_1": "23rd Street",                          |
    |               "cross_street_2": "24th Street",                          |
    |               "id": 1,                                                  |
    |               "images": [                                               |
    |                   "https://s3.amazonaws.com/resy.com/images/venues/..." |
    |               ],                                                        |
    |               "latitude": 40.745812,                                    |
    |               "longitude": -73.9822091,                                 |
    |               "max_party_size": 10,                                     |
    |               "menu_items": [                                           |
    |                   "Aged Clawhammer Farms Ribeye",                       |
    |                   "Chickpea & Quinoa Cake"                              |
    |               ],                                                        |
    |               "name": "Test Venue",                                     |
    |               "phone_number": "7184734811",                             |
    |               "postal_code": "10016",                                   |
    |               "price_range_id": 4,                                      |
    |               "rater": "NY Times",                                      |
    |               "rater_image": "https://s3.amazonaws.com/resy.com/im...", |
    |               "rater_star_scale": 5,                                    |
    |               "rater_star_score": 4.75,                                 |
    |               "state": "NY",                                            |
    |               "tagline": "Yummy food!",                                 |
    |               "type": "Vegan Joint",                                    |
    |               "url": "http://resy.com/"                                 |
    |           }                                                             |
    |       }                                                                 |
    |   ]                                                                     |
    | }                                                                       |
    +-------------------------------------------------------------------------+

    +-------------------------------------------------------------------------+
    | Notes                                                                   |
    +-------------------------------------------------------------------------+
    | o For the sake of logging and tracking, if an auth_token is available   |
    |   it should be sent with a request even though it is not required.      |
    |                                                                         |
    | o "guest_token" will only be present when an auth_token is not pro-     |
    |   vided.  The guest_token should be stored and submitted with subseq-   |
    |   uent requests as the auth_token.                                      |
    |                                                                         |
    | o "lock_token" is deprecated and should never be used.                  |
    +-------------------------------------------------------------------------+

# /2/venues

### GET

    Gets a list of venues by location ID.

    +-------------------------------------------------------------------------+
    | Parameter Name    | Req (Y/N) | Details                                 |
    |-------------------|-----------|-----------------------------------------|
    | location_id       |     Y     |                                         |
    +-------------------------------------------------------------------------+

    +-------------------------------------------------------------------------+
    | Response Code | Details                                                 |
    |---------------|---------------------------------------------------------|
    | 200           |                                                         |
    |---------------|---------------------------------------------------------|
    | 404           |                                                         |
    +-------------------------------------------------------------------------+

    +-------------------------------------------------------------------------+
    | Response                                                                |
    +-------------------------------------------------------------------------+
    | {                                                                       |
    |   [                                                                     |
    |       "id": 1,                                                          |
    |       "location": {                                                     |
    |           "address_1": "315 Park Avenue South",                         |
    |           "address_2": "",                                              |
    |           "city": "New York",                                           |
    |           "latitude": 40.745812,                                        |
    |           "longitude": -73.9822091,                                     |
    |           "neighborhood": "Flatiron",                                   |
    |           "postal_code": "10010",                                       |
    |           "state": "ny"                                                 |
    |       },                                                                |
    |       "name": "Test Venue",                                             |
    |       "phone_number": "2125551212",                                     |
    |       "price_range": 3,                                                 |
    |       "rating": 4.9,                                                    |
    |       "tagline": "Yummy food!",                                         |
    |       "type": "Vegan Joint"                                             |
    |   ]                                                                     |
    | }                                                                       |
    +-------------------------------------------------------------------------+
