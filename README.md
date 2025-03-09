# KGHFS - Grandstream HTTP Firmware Server

## Overview
KGHFS (Grandstream HTTP Firmware Server) is a Python-based HTTP server designed to manage and serve firmware files for Grandstream devices. It dynamically provides the appropriate firmware to requesting devices, checks for the latest firmware versions, and downloads updates when required.

## Features
- **HTTP Server for Firmware Distribution**: Serves firmware files dynamically based on device requests.
- **Automatic Firmware Version Detection**: Extracts model details from the User-Agent header.
- **Firmware Version Comparison**: Checks local firmware versions and compares them with the latest available online versions.
- **Automatic Firmware Updates**: Downloads and extracts the latest firmware for supported Grandstream devices.
- **Supports Multiple Models**: Maintains a mapping of model names to firmware families.
- **Verbose Logging**: Provides detailed logs when enabled.
- **Efficient File Handling**: Uses progress indicators for downloads and ensures efficient file serving.
- **Supports Parallel Processing**: Runs the HTTP server in a separate thread for better performance.

## How It Works
1. **Device Requests Firmware**: The Grandstream device sends a GET request to `http://server-ip/firmware-file.bin`.
2. **Model Detection**: The server extracts the model name from the User-Agent header.
3. **Version Matching**: Checks the latest firmware version available locally and compares it with the online version.
4. **Firmware Delivery**: If the requested file exists, it is served to the device.
5. **Automatic Updates**: If the local version is outdated, the user can run `-U` to update.

## Requirements
- **Python 3.7+**
- **Required Python Modules:**
  - `requests`
  - `argparse`
  - `http.server`
  - `threading`
  - `zipfile`
  - `tqdm`
  - `re`

## Installation
1. Clone the repository or download `kghfs.py`.
2. Install the required dependencies:
   ```sh
   pip install requests tqdm
   ```
3. Run the script:
   ```sh
   python kghfs.py -h
   ```

## Usage
### Start HTTP Firmware Server
```sh
python kghfs.py
```
By default, the server runs on port `80` and serves firmware files from the `Firmware/` directory.

### Enable Verbose Mode
```sh
python kghfs.py -V
```
Provides additional logging for debugging and monitoring purposes.

### Check and Download Latest Firmware
```sh
python kghfs.py -U
```
Prompts for a Grandstream model name and downloads the latest firmware if available.

### Print Version Information
```sh
python kghfs.py -v
```
Displays the current version of KGHFS.

## Example Output
```
[VERBOSE] Requested path: /grp2600fw.bin
[VERBOSE] Extracted Model: GRP2601P
[VERBOSE] Local firmware version: 1.0.5.60
[VERBOSE] Latest firmware version: 1.0.5.71
Downloading latest firmware...
```

## Supported Devices
The script supports a wide range of Grandstream models, including but not limited to:
- GRP2601, GRP2602, GRP2603, GRP2612, GRP2613, GRP2614, GRP2615, GRP2616
- WP810, WP820, WP822, WP825
- UCM6301, UCM6302, UCM6304, UCM6308

## Future Improvements
- Add HTTPS support for secure firmware distribution.
- Implement a configuration file for customizable settings.
- Provide a web interface for easier management.

## License
This project is developed for internal use and is not licensed for commercial redistribution.
