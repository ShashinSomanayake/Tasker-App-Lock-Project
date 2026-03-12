<h1 align="center">🔒 Tasker Advanced App Locker</h1>

<p align="center">
A powerful <b>Tasker automation project</b> that turns your Android device into a fully customizable <b>application locker</b>.
</p>

<hr>

<h2>📖 Description</h2>

<p>
This Tasker project turns your Android device into a <b>fully customizable application locker</b>.
When you try to open a protected app
(<i>WhatsApp, TikTok, Telegram, Reddit, Instagram, etc.</i>) or enter critical system areas
(<b>Developer Options, Device Administrators, or Tasker’s own settings</b>),
a <b>full-screen lock scene</b> appears.
</p>

<p>
The scene features a modern <b>glass-morphism design</b> with floating animations,
a pulsing fingerprint sensor, and a subtle <b>3D tilt effect</b> that reacts to device orientation.
</p>

<p>
Authentication is handled by Android’s <b>native biometric prompt</b>
(fingerprint / face) or a fallback <b>PIN</b>.
If authentication succeeds, the lock screen fades out and access is granted.
If it fails, a notification is shown and optionally the front camera captures an
<b>intruder selfie</b>.
</p>

<p>
The lock automatically re-enables itself after a configurable timeout and can also
be triggered manually via a <b>Quick Settings tile</b> or a dedicated Tasker task.
</p>

<hr>

<h2>⚙️ Behind the Scenes</h2>

<p>The project uses several Tasker automation mechanisms:</p>

<ul>
<li><b>Logcat Event profiles</b> to detect when protected settings are opened.</li>
<li><b>Application context profiles</b> to intercept launches of protected apps.</li>
<li><b>Display Off and Shutdown profiles</b> to automatically relock everything.</li>
<li><b>Scenes with embedded HTML/JavaScript</b> to present a smooth animated lock UI.</li>
<li><b>Tasks</b> that manage authentication, timeouts, and profile control.</li>
</ul>

<p>
All protected apps and settings are <b>fully customizable</b> inside Tasker.
You can add or remove packages without touching code.
The lock screen appearance can also be modified by editing the inline CSS in the scene.
</p>

<p>
Originally shared on Reddit, this project has evolved into a
<b>polished production-ready app locker</b> that works on any Android device with Tasker installed.
</p>

<p>
It respects your privacy — <b>no data ever leaves your device</b>.
</p>

<hr>

<h2>✨ Features</h2>

<ul>
<li>🔐 Lock any app by adding its package name</li>
<li>⚙️ Protect system settings (Developer Options, Device Admin, Tasker preferences)</li>
<li>👆 Biometric + PIN authentication</li>
<li>🎨 Beautiful animated lock screen (glass card, glow, fingerprint animation)</li>
<li>🔁 Auto-relock when screen turns off or device shuts down</li>
<li>📸 Intruder selfie capture on failed authentication</li>
<li>🧩 Manual lock/unlock via Quick Settings or Tasker task</li>
<li>⏱ Configurable timeout before relocking</li>
<li>🛠 Fully customizable UI and protected apps list</li>
</ul>

<hr>

<h2>📋 Requirements</h2>

<ul>
<li><b>Tasker</b> (latest version recommended)</li>
<li><b>Android 5.0+</b></li>
<li>Logcat permission (ADB or root may be required on newer Android versions)</li>
<li>Device with biometric hardware for fingerprint/face authentication</li>
</ul>

<hr>

<h2>🔧 Installation</h2>

<h3>1️⃣ Import the Project</h3>

<ol>
<li>Copy the provided XML code.</li>
<li>Open Tasker.</li>
<li>Long-press the <b>Home</b> icon.</li>
<li>Select <b>Import Project</b>.</li>
<li>Paste the XML.</li>
</ol>

<h3>2️⃣ Grant Permissions</h3>

<p><b>Logcat permission</b> (needed for settings protection):</p>

<pre><code>adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_LOGS</code></pre>

<p>
Root users can grant this permission via a root shell instead.
</p>

<p>
Also enable <b>Display over other apps</b> permission for Tasker.
</p>

<h3>3️⃣ Customize Apps (Optional)</h3>

<p>
Edit the profile <b>"Tasker Lock (Apps Lock)"</b> and add or remove apps
from the App context list.
</p>

