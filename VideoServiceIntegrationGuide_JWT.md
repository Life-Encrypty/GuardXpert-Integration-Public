# How to Use Our Video Services

This guide will help you integrate our video services into your platform. Please follow the steps below carefully to ensure proper functionality.

## Prerequisites

Before proceeding, ensure you have the following data ready:
- **User Information**: This includes user details such as name, ID, mobile number, email, etc.
- **Platform Information**: Details about the user's platform, IP address, browser, and model.

## Step 1: Set Session Storage Using JWT (Server-Side Encoding and Decoding)

The client must store user and platform information in the browser's sessionStorage as an HS256 JWT. This token should be placed in a variable called 'otherData'. The JWT will contain the following user data:

```javascript
{
  "name": "Abdallah Awad",
  "userName": "userName",
  "id": "1",
  "mobile": "adadads",
  "clientId": "12", // This will be provided in production, you can use dummy in it for now
  "email": "ahmed@gmail.com",
  "contentId": "b1e543864ccf4473901b79823e0a2067", // This will be the content ID for Apple
  "otherContentId": "b1e543864ccf4473901b79823e0a2067", // This will be the content ID for other platforms
  "pullZone": "guardtestaccount", // This will be for development only, You will get your pull zone after contract
  "vlib": "289252",
  "platform": "windows",
  "ip": "192.168.1.1",
  "browser": "firefox",
  "model": "pop os"
}
```

The encoding and decoding of this JWT must be handled server-side. The client will receive the pre-encoded token from the server, and the server will handle decoding and validating the token on every request. The secret key required for encoding and decoding the JWT will also be stored and managed on the server side.

Important Notes:

    Token Maintenance: The client must ensure that the JWT token is sent to the server with each request for validation and access.
    Server-Side Security: All encoding and decoding operations for the JWT MUST be handled server-side to ensure the security of the token and prevent tampering by the client.
    Pull Zone: You will get your pull zone after contract.

## Step 2: Set Up the Video Container

The video will be displayed within a specific HTML element. Ensure that the location where you want to display the video has the following attributes:

```html
<div id="content">
    <div id="video-container" class="video-container">
        <!-- Video will be injected here -->
    </div>
</div>
```

## Step 3: Implement Scripts

The video player behavior depends on the user's platform. If the scripts do not load in order, nothing will work.

**Note**: you **MUST** perform step 1 before this step

### 3.1: List of scripts to load

all scripts **MUST** be loaded in the order.

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>

<link rel=stylesheet media='all' type='text/css' href='https://vjs.zencdn.net/8.6.1/video-js.css' />
<style>
    .vjs-poster {
        background-size: 100% !important;
    }
</style>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/video.min.js"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/videojs-contrib-eme.min.js"></script>


<script type="text/javascript"
    src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.0.0/shaka-player.compiled.js"></script>


<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/p.js"
    integrity="sha384-bn0IXpLp4YlhFQt9oZHkw1Qg/nC6U4qiqjR+F0LzF8/wzNA0dai1kd/HZsR8XxH4"
    crossorigin="anonymous"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/apple.js"
    integrity="sha384-rbIcZGUXQpBVgW54jb04mORuhoFFe2/Bh9c5d97gO8ZiFGtCEYIS9QvL9jalfION"
    crossorigin="anonymous"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/ez.js"
    integrity="sha384-jTt2xMVzY4PrC+0dNktgxqt/y0KIVbzGuA0Rqzyt/33QR5jPRqn2vH5MjmzGnt/K"
    crossorigin="anonymous"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/helper.js"
    integrity="sha384-9gkiFT5rxc4kfH2Yl5p0bMPRr8iH3q8Ht54IDfYA5FiuJLqp1WA44iFvi7HW0dYI"
    crossorigin="anonymous"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/shaka.js"
    integrity="sha384-twkccPYcGboZgOlZPaT3BsgBKLh2xvRXaoSldCU6QQvMPyjS4pn3FLKXb9DLCqNK"
    crossorigin="anonymous"></script>
<script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/event-listeners.js"
    integrity="sha384-GHxaFNd+85Dc/WDURhwuan+swaXLPdlVD4rkNC0hSzHVXbBRkJvETPL/mVrv0H3x"
    crossorigin="anonymous"></script>
