# Lime

**Base url**: `https://web-production.lime.bike/api/rider`

## Methods

### Login

Login is in two step:

+ Request code with your phone number, you ll receive an sms
+ Send back this code

#### Request sms code

:warning: Account must exist

**Method**: `GET`

**Path**: `/v1/login`

**Parameters**:

| Parameters | Descriptions             | Mandatory |
| ---------- | ------------------------ | :-------: |
| phone      | phone number intl format | X         |


**Exemple**

will send an sms to `06 12 34 56 78` phone with an OTP code.

```bash
curl --request GET \
  --url 'https://web-production.lime.bike/api/rider/v1/login?phone=%2B33612345678'
```

#### Send back OTP code

**Method**: `POST`

**Path**: `/v1/login`

**Header**:

| Header       | Value            | Mandatory |
| ------------ | ---------------- | :-------: |
| content-type | application/json | X         |

**Parameters**:

| Parameters | Descriptions             | Mandatory |
| ---------- | ------------------------ | :-------: |
| phone      | phone number intl format | X         |
| login_code | OTP code (length of 6)   | X         |


**Exemple**

```bash
curl --request POST \
  --cookie-jar - \
  --url 'https://web-production.lime.bike/api/rider/v1/login' \
  --header 'Content-Type: application/json' \
  --data '{"login_code": "123456", "phone": "+33612345678"}'
```

```JSON
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX3Rva2VuIjoiRk9PQkFSRUlSWkhBMiIsImxvZ2luX2NvdW50IjoyfQ.K5nmvUu92hYXQyeYG6O0rqo0ef2mkp7PMdtp9NrgwOE",
    "user": {
        "id": "FOOBAREIRZHA2",
        "type": "users",
        "attributes": {
            "token": "FOOBAREIRZHA2",
            "phone_number": "33612345678",
            "email_address": null,
            "has_verified_email_address": false,
            "name": "Lime Rider",
            "given_name": "Lime",
            "surname": "Rider",
            "default_payment_method": null,
            "referral_code": "REZHETH",
            "num_trips": 0,
            "edu": false,
            "subscription_item_states": [],
            "juicer_profile_status": null,
            "juicer_profile_initial_activated_at": null,
            "balance_cents": 0,
            "pending_balance_cents": 0,
            "currency": "USD"
        }
    }
}
```

Cookie


```
# https://curl.haxx.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

#HttpOnly_web-production.lime.bike	FALSE	/	TRUE	0	_limebike-web_session	U0pwQlVjcVRwMXZUTWovcHh3U251MERYTGE2dWpMdFdmNW9sL0d4SHBRVGtZd2VXN20yMjhJczhlR21nUkVHczlEREUweGNpYmtEWVFvQXBoQVNuRWdZWkVBajJPaHhDeStuUmttYVdYYWVsRDJEMUZvNE5YNU4xc1FlcjlDMi8xOVNMcDM3M3JhQWd0TDF2OWphMGR3PT0tLTBDYUtNeUJLcXRmNVd4YnorSEhlTWc9PQ%3D%3D--c8889db210d22bb4a96307b74d39c4b64d48777f
```

### Get bicycles by lat/lng

:warning: Auth (bearer AND cookie) are mandatory for this endpoint

**Method**: `GET`

**Path**: `/v1/views/main`

**Header**:

| Header        | Value        | Mandatory |
| ------------- | ------------ | :-------: |
| authorization | Bearer TOKEN | X         |

**Cookie**:

| Cookie                | Mandatory |
| --------------------- | :-------: |
| _limebike-web_session | X         |

**Parameters**:

| Parameters           | Descriptions | Mandatory |
| -------------------- | ------------ | :-------: |
| map_center_latitude  | latitude     | X         |
| map_center_longitude | Longitude    | X         |
| user_latitude        | Latitude     | X         |
| user_longitude       | Longitude    | X         |

**Exemple**

```bash
curl --request GET \
  --url 'https://web-production.lime.bike/api/rider/v1/views/main?map_center_latitude=38.907192&map_center_longitude=-77.036871&user_latitude=38.907192&user_longitude=-77.036871' \
  --header 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c' \
  --cookie '_limebike-web_session=N0xLYmE5ZytSSkRZa0FwQUdvYk1TalBaVWwzcnRDWUloT1Y1Z2ZNOVZSc0NCd3ZRZTFOVkxaS2lOcHFpemx6Y1pxT3ZudU1Zenk2ODlYRHBFZ1dxRWtaZGQybzRTQm96V09TWVdycENLcUltMHYzRWlUaEZlMDBqOCt4ODJqSWZwR09PSEtuNDdINnF3VGpkR3g2SjRBPT0tLTlJVHhSVFRDOE1CNm14S203VGxRd2c9PQ%253D%253D--9f55d56be64fefc5d5af3daf9e2fe9f7d7408cc0'
```

