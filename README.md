# ios-toolbox 🧰
A list of tools to help iOS developers on daily basis

### CLI Tools 🛠

* [fastlane](https://docs.fastlane.tools/) - The easiest way to automate beta deployments and releases for your iOS and Android apps.
* [ios-deploy](https://github.com/ios-control/ios-deploy) - Install and debug iOS apps from the command line. Designed to work on un-jailbroken devices.
* [libimobiledevice](https://github.com/libimobiledevice/libimobiledevice) - A cross-platform protocol library to communicate with iOS devices.
* [SwiftInfo](https://github.com/rockbruno/SwiftInfo) - Extract and analyze the evolution of an iOS app's code.

### Deeplinks 🔗
Easily test deeplink on simulator from CLI

```sh
xcrun simctl openurl booted "{DEEPLINK}"
```

Example:
```sh
xcrun simctl openurl booted "my_app://path/to/view"
```

### Push Notifications 📬

Trigger remote push notification from curl request to test your application.

```sh
curl -v \
-d '{"aps":{"alert":"test","sound":"default"}}' \
-H "apns-topic:$BUNDLE" \
-H "apns-expiration: 1" \
-H "apns-priority: 10" \
--http2 \
--cert $PATH_TO_PEM_FILE:$PASSPHRASE \
https://api.development.push.apple.com/3/device/$DEVICE_TOKEN
```
* `$BUNDLE` to replace with your bundle app
* `$PATH_TO_PEM_FILE` to replace with path to your pem file
* `$PASSPHRASE` to replace with your passphrase used with your pem file
* `$DEVICE_TOKEN` to replace with the device token you want to target

Note that you can replace `https://api.development.push.apple.com` with `https://api.push.apple.com` for production test.

Example:

__Default notification__

```sh
curl -v \
-d '{"aps":{"alert":"test","sound":"default"}}' \
-H "apns-topic:com.yourcompanyname.yourappname" \
-H "apns-expiration: 1" \
-H "apns-priority: 10" \
--http2 \
--cert certfile.pem:1234 \
https://api.development.push.apple.com/3/device/123456789
```

__Silent notification__

```sh
curl -v \
-d '{"aps":{"content-available":1}, "key":"value"}' \
-H "apns-topic:com.yourcompanyname.yourappname" \
-H "apns-expiration: 1" \
-H "apns-priority: 10" \
--http2 \
--cert certfile.pem:1234 \
https://api.development.push.apple.com/3/device/123456789
```