<script>
```
### 3.2: Trigger Video Playback
Trigger the play event to start the video playback:
```js
const playEvent = new Event('play');
document.dispatchEvent(playEvent);
```

### 3.3: Demo Integration
For simplicity we will load every thing in one page.
Here’s a full demo that sets up the video player:

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Shaka Player Demo</title>
    <script>
        sessionStorage.setItem('otherData', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiQWJkYWxsYWggQXdhZCIsInVzZXJOYW1lIjoidXNlck5hbWUiLCJpZCI6IjEiLCJtb2JpbGUiOiJhZGFkYWRzIiwiY2xpZW50SWQiOiIxMiIsImVtYWlsIjoiYWhtZWRAZ21haWwuY29tIiwiY29udGVudElkIjoiYjFlNTQzODY0Y2NmNDQ3MzkwMWI3OTgyM2UwYTIwNjciLCJvdGhlckNvbnRlbnRJZCI6ImIxZTU0Mzg2NGNjZjQ0NzM5MDFiNzk4MjNlMGEyMDY3IiwicHVsbFpvbmUiOiJndWFyZHRlc3RhY2NvdW50IiwidmxpYiI6IjI4OTI1MiIsInBsYXRmb3JtIjoid2luZG93cyIsImlwIjoiMTkyLjE2OC4xLjEiLCJicm93c2VyIjoiZmlyZWZveCIsIm1vZGVsIjoicG9wIG9zIn0.pEpb2ZCk4AeZ0GUmuJJuP0AzeNWnvY1L8spgnmENp20');
    </script>


    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>

    <link rel=stylesheet media='all' type='text/css' href='https://vjs.zencdn.net/8.6.1/video-js.css' />
    <style>
        .vjs-poster {
            background-size: 100% !important;
        }
    </style>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/video.min.js"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/videojs-contrib-eme.min.js"></script>


    <script type="text/javascript"
        src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.0.0/shaka-player.compiled.js"></script>

</head>

<body>

    <!-- Button to trigger the custom event -->
    <button id="playButton">Play Video</button>

    <div id="content">
        <div id="video-container" class="video-container"></div>
    </div>

    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/p.js"
        integrity="sha384-bn0IXpLp4YlhFQt9oZHkw1Qg/nC6U4qiqjR+F0LzF8/wzNA0dai1kd/HZsR8XxH4"
        crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/apple.js"
        integrity="sha384-rbIcZGUXQpBVgW54jb04mORuhoFFe2/Bh9c5d97gO8ZiFGtCEYIS9QvL9jalfION"
        crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/ez.js"
        integrity="sha384-jTt2xMVzY4PrC+0dNktgxqt/y0KIVbzGuA0Rqzyt/33QR5jPRqn2vH5MjmzGnt/K"
        crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/helper.js"
        integrity="sha384-9gkiFT5rxc4kfH2Yl5p0bMPRr8iH3q8Ht54IDfYA5FiuJLqp1WA44iFvi7HW0dYI"
        crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/shaka.js"
        integrity="sha384-twkccPYcGboZgOlZPaT3BsgBKLh2xvRXaoSldCU6QQvMPyjS4pn3FLKXb9DLCqNK"
        crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.7/event-listeners.js"
        integrity="sha384-GHxaFNd+85Dc/WDURhwuan+swaXLPdlVD4rkNC0hSzHVXbBRkJvETPL/mVrv0H3x"
        crossorigin="anonymous"></script>
    <script>
        // Get references to the button and video element
        const playButton = document.getElementById('playButton');

        // Add click event to the button to dispatch the custom event
        playButton.addEventListener('click', function () {
            const playEvent = new Event('play');
            document.dispatchEvent(playEvent);
        });
    </script>
</body>

</html>
```


## Step 4: Perform Equality Checks (Optional):

For Step 4, which involves performing equality checks to determine if a user is suspicious (potentially trying to hack the system), here's the approach:

- **Purpose of the Step**: This step is optional and is intended to identify users who might be attempting to hack or manipulate the system by checking specific conditions or patterns in their data.

- **Process**: 
    * You will need to perform equality checks on certain data fields or patterns.
    * These checks will look for anomalies or irregularities that may indicate suspicious activity.

- **Next Steps**:
    * If you decide to perform these checks, please let us know.
    * We will then send you an email with detailed instructions on how to implement these checks.

## Step 5: Integration Testing

Please note that the links provided in this document are for testing purposes only. Production links will be provided privately to each client upon successful completion of the testing phase.

## Conclusion

By following these steps, you will successfully integrate our video service into your platform. If you encounter any issues or need further assistance, please contact our support team.
