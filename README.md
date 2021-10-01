# GameStackUnityDemo
This package is a Unity project that demonstrates intergrating the GameStack user and leaderboard APIs into your Unity game.

## Prerequisites
To try the demonstrations in this package you will need to complete the following setup.

### 1) Signup for a GameStack creator account
You will need a GameStack creator account before you can use any of the leaderboard demo levels. You can do this via a CURL call to the GameStack API.

**Example**
```sh
curl -H 'Content-Type: application/json' -d '{"email":"some@email.com","first_name":"ContactsFirstName","last_name":"ContactsLastName","organization":"ContactsOrganizationName","password":"test"}' http://localhost:8070/signup
```

See the [User API](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/UserAPIs.md#creator-quick-start) quick start guide for more information.

### 2) Loging to your GameStack creator account
To make calls to the leaderboard APIs for creating applications and leaderboards you will need an access token to include in your calls to the leaderboard APIs.

You can use the following example CURL call to login with your GameStack creator account.

```sh
curl -H 'Content-Type: application/json' -d '{"email":"some@email.com","password":"test"}' http://localhost:8070/login
```

You you will need the `token::access_token` from login the response.

```json
{
  ...
  "token":{
    "access_token":"eyJhbGciOiJIUzUxMiIsImtpZCI6IjEzMDM0MGIyLWU4YjYtNGRlOC05MzE2LTE2ZjFlN2Q1ZTIzZiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiIzMjM3NjA0M2QzMDVjZWMyYTQyZTY3YThlNjNmMjM3YyIsImV4cCI6MTYzMDQ3MDQyNiwic3ViIjoiYTZhZTAzYzUtN2JiYy00NDE2LTljOTMtZWVmYWNjNGU0OGE5In0.ojn7eFv2A5F7dOGSvYbQr-rh3TknZkjtI8RfQ1mDd3tTPUlGiq-TTcweZ6ZPHZ_uwvfZ3sOaXWcGiGpfRoi7lA",
    ...
  }
}
```

See the [Authenticate](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/UserAPIs.md#authenticate) section of the creator quick start guide for more information.

### 3) Create an application
To create leaderboards you will first need to make an application. You can use the following example CURL call to create an application.

```sh
curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"DemoGame"}' http://localhost:8080/app
```

If successful you will get a response with you new applications ID.

**Sample response**
```json
{"application_id":"7cb1fa38b8e15fb78fe2dc1984a24dbeb87cdc69"}
```

**IMPORTANT**: Replace the placholder value for the `ApplicationID` variable in `Assets->Scripts->Constants.cs` with your application ID.

See the [Create application](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/LeaderboardAPIs.md#create-application) section of the Leaderboard API guide for more information.

### 4) Create leaderboards
Next you will need to create sample leaderboards to interact with in the demo levels. You can use the following example CURL calls to create the required leaderboards. Make sure to note the leaderboard IDs returned as you will need these for later steps.

<details>
  <summary>FightingGameDemo Leaderboard</summary>

  ```sh
  curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"FightingGameDemo","dimensions":{"wins":{"data":{"type":"INT"}},"losses":{"data":{"type":"INT"}},"hitPecentage":{"data":{"type":"FLOAT"}},"mode":{"data":{"type":"STRING"}}}}' http://localhost:8080/app/<your_applciation_id>/leaderboard
  ```

</details>

<details>
  <summary>FPSDemo Leaderboard</summary>

  ```sh
  curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"FPSDemo","dimensions":{"kills":{"data":{"type":"INT"}},"deaths":{"data":{"type":"INT"}},"accuracy":{"data":{"type":"FLOAT"}},"level":{"data":{"type":"STRING"}}}}' http://localhost:8080/app/<your_applciation_id>/leaderboard
  ```

</details>

<details>
  <summary>RPGDemo Leaderboard</summary>

  ```sh
  curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"RPGDemo","dimensions":{"enemiesKilled":{"data":{"type":"INT"}},"spellsCast":{"data":{"type":"INT"}},"averageDPS":{"data":{"type":"FLOAT"}},"dungeon":{"data":{"type":"STRING"}}}}' http://localhost:8080/app/<your_applciation_id>/leaderboard
  ```

</details>

<details>
  <summary>SportsDemo Leaderboard</summary>

  ```sh
  curl -H 'Content-Type: application/json' -H 'Authorization: Bearer <your_access_token>' -d '{"name":"SportsDemo","dimensions":{"wins":{"data":{"type":"INT"}},"losses":{"data":{"type":"INT"}},"rushYards":{"data":{"type":"INT"}},"passYards":{"data":{"type":"INT"}},"completionPercentage":{"data":{"type":"FLOAT"}},"mode":{"data":{"type":"STRING"}}}}' http://localhost:8080/app/<your_applciation_id>/leaderboard
  ```

</details>

If successful you will get responses with your new leaderboards ID.

**Sample response**
```json
{"leaderboard_id":"leaderboard_5e4be46964896293a3f626d0304fg6cb37a35279"}
```

**IMPORTANT**: Replace the placholder value(s) for the `FightingGameDemoLeaderboardID`, `FPSDemoLeaderboardID`, `RPGDemoLeaderboardID`, and `SportsDemoLeaderboardID` variable(s) in `Assets->Scripts->Constants.cs` with your leaderboard ID(s).

See the [Create leaderboard](https://github.com/GameStackTech/GameStackDocs/blob/main/docs/LeaderboardAPIs.md#create-leaderboard) section of the Leaderboard API guide for more information.

### 4) Create a GameStack player account
You will need a to create a GameStack player account to login, put stats to, and get stats from your leaderboard(s). The easiest way to create a GameStack player account is with the player signup flow in the demo. You can also do this via CURL (see section below for more information).

<details>
  <summary>GameStack player create via CURL</summary>

  You can use the following CURL command to create a GameStack player account.

  ```sh
  curl -H 'Content-Type: application/json' -d '{"username":"some_username","email":"some@email.com","name":"Some User","password":"test"}' http://localhost:8070/players/signup
  ```

</details>

## Using the demo