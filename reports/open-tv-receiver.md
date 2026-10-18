# Open TV Receiver: experimental AirPlay receiver for Android TV

Open TV Receiver is an experimental GPL-3.0 derivative of [jqssun/android-airplay-server](https://github.com/jqssun/android-airplay-server), using UxPlay and Android native media components. It targets iPhone/iPad screen mirroring on Android TV, including testing on Xiaomi Mi Box and Google TV devices.

No added advertisements, accounts, billing, subscriptions or artificial session-duration limit. This is an independent project, not an Apple-certified product. Device compatibility remains unconfirmed.

## Installation readiness

Test build: **0.1.1-test2**, version code **31**. Package: `local.mibox.receiver`.

| Check | Result |
| --- | --- |
| Minimum Android | Android 7.0 / API 24 |
| APK v2 signature and content digest | PASS |
| APK ZIP integrity | PASS |
| ARM32 and ARM64 native libraries | PASS |
| Android TV launcher | Present |
| Touchscreen | Optional |
| Physical Mi Box 4 installation | NOT RUN |
| Real iPhone AirPlay playback | NOT RUN |

APK SHA-256: `a7cea09cb5ce680221e93bd560b9e3445601372e121497026bd96c4e010d817b`.

Artifact checks indicate suitability for an installation attempt on an ARM Mi Box running Android 7.0 or newer. They do not prove physical-device installation or working AirPlay.

## Connection and installation

1. Check the TV's Android version.
2. Transfer the test APK to a USB drive and open it with a TV file manager. Allow installation from that file manager when prompted.
3. Launch **Open TV Receiver** and start the receiver.
4. Connect the iPhone/iPad and TV to the same local network.
5. Open iPhone Control Center → Screen Mirroring and look for **Open TV Receiver**.

Discovery and audio/video use the local IP network. Bluetooth pairing is not the screen-mirroring transport. Wi-Fi client isolation, VPNs and multicast filtering can prevent discovery. Peer-to-peer AirPlay is not promised.

Direct Photos JPEG/HEIC and MP4/MOV sharing must be tested separately from screen mirroring. DRM-protected streaming is unsupported.

## Testing status

The existing feature report records 45 checks: 19 PASS, 1 FAIL, 2 FIXED, 2 PARTIAL and 21 NOT RUN. Build, lint, APK inspection, PIN entropy tests and emulator installation/UI checks passed. The synthetic OPTIONS probe returned an empty response; that inconclusive failure does not establish real AirPlay compatibility.

Physical discovery, PIN pairing, H.264/HEVC mirroring, direct Photos sharing, audio sync, network recovery and long sessions still need real sender/receiver tests.

## Community contributions

Compatibility reports should include app version, TV model, Android version, sender model, iOS version, exact steps and separate PASS/FAIL/NOT RUN results for each feature. State test duration. Remove Wi-Fi names, addresses, credentials, device identifiers and personal media from attachments.

Search terms: Android TV AirPlay receiver, Xiaomi Mi Box, Google TV, iPhone screen mirroring, iPad, open source, no ads.

## Source and downloads

The sanitized source package, installation guide and detailed evidence are prepared, but are **not yet hosted in this repository**. This page publishes the project report only; no public APK download or full source repository is claimed. Do not build or download binaries from this report alone.

Upstream base: android-airplay-server v0.0.30, revision `1fa1d609afdae9042be07ec430591339b8583e15`. Preserve upstream attribution, GPL licensing and complete corresponding source when distributing binaries.
