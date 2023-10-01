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
      {
         "name": "La Liga",
         "category": {
            "name": "Spain",
            "key": "spain"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-spain-laliga",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "ESP",
                  "name": "Cadiz",
                  "abbreviation": "CAD",
                  "researchId": "",
                  "key": "c46ff-cadiz-cf"
               },
               "cutoffTime": "2023-10-01T19:00:00Z",
               "name": "Atletico Madrid V Cadiz",
               "id": 19041499,
               "type": "EVENT_TYPE_EVENT",
               "key": "c4248-atletico-madrid-v-c46ff-cadiz-cf",
               "home": {
                  "nationality": "ESP",
                  "name": "Atletico Madrid",
                  "abbreviation": "ATM",
                  "researchId": "",
                  "key": "c4248-atletico-madrid"
               },
               "status": "TRADING"
            },
            {
               "markets": {},
               "away": {
                  "nationality": "ESP",
                  "name": "Valencia",
                  "abbreviation": "VCF",
                  "researchId": "",
                  "key": "c427b-valencia-cf"
               },
               "cutoffTime": "2023-10-01T19:00:00Z",
               "name": "Real Betis Balompié V Valencia",
               "id": 19041481,
               "type": "EVENT_TYPE_EVENT",
               "key": "cca90a-real-betis-seville-v-c427b-valencia-cf",
               "home": {
                  "nationality": "ESP",
                  "name": "Real Betis Balompié",
                  "abbreviation": "RBB",
                  "researchId": "",
                  "key": "cca90a-real-betis-seville"
               },
               "status": "TRADING"
            }
         ]
      },
      {
         "name": "Indian Super League",
         "category": {
            "name": "India",
            "key": "india"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-india-indian-super-league",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "IND",
                  "name": "Jamshedpur FC",
                  "abbreviation": "JAM",
                  "researchId": "",
                  "key": "cad52d-jamshedpur-fc"
               },
               "cutoffTime": "2023-10-01T14:30:00Z",
               "name": "Kerala Blasters FC V Jamshedpur FC",
               "id": 19917406,
               "type": "EVENT_TYPE_EVENT",
               "key": "c3c49-kerala-blasters-fc-v-cad52d-jamshedpur-fc",
               "home": {
                  "nationality": "IND",
                  "name": "Kerala Blasters FC",
                  "abbreviation": "KER",
                  "researchId": "",
                  "key": "c3c49-kerala-blasters-fc"
               },
               "status": "TRADING_LIVE"
            }
         ]
      },
      {
         "name": "LFF Cup",
         "category": {
            "name": "Lithuania",
            "key": "lithuania"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-lithuania-lff-cup",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "LTU",
                  "name": "FA Siauliai",
                  "abbreviation": "SIA",
                  "researchId": "",
                  "key": "c7652f-futbolo-akademija-siauliai"
               },
               "cutoffTime": "2023-10-01T14:30:00Z",
               "name": "FK Transinvest V FA Siauliai",
               "id": 20240586,
               "type": "EVENT_TYPE_EVENT",
               "key": "c103376-fk-transinvest-v-c7652f-futbolo-akademija-siauliai",
               "home": {
                  "nationality": "LTU",
                  "name": "FK Transinvest",
                  "abbreviation": "TRA",
                  "researchId": "",
                  "key": "c103376-fk-transinvest"
               },
               "status": "TRADING_LIVE"
            }
         ]
      },
      {
         "name": "Premier League",
         "category": {
            "name": "Russia",
            "key": "russia"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-russia-premier-league",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "RUS",
                  "name": "FK Dinamo Moscow",
                  "abbreviation": "DMO",
                  "researchId": "",
                  "key": "c42d4-fc-dinamo-moscow"
               },
               "cutoffTime": "2023-10-01T16:00:00Z",
               "name": "RFK Akhmat Grozny V FK Dinamo Moscow",
               "id": 19650282,
               "type": "EVENT_TYPE_EVENT",
               "key": "c1a6406-rfk-akhmat-grozny-v-c42d4-fc-dinamo-moscow",
               "home": {
                  "nationality": "RUS",
                  "name": "RFK Akhmat Grozny",
                  "abbreviation": "AKH",
                  "researchId": "",
                  "key": "c1a6406-rfk-akhmat-grozny"
               },
               "status": "TRADING_LIVE"
            }
         ]
      },
      {
         "name": "Super League 1",
         "category": {
            "name": "Greece",
            "key": "greece"
         },
         "sport": {
            "name": "Soccer",
            "key": "soccer"
         },
         "key": "soccer-greece-super-league-1",
         "events": [
            {
               "markets": {},
               "away": {
                  "nationality": "GRC",
                  "name": "AE Kifisia FC",
                  "abbreviation": "AEK",
                  "researchId": "",
                  "key": "c3a5f-kifisias"
               },
               "cutoffTime": "2023-10-01T14:30:00Z",
               "name": "Aris Thessaloniki V AE Kifisia FC",
               "id": 20135045,
               "type": "EVENT_TYPE_EVENT",
               "key": "c3a30-aris-thessaloniki-fc-v-c3a5f-kifisias",
               "home": {
                  "nationality": "GRC",
                  "name": "Aris Thessaloniki",
                  "abbreviation": "ARIS",
                  "researchId": "",
                  "key": "c3a30-aris-thessaloniki-fc"
               },
               "status": "TRADING_LIVE"
            }
         ]
      }
   ]
}

```

## Potential technical problems



