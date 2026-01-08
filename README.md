# Year View Calendar

A single-file HTML application that displays your Google Calendar in a continuous year-grid view with weekend alignment and all-day event spanning.

## Features

- **Full Year View**: See the entire year in a single continuous grid
- **Weekend Alignment**: Weekends always align vertically (columns 6-7) with distinct styling
- **Event Spanning**: All-day events span across the days they occupy
- **Simple Setup**: Just paste your Google Calendar's iCal feed URL (no API keys needed!)
- **Multiple Weeks Per Row**: Compact cells show many weeks on wide screens

## Quick Start (Recommended: iCal Feed Method)

### 1. Get Your Google Calendar iCal Feed URL

1. Go to [Google Calendar](https://calendar.google.com/)
2. On the left sidebar, find the calendar you want to use
3. Click the three dots (⋮) next to the calendar name
4. Select **"Settings and sharing"**
5. Scroll down to the **"Integrate calendar"** section
6. Find **"Secret address in iCal format"** (or just "Calendar address" if it's a public calendar)
7. Copy the URL (it will look like: `https://calendar.google.com/calendar/ical/.../basic.ics`)

**Note**: If you only see "Public address" and not "Secret address", you can:
- Make the calendar public temporarily to get the public address, OR
- Share the calendar with "Make available to public" and copy that URL

### 2. Use the Calendar

1. Open `index.html` in your web browser
2. Paste the iCal feed URL into the input field
3. Click "Load Calendar"
4. Select the year you want to view
5. Your events will appear on the calendar!

The URL will be saved in your browser, so you won't need to paste it again next time.

## Alternative Setup (OAuth Method)

If you prefer to use OAuth authentication instead of iCal feeds:

### 1. Get Google OAuth Client ID

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the Google Calendar API:
   - Navigate to "APIs & Services" > "Library"
   - Search for "Google Calendar API"
   - Click "Enable"
4. Create OAuth 2.0 credentials:
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" > "OAuth client ID"
   - If prompted, configure the OAuth consent screen:
     - Choose "External" (unless you have a Google Workspace)
     - Fill in required fields (App name, User support email, Developer contact)
     - Add your email as a test user
   - For Application type, choose "Web application"
   - Name it (e.g., "Year View Calendar")
   - Under "Authorized JavaScript origins", add:
     - `http://localhost`
     - `http://127.0.0.1`
     - `file://` (if opening HTML directly)
   - Under "Authorized redirect URIs", add:
     - `http://localhost`
     - `http://127.0.0.1`
   - Click "Create"
5. Copy the **Client ID** (looks like: `xxxxx.apps.googleusercontent.com`)

### 2. Configure the HTML File

1. Open `index.html` in a text editor
2. Find the line near the top of the `<script>` section:
   ```javascript
   const CLIENT_ID = 'YOUR_CLIENT_ID_HERE.apps.googleusercontent.com';
   ```
3. Replace `YOUR_CLIENT_ID_HERE.apps.googleusercontent.com` with your actual Client ID
4. Save the file

### 3. Use the Application

**Option A: Open directly in browser**
- Double-click `index.html` or open it in your browser
- Note: Some browsers may block the Google Sign-In popup when opening from `file://` protocol
- If this happens, use Option B

**Option B: Use a local web server (Recommended)**

Using Python 3:
```bash
# Navigate to the project directory
cd /path/to/YearView

# Start a simple HTTP server
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

Using Node.js (if you have it):
```bash
# Install http-server globally (one time)
npm install -g http-server

# Start the server
http-server -p 8000
```

Then open `http://localhost:8000` in your browser.

### 4. Sign In and Use

1. Click "Sign in with Google"
2. Select your Google account (if you're already logged in, it will use that session)
3. Grant calendar read permissions
4. Select a calendar from the dropdown
5. Optionally change the year using the year selector
6. View your all-day events displayed across the year grid!

## How It Works

- **iCal Feed Method** (Recommended): Simply fetches your calendar's iCal feed directly - no authentication needed!
- The calendar displays all 365/366 days of the year in a continuous grid
- Weekends (Saturday and Sunday) are always aligned in the same columns, with a distinct gray gradient
- Months flow continuously without visual breaks
- Only all-day events are displayed (timed events are not shown)
- Multi-day events span across all the days they occupy
- Small 35px-wide cells allow multiple weeks to fit on the same row on wide screens
- Your iCal URL and year preference are saved in browser localStorage

## Troubleshooting

**"Failed to load calendar" error:**
- Make sure the iCal URL is correct and accessible
- Try opening the URL directly in your browser - it should show ICS file content
- Check if the calendar is set to "Public" or if you're using the "Secret address"
- Some calendars may require the calendar to be publicly accessible

**Events not showing:**
- Only all-day events are displayed (timed events are filtered out)
- Make sure your events are within the selected year
- Try refreshing the page and loading the calendar again

**CORS errors (blocked by browser):**
- If you see CORS errors, you may need to use a CORS proxy or serve the file from a web server
- Try using a local web server: `python3 -m http.server 8000` then open `http://localhost:8000`

**Weekends not aligning:**
- Weekends should automatically align in columns 6 (Saturday) and 7 (Sunday)
- The grid is calculated based on the first day of the year

**Calendar loads but shows old data:**
- Google Calendar caches iCal feeds. Changes may take a few minutes to appear
- Try adding `?nocache=` + timestamp to the URL to force refresh

## Privacy

- All authentication happens through Google's official OAuth flow
- The access token is stored only in your browser's localStorage
- No data is sent to any server except Google's API
- All processing happens locally in your browser

## License

Free to use and modify for personal use.
