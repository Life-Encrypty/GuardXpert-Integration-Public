# How to Use Our Video Services

This guide will help you integrate our video services into your platform. Please follow the steps below carefully to ensure proper functionality.

## Prerequisites

Before proceeding, ensure you have the following data ready:
- **User Information**: This includes user details such as name, ID, mobile number, email, etc.
- **Platform Information**: Details about the user's platform, IP address, browser, and model.

## Step 1: Set Session Storage Using JWT (Server-Side Encoding and Decoding)

Before navigating to the video page, the client must store user and platform information in the browser's sessionStorage as an HS256 JWT. This token should be placed in a variable called 'otherData'. The JWT will contain the following user data:

```javascript
{
    "name": "Abdallah Awad",
    "userName": "userName",
    "id": "17",
    "mobile": "+201000000000",
    "clientId": "4", // This will be provided in production, you can use dummy in it for now
    "email": "mail@mail.com",
    "contentId": "9690619a-f9b4-43f3-8d86-a0c770df84dc", // This will be the content ID for Apple
    "otherContentId": "db9d9c3e3f424c75bea7f69c59db038c", // This will be the content ID for other platforms
    "pullZone": "GuardXpert", // This will be for development only, You will get your pull zone after contract
    "vlib": "289252",
    "platform": "linux",
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


The video will be displayed within a specific HTML element. To support **Apple mobile devices only**, ensure that the location where you want to display the video has the following structure and attributes:

```html  
<div id="content">  
    <div id="video-container" class="video-container">  
        <video-js id='player' controls preload='auto' class='vjs-16-9 vjs-big-play-centered'></video-js>  
    </div>  
</div>
```

### **Explanation of Elements:**

* **`id="player"`**: This unique ID targets the video element for video.js to initialize and control.  
* **`controls`**: Displays player controls for playback.  
* **`preload='auto'`**: Preloads video content, allowing a faster initial playback.  
* **`class='vjs-16-9 vjs-big-play-centered'`**: Sets a responsive 16:9 aspect ratio and centers the play button.

This setup ensures compatibility with Apple devices and an optimized video experience.


## Step 3: Implement Platform-Specific Scripts

The video player behavior depends on the user's platform. You will need to include platform-specific scripts that we will provide to ensure the video plays correctly.

If the scripts do not load in order, nothing will work.

### Android, Windows & MacOS Platform:

You must load the following scripts in order:

```html

    <script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>

    <script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>
            
    <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.0.0/shaka-player.compiled.js"></script>

    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/other/ez.js" integrity="sha384-lPClooIouJZThzD1ncddY+FxV1XPSRoI5O4piYg5VL8EEqPPxkcDsqXD9t1uyH8/" crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/other/helper.js" integrity="sha384-QTeyqhwKjsHqokGEA0iRA44X/6wU56wMbiEUK23bsGy1rY3JJZHRzxU+8/pLWWiK" crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/other/shaka.js" integrity="sha384-lY3erxUPbUbKnpzh2rywG+FEAAR7AyoZ3zHKmqKNs1QeNax8kLzWNGTC0DFrkNl6" crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/other/event-listeners.js" integrity="sha384-fqkTmY7/dVFi0pDTZMKjJpTX6tTdSTFfdAo0RKGcKWbQwYyI94D11QeGNuf9iNdI" crossorigin="anonymous"></script>
```

###  Apple Mobile Devices:

For Apple devices, You must load the following scripts in order.

```html

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/apple/video.min.js" integrity="sha384-7WJd15qzjuxEd6cGsqMXUooY6KsQuT9lKEkD7sFJVQKpTh3I5MbGcoGoJEMzNZJf" crossorigin="anonymous"></script>
    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/apple/videojs-contrib-eme.min.js" integrity="sha384-HIRjVqpYOdeAgk+qOZtSEwdW7jgRlTN7YDzNLKZKLKLc7rz+LHpcTh9tfQ9uqiKS" crossorigin="anonymous"></script>

    <script type="text/javascript" src="https://GuardXpert.b-cdn.net/libs/v0.5.1/apple/apple.js" integrity="sha384-DUe08ljBTE0ySGEZOQd6Efuzpy4hN7kWrx8daH2qVn51oKt7zUWC8JNuJQ8x7dHP" crossorigin="anonymous"></script>

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
