# Midjourney Video Automation

> [!TIP]
>
> You can use Midjourney Video Automation directly from APIFY platform [apify.com/igolaizola/midjourney-video-automation](https://apify.com/igolaizola/midjourney-video-automation)
>
> If you want to generate images instead, check out [apify.com/igolaizola/midjourney-automation](https://apify.com/igolaizola/midjourney-automation)

## 🎥 What does Midjourney Video Automation do?

Midjourney Video Automation empowers you to automate video generation on [Midjourney](https://www.midjourney.com) using both text prompts and existing images—no manual intervention required. With this actor, you can:

- 🤖 **Bulk process** multiple prompts or image inputs to create videos
- 🎞️ **Text-to-Video**: generate a sequence of images from prompts and stitch them into a short video
- 📸 **Image-to-Video**: convert your own images (via URLs or a Google Drive folder) into videos, optionally enhanced with prompts
- ⚡ **Extensions**: add extra seconds to each video (4 s per extension)
- 🔄 **Concurrency**: run multiple jobs in parallel
- ⏳ **Randomized wait times** between operations to mimic human usage
- 📁 **Album HTML**: auto-generate an `album.html` in Key-Value storage for easy browsing and downloading

## 🔑 Prerequisites

1. An active Midjourney subscription (Standard Plan or higher to use **Relaxed** mode)
2. Your Midjourney cookie for authentication
3. The [Cookie-Editor Chrome extension](https://chromewebstore.google.com/detail/cookie-editor/hlkenndednhfkekhgcdicdfddnkalmdm)

## 🚀 Setup Guide

### 1. Getting Your Midjourney Cookie

1. Install the **Cookie-Editor** Chrome extension.
2. Log in to [www.midjourney.com](https://www.midjourney.com).
3. Click the Cookie-Editor icon and grant permissions if prompted.
4. Choose **Export** → **Export as Header String**.
5. Copy the resulting cookie string.

### 2. Running the Actor

1. In the actor's input form, paste your cookie into the `cookie` field.
2. Provide either:

   - A list of **text prompts** (`prompts`) for text-to-video, or
   - A list of **image URLs** (`images`) and/or a **Google Drive folder URL** (`googleDriveFolder`) for image-to-video.

3. Choose your **mode** (`relaxed`, `fast`, or `turbo`).
4. (Optional) Set the number of **extensions** to lengthen each video by 4 s each.
5. Configure **concurrency**, **minWait**, **maxWait**, and **jobTimeout** as needed.
6. Select your **proxy configuration** (Apify Proxy recommended).
7. Click **Run**.

## ⚙️ Input Parameters

| Parameter            | Type    | Description                                                                                                    | Default                   |
| -------------------- | ------- | -------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `cookie`             | String  | Your Midjourney authentication cookie (from Cookie-Editor).                                                    | —                         |
| `prompts`            | Array   | List of text prompts for text-to-video generation.                                                             | —                         |
| `images`             | Array   | List of image URLs for image-to-video conversion. Supports mixing with `prompts`.                              | —                         |
| `googleDriveFolders` | Array   | Public Google Drive folder URLs containing images for image-to-video conversion. Maximum 50 images per folder. | —                         |
| `mode`               | Select  | Generation speed mode:<br>• `relaxed` ("Pro Plan" or higher)<br>• `fast`<br>• `turbo`                          | `relaxed`                 |
| `private`            | Boolean | Generate private videos in stealth mode. ("Pro Plan" or higher)                                                | `false`                   |
| `extensions`         | Integer | Number of 4-second extensions to append to each video (max 4).                                                 | `0`                       |
| `concurrency`        | Integer | Number of concurrent jobs to run in parallel.                                                                  | `1`                       |
| `minWait`            | Integer | Minimum randomized wait time between operations (seconds).                                                     | `5`                       |
| `maxWait`            | Integer | Maximum randomized wait time between operations (seconds).                                                     | `10`                      |
| `jobTimeout`         | Integer | Maximum time to wait for a job to complete before skipping (seconds).                                          | `300`                     |
| `proxyConfiguration` | Object  | Proxy configuration settings. Defaults to Apify Residential proxy.                                             | Apify Proxy (RESIDENTIAL) |

## 📋 Output Format

Results are returned as an array of JSON objects. Example:

```json
[
  {
    "album_url": "https://api.apify.com/v2/key-value-stores/XXX/records/album.html#<runId>",
    "prompt": "A futuristic city skyline at dusk --v 6.1",
    "url": "https://cdn.midjourney.com/<jobId>/video.mp4",
    "preview_url": "https://cdn.midjourney.com/<jobId>/preview.jpg",
    "job_id": "<jobId>",
    "extensions": 1,
    "image_url": "https://drive.google.com/uc?id=<fileId>"
  }
]
```

| Field         | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| `album_url`   | Link to the generated `album.html` for browsing/downloading all videos. |
| `prompt`      | The text prompt used.                                                   |
| `url`         | Direct link to the generated video file (.mp4).                         |
| `preview_url` | Thumbnail link for the video (.gif)                                     |
| `job_id`      | Unique identifier for the generation job.                               |
| `extensions`  | Number of 4-second extensions applied.                                  |
| `image_url`   | Original image URL.                                                     |

## 🎞️ Accessing Generated Videos

The actor saves an "album.html" file to the KeyValue store for easy browsing and downloading of generated videos. You can access it by:

- Clicking any "Album URL" field in the results table
- Going to Run > Storage > KeyValueStore and finding the "album.html" file

The album interface provides several features:

- Filter videos by prompt text or other metadata
- Select multiple videos for batch operations
- Open videos in new tabs for detailed viewing
- Download selected videos as a ZIP file

Here's an example album showcasing some generated videos so you can see how your results will be displayed: [Browse Example Gallery](https://igolaizola.github.io/midjourney-video-automation/)

## ⚠️ Usage Guidelines & Best Practices

### Account Safety

- Midjourney may flag excessive automation; use responsibly.
- Only automate tasks you would normally perform manually.
- Avoid continuous 24/7 runs.

### Performance Optimization

- Start with low concurrency (1–2) and increase based on success rates.
- Use proxies from your region for more reliable access.
- Tune `minWait`/`maxWait` to balance speed and rate-limit safety.
- Update your cookie periodically for long sessions.

### General Tips

- Test with a small batch of prompts or images first.
- Use clear, descriptive prompts for better video content.
- Monitor and review failed jobs; they won't halt your run.

## 💳 Pricing & Credits

Apify's [Free plan](https://apify.com/pricing) includes \$5 in monthly credits—ideal for testing.
For regular usage, we recommend the [\$49/month Personal plan](https://apify.com/pricing), which provides ample credits for ongoing Midjourney Video Automation.