<h3>4️⃣ Enable Profiles</h3>

<p>
All profiles are disabled after import. Enable them manually or run the
<b>"All Profiles On"</b> task.
</p>

<h3>5️⃣ Test</h3>

<p>
Open a protected app or settings panel.  
The lock screen should appear immediately.
</p>

<hr>

<h2>⚙️ How It Works</h2>

<h3>Profiles</h3>

<table>
<tr>
<th>Profile Name</th>
<th>Trigger</th>
<th>Action</th>
</tr>

<tr>
<td>Tasker Lock (Apps Lock)</td>
<td>Protected app launch</td>
<td>Runs App Lock task</td>
</tr>

<tr>
<td>Developer Settings Lock</td>
<td>Logcat ~RDevelopmentSettings</td>
<td>Runs App Lock task</td>
</tr>

<tr>
<td>Administrative Apps Lock</td>
<td>Logcat ~RDeviceAdminSettings</td>
<td>Runs App Lock task</td>
</tr>

<tr>
<td>Tasker Settings Lock</td>
<td>Logcat entry from Tasker</td>
<td>Runs App Lock task</td>
</tr>

<tr>
<td>Lock All On Display Off</td>
<td>Screen turned off</td>
<td>Runs All Profiles On</td>
</tr>

<tr>
<td>Lock All On Shutdown</td>
<td>Device shutdown</td>
<td>Runs All Profiles On</td>
</tr>

</table>

<hr>

<h3>Tasks</h3>

<p><b>App Lock</b></p>
<ul>
<li>Displays the lock scene</li>
<li>Waits for biometric or PIN authentication</li>
</ul>

<p><b>On Success</b></p>
<ul>
<li>Temporarily disables lock profiles</li>
<li>Shows success notification</li>
<li>Re-enables lock profiles after timeout</li>
</ul>

<p><b>On Failure</b></p>
<ul>
<li>Shows failure notification</li>
<li>Optionally takes an intruder photo</li>
<li>Keeps lock screen active</li>
</ul>

<hr>

<h3>Scene</h3>

<p>
The lock interface is a <b>WebView-based scene</b> using embedded HTML, CSS and JavaScript.
</p>

<p>It includes:</p>

<ul>
<li>Glass-morphism lock card</li>
<li>Animated glowing border</li>
<li>Interactive fingerprint sensor</li>
<li>Floating lock icon</li>
<li>Smooth fade-out unlock animation</li>
</ul>

<p>
JavaScript communicates with Tasker tasks using:
</p>

<pre><code>tasker.run('App Lock')</code></pre>

<hr>

<h2>🎨 Customization</h2>

<h3>Adding or Removing Apps</h3>

<ol>
<li>Open <b>Profiles → Tasker Lock (Apps Lock)</b></li>
<li>Tap the <b>App context</b></li>
<li>Add or remove packages</li>
</ol>

<h3>Changing Lock Timeout</h3>

<p>
Edit the <b>Applock Time</b> task and modify the timeout value.
</p>

<h3>Changing Lock Screen Design</h3>

<ol>
<li>Open scene <b>App Lock Check</b></li>
<li>Edit the WebView HTML/CSS</li>
<li>Modify colors, layout, animations</li>
</ol>

<h3>Intruder Selfie</h3>

<p>
Enable the <b>Take Camera Photo</b> action in the <b>App Lock</b> task
if you want intruder capture.
</p>

<hr>

<h2>📜 License</h2>

<p>
This project is licensed under the <b>MIT License</b>.
You are free to use, modify and distribute it with proper attribution.
</p>

<hr>

<h2>🙏 Credits</h2>

<ul>
<li>Original concept by <b>u/FM_tasks</b> on Reddit</li>
<li>Improved and polished by the community</li>
<li>Built with <b>Tasker</b>, the most powerful Android automation tool</li>
</ul>

<hr>

<h2>🚀 Contributing</h2>

<p>
Found a bug or want to add a feature?
Feel free to open an issue or submit a pull request on GitHub.
</p>

<hr>

<h2 align="center">📱 Screenshots</h2>

<p align="center">
<img src="screenshots/lockscreen.png" width="300">

</p>

<p align="center">
<b>Enjoy your secured device! 🔒</b>
</p>
