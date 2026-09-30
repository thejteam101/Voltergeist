# Privacy Policy — Voltergeist



**App:** Voltergeist

**Developer:** TheJTeam

**Effective date:** 1 October 2026

## Summary


Voltergeist does not collect your data. The developer — TheJTeam — operates no servers, receives no information about you or your usage of this app, and earns nothing from your personal information. All processing described below happens on your own device or on services you choose to connect (your Hue bridge, your Apple Music account, your Spotify account, and so on). Where data leaves the device at all, it goes to services you control, not to the developer.

## 1. Who We Are

Voltergeist is developed and published by **TheJTeam**, an independent developer based in the **United Kingdom**.

Because there is no server infrastructure, there is no data stored on the developer's systems to request, correct, or delete. All mechanisms for exercising your rights are described in Section 9.

## 2. The Short Version



| What | Where processed | Leaves your device? |
| --- | --- | --- |
| Camera frames (Doorstep Counter) | On-device Neural Engine | Never, by default |
| Visitor counts and group sizes | On-device (UserDefaults) | Over local mesh only, if enabled |
| Time-lapse video (opt-in) | On-device / your Photos library | Never uploaded |
| Diagnostics recording (developer screen) | On-device only | Never |
| Microphone audio | On-device (live analysis only) | Never |
| App settings and preferences | On-device (UserDefaults, App Group) | Never |
| Keychain secrets (Hue, Spotify, Home Assistant, Kids Mode PIN) | Device Keychain / iCloud Keychain | Never to developer |
| Hue bridge name and IP address | Your iCloud Private Database (optional) | To Apple iCloud only |
| Spotify playback (if connected) | Spotify's servers, under your account | To Spotify only |
| Apple Music (if used) | Apple's servers, under your Apple ID | To Apple only |
| WeatherKit forecast (when enabled) | Apple's servers | To Apple only, approximate location |
| Home Assistant commands | Your own Home Assistant server | To your own server only |
| Live Activity push token (if server configured) | Your self-hosted HTTPS server | To your own server only |
| Mesh peer communication | Local network (TLS-PSK encrypted) | Other Voltergeist devices on your LAN only |
| On-device AI help (Foundation Models) | On-device only | Never |
| Diagnostics logs | On-device only | Never |

## 3. Data the App Processes — Full Detail



### 3.1 Camera



**Doorstep Counter (default behaviour)**

When you use the Doorstep Counter, the camera captures a live video feed. Each frame is passed to Apple's Vision framework (`DetectHumanRectanglesRequest`) running on the Neural Engine on your device. Vision returns bounding rectangles; the frame itself is immediately released. The app records the *number* of people who crossed the counting line, the group size, and arrival timestamps. No image data, no face data, and no body-landmark data are stored. The counter uses human-rectangle detection only; no face-recognition or person-identification technology is used.

**Time-lapse recording (opt-in)**

If you choose to enable the time-lapse recorder in Doorstep Counter settings, the app writes HEVC video segments to the app's Application Support folder on your device. Recording begins only when you start the counter with this setting on. You may watch, share, or delete recordings from within the app. If you tap "Save to Photos", the video is added to your own Photos library; the app never reads any other media in your library. Nothing is uploaded to any server.

**Detection Diagnostics recording (developer screen)**

A developer-only screen can record a short test clip — up to five minutes — with detection overlays burnt in. Recording starts only when you tap the Record button and confirm. The file is stored in the app's container and is not uploaded.

**QR code scanning**

The camera is also used to scan QR codes on smart-device setup guides. No images are stored.

### 3.2 Microphone



The microphone is used exclusively for real-time audio analysis to drive voice-reactive lighting effects and voice modulation. Audio is analysed on-device; no audio is recorded, stored, or transmitted.

### 3.3 HomeKit



Voltergeist reads and controls HomeKit accessories via Apple's HomeKit framework. All communication happens over your local network through HomeKit's encrypted channel. Your HomeKit data is managed by Apple under your Apple ID; the developer receives none of it.

### 3.4 Philips Hue



Light commands are sent directly to your Hue bridge over your local network using HTTPS with certificate pinning (Bridge Pro) or HTTP (legacy bridges). Commands never leave your home network.

When you pair a bridge, the app may contact `discovery.meethue.com` over HTTPS to retrieve the bridge's local IP from Signify's discovery service. No personal data is sent in this request. You can also enter your bridge IP manually to avoid this call.

Hue bridge **credentials** (username and client key) are stored in the device Keychain, optionally synced via iCloud Keychain. They are never written to CloudKit records. If you enable iCloud sync, the bridge's **name** and **IP address** (not credentials) are stored in a CloudKit Private Database record visible only to you via your own Apple ID.

