# Smart Meeting System Auth Endpoint

---

## Installation

In terminal, run the following command to clone the repo:

`$ git clone https://github.com/jiayizhg/smart-meeting-system-auth-endpoint.git`

## Setup

1. In terminal, cd into the cloned repo:

   `$ cd smart-meeting-system-auth-endpoint`

1. Then install the dependencies:

   `$ npm install`

1. Create an environment file to store your Meeting SDK credentials:

   `$ touch .env`

1. Add the following code to the `.env` file, and insert your [Zoom Meeting SDK credentials](https://developers.zoom.us/docs/meeting-sdk/developer-accounts/#get-meeting-sdk-credentials):

   ```
   ZOOM_MEETING_SDK_KEY=MEETING_SDK_KEY_HERE
   ZOOM_MEETING_SDK_SECRET=MEETING_SDK_SECRET_HERE
   ```

1. Save and close `.env`.

1. Start the server:

   `$ npm run start`

## Usage

Make a POST request to `http://localhost:4000` (or your deployed url) with the following request body:

| Key                   | Value Description |
| -----------------------|-------------|
| meetingNumber          | Required, the Zoom Meeting or Webinar Number. |
| role                   | Required, `0` to specify participant, `1` to specify host.  |

### Example Request

POST `http://localhost:4000`

Request Body:

```json
{
  "meetingNumber": "123456789",
  "role": 0
}
```

If successful, the response body will be a JSON representation of your Meeting SDK JWT:

```json
{
  "signature": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzZGtLZXkiOiJhYmMxMjMiLCJtbiI6IjEyMzQ1Njc4OSIsInJvbGUiOjAsImlhdCI6MTY0NjkzNzU1MywiZXhwIjoxNjQ2OTQ0NzUzLCJhcHBLZXkiOiJhYmMxMjMiLCJ0b2tlbkV4cCI6MTY0Njk0NDc1M30.UcWxbWY-y22wFarBBc9i3lGQuZAsuUpl8GRR8wUah2M"
}
```

In the [Meeting SDK](https://developers.zoom.us/docs/meeting-sdk/auth/#join-meetings-and-webinars-with-the-meeting-sdk-jwt), pass in the `signature` to the `join()` function:

```js
// Make http request to your auth endpoint to get the Meeting SDK JWT

// Meeting SDK - web - Client View - example:
ZoomMtg.join({
  signature: signature,
  sdkKey: sdkKey,
  userName: userName,
  meetingNumber: meetingNumber,
  passWord: password
})

// Meeting SDK - web - Component View - example:
client.join({
  signature: signature,
  sdkKey: sdkKey,
  userName: userName,
  meetingNumber: meetingNumber,
  password: password
})
```

