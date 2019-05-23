# ios-toolbox
A list of tools to help iOS developers on daily basis

### Deeplinks
Easily test deeplink on simulator from CLI

```
xcrun simctl openurl booted "{DEEPLINK}"
```

Example:
```
xcrun simctl openurl booted "my_app://path/to/view"
```

### Push Notifications

Trigger remote push notification from curl request to test your application.

```
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
```
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
```
curl -v \
-d '{"aps":{"content-available":1}, "key":"value"}' \
-H "apns-topic:com.yourcompanyname.yourappname" \
-H "apns-expiration: 1" \
-H "apns-priority: 10" \
--http2 \
--cert certfile.pem:1234 \
https://api.development.push.apple.com/3/device/123456789
```