### 3.5 Govee



Light commands are sent via UDP broadcast to Govee devices on your local network. No data leaves your home network. An optional Govee API key may be stored in the Keychain for potential future cloud features; no cloud calls are made by the current version of the app.

### 3.6 Nanoleaf



Light commands are sent to Nanoleaf panels over your local network via their HTTP API. Nanoleaf auth tokens are stored in the device Keychain. No data leaves your home network.

### 3.7 Home Assistant



If you enable the Home Assistant integration, you supply the URL of your own Home Assistant instance and a long-lived access token. The app sends light-control commands to that URL. Your access token is stored in the device Keychain. The developer has no access to your Home Assistant server.

### 3.8 Spotify (optional)



If you choose to connect your Spotify account, the app performs an OAuth 2.0 PKCE authentication flow via `ASWebAuthenticationSession`, exchanges and refreshes access tokens with `accounts.spotify.com`, and sends playback-state queries and commands to `[api.spotify.com/v1](https://api.spotify.com/v1)`. Spotify OAuth tokens are stored in the device Keychain. No Spotify data is forwarded to the developer.

Spotify's privacy policy applies: [spotify.com/legal/privacy-policy](https://www.spotify.com/legal/privacy-policy/)

### 3.9 Apple Music and MusicKit



If you use the Apple Music integration, playback is handled by Apple's MusicKit framework under your Apple ID. Voltergeist does not receive or store your library data.

Apple's privacy policy applies: [apple.com/legal/privacy](https://www.apple.com/legal/privacy/)

### 3.10 WeatherKit (when enabled)



The app contains code for a Halloween evening weather forecast powered by Apple WeatherKit. **This feature requires an Apple WeatherKit entitlement and an approximate-location permission; when the entitlement is not present on the installed build, no location is requested and no WeatherKit call is made.**

When the feature is active, the app requests approximate location (accurate to a few kilometres). No precise location is ever recorded or shared. The `NSLocationDefaultAccuracyReduced` key in the app's configuration ensures reduced accuracy is always used.

Apple's WeatherKit attribution is displayed in the app as required. Apple's privacy policy governs WeatherKit data: [apple.com/legal/privacy](https://www.apple.com/legal/privacy/)

### 3.11 Mesh Network (ReceiverKit / SenderKit)



Voltergeist can synchronise show state across multiple Apple devices on the same local network using Bonjour and a TLS-PSK encrypted peer-to-peer connection. When active, your device's **name** and a **vendor identifier** (Apple's `identifierForVendor`, a per-app UUID that resets on reinstall) are shared with other Voltergeist instances on the same LAN. All communication stays on your local network.

### 3.12 Live Activity push server (optional, self-hosted)



If you configure a self-hosted HTTPS server URL in Settings, the app may send your device's vendor identifier, device name, APNs push token, device role, and a household identifier (derived from the mesh pre-shared key) to your server. The server URL must use HTTPS. The developer provides no server; all data goes to an endpoint you control.

### 3.13 On-device AI / Apple Intelligence (Siri, App Intents, Foundation Models)



Voice commands via Siri, Shortcuts automation, and the conversational help assistant all run on-device via Apple's Foundation Models framework (Apple Intelligence). The app does not hold a Private Cloud Compute entitlement; queries are never sent off-device by the app. Apple's own system may route Siri requests through its infrastructure according to Apple's policies; the developer receives no part of that data.

### 3.14 Kids Mode



Kids Mode is a parental-lock feature. The exit PIN is stored as a salted SHA-256 hash in the Keychain; the plaintext PIN is never stored. Biometric authentication (Face ID, Touch ID, Optic ID) is handled entirely by the operating system; no biometric data is accessible to the app. Kids Mode is session-only and always deactivates on force-quit.

### 3.15 WatchConnectivity and watchOS



The Apple Watch companion communicates with the iPhone/iPad host via WatchConnectivity over an encrypted channel managed by the system. No data is transmitted off the Apple ecosystem.

### 3.16 Custom sound import (optional, self-hosted)



If you configure a custom sound-import server URL in Settings, the app may poll a manifest on that server and download audio files to the app's container. The server URL is under your control. No device information is sent beyond a standard HTTPS GET request.

### 3.17 Usage metrics and diagnostics logs



Performance metrics and diagnostic logs are stored on-device only. None are uploaded anywhere.

## 4. Data That Never Leaves the Device



* Camera frames (Vision processes them and discards them).


* Microphone audio (processed in real time; not stored or transmitted).


* Face data (the app does not compute face data).


* Biometric data (handled entirely by iOS; not accessible to the app).


* Kids Mode PIN plaintext.


* Usage metrics.


* Diagnostics logs.


* On-device AI responses.


* App settings and preferences.



## 5. Third-Party Services You May Choose to Connect



| Service | What Voltergeist sends | Their policy |
| --- | --- | --- |
| Philips Hue (Signify) — local bridge | Light commands over LAN | [signify.com/privacy](https://www.google.com/search?q=https://www.signify.com/en-gb/privacy) |
| Philips Hue — cloud discovery | Bridge serial number lookup at discovery.meethue.com | [signify.com/privacy](https://www.google.com/search?q=https://www.signify.com/en-gb/privacy) |
| Spotify | OAuth tokens, playback commands under your account | [spotify.com privacy](https://www.spotify.com/legal/privacy-policy/) |
| Apple Music (MusicKit) | Playback requests under your Apple ID | [apple.com/legal/privacy](https://www.apple.com/legal/privacy/) |
| HomeKit / iCloud | Light/sensor commands; Hue bridge metadata in your iCloud Private DB | [apple.com/legal/privacy](https://www.apple.com/legal/privacy/) |
| Apple WeatherKit (when enabled) | Approximate location, once per forecast fetch | [apple.com/legal/privacy](https://www.apple.com/legal/privacy/) |
| Home Assistant | Light commands to your own server | Your own server |
| Self-hosted Live Activity server | Vendor UUID, device name, APNs token | Your own server |
| Self-hosted sound-import server | Standard HTTPS GET | Your own server |

## 6. Camera and Recording — Honest Summary



| Scenario | What happens |
| --- | --- |
| Doorstep Counter running, time-lapse **off** (default) | Camera frames processed on-device by Vision and immediately discarded. Nothing is written to storage. |
| Doorstep Counter running, time-lapse **on** (opt-in) | HEVC video segments written to the app's Application Support folder on your device. You control them entirely. |
| Time-lapse "Save to Photos" | A copy is added to your own Photos library. The app never reads other photos. |
| Detection Diagnostics recording (developer screen) | A short test clip (max 5 minutes) with detection overlays stored in the app's container. Never uploaded. |

## 7. Children



Voltergeist is not directed at children under 13 (or under 16 in the EEA and UK). The app does not knowingly collect personal data from children.

**Kids Mode** is a parental-lock feature for adults who want to hand a device to a child in a restricted state. It does not enable or require any data collection from children. Parents and guardians retain full control.

## 8. Security



* Credentials are stored in the iOS Keychain, encrypted and access-controlled by the operating system.


* Hue bridge communication uses HTTPS with certificate pinning where available.


* Mesh peer communication uses TLS-PSK (Transport Layer Security with a pre-shared key).


* iCloud data (Hue bridge metadata) is stored in your CloudKit Private Database, accessible only via your Apple ID.


* The app does not send any data to the developer's servers; there are no developer servers.



## 9. Your Rights (UK GDPR / EU GDPR / CCPA)



Because the developer operates no servers and receives no personal data, there is nothing for the developer to provide access to, correct, or delete on request. To exercise all privacy rights in full:

* **Delete all on-device data:** Delete the Voltergeist app. This removes all UserDefaults, the App Group, the app container (time-lapse recordings, diagnostics logs), and the app's Keychain entries.


* **Delete iCloud data:** Settings ▸ [your name] ▸ iCloud ▸ Manage Account Storage ▸ Voltergeist → delete.


* **Revoke Spotify access:** In your Spotify account settings at [spotify.com/account/apps](https://www.spotify.com/account/apps/). Tap "Disconnect" in Voltergeist ▸ Spotify to delete local tokens.


* **Revoke Apple Music access:** iOS Settings ▸ Privacy & Security ▸ Media & Apple Music.


* **Revoke HomeKit access:** iOS Settings ▸ Privacy & Security ▸ HomeKit.


* **Delete time-lapse recordings:** Voltergeist ▸ Doorstep Counter ▸ Recordings, or the Files app.


* **Reset Kids Mode:** Settings ▸ Reset Kids Mode PIN inside the app.



UK and EEA residents may also contact the [UK Information Commissioner's Office (ICO)](https://ico.org.uk) or their national supervisory authority.

## 10. Changes to This Policy



Material changes will be noted in the App Store release notes. The effective date at the top of this document will be updated. Continued use after an effective date constitutes acceptance of the changes.

## 11. Legal Basis (UK/EU residents)



Processing of any personal data described in this policy (primarily the optional transmission of Hue bridge metadata to iCloud, and the optional transmission of a vendor UUID and APNs token to a user-configured server) is carried out on the basis of **your consent** (given when you enable iCloud sync or configure a heartbeat server) and **legitimate interest** in providing the functionality you have requested.

---

Voltergeist — © 2026 TheJTeam. All rights reserved.
