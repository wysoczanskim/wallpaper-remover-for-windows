# How to clear the wallpaper path and sets a solid color background on user login

This is a quick Windows scripting task:

## Step 1 — Create the Script

1. Open **Notepad**
2. Paste this:
```powershell
# Set background color to black (RGB 0,0,0)
Set-ItemProperty -Path "HKCU:\Control Panel\Colors" -Name Background -Value "0 0 0"

# Remove wallpaper
Set-ItemProperty -Path "HKCU:\Control Panel\Desktop" -Name Wallpaper -Value ""

# Apply changes immediately
RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
```

3. Save as `black-wallpaper.ps1` — make sure to change "Save as type" to **All Files**, otherwise Notepad adds `.txt` to the end

The `Background` registry value `0 0 0` sets the solid color to pure black.

## Step 2 — Add to Task Scheduler

1. Press `Win`, search **Task Scheduler**, open it
2. Click **Create Basic Task** on the right
3. Name it something like `Black Wallpaper`
4. Trigger: **When I log on** → Next
5. Action: **Start a program** → Next
6. Fill in:
    - **Program:** `powershell.exe`
    - **Arguments:** `-WindowStyle Hidden -ExecutionPolicy Bypass -File "C:\Users\YourName\black-wallpaper.ps1"`
    - Replace `YourName` with your actual Windows username
7. Click **Finish**

No admin prompt, no visible window on startup.

## Step 3 — Test It

Before rebooting, right-click your new task in Task Scheduler → **Run**. Your wallpaper should go black immediately. If it works, you're done — it'll run automatically every login.