```JSON
{
	"data": {
		"id": "views::mainview",
		"type": "main_view",
		"attributes": {
			"user": {
				"id": "FOOBAR66B5TNR",
				"type": "users",
				"attributes": {
					"token": "FOOBAR66B5TNR",
					"phone_number": "33612345678",
					"email_address": null,
					"has_verified_email_address": false,
					"name": "Lime Rider",
					"given_name": "Lime",
					"surname": "Rider",
					"default_payment_method": null,
					"referral_code": "RYFAFTY",
					"num_trips": 0,
					"edu": false,
					"subscription_item_states": [],
					"juicer_profile_status": null,
					"juicer_profile_initial_activated_at": null,
					"balance_cents": 0,
					"pending_balance_cents": 0,
					"currency": "USD"
				}
			},
			"nearby_locked_bikes": [
				{
					"id": "KTJUMCB2UCYXK",
					"type": "bikes",
					"attributes": {
						"status": "locked",
						"plate_number": null,
						"latitude": 38.905481,
						"longitude": -77.034892,
						"last_activity_at": "2018-05-28T13:25:55.000Z",
						"bike_icon": null,
						"type_name": "scooter",
						"battery_level": "high",
						"meter_range": 29970,
						"rate_plan": "<b><font color='#0DC000' size='20' face='Montserrat'>$1</font></b><font color='#4A4A4A' size='16' face='Montserrat'> to unlock + </font><b><font color='#0DC000' size='20' face='Montserrat'>15¢ </font></b> <font color='#4A4A4A' size='16' face='Montserrat'> per 1 minutes</font>",
						"rate_plan_short": "<b><font color='#7AD319' size='16' face='Montserrat'>$1</font></b><font color='#444A57' size='12' face='Montserrat'> unlock + </font><b><font color='#7AD319' size='16' face='Montserrat'>15¢ </font></b> <font color='#444A57' size='12' face='Montserrat'> / 1 min</font>",
						"bike_icon_id": 6,
						"last_three": "886"
					}
				}
			],
			"nearby_parking_spots": [],
			"most_recent_trip": null,
			"auto_promotion": null,
			"default_bike_icon": {
				"id": "1",
				"type": "icons",
				"attributes": {
					"url": "https://d22d5yy1i19g9i.cloudfront.net/icons/default_pin.png?fingerprint=92bcf96642bd8a61eb4f4cca70794496",
					"description_icon_url": null,
					"description_link_url": null,
					"description": ""
				}
			},
			"cluster_icon": {
				"id": "2",
				"type": "icons",
				"attributes": {
					"url": "https://d22d5yy1i19g9i.cloudfront.net/icons/default_cluster.png?fingerprint=23bbfa670fea1998a61b91512c1a15d9",
					"description_icon_url": null,
					"description_link_url": null,
					"description": ""
				}
			},
			"icons": [
				{
					"id": "1",
					"type": "icons",
					"attributes": {
						"url": "https://d22d5yy1i19g9i.cloudfront.net/icons/default_pin.png?fingerprint=92bcf96642bd8a61eb4f4cca70794496",
						"description_icon_url": null,
						"description_link_url": null,
						"description": ""
					}
				}
			],
			"needs_taxi": false
		}
	},
	"meta": {
		"min_ios_version": "1.22.1",
		"min_android_code": 19,
		"flags": "IOS_VERSION_V1.0,ANDROID_VERSION_V1.0",
		"groups": {
			"complete_your_profile_v1": true,
			"show_auto_reload": true,
			"map_levels_v1": true,
			"apple_pay": true,
			"force_location_permission_v1": true,
			"unlock_button_group": "control",
			"default_to_unlock_group": "control",
			"take_photo": "control",
			"show_battery_level_on_map": false,
			"unlock_preview": false
		},
		"trip_id": null,
		"blocker": "MISSING_PAYMENT_METHOD",
		"notifications": [],
		"messages": []
	}
}
```

## Implementations

* https://www.npmjs.com/package/@multicycles/lime (JavaScript)