# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Home Assistant custom integration for Tuya BLE devices. Provides local BLE connectivity while requiring Tuya cloud credentials for device setup. Community-maintained fork tracking pull requests while original maintainer PlusPlus-ua is offline.

## Architecture

- **Integration Entry Point**: `custom_components/tuya_ble/__init__.py` - Sets up platforms and manages device lifecycle
- **Device Communication**: `custom_components/tuya_ble/tuya_ble/` subdirectory contains core BLE protocol implementation
- **Cloud Integration**: `cloud.py` handles Tuya IoT API for device credentials and metadata
- **Platform Modules**: Separate files for each Home Assistant platform (sensor, switch, climate, etc.)
- **Device Categories**: Support for fingerbots, sensors, locks, climate devices based on category_id mapping

## Key Implementation Details

The integration uses a coordinator pattern in `devices.py` with `TuyaBLECoordinator` managing device state updates. Device discovery happens via Bluetooth service UUID `0000a201-0000-1000-8000-00805f9b34fb`.

Each device requires:
- BLE address for local connection
- Device ID and encryption key from Tuya cloud
- Product category mapping in device definitions

Platform entities are created dynamically based on device capabilities defined in the `tuya_ble` module.

## Dependencies

- `tuya-iot-py-sdk==0.6.6` for cloud API
- Home Assistant bluetooth integration
- `bleak-retry-connector` for BLE reliability

## Installation

HACS-compatible integration. No build process - files are deployed directly to `custom_components/tuya_ble/` in Home Assistant configuration.