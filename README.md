# OpenAI Realtime Embedded SDK

## Table of Contents

- [Platform Support](#platform-support)
- [Installation](#installation)
- [Usage](#usage)

## Platform Support

This SDK supports the following hardware:

**Primary Target (Default):**
* [M5Stack AtomS3R](https://shop.m5stack.com/products/atoms3r-dev-kit) with [Atomic Echo Base](https://shop.m5stack.com/products/atomic-echo-base)

**Also Supported:**
* [Freenove ESP32-S3-WROOM](https://www.amazon.com/gp/product/B0BMQ8F7FN)
* [Sonatino - ESP32-S3 Audio Development Board](https://www.amazon.com/gp/product/B0BVY8RJNP)

You can get ESP32-S3 boards for less on eBay/AliExpress.

## Installation

### Prerequisites

1. Install [PlatformIO](https://platformio.org/install)
2. Initialize git submodules:
   ```bash
   git submodule update --init --recursive
   ```

### Environment Variables

Set your credentials as environment variables:
```bash
export WIFI_SSID="your_wifi_ssid"
export WIFI_PASSWORD="your_wifi_password"
export OPENAI_API_KEY="sk-your-api-key"
```

### Build

**For M5Stack AtomS3R (default):**
```bash
pio run -e m5stack-atoms3r
```

**For generic ESP32-S3:**
```bash
pio run -e esp32s3
```

### Flash

```bash
pio run -e m5stack-atoms3r -t upload
```

### Monitor

```bash
pio device monitor
```

### All-in-one (build, flash, monitor)

```bash
pio run -e m5stack-atoms3r -t upload -t monitor
```

## Usage
