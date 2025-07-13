# Review Gate V2 - Testing Guide

## Prerequisites

- Cursor IDE installed
- Extension files in `V2/cursor-extension/` folder

## Installation Steps

### 1. Remove Old Extension (IMPORTANT!)

If you previously had Review Gate V2 installed:

1. Open Cursor
2. Go to Extensions panel (Cmd/Ctrl + Shift + X)
3. Search for "Review Gate V2" or "review-gate-v2"
4. Click the gear icon → **Uninstall**
5. **Restart Cursor completely** (Quit and reopen)

### 2. Install New Extension

1. In Cursor, go to Extensions panel
2. Click the "..." menu → **Install from VSIX...**
3. Navigate to `/V2/cursor-extension/review-gate-v2-2.7.3.vsix`
4. Select the file and install
5. **Reload Window** (Cmd/Ctrl + R)

### 3. Verify Installation

Check Command Palette (Cmd/Ctrl + Shift + P) for:

- ✅ `Review Gate: Open Review Gate v2`
- ✅ `Review Gate: Toggle Sound Notifications` ← **NEW**

## Testing Features

### A. Sound Toggle Feature

1. **Via Command Palette:**

   - Open Command Palette (Cmd/Ctrl + Shift + P)
   - Type "Review Gate: Toggle Sound Notifications"
   - Execute command to toggle sound on/off

2. **Via Header Button:**

   - Open Review Gate popup (Cmd/Ctrl + Shift + R)
   - Look for volume icon in header (🔊/🔇)
   - Click to toggle sound

3. **Settings Persistence:**
   - Open Settings (Cmd/Ctrl + ,)
   - Search "Review Gate"
   - Verify "Enable Sound" checkbox matches current state

### B. Countdown Timer

1. **Auto-start Timer:**

   - Open Review Gate popup
   - Timer should show "05:00" and start counting down
   - Timer color: Gray → Orange (3 min) → Red (1 min) → Red+bold (expired)

2. **Timer Reset:**
   - Send a message in the popup
   - Timer should reset to "05:00"
   - Open popup again - timer restarts

### C. Sound Notifications

1. **Default Sound:**

   - Enable sound (if disabled)
   - Focus the popup window
   - Should hear default beep/ding sound

2. **Custom Sound (Required):**
   - Place `ding.mp3` file in `/V2/cursor-extension/` folder
   - Reload Cursor window
   - Focus popup - should play your custom sound
   - **Note:** No sound will play without ding.mp3 file

### D. MCP Integration Testing

_Note: Requires MCP server setup_

1. Configure MCP server connection
2. Open Review Gate popup
3. Verify "MCP Active" status appears in header
4. Timer should auto-start when MCP is called

## Troubleshooting

### Commands Not Appearing

- **Solution:** Uninstall old extension first, then install new .vsix
- Restart Cursor completely between uninstall/install

### Sound Not Working

- Check if sound is enabled in settings
- Verify volume icon shows 🔊 (enabled) not 🔇 (disabled)
- Try toggling sound via command palette

### Timer Not Visible

- Refresh the popup (close and reopen)
- Check browser console in popup for errors

### Custom Sound Not Playing

- Ensure `ding.mp3` is directly in `/V2/cursor-extension/` folder
- Reload Cursor window after adding file
- File must be named exactly `ding.mp3`
- **Without this file, no sound will play at all**

## Expected Behavior Summary

| Feature         | Expected Result                                                      |
| --------------- | -------------------------------------------------------------------- |
| Command Palette | Shows both "Open Review Gate v2" and "Toggle Sound Notifications"    |
| Header UI       | Volume icon (🔊/🔇) + countdown timer (05:00)                        |
| Sound Toggle    | Persists setting, updates icon, works via button or command          |
| Timer           | Auto-starts at 05:00, counts down, changes colors, resets on message |
| Sound           | Plays on focus (if enabled), requires ding.mp3 file                  |

## File Structure

```
V2/cursor-extension/
├── extension.js          # Main extension code
├── package.json          # Extension manifest with commands
├── icon.png             # Extension icon
├── ding.mp3            # Required sound file for notifications
└── review-gate-v2-2.7.3.vsix  # Installable package
```

## Version Info

- **Package Version:** 2.7.3
- **Features Added:** Sound toggle, countdown timer, custom sound support
- **VS Code Engine:** ^1.60.0
