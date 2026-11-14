# Changelog

## [2.1.0](https://github.com/Mfoldager17/ha-tesla-bridge/compare/v2.0.0...v2.1.0) (2026-11-14)


### Features

* Bluetooth through an ESP32 – free commands and wake-ups while the car is home ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* **dashboard:** new dashboard with 3D car, controls, data, usage, settings and setup ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* **dashboard:** telemetry intervals per field with a live cost estimate ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* entities show when they wait for the car (pending / waiting_for, wake-up icon) ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* guided setup script (install.sh) and automatic partner domain registration ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* Home Assistant integration without MQTT, with an embedded broker as alternative ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* **integration:** actions wait for the car like Teslemetry and show the car's error ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* interactive setup guide website and step-by-step docs ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* reverse proxy or tunnel (e.g. Cloudflare Tunnel), any certificate folder, Nginx Proxy Manager not required ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* seat and steering-wheel heat turn the climate on first (optional) ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* **security:** token always on, MQTT and ESP32 logins, hardened containers, review fixes ([bfda378](https://github.com/Mfoldager17/ha-tesla-bridge/commit/bfda37814c66f6ab6b362e726d46594210f27d48))
* **security:** token always on, MQTT and ESP32 logins, hardened containers, review fixes ([793fd84](https://github.com/Mfoldager17/ha-tesla-bridge/commit/793fd843665647cc35f5220bac61c23a4accbdd3))
* versioned releases with a changelog, release channels and update notices ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))


### Bug fixes

* a renewed Tesla token is kept when the disk is full; container logs are capped ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))
* parked car – invalid gear becomes P, invalid speed 0, invalid range keeps the last value ([842e7c8](https://github.com/Mfoldager17/ha-tesla-bridge/commit/842e7c813a733487b02335b4bc85d6bc76684e9e))


### Documentation

* new screenshots with the map, and Dependabot for every dependency ([c4d8a8b](https://github.com/Mfoldager17/ha-tesla-bridge/commit/c4d8a8bdb1f323aaf65ca98c1216ba5293150216))

## 2.0.0 (2026-11-14)

The integration now lives in its own repository and has its own releases. Until 2.0.0 it was part of [tesla-bridge](https://github.com/Mfoldager17/tesla-bridge), whose [changelog](https://github.com/Mfoldager17/tesla-bridge/blob/main/CHANGELOG.md) has the history up to here.

### ⚠ BREAKING CHANGES

* install it from this repository: in Home Assistant, remove the old *Tesla Bridge* entry (`Mfoldager17/tesla-bridge`) from the Marketplace and add `https://github.com/Mfoldager17/ha-tesla-bridge`. Your devices, entities and automations stay as they are.
