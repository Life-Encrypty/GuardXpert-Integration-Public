# How to Use Our Video Services

This guide will help you integrate our video services into your platform. Please follow the steps below carefully to ensure proper functionality.

## Prerequisites

Before proceeding, ensure you have the following data ready:
- **User Information**: This includes user details such as name, ID, mobile number, email, etc.
- **Platform Information**: Details about the user's platform, IP address, browser, and model.

## Step 1: Set Session Storage

Before navigating to the video page, you must set certain variables in the browser's `sessionStorage`. These variables are required for user authentication and platform validation. Below is an example of the required session storage data:

```javascript
const user = {
        "name": "Abdallah Awad",
        "userName": "userName",
        "id": "17",
        "mobile": "+201555440557",
        "clientId": "4",
        "email": "ahmed@gmail.com",
        "contentId": "f2e4d030-a478-476f-b7f8-4d8a5f126958", // this will be content id for apple
        "otherContentId": "77381421f799427188e44e87c2c6991d",// this will be content id for other platforms 
        "vlib":"289252",
        "platform":"linux",
        "ip":"192.168.1.1",
        "browser":"firefox",
        "model":"pop os"
    };
for (const [key, value] of Object.entries(user)) {
            sessionStorage.setItem(key, value);
        }
sessionStorage.setItem('userData', JSON.stringify(user));
```

Ensure that these values are set before the user accesses the video page.

## Step 2: Set Up the Video Container

The video will be displayed within a specific HTML element. Ensure that the location where you want to display the video has the following attributes:
- **ID**: `video-container`
- **Class**: `video-container`

Example HTML:

```html
<div id="video-container" class="video-container">
    <!-- Video will be displayed here -->
</div>
```

## Step 3: Implement Platform-Specific Scripts

The video player behavior depends on the user's platform. You will need to include platform-specific scripts that we will provide to ensure the video plays correctly.

### Android & Windows Platform:

You must load the following scripts in order:

```html
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.10.9/controls.min.css" integrity="sha512-nAqZrxye1O18iXFtwikO1NfjqYHl9A/mmInP5L3Fw5wbjZlyEjmh5HayNVHjhC+vMlun/shMRGtR/EGtuq+LcA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.10.9/shaka-player.compiled.js" integrity="sha512-16krjbsmAuIW+PFjk5jwlvwBe50Fv9o80R0rWQMUKvI8uN8bw3YFhmW5bcxogh79ql2pYurAJvoiUEeW4sH+xA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.10.9/shaka-player.compiled.min.js" integrity="sha512-dmZoZUUEksD0wBjnZY14+ZhNADGr4yrkrVm7SbWIJQKZbmNADxMaGLW71/JdAZf8r5I9l58t29v1L4abF6k3uA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.10.9/shaka-player.ui.min.js" integrity="sha512-k2UXeOpu53Wnx7wkOTQEHddBtfs49jawEg0Y8co2ZxBLML5h42IcpDPi7alF/rA4BguYAoSBNkZxCrlno7lWAw==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

    <script src="https://GuardXpert.b-cdn.net/libs/fcea74ab-99d0-4f5f-ac12-78bb82c92331/U2FsdGVkX18R2OGsfeG8EvzUWRvakNmYiEGupiRa+e8=.js"
    integrity="sha256-S6Acyr+FXAMEfU4UbDDoogwRnvjAq3Oc5/5UfIWNKjQ="
        crossorigin="anonymous"></script>

    <script src="https://GuardXpert.b-cdn.net/libs/fcea74ab-99d0-4f5f-ac12-78bb82c92331/U2FsdGVkX1+WTBrHnCbiZN5TQ2ceIed6jpSNkJeoO0c=.js"
    integrity="sha256-ycYppG7my4zLl7ISGSow8XpyKVZgUeITN4r1xtKzGGw="
        crossorigin="anonymous"></script>

    <script src="https://GuardXpert.b-cdn.net/libs/fcea74ab-99d0-4f5f-ac12-78bb82c92331/U2FsdGVkX195oY+ZT10q7x5fXc1RwLMONpVXywZexws=.js"
    integrity="sha256-F4YVkXldfDDrCBZGxzzwrxrS27ffLUN933RJ9pDslbk="
        crossorigin="anonymous"></script>


```

###  Apple Devices:

For Apple devices, you will need to load the specific scripts we provide for FairPlay DRM.

```html
<script src="https://GuardXpert.b-cdn.net/libs/47e7c4fe-f20a-4df4-8ab8-628732898350/U2FsdGVkX18NyLTah0X803speHo8WreUnKr0zS4ma8A%3D.js"
integrity="sha256-ywYqJjONyj+y7lG3mxRDWDdZn8gEhGDNMGjQvaAJ28o="
        crossorigin="anonymous"></script>

```

## Step 4: Suspicious User Notification for Apple Devices

For users on Apple devices, it is required that you notify us if the user is deemed suspicious. This can be handled by sending a notification to our system with the user’s details.

### 4.1- How to Determine If a User Is Suspicious

To assess whether a user is suspicious, the following checks should be performed:

**Retrieve Required Variables from Session Storage:**

We retrieve certain key details from sessionStorage, including:
```
'U2FsdGVkX19GiT0oJSLH3RJNoTl5mRod'
'U2FsdGVkX1+VKy8KrqEIMiGDY8tt3RnX3Ak/7eJiA0w=' 
'U2FsdGVkX1852JHdAePVhKS4lZKbEMsj' 
'U2FsdGVkX19ik3AfvSufbzl+bBEcYX5kZUU4/U6RJpo='
```

**Perform Equality Checks:**

This is not code, this is the logic you have to do:

```
if(
    (
    'U2FsdGVkX19GiT0oJSLH3RJNoTl5mRod' = 'U2FsdGVkX18hKQYqjD4D6AUaKPZpaiY3' 
    && 
    'U2FsdGVkX1852JHdAePVhKS4lZKbEMsj' = 'U2FsdGVkX1/IdX8BvGjrSpqI901TaJaEL0+CKOCEGfk='
    )
    ||
    ('U2FsdGVkX1+VKy8KrqEIMiGDY8tt3RnX3Ak/7eJiA0w=' != 'U2FsdGVkX1/jalokph0/XZsE6lAHSfwXu01Ia4Kzi/XXnu7n/y0kAw==')
    ||
    ('U2FsdGVkX19ik3AfvSufbzl+bBEcYX5kZUU4/U6RJpo=' != 'U2FsdGVkX19UzfRSUYu+Sy+yGLnM5bNojx7/eealJIsmSBnHtpBvzw==')
    
)
{
    user is suspicious
}

```

## Conclusion

By following these steps, you will successfully integrate our video service into your platform. If you encounter any issues or need further assistance, please contact our support team.
