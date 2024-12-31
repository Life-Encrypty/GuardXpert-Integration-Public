
# GuardXpert Video Embedding Documentation

Welcome to the GuardXpert video embedding guide. This document explains how to use the GuardXpert iframe in your own website or application. Depending on your use case, you’ll follow slightly different steps, but the core concept is the same: upload a video in our dashboard, retrieve its **videoID**, and then embed the provided `<iframe>` code wherever you want the video to be displayed.


## Table of Contents
1. Overview  
2. Prerequisites  
3. Embedding the Video  
   - Iframe Structure  
   - Parameters  
4. Use Cases  
   - 1. Dashboard Users (Production)  
   - 2. Testing Users  
5. Common Troubleshooting  
6. FAQ  
7. Contact & Support


## Overview

GuardXpert provides a straightforward video hosting and streaming solution. Once you upload your video to our dashboard and the video processing is complete, we generate a shareable `<iframe>` snippet. You can simply copy and paste this snippet into your own webpage or application to display the video securely.


## Prerequisites

- **GuardXpert Dashboard Access**: You need a valid GuardXpert account to upload and manage your videos.  
- **Browser or Development Environment**: Ensure you have a modern browser for testing the embedded iframe.  
- **Permission to Edit Webpages**: You (or your development team) must be able to modify the HTML of your site to embed the iframe.


## Embedding the Video

### Iframe Structure

Below is the basic structure of the iframe you will receive:

```html
<iframe
  id=“videoIframe”
  src=“https://GuardXpert.b-cdn.net/libs/iframe-query2/main.html?videoID=20167d2446414b99bcbf4783eaeabdd9&account=GuardXpert”
  width=“800”
  height=“450”
  allow=“encrypted-media; fullscreen; autoplay”>
</iframe>
```

**Key Attributes**:

- `id`: A unique identifier for the iframe (e.g., `videoIframe`).  
- `src`: The URL endpoint containing query parameters (`videoID` and `account`).  
- `width` / `height`: Dimensions of the video player (in pixels).  
- `allow`: Enables specific features, such as `autoplay`, `fullscreen`, and `encrypted-media`.

### Parameters

1. **videoID**  
   - A unique identifier for your video, automatically generated after video processing.  
   - Example: `videoID=20167d2446414b99bcbf4783eaeabdd9`

2. **account**  
   - The account name or identifier assigned to you by GuardXpert.  
   - Example: `account=GuardXpert` (production) or a “test” account during the trial phase.

Putting it all together, the `src` URL should look like this:

https://GuardXpert.b-cdn.net/libs/iframe-query2/main.html?videoID=<VIDEO_ID>&account=<ACCOUNT_NAME>

Replace `<VIDEO_ID>` with your actual video ID, and `<ACCOUNT_NAME>` with the provided account.


## Use Cases

### 1. Dashboard Users (Production)

This scenario is for users who have a production GuardXpert account. Here’s the step-by-step flow:

1. **Upload Your Video**  
   - Log in to the GuardXpert dashboard.  
   - Navigate to the “Upload” section and select the video you want to process.

2. **Wait for Processing**  
   - GuardXpert will process the video for optimal streaming performance.  
   - Once processing is complete, you’ll see a unique `videoID` associated with your uploaded file.

3. **Get the Iframe**  
   - The dashboard will display an iframe snippet containing your `videoID` and your production `account` name.  
   - Copy this `<iframe>` code.

4. **Embed in Your Site**  
   - Open the HTML file or content management system (CMS) where you want the video to appear.  
   - Paste the `<iframe>` code.  
   - Adjust the `width` and `height` if desired.

5. **Verify**  
   - Load your webpage to confirm the video plays correctly and meets your design requirements.

Example:

``` html
<iframe
  id=“videoIframe”
  src=“https://GuardXpert.b-cdn.net/libs/iframe-query2/main.html?videoID=<YOUR_VIDEO_ID>&account=<YOUR_ACCOUNT>”
  width=“800”
  height=“450”
  allow=“encrypted-media; fullscreen; autoplay”>
</iframe>
```


### 2. Testing Users

For testing purposes (e.g., trials, demos, or staging environments), you’ll follow a similar process, but you might receive a temporary “test” account name instead of your production account name. Here’s how:

1. **Upload the Test Video**  
   - Use the same GuardXpert dashboard to upload your video.  
   - Wait for processing to complete.

2. **Retrieve the `videoID`**  
   - After processing, copy the `videoID` from the dashboard.

3. **Embed with the Test Account**  
   - If you’re still in a trial phase, you’ll receive an iframe snippet with a placeholder `account` parameter (e.g., `account=testAccount`).  
   - Paste the snippet into your site.

4. **Upgrade to Production**  
   - Once your contract is finalized, GuardXpert will provide you with the real `account` name (e.g., `GuardXpert`).  
   - Replace `account=testAccount` with your new `account` in the iframe’s `src` attribute.

Example (Test Environment):

``` html
<iframe
  id=“videoIframe”
  src=“https://GuardXpert.b-cdn.net/libs/iframe-query2/main.html?videoID=<YOUR_VIDEO_ID>&account=testAccount”
  width=“800”
  height=“450”
  allow=“encrypted-media; fullscreen; autoplay”>
</iframe>
```

Example (Production after Upgrade):

``` html
<iframe
  id=“videoIframe”
  src=“https://GuardXpert.b-cdn.net/libs/iframe-query2/main.html?videoID=<YOUR_VIDEO_ID>&account=GuardXpert”
  width=“800”
  height=“450”
  allow=“encrypted-media; fullscreen; autoplay”>
</iframe>
```

—

## Common Troubleshooting

1. **Video Not Displaying**  
   - Check the `videoID`: Make sure it’s spelled correctly and that the video has completed processing.  
   - Check the `account`: Use the correct account name for your environment (test vs. production).

2. **Autoplay Not Working**  
   - Some browsers block autoplay by default. User interaction may be required to start the video.

3. **Incorrect Sizing**  
   - Adjust the `width` and `height` attributes to fit your layout.  
   - Consider responsive design by setting `width=“100%”` if needed.

4. **Console Errors**  
   - Check your browser’s developer console. If you see errors related to the iframe URL, confirm you have the correct parameters.


## FAQ

**Q1: Do I need any special libraries or scripts on my website to display the iframe?**  
A: No. The iframe is fully self-contained. Just copy and paste the provided code.

**Q2: How secure is the embedded video?**  
A: GuardXpert uses secure CDN endpoints, and the iframe only loads from our trusted domain. Further security measures, such as token-based access, can be discussed if required.

**Q3: Can I customize the video player look-and-feel?**  
A: Currently, styling is controlled on the GuardXpert side. Future updates may allow user-defined themes or colors.


## Contact & Support

- **Email**: info@guardxpert.com  

If you encounter any issues not covered in this documentation, please reach out to our support team. We’ll be happy to assist!


_Last updated: 2024-12-31_  
_GuardXpert © 2024. All rights reserved._
