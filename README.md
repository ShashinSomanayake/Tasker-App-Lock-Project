# Tasker-App-Lock-Project
A comprehensive, biometric‑protected app locker built with Tasker for Android. It locks selected apps and sensitive system settings behind a beautiful, animated lock screen that supports fingerprint / PIN authentication.

📖 Description

This Tasker project turns your Android device into a fully customizable application locker.
When you try to open a protected app (WhatsApp, TikTok, Telegram, Reddit, Instagram, etc.) or enter critical system areas (Developer Options, Device Administrators, or Tasker’s own settings), a full‑screen lock scene appears.
The scene features a modern glass‑morphism design with floating animations, a pulsing fingerprint sensor, and a subtle 3D tilt effect that reacts to device orientation.

Authentication is handled by Android’s native biometric prompt (fingerprint / face) or a fallback PIN.
If authentication succeeds, the lock screen fades out and you gain access.
If it fails, a notification is shown and, optionally, the front camera takes a photo of the intruder (the “thief” feature).
The lock also automatically re‑enables itself after a configurable timeout and can be triggered manually via a quick settings tile or a dedicated task.

Behind the scenes, the project uses:

Logcat Event profiles to detect when protected settings are opened.

Application context profiles to intercept the launch of specified apps.

Display Off and Shutdown profiles to re‑lock everything when the screen turns off or the device is about to shut down.

Scenes with embedded HTML/JavaScript to present the lock UI, complete with smooth enter/exit animations and direct communication with Tasker tasks.

Tasks that show the lock scene, wait for biometric/PIN input, handle timeouts, and toggle profiles on/off.

All protected apps and settings are easily customizable inside Tasker – you can add or remove packages without touching a single line of code. The lock screen’s appearance can also be tweaked by editing the inline CSS inside the scene.

Originally shared on Reddit, this project has evolved into a polished, production‑ready app locker that works on any Android device with Tasker installed. It respects your privacy (no data leaves your device) and gives you fine‑grained control over which apps and system panels are protected.

✨ Features

Lock any app – just add its package name to the profile.

Protect system settings – Developer Options, Device Admin list, Tasker preferences.

Biometric + PIN authentication – uses Android’s native prompt.

Beautiful animated lock screen – glass card, floating icon, rotating glow, fingerprint sensor animation.

Auto‑relock on screen off or device shutdown.

Intruder selfie – takes a photo if authentication fails (optional).

Manual lock/unlock – via a dedicated task (can be assigned to a home screen widget or Quick Tile).

Timeout – lock automatically re‑enables after a set time.

Fully customizable – add apps, change colors, animations, timeout, etc.

📋 Requirements

Tasker (latest version recommended) – Google Play

Android 5.0+ (Logcat permissions may require ADB or root on some devices)

For biometric authentication: device with fingerprint/face hardware and enrolled credentials

🔧 Installation

Import the project

Copy the provided XML code.

In Tasker, long‑press the “Home” icon → Import → Import Project → paste the XML.

Grant necessary permissions

Logcat permission (for settings‑lock profiles):

On Android 9+, run this ADB command once:
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_LOGS

Alternatively, root users can grant via a root shell.

Display over other apps permission for the lock scene.

Customize the app list (optional)

Edit the profile “Tasker Lock (Apps Lock)” and add/remove applications under the App tab.

Enable the profiles

All profiles are disabled by default after import. Enable them one by one or use the All Profiles On task.

Test

Open a protected app or a settings page – the lock screen should appear.

⚙️ How It Works

Profiles
Profile Name	Trigger	Action
Tasker Lock (Apps Lock)	Launch of any selected app	Runs App Lock task
Developer Settings Lock	Logcat entry ~RDevelopmentSettings	Runs App Lock task
Administrative Apps Lock	Logcat entry ~RDeviceAdminSettings	Runs App Lock task
Tasker Settings Lock	Logcat entry from Tasker’s AppLocaleUtil	Runs App Lock task
Lock All On Display Off	Display OFF	Runs All Profiles On
Lock All On Shutdown	Device shutdown	Runs All Profiles On
Tasks
App Lock – Shows the lock scene (App Lock Check), then waits for biometric/PIN input.

On success: turns off all lock profiles (so you can use the app/settings), shows success notification, then re‑enables profiles after a timeout (configurable via Applock Time task).

On failure/cancel: shows failure notification, optionally takes a photo (task thief), and keeps the lock scene active.

All Profiles On / Off – Enables/disables all four lock profiles.

Destroy App Lock Scene – Smoothly closes the lock screen without unlocking.

Manual App Lock – Turns on the app‑lock profile manually.

Scene

The lock screen is a WebView element with embedded HTML/CSS/JS. It includes:

A glass card with animated glowing border.

A large lock icon that runs the App Lock task when tapped.

A fingerprint‑sensor graphic that also triggers authentication.

JavaScript that calls tasker.run('App Lock') to re‑trigger authentication.

Smooth fade‑out animation (animatedDestroy()) when unlocking.

🎨 Customization

Adding/removing apps
Go to Profiles → Tasker Lock (Apps Lock).

Tap the App context (the one with the app list).

Use the + / – buttons to add or remove apps by package name.

Changing lock timeout
Edit the Applock Time task – it asks for minutes. Modify the default value or the logic.

Adjusting the lock screen design
Open the scene App Lock Check.

Tap the WebView element and edit the HTML/CSS inside.
You can change colors, animations, text, or even replace the whole layout.

Intruder selfie
In the App Lock task, locate the action “Take Camera Photo” (code 101).
Uncomment or enable it if you want it to run on failed attempts.

📜 License
This project is licensed under the MIT License.
You are free to use, modify, and distribute it, provided that you include the original copyright notice.

🙏 Credits
Original idea and initial implementation by u/FM_tasks on Reddit.
Enhanced and polished by the community.
Built with Tasker – the most powerful automation tool for Android.

🚀 Contributing
Found a bug or have a feature request? Feel free to open an issue or submit a pull request on GitHub.

📱 Screenshots
(Include images of the lock screen, profile list, and task list here)

Enjoy your secured device! 🔒
