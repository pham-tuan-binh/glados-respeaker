# GLaDOS Voice Assistant on ReSpeaker Lite Kit

This project integrates the iconic voice of GLaDOS from Portal into your smart home by deploying it on a ReSpeaker Lite Kit using ESPHome and Home Assistant.

## Overview

This project turns a ReSpeaker Lite Kit from Seeed Studio into a voice assistant that responds in the voice of GLaDOS from the Portal games. It uses:

- **Home Assistant** - For handling voice commands and automation
- **ESPHome** - For firmware and integration with Home Assistant
- **microWakeWord** - For lightweight wake word detection
- **Piper** - For text-to-speech in the style of GLaDOS
- **Google Generative AI** - For LLM
- **Whisper** - For speech-to-text

## Hardware Requirements

- [ReSpeaker Lite Kit](https://www.seeedstudio.com/ReSpeaker-Lite-Voice-Assistant-Kit-Full-Kit-of-2-Mic-Array-pre-soldered-XIAO-ESP32S3-Mono-Enclosed-Speaker-and-Enclosure.html?sensecap_affiliate=3gToNR2&referring_service=link) from Seeed Studio
- USB Type-C Cable with Data Transfer Capabilities

_If you don't have the ReSpeaker Lite kit yet, consider buying from my link above. It helps me a lot, building and compiling these resources. Also, if you want to buy anything from Seeed, this is my coupon: 5EB420ZS_

## Software Requirements

- [Home Assistant](https://www.home-assistant.io/)
- Assist Pipeline configured in Home Assistant

## Assist Pipeline Configuration

For setting up Assist with ReSpeaker Lite, this guide is ultra helpful: [Local Voice Assistant With Seeed Studio ReSpeaker Lite](https://smarthomecircle.com/local-voice-assistant-with-seeed-studio-respeaker-lite). I don't find the need to rewrite everything in this repository, besides, the above guide links to a comprehensive video.

However, there are a few things that are different, which I'll list below.

## Piper Voice Configuration

To use the custom GLaDOS voice, you should put the **.onnx and .onnx.json** file in /piper directory of this repository into /share/piper of your Home Assistant setup. After putting it there, a restart and you should be able to find GLaDOS in **American Language** category in Text-To-Speech configuration of Piper in Assist.

The GLaDOS voice was not trained by me, but from this [awesome work of dnhkng](https://github.com/dnhkng/GLaDOS).

## GLaDOS Wake Word Integration and Custom RGB

The ESPHome **base yaml** for ReSpeaker Lite can be found in the /esphome/common directory of this repository. You need to put this file into the /config/esphome/common directory of your Home Assistant set up.

Using this base yaml, you can easily setup any ReSpeaker Lite device with this simple yaml:

```yaml
packages:
  respeaker-satellite: !include common/respeaker-satellite-base.yaml

esphome:
  name: respeaker-satellite
  friendly_name: GLaDOS

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

You can set up wifi_ssid and wifi_password using the secret tab.

## Credits

This project stands on the shoulders of these amazing open-source projects:

- [Respeaker-Lite-ESPHome-integration](https://github.com/formatBCE/Respeaker-Lite-ESPHome-integration/tree/main) - ESPHome template for ReSpeaker
- [GLaDOS Voice](https://github.com/dnhkng/GLaDOS) - GLaDOS voice model for TTS
- [microWakeWord](https://github.com/kahrendt/microWakeWord) - Lightweight wake word detection

## License

This project is released under the MIT License. See the LICENSE file for details.

---

_Note: Aperture Science does not guarantee that the Genetic Lifeform and Disk Operating System will not flood your home with deadly neurotoxin. Please proceed at your own risk._
