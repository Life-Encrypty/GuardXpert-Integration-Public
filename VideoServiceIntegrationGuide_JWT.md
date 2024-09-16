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

## Step 3: Implement Platform-Specific Scripts

The video player behavior depends on the user's platform. You will need to include platform-specific scripts that we will provide to ensure the video plays correctly.

If the scripts do not load in order, nothing will work.

### Android & Windows Platform:

You must load the following scripts in order:

```html

    <script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>

    <script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>
            
    <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.0.0/shaka-player.compiled.js"></script>

    <script src="https://GuardXpert.b-cdn.net/libs/v0.4.1/e8erhf348gfrez.js"
    integrity="sha256-hZ2R3/9ZlHgQeOeDp7jTgnoc9JgwXzIWiGR71cqgeB4=" crossorigin="anonymous"></script>
    <script src="https://GuardXpert.b-cdn.net/libs/v0.4.1/hd8r32gfwbifjne3eur.js"
    integrity="sha256-tdv5nDVilCFW+jG0Kcuzd59NQQ9Cntj7J4J3RYme39U=" crossorigin="anonymous"></script>
    <script src="https://GuardXpert.b-cdn.net/libs/v0.4.1/suwidgewyvf723gga.js"
    integrity="sha256-t/mY1ws+BI7cQuZuN+j5HUVz5dhn0aFW1iq6rzUaw7c=" crossorigin="anonymous"></script>
    <script src="https://GuardXpert.b-cdn.net/libs/v0.4.1/event-listeners.js"
    integrity="sha256-9RbAnpmrQwu1pWEjOLzYcKJUxcGjCOj4gS4fdAVkWw4=" crossorigin="anonymous"></script>

```

###  Apple Devices:

For Apple devices, You must load the following scripts in order.

```html

    <script src="https://cdn.jsdelivr.net/npm/jwt-decode/build/jwt-decode.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/platform/1.3.6/platform.min.js"></script>

    <script
        src="https://GuardXpert.b-cdn.net/libs/v0.3.1/apple/b82r3yhf43fgy.js"
        integrity="sha256-YajZqtkwnhY1r3gPvKjoUeaILeao08Q15vu/htOZ7UU=" crossorigin="anonymous">
    </script>

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
