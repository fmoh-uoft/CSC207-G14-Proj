# CSC207-G14-Proj


## Project description (tentative)

A sports betting app that allows you to:
 - view scores across sports (TBD on which)
 - place bets
 - view spreads for various teams
 - earn (fake) money from your successful bets
 - view scoreboard of the highest earners
 - TBD on more

## Application description

Java web app that provides the UI to view your sports betting page. This java app will follow the MVC pattern and persist user-specific content in a database.


## APIs to use

The [CloudBet API](https://www.cloudbet.com/api/#/) looks to cover viewing scores, and viewing spreads/odds for any match-up.

### Link to API use

https://hopp.sh/r/lYRZMjmORsXx

### Screenshot of usage, checking today's games
<img width="1295" alt="image" src="https://github.com/fmoh-uoft/CSC207-G14-Proj/assets/145361461/705dcaf8-f31b-49d0-9f89-be22a53ee608">

### Sample Java code
```java
package api;
import okhttp3.*;
import org.json.JSONException;
import org.json.JSONObject;
import java.io.IOException;
public class CloudBetAPI {
    public static void main(String[] args) {
        OkHttpClient client = new OkHttpClient().newBuilder()
                .build();
        Request request = new Request.Builder()
                .url(String.format("https://sports-api.cloudbet.com/pub/v2/odds/fixtures?sport=%s&date=%s&limit=%s",
                        "soccer", "2023-10-01", 10))
                .addHeader("X-API-Key",  System.getenv("API_TOKEN"))
                .addHeader("Content-Type", "application/json")
                .build();
        try {
            Response response = client.newCall(request).execute();
            JSONObject responseBody = new JSONObject(response.body().string());

            if (response.code() == 200) {
                System.out.println(responseBody);
            } else {
                throw new RuntimeException(responseBody.getString("message"));
            }
        } catch (IOException | JSONException e) {
            throw new RuntimeException(e);
        }
    }
}

```

#### Output
```java
{
   "competitions": [
      {
         "name": "Serie A",
         "category": {
            "name": "Italy",
            "key": "italy"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-italy-serie-a",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "ITA",
                  "name": "Juventus",
                  "abbreviation": "JUV",
                  "researchId": "",
                  "key": "c4d33-juventus-turin"
               },
               "cutoffTime": "2023-10-01T16:00:00Z",
               "name": "Atalanta BC V Juventus",
               "id": 20089364,
               "type": "EVENT_TYPE_EVENT",
               "key": "c1a620b-atalanta-bc-v-c4d33-juventus-turin",
               "home": {
                  "nationality": "ITA",
                  "name": "Atalanta BC",
                  "abbreviation": "ATA",
                  "researchId": "",
                  "key": "c1a620b-atalanta-bc"
               },
               "status": "TRADING_LIVE"
            },
            {
               "markets": {},
               "away": {
                  "nationality": "ITA",
                  "name": "Frosinone Calcio",
                  "abbreviation": "FRO",
                  "researchId": "",
                  "key": "c4c7d-frosinone-calcio"
               },
               "cutoffTime": "2023-10-01T18:45:00Z",
               "name": "AS Roma V Frosinone Calcio",
               "id": 20089385,
               "type": "EVENT_TYPE_EVENT",
               "key": "c4d0b-as-roma-v-c4c7d-frosinone-calcio",
               "home": {
                  "nationality": "ITA",
                  "name": "AS Roma",
                  "abbreviation": "ROM",
                  "researchId": "",
                  "key": "c4d0b-as-roma"
               },
               "status": "TRADING"
            }
         ]
      },
      {
         "name": "Bundesliga",
         "category": {
            "name": "Germany",
            "key": "germany"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-germany-bundesliga",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "DEU",
                  "name": "FC Augsburg",
                  "abbreviation": "FCA",
                  "researchId": "",
                  "key": "c3629-fc-augsburg"
               },
               "cutoffTime": "2023-10-01T15:30:00Z",
               "name": "Freiburg V FC Augsburg",
               "id": 19649472,
               "type": "EVENT_TYPE_EVENT",
               "key": "c35ff-sc-freiburg-v-c3629-fc-augsburg",
               "home": {
                  "nationality": "DEU",
                  "name": "Freiburg",
                  "abbreviation": "SCF",
                  "researchId": "",
                  "key": "c35ff-sc-freiburg"
               },
               "status": "TRADING_LIVE"
            }
         ]
      },
      ....
   ]
}

```

## Potential technical problems



