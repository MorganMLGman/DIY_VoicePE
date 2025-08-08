# DIY VoicePE

A DIY alternative to the popular [VoicePE](https://github.com/esphome/home-assistant-voice-pe) speaker using ESP32-S3 and ESPHome.

## Overview

<p>
<img width="200" alt="DIY Voice Full View" src="assets/photo_3_2025-02-14_18-01-07.jpg">
<img width="200" alt="DIY Voice LED Ring On" src="assets/photo_2_2025-02-14_18-01-07.jpg">
<img width="200" alt="DIY Voice LED Ring Off" src="assets/photo_1_2025-02-14_18-01-07.jpg">
<img height="150" alt="DIY Voice Gif" src="assets/20250214_175500(1).gif">
</p>

This project provides an open-source, customizable voice assistant device that integrates with Home Assistant. Build your own voice-controlled smart home device with visual feedback and high-quality audio processing.

## Features

- 🎤 **High-quality voice recognition** using digital microphone (INMP441)
- 🔊 **Clear audio output** with MAX98357A amplifier
- 💡 **Visual feedback** with customizable LED ring (WS2812B)
- 🏠 **Home Assistant integration** via ESPHome
- 🔧 **Fully customizable** configuration and behavior
- 📱 **OTA updates** for easy maintenance

## Hardware Requirements

### Core Components
- ESP32-S3 development board (e.g., ESP32-S3-DevKitC-1)
- INMP441 digital microphone
- MAX98357A I2S amplifier
- Speaker (4-8 ohm, 3-5W recommended)
- WS2812B LED ring (12 LEDs)

### Pin Configuration
| Component | ESP32-S3 Pin |
|-----------|--------------|
| Microphone SD | GPIO15 |
| Microphone WS | GPIO14 |
| Microphone SCK | GPIO13 |
| Speaker DIN | GPIO10 |
| Speaker LRC | GPIO7 |
| Speaker BCLK | GPIO8 |
| LED DI | GPIO21 |

## Quick Start

### 1. Prerequisites
- [ESPHome](https://esphome.io/) 2025.5.1 or later
- [Home Assistant](https://www.home-assistant.io/) instance
- USB-C cable for programming

### 2. Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/MorganMLGman/DIY_VoicePE.git
   cd DIY_VoicePE
   ```

2. **Install ESPHome:**
   ```bash
   pip install esphome
   ```

3. **Validate configuration:**
   ```bash
   esphome config diy-voicepe-esp32-s3.yaml
   ```

4. **Build and upload:**
   ```bash
   esphome run diy-voicepe-esp32-s3.yaml
   ```

### 3. Configuration

1. Connect to the device's Wi-Fi hotspot after first boot
2. Configure your Wi-Fi credentials
3. Add the device to Home Assistant
4. Configure voice assistant settings in Home Assistant

## Customization

The configuration can be customized by editing `diy-voicepe-esp32-s3.yaml`. Key areas for customization:

- **LED behavior**: Modify light effects and colors
- **Audio settings**: Adjust volume levels and sound files
- **Pin assignments**: Change GPIO pins to match your hardware
- **Voice assistant settings**: Configure wake words and responses

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed development guidelines.

### Project Structure
```
DIY_VoicePE/
├── diy-voicepe-esp32-s3.yaml          # Main ESPHome configuration
├── diy-voicepe-esp32-s3.factory.yaml  # Factory reset configuration
├── assets/                             # Documentation images
├── sounds/                             # Audio files for responses
└── static/                             # Static website files
```

## Troubleshooting

### Common Issues

**Device not connecting to Wi-Fi:**
- Check Wi-Fi credentials in configuration
- Ensure 2.4GHz network is available
- Try factory reset configuration

**Audio quality issues:**
- Check speaker connections and impedance
- Verify I2S pin assignments
- Adjust audio gain settings

**LED not working:**
- Verify WS2812B data pin connection
- Check power supply to LEDs
- Confirm LED count in configuration

### Getting Help

- Check [existing issues](https://github.com/MorganMLGman/DIY_VoicePE/issues)
- Join the [ESPHome Discord](https://discord.gg/KhAMKrd)
- Review [ESPHome documentation](https://esphome.io/)

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [ESPHome](https://esphome.io/) for the amazing platform
- [Home Assistant Voice PE](https://github.com/esphome/home-assistant-voice-pe) for inspiration
- The open-source community for continuous improvements
