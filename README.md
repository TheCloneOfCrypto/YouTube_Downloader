# Media Downloader

A powerful application to download videos, extract audio, and transcribe content from various platforms like YouTube and Vimeo.

## Features

- **Video Download**: Download videos in the best available quality
- **Audio Extraction**: Extract high-quality audio from videos
- **Text Transcription**: Convert video to text using OpenAI's Whisper AI
- **VTT to DOCX Conversion**: Automatically convert transcriptions to Word documents
- **Google Drive Integration**: Automatically upload transcriptions to Google Drive

## Setup

### Prerequisites

- Node.js and npm installed
- yt-dlp installed on your system
- OpenAI API key (for text transcription)

### Installation

1. Clone or download this repository
2. Install dependencies:
   ```
   npm install
   ```
3. Set up your environment variables in the `.env` file:
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   GOOGLE_DRIVE_WEBHOOK_URL=your_google_drive_webhook_url_here
   ```

### Google Drive Integration Setup (Optional)

To enable automatic uploading of transcriptions to Google Drive:

1. Go to https://script.google.com/ and create a new project
2. Copy the contents of `google-drive-webhook.gs` into the editor
3. Save the project
4. Deploy as a web app:
   - Click "Deploy" > "New deployment"
   - Select "Web app" as the deployment type
   - Set "Execute as" to "Me"
   - Set "Who has access" to "Anyone" (or "Anyone with Google account" for more security)
   - Click "Deploy"
5. Copy the web app URL and add it to your `.env` file as `GOOGLE_DRIVE_WEBHOOK_URL`

This will automatically upload DOCX transcriptions to a folder named "Media Downloader" in your Google Drive.

## Usage

### Option 1: Using the Shortcut

1. Double-click the "Media Downloader.lnk" shortcut file
2. The application will start automatically:
   - The Express server will start
   - The Vite development server will start
   - Your browser will open to the application

3. To pin the shortcut to your taskbar:
   - Right-click on the "Media Downloader.lnk" file
   - Select "Pin to taskbar"

### Option 2: Manual Start

1. Start the Express server:
   ```
   npm run server
   ```

2. In a separate terminal, start the Vite development server:
   ```
   npm run dev
   ```

3. Open your browser to http://localhost:5175

## How to Use

1. Enter a URL from YouTube, Vimeo, or another supported platform
2. Select the desired format:
   - **Video**: Download the video in high quality
   - **Audio**: Extract just the audio as MP3
   - **Text**: Transcribe the audio to text using OpenAI Whisper
3. Click the Download/Transcribe button
4. Once processing is complete, click the download link to access your file

## Deploying to Replit

To deploy this application to Replit:

1. Create a new Replit project
2. Import this repository or upload the files
3. Set up the environment variables in the Replit Secrets tab:
   - Add `OPENAI_API_KEY` with your OpenAI API key
   - Add `GOOGLE_DRIVE_WEBHOOK_URL` with your Google Apps Script web app URL
4. Modify the server.js file to use Replit's environment:
   ```javascript
   const port = process.env.PORT || 3001;
   ```
5. Update the start command in the `.replit` file:
   ```
   run = "npm run server"
   ```
6. Click "Run" to start the application

### Setting Up Replit Webhooks

You can set up Replit to automatically trigger actions when files are created:

1. In your Replit project, go to the "Tools" tab
2. Select "Webhooks"
3. Create a new webhook that triggers on file creation events
4. Set the webhook URL to your Google Drive webhook endpoint
5. Configure the webhook to filter for specific file types (e.g., .docx)

This will allow your Replit app to automatically send files to Google Drive whenever they are created.

## Text Transcription Options

The application provides two methods for text transcription:

1. **OpenAI Whisper (Recommended)**: 
   - High-quality AI-powered transcription
   - Requires an OpenAI API key in the `.env` file
   - Works with any video, regardless of whether it has subtitles

2. **YouTube Subtitles (Fallback)**:
   - Used automatically if Whisper transcription fails
   - No API key required
   - Only works for videos that have subtitles
   - Quality depends on the original subtitles

The app will automatically try Whisper first, and if that fails (e.g., due to missing API key), it will fall back to using YouTube subtitles if available.

## Troubleshooting

- **Text transcription not working**: 
   - Make sure you've added your OpenAI API key to the `.env` file or Replit Secrets
   - If you don't have an OpenAI API key, make sure the video has subtitles for the fallback method to work
   - Some videos may not have subtitles available, in which case you'll need to use Whisper
- **Download errors**: Some videos may be restricted or require authentication
- **Server not starting**: Make sure ports 3001 and 5175 are available (not applicable on Replit)
- **Google Drive integration not working**: Verify your webhook URL is correct and the Google Apps Script has the necessary permissions

## License

This project is open source and available under the MIT License.
