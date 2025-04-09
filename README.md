# Obscenity Remover

=======================================
= Chrome Extension - NLP Text Filter =
=======================================

A local Chrome extension that filters out unwanted words from webpages using a custom dictionary and a native Python backend. Supports masking or removing words, site whitelisting, and password-protected settings.

----------------------
| Features           |
----------------------

- [x] Filters webpage text in real-time  
- [x] Uses a local JSON dictionary  
- [x] Supports word masking or removal  
- [x] Works only on whitelisted websites  
- [x] Native Python backend via Chrome native messaging  
- [x] Password-protected settings interface  

----------------------
| Installation Steps |
----------------------

1. Clone or download this repository  
2. Open Chrome and navigate to: `chrome://extensions`  
3. Enable "Developer mode" (toggle at the top right)  
4. Click "Load unpacked" and select the `extension/` folder  
5. Copy the Extension ID shown under your extension  
6. Edit `native_host/com.obscenity.remover.json`:
   - Replace `<YourExtensionID>` with the actual Extension ID  
   - Replace the `path` field with the full path to `filter.py` on your system  
7. Register the native host:
   - **Windows**: create and run a `.reg` file pointing to `com.obscenity.remover.json`  
   - **macOS**: copy the JSON file to `~/Library/Application Support/Google/Chrome/NativeMessagingHosts/`  
   - **Linux**: copy the JSON file to `~/.config/google-chrome/NativeMessagingHosts/`  
8. Ensure Python is installed (`python --version`)  
9. Restart Chrome  

----------------------
| Using the Extension |
----------------------

- The extension activates only on websites listed in the whitelist  
- To configure settings:
  - Right-click the extension icon → Options  
  - Or go to `chrome://extensions`, click "Details" → "Extension Options"  
- Enter the password (default: `admin`) to access settings  
- Add or remove websites to the whitelist  
- Add or remove words from the dictionary  
- Choose between `mask` (replace with #) or `remove`  
- Click "Save Changes"  
- Refresh any open page to apply the new filters  

------------------------
| Native Messaging Note |
------------------------

- Communication between Chrome and the Python script is done via Chrome’s native messaging API  
- Python script reads and writes JSON messages over `stdin` and `stdout`  
- Only your extension can talk to the Python backend (locked via `allowed_origins`)  
- All filtering is done locally  

--------------------
| Dictionary Format |
--------------------

The dictionary file `dictionary.json` uses this format:

```json
{
  "words": [
    { "text": "spoiler", "type": "mask" },
    { "text": "NSFW", "type": "remove" }
  ]
}
```

--------------------
| Example Behavior  |
--------------------

Input:  
`This contains a spoiler and NSFW content.`

Output:  
`This contains a ####### and content.`

-----------------
| Security Note |
-----------------

- Password stored locally  
- All filtering is offline  
- Native host locked to extension ID  

--------------------
| Future Features  |
--------------------

- Auto-update on dynamic content  
- Regex optimization  
- Optional UI themes  

----------------------
| License & Credits  |
----------------------

- Open source  
- Built using Chrome Extensions + Python  
- NLP flexible and extendable  