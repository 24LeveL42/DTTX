# ⬡ TACMAP — Military Tabletop Exercise Map

A real-time collaborative tactical map for tabletop exercises.  
Participants scan a QR code to move their unit — no clustering, no touching other people's pieces.

---

## 🚀 Quick Deploy (GitHub Pages)

1. **Fork or upload** these files to a GitHub repo
2. Go to **Settings → Pages → Deploy from branch → main / root**
3. Your app is live at: `https://yourusername.github.io/your-repo/`

---

## 🔧 Firebase Setup (Required for multi-device sync)

Takes ~2 minutes:

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. **Create project** (name it anything)
3. Click **"Build" → "Realtime Database" → "Create database"**
   - Choose region (any)
   - **Start in test mode** (for exercises; you can secure it later)
4. Go to **Project Settings → General → Your apps → Add app → Web (</>) **
5. Register app, copy the **firebaseConfig** JSON object
6. Paste that JSON into TACMAP's setup screen

---

## 📋 How to Run an Exercise

### Host (Command Center)
1. Open `index.html` on a large display
2. Paste Firebase config and start session
3. Add your units (name, callsign, icon)
4. Click **QR CODES** — print or display them
5. Use **NEXT TURN** to advance turns in order

### Participants
1. Scan their unit's QR code with any phone browser
2. Wait for their turn (banner glows green)
3. Drag their icon to new position
4. Tap **CONFIRM MOVE**

---

## 🗺 Map Image (Optional)

To use your own map image instead of the default tactical overlay:

1. Host your map image (or add it to the repo)
2. In `index.html`, find the comment `// Background terrain (simple procedural map)`
3. Load your image:
```js
mapImg = new Image();
mapImg.src = 'your-map.jpg';  // or full URL
mapImg.onload = draw;
```

Best results: JPG/PNG, same aspect ratio as your display.

---

## 🔒 Security (For real exercises)

Before going live with sensitive exercises, update Realtime Database rules:

```json
{
  "rules": {
    "$session": {
      ".read": true,
      "units": {
        "$unitId": {
          ".write": true
        }
      },
      "turn": {
        ".write": false
      },
      "meta": {
        ".write": false
      }
    }
  }
}
```

---

## 📁 Files

| File | Purpose |
|------|---------|
| `index.html` | Command center (host display) |
| `player.html` | Participant view (via QR) |
| `README.md` | This file |

---

## 💡 Tips

- **Large display**: Open `index.html` on a projector or big screen
- **QR codes**: Print one per participant, or show on a tablet to scan
- **Demo mode**: No Firebase needed, single-device testing only
- **Admin can drag too**: Host can reposition any unit at any time
- **Turn order**: Click any unit in the sidebar to jump to their turn

---

Built for military tabletop exercises. No app install required — pure browser.
