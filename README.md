<h2>Features</h2>
<ul>
<li><strong>3 rooms, 4 lights + 1 fan each</strong> — tap a tile to toggle</li>
<li><strong>Swipe left / right</strong> (or UP / DOWN buttons) to switch rooms</li>
<li><strong>OK button</strong> = turn off everything in the current room</li>
<li><strong>Fan control</strong> — tap card for on/off, <code>−</code> / <code>+</code> for speed, 4-step speed bar</li>
<li><strong>Room temperature &amp; humidity</strong> from any Home Assistant sensor</li>
<li><strong>Battery %</strong> and charging status from the on-board BQ27220 fuel gauge</li>
<li><strong>Material Design Icons</strong> — the same icon set Home Assistant uses</li>
<li><strong>Deep sleep on battery</strong> — wakes when you pick it up (IMU) or press OK</li>
<li>Fast partial ePaper refresh, with a full clean-up every 30th frame</li>
</ul>
<h2>Hardware</h2>
<table>
<thead>
<tr>
<th>Part</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr>
<td>Device</td>
<td>Seeed Studio reTerminal Sticky</td>
</tr>
<tr>
<td>MCU</td>
<td>ESP32-S3, 32 MB flash</td>
</tr>
<tr>
<td>Display</td>
<td>3.97" ePaper, 800×480 (used as 480×800 portrait)</td>
</tr>
<tr>
<td>Touch</td>
<td>GT911</td>
</tr>
<tr>
<td>On-board sensors used</td>
<td>SHT40 (temp/humidity), LSM6DS3TR-C (wake-on-motion), BQ27220 (battery), PCF8563 (RTC)</td>
</tr>
</tbody>
</table>
<h2>Requirements</h2>
<ul>
<li>Home Assistant with the ESPHome integration</li>
<li>ESPHome <strong>2025.x or newer</strong> (needs the <code>epaper_spi</code> platform with the <code>seeed-reterminal-sticky</code> model)</li>
<li>Light and fan entities already in Home Assistant</li>
</ul>
<h2>Setup</h2>
<ol>
<li><strong>Clone the repo</strong>
   <code>bash
   git clone https://github.com/techiesms/reTerminal-Sticky-HA-Panel.git
   cd reTerminal-Sticky-HA-Panel</code></li>
<li><strong>Add your secrets</strong>
   <code>bash
   cp secrets.example.yaml secrets.yaml</code>
   Fill in Wi-Fi, API key and OTA password. Generate an API key at <a href="https://esphome.io/components/api.html">esphome.io/components/api</a>.</li>
<li><strong>Set your entities</strong> — open <code>reterminal-sticky-panel.yaml</code> and edit the <code>substitutions:</code> block:</li>
<li>Room names (<code>room1</code> … <code>room3</code>)</li>
<li>Light, fan, temperature and humidity entity IDs (find them in <strong>Developer Tools → States</strong>)</li>
<li>Tile labels (keep them ~10 characters)</li>
<li><strong>Flash over USB</strong> (first time)
   <code>bash
   esphome run reterminal-sticky-panel.yaml</code></li>
<li><strong>Allow Home Assistant actions</strong> — in Home Assistant go to
   <strong>Settings → Devices &amp; services → ESPHome → reTerminal Sticky → Configure</strong> and enable
   <strong>"Allow the device to perform Home Assistant actions"</strong>. Without this, taps do nothing.</li>
</ol>
<h2>Controls</h2>
<table>
<thead>
<tr>
<th>Action</th>
<th>Result</th>
</tr>
</thead>
<tbody>
<tr>
<td>Tap a light tile</td>
<td>Toggle that light</td>
</tr>
<tr>
<td>Tap the fan card</td>
<td>Fan on / off</td>
</tr>
<tr>
<td>Tap <code>−</code> / <code>+</code></td>
<td>Fan slower / faster</td>
</tr>
<tr>
<td>Swipe left / right, or UP / DOWN</td>
<td>Previous / next room</td>
</tr>
<tr>
<td>Tap the header</td>
<td>Next room</td>
</tr>
<tr>
<td>OK button</td>
<td>Turn off all lights + fan in this room</td>
</tr>
</tbody>
</table>
<h2>Battery &amp; sleep</h2>
<ul>
<li>On battery the panel sleeps after <strong>45 s</strong> of no activity (change <code>awake_seconds</code>).</li>
<li>The ePaper keeps the last image while asleep and shows <em>"Sleeping – lift me or press OK"</em>.</li>
<li>It <strong>never sleeps while charging</strong> or when the <strong>Stay Awake</strong> switch is on.</li>
</ul>
<blockquote>
<p><strong>Before a wireless (OTA) update:</strong> turn on <strong>Stay Awake</strong> in Home Assistant or plug in USB — otherwise the device may sleep mid-update.</p>
</blockquote>
<h2>Troubleshooting</h2>
<table>
<thead>
<tr>
<th>Problem</th>
<th>Fix</th>
</tr>
</thead>
<tbody>
<tr>
<td>Taps beep but nothing switches</td>
<td>Enable "Allow the device to perform Home Assistant actions" (step 5)</td>
</tr>
<tr>
<td>Tiles show <code>--</code> or <code>Unavailable</code></td>
<td>Check the entity IDs in <code>substitutions</code></td>
</tr>
<tr>
<td>Screen is upside down</td>
<td>Change <code>rotation: 90</code> to <code>270</code></td>
</tr>
<tr>
<td>Battery never charges</td>
<td>Make sure <code>charge_enable</code> is on at boot (it's active-LOW)</td>
</tr>
<tr>
<td>Device switches off completely</td>
<td>GPIO45/46 power latch must stay HIGH — don't remove those outputs</td>
</tr>
</tbody>
</table>
<h2>Video</h2>
<p>Full build and walkthrough on the <a href="https://youtu.be/qoTz3yT_c4g?si=U-FWFm9rBf3kyYN-">techiesms YouTube channel</a>.</p>
<h2>Links</h2>
<ul>
<li>Store: <a href="https://techiesms.com">techiesms.com</a></li>
<li>Courses: <a href="https://techiesms.graphy.com">techiesms.graphy.com</a></li>
</ul>
<h2>License</h2>
<p>MIT — see <a href="LICENSE">LICENSE</a>.</p>
