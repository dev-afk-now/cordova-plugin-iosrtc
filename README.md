WebRTC is [now available in all major browsers](https://caniuse.com/#search=webrtc), including Android and iOS. However, when it comes to WebViews outside the browser, things are not so rosy. As of iOS 12.2, Apple still doesn't have getUserMedia() supported in Standalone Web Apps and similar contexts outside Safari. The iOS 13 beta briefly supported it, and [Google's team even congratulated Apple](https://twitter.com/QbixApps/status/1156664231825047552) but they pulled it.

This cordova plugin is designed to be a drop-in replacement allowing you to use getUserMedia() in your websites AND cordova apps. It combines several techniques, capturing [native camera feeds](https://webrtc.org/native-code/ios/) and sending them over a local WebRTC connection ([SDP with no signaling server](https://en.wikipedia.org/wiki/Session_Description_Protocol)) to the local WebView, which then receives it as an actual [MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream) object you can use. From there, the actual [WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API) is supported, including sending MediaStreams. You can also send it via WebSocket to be [streamed live to Facebook or YouTube using RMTP](https://github.com/Qbix/Canvas-Streaming-Example).

[Here is a demo video](https://twitter.com/i/status/1156664231825047552) of the plugin working, delivering a MediaStream with a ~100ms delay in a Cordova app on an iPad.

This plugin is part of Qbix's Cordova project, to help Web developers build apps that work everywhere. We maintain these plugins for our [Qbix Platform](https://github.com/Qbix/Platform), an open source operating system for building apps that out of the box can support integration with contacts, notifications, payments, videoconferencing, and much more. Focus on building your app, not wrestling with platforms.

## Requirements

In order to make this Cordova plugin run into a iOS application some requirements must be satisfied in both development computer and target devices:

* Xcode >= 7.2.1
* iOS >= 9 (run on lower versions at your own risk, but don't report issues)
* `cordova-ios` 4.X


## Installation

Within your Cordova project:

```bash
$ cordova plugin add https://github.com/Qbix/cordova-plugin-iosrtc.git
```

(or add it into a `<plugin>` entry in the `config.xml` of your app).

## Building

* [Building](docs/Building.md): Guidelines for building a Cordova iOS application including the *cordova-plugin-iosrtc* plugin.
* [Building `libwebrtc`](docs/BuildingLibWebRTC.md): Guidelines for building Google's *libwebrtc* with modifications needed by the *cordova-plugin-iosrtc* plugin (just in case you want to use a different version of *libwebrtc* or apply your own changes to it).

## Usage

The plugin exposes the `cordova.plugins.iosrtc` JavaScript namespace which contains all the WebRTC classes and functions.

```javascript
// Just for Cordova apps.
var pc = new cordova.plugins.iosrtc.RTCPeerConnection({
  iceServers: []
});

MediaDevices.getUserMedia = cordova.plugins.iosrtc.getUserMedia;

```

And that's all. It's supposed to be a drop-in replacement.

## Who Uses It

[People and companies](WHO_USES_IT.md) using *cordova-plugin-iosrtc*.

If you are using the plugin we would love to [hear back from you](https://qbix.com/about)!

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).

**Credit**

This plugin was initially developed at eFace2Face, and later maintained by the community, including:
* [Saúl Ibarra Corretgé](http://bettercallsaghul.com) (_The OpenSource Warrior Who Does Not Burn_).
* [Iñaki Baz Castillo](https://inakibaz.me/) (no longer active maintainer)
* [Saúl Ibarra Corretgé](http://bettercallsaghul.com) (no longer active maintainer)

It has now been forked is being maintained by Qbix, Inc.

## License

[MIT](./LICENSE) :)
