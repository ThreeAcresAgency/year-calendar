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


## How It Works

- Simply fetches your calendar's iCal feed directly - no authentication needed!
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

- No authentication required - uses public iCal feeds
- All data processing happens locally in your browser
- Your iCal URL is stored only in your browser's localStorage
- No data is sent to any server except when fetching the iCal feed

## License

Free to use and modify for personal use.
