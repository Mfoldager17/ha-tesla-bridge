# Tesla Bridge for Home Assistant

[![Release](https://img.shields.io/github/v/release/Mfoldager17/ha-tesla-bridge?sort=semver)](https://github.com/Mfoldager17/ha-tesla-bridge/releases) [![Checks](https://github.com/Mfoldager17/ha-tesla-bridge/actions/workflows/checks.yml/badge.svg)](https://github.com/Mfoldager17/ha-tesla-bridge/actions/workflows/checks.yml)

The Home Assistant integration for **[Tesla Bridge](https://github.com/Mfoldager17/tesla-bridge)**, a self-hosted replacement for Teslemetry. Your car streams to your own server, and you control it through Tesla's official Fleet API, with no middleman and no subscription.

This repository is only the integration. **The bridge itself runs in Docker on your server.** Set it up first with the [Tesla Bridge guide](https://github.com/Mfoldager17/tesla-bridge#get-started).

## What it does

- Connects to the bridge on your network: `http://<server>:8090`, with the bridge's token.
- **Live, without polling.** Changes arrive over Server-Sent Events. If the connection drops, it catches up on everything that happened.
- **About 80 entities per car, named like Teslemetry's.** They cover battery and charging, climate, seat and steering wheel heat, locks, doors, windows, frunk and trunk, sentry, where the car is, and the bridge's Fleet API cost. See [all entities](https://github.com/Mfoldager17/tesla-bridge/blob/main/docs/entities.md).
- **Commands feel instant.** A lock shows *locking*, and a sleeping car shows that it is being woken up. The action waits until the car has done it, or fails with the car's own error.
- Entities become *unavailable* while the bridge is down. If the token changes, it asks for the new one.
- Its setup dialog is in English and Danish.

You don't need MQTT for this. If you would rather use MQTT, the bridge can publish the same entities through your broker instead, and then you don't need this integration at all. See [the two ways](https://github.com/Mfoldager17/tesla-bridge/blob/main/docs/4-home-assistant.md).

## Install

1. Home Assistant → **Marketplace** → **Add from link** → `https://github.com/Mfoldager17/ha-tesla-bridge`
2. Install **Tesla Bridge** and **restart Home Assistant**.
3. **Settings → Devices & services → Add integration → Tesla Bridge.**
4. Fill in:
   - **URL:** `http://<server-IP>:8090`
   - **Token:** `Bridge__Web__Token` from the bridge's `.env`. If you didn't set one, use the token the bridge made: `docker compose exec tesla-bridge cat /data/web-token`

**Without the Marketplace:** copy `custom_components/tesla_bridge` into Home Assistant's `config/custom_components/`, restart, and continue from step 3.

### Moving from the tesla-bridge repository

Up to 2.0.0, the integration was part of `Mfoldager17/tesla-bridge`. To move:

1. In the Marketplace, remove **Tesla Bridge** (`Mfoldager17/tesla-bridge`).
2. Add `https://github.com/Mfoldager17/ha-tesla-bridge` and install it (as above).
3. Restart Home Assistant.

The integration keeps its name (`tesla_bridge`), so your devices, entities, automations and dashboards stay as they are.

## Versions

The integration and the bridge have their own version numbers and their own releases:

| You update | Where | What it changes |
|---|---|---|
| **This integration** | Home Assistant → *Settings → Updates* (from the Marketplace), then restart | the entities in Home Assistant |
| **The bridge** | on your server: `docker compose pull && docker compose up -d` ([how](https://github.com/Mfoldager17/tesla-bridge/blob/main/docs/updating.md)) | the bridge, its dashboard and everything that talks to the car |

They don't have to match. A newer bridge always works with an older integration. If the integration needs a newer bridge than you run, Home Assistant shows a **repair** saying which version is needed.

The bridge's own update entity in Home Assistant (*Tesla Bridge* under *Settings → Updates*, with no install button) tells you when a new bridge is out. It is installed on the server, not in Home Assistant.

## Development

The tests run the integration in a real Home Assistant ([pytest-homeassistant-custom-component](https://github.com/MatthewFlamm/pytest-homeassistant-custom-component)) against a real bridge with its built-in simulator:

```bash
# in a clone of tesla-bridge: the bridge with the pretend car, on :8080
cd src/TeslaBridge && Bridge__Web__Token=dev-token ASPNETCORE_ENVIRONMENT=Development dotnet run

# here
pip install -r requirements_test.txt
BRIDGE_TOKEN=dev-token python -m pytest tests -v
ruff check . && ruff format --check .
```

CI does the same against tesla-bridge's `main` on every pull request and once a week. It also runs Home Assistant's `hassfest` and the Marketplace's own check.

Releases follow [release-please](https://github.com/googleapis/release-please). Commit titles like `feat:` / `fix:` become the changelog. Merging its release PR tags the version and makes the GitHub Release, which the Marketplace offers as an update. Raise `MIN_BRIDGE_VERSION` in `const.py` when the integration starts using something a newer bridge added.

## License

[MIT](LICENSE). Not affiliated with Tesla, Inc.
