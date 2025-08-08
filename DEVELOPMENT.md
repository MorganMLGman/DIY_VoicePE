# Development Guide

This guide provides detailed information for developers working on the DIY VoicePE project.

## Architecture Overview

The DIY VoicePE is built on ESPHome, which provides a YAML-based configuration system for ESP32 devices. The main components include:

### Core Components

1. **Voice Assistant Pipeline**
   - Microphone capture (I2S INMP441)
   - Audio processing and streaming
   - Voice assistant integration with Home Assistant

2. **Audio Output**
   - I2S DAC (MAX98357A) for speaker output
   - Sound file playback for system responses
   - Volume control and audio routing

3. **Visual Feedback**
   - WS2812B LED ring for status indication
   - Dynamic lighting effects based on assistant state
   - Customizable color schemes

4. **Connectivity**
   - Wi-Fi for Home Assistant communication
   - OTA updates for firmware management
   - Web server for configuration

## Configuration Structure

### Main Configuration File: `diy-voicepe-esp32-s3.yaml`

```yaml
substitutions:          # Pin definitions and constants
esphome:               # Device identification and boot logic
esp32:                 # Hardware platform configuration
wifi:                  # Network connectivity
api:                   # Home Assistant API
ota:                   # Over-the-air updates
web_server:            # Configuration web interface
```

### Factory Configuration: `diy-voicepe-esp32-s3.factory.yaml`

Simplified configuration for initial device setup and factory reset scenarios.

## Pin Mapping

| Function | GPIO | Component | Notes |
|----------|------|-----------|-------|
| Mic SD | 15 | INMP441 Data | I2S data line |
| Mic WS | 14 | INMP441 Word Select | Left/Right channel |
| Mic SCK | 13 | INMP441 Clock | I2S clock |
| Speaker DIN | 10 | MAX98357A Data | I2S data to DAC |
| Speaker LRC | 7 | MAX98357A LRC | Word select |
| Speaker BCLK | 8 | MAX98357A Clock | Bit clock |
| LED DI | 21 | WS2812B Data | LED control signal |

## Development Environment Setup

### Prerequisites

1. **Python Environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install esphome
   ```

2. **Development Tools**
   ```bash
   # Optional but recommended
   pip install pre-commit
   pre-commit install
   ```

### Building and Testing

1. **Validate Configuration**
   ```bash
   esphome config diy-voicepe-esp32-s3.yaml
   ```

2. **Compile Firmware**
   ```bash
   esphome compile diy-voicepe-esp32-s3.yaml
   ```

3. **Upload to Device**
   ```bash
   esphome upload diy-voicepe-esp32-s3.yaml
   ```

4. **Monitor Logs**
   ```bash
   esphome logs diy-voicepe-esp32-s3.yaml
   ```

## Voice Assistant States

The device implements several states for voice assistant operation:

| State ID | State Name | LED Behavior | Description |
|----------|------------|--------------|-------------|
| 1 | Idle | Dim breathing | Waiting for wake word |
| 2 | Waiting | Solid color | Ready for command |
| 3 | Listening | Pulsing | Recording voice command |
| 4 | Thinking | Spinning | Processing command |
| 5 | Replying | Speaking pattern | Playing response |
| 10 | Not Ready | Slow pulse | Connecting/initializing |
| 11 | Error | Red flash | Error state |

## Customization Guidelines

### Adding New LED Effects

1. Define the effect in the `light` section:
   ```yaml
   light:
     - platform: neopixel
       effects:
         - name: "Custom Effect"
           addressable_rainbow:
             name: Rainbow
             speed: 10
             width: 50
   ```

2. Update the control script to use the new effect:
   ```yaml
   script:
     - id: control_leds
       then:
         - if:
             condition:
               # Your condition here
             then:
               - light.turn_on:
                   id: led_ring
                   effect: "Custom Effect"
   ```

### Adding Sound Files

1. Place audio files in the `sounds/` directory
2. Define them in the configuration:
   ```yaml
   http_request:
     # existing config
   
   globals:
     - id: custom_sound
       type: std::string
       initial_value: '"sounds/custom.mp3"'
   ```

3. Use in scripts:
   ```yaml
   script:
     - id: play_custom_sound
       then:
         - http_request.get:
             url: !lambda return id(custom_sound);
   ```

### Hardware Modifications

When changing hardware components:

1. Update pin assignments in `substitutions` section
2. Modify component configurations as needed
3. Test thoroughly on actual hardware
4. Update documentation and pin mapping tables

## Debugging

### Common Debug Scenarios

1. **Audio Issues**
   - Check I2S pin connections
   - Verify speaker impedance and power
   - Monitor audio logs for clipping/distortion

2. **Microphone Problems**
   - Validate I2S microphone connections
   - Check audio gain settings
   - Test with simple audio capture

3. **LED Issues**
   - Verify data pin connection
   - Check power supply to LED strip
   - Test with simple color commands

4. **Connectivity Problems**
   - Monitor Wi-Fi signal strength
   - Check Home Assistant connectivity
   - Verify API key configuration

### Log Analysis

Enable detailed logging for debugging:

```yaml
logger:
  level: DEBUG
  logs:
    voice_assistant: DEBUG
    audio: DEBUG
    wifi: INFO
```

## Testing Procedures

### Unit Testing

1. **Configuration Validation**
   - YAML syntax checking
   - Component compatibility verification
   - Pin assignment validation

2. **Hardware Testing**
   - Individual component functionality
   - I2S audio pipeline testing
   - LED pattern verification

3. **Integration Testing**
   - Home Assistant connectivity
   - Voice assistant pipeline
   - OTA update functionality

### Performance Testing

- Memory usage monitoring
- Audio latency measurement
- Wi-Fi stability testing
- Power consumption analysis

## Release Process

1. **Version Tagging**
   - Follow semantic versioning
   - Update configuration version references
   - Create release notes

2. **CI/CD Pipeline**
   - Automated firmware building
   - Artifact publishing
   - Documentation deployment

3. **Quality Assurance**
   - Hardware testing on reference design
   - Compatibility verification
   - Performance regression testing

## Contributing Guidelines

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines, including:

- Code style standards
- Pull request process
- Issue reporting guidelines
- Community standards