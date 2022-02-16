# Grauninha

Servidor comunitário Grauninha, parte do projeto Grauna que também conta com o coletor de sites Grauna Memória.
## Getting Started

You can one-click-deploy this project to balena using the button below:

[![deploy-with-balena](https://balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com//Instituto-Nupef/grauninha&defaultDeviceType=intel-nuc)

## Manual Deployment

Alternatively, deployment can be carried out by manually creating a [balenaCloud account](https://dashboard.balena-cloud.com) and application, flashing a device, downloading the project and pushing it via the [balena CLI](https://github.com/balena-io/balena-cli).

### Application Environment Variables

Application envionment variables apply to all services within the application, and can be applied fleet-wide to apply to multiple devices.

| Name           | Description                                                                                                       |
| -------------- | ----------------------------------------------------------------------------------------------------------------- |
| `TZ`           | Inform services of the [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) in your location. |
| `SET_HOSTNAME` | Set a custom hostname on application start. Default is `grauna`.                                               |

## Usage

  Once your device joins the fleet you'll need to allow some time for it to download the various services.

  When it's done you should be able to access the access the dashboard at <http://grauna.local>.

  Services run in following ports:
  - Nginx Proxy Manager: <http://grauna.local:81>
  - Jellyfin: <http://grauna.local:82>
  - Filebrowser: <http://grauna.local:83>
  - Kolibri: <http://grauna.local:84>
  - Kiwix: <http://grauna.local:85>
  - Nextcloud: <http://grauna.local:86>
  - MeTube: <http://grauna.local:87>
  - Portal: <http://grauna.local:88>
  - PiHole: <http://grauna.local:89>
  - Resilio-Sync: <http://grauna.local:8888>

  Create mappings using Nginx Proxy Manager to have custom domains. Ex.: jellyfin.grauna.local

## Contributing

Please open an issue or submit a pull request with any features, fixes, or changes.
