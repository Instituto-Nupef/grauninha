# Grauninha
ADAPTAR PARA VERSAO BASEADA NA @@ _ PROJETO SOCIAL BOND


[![Balena Release](https://github.com/Instituto-Nupef/grauninha/actions/workflows/balena-tag-release.yml/badge.svg)](https://github.com/Instituto-Nupef/grauninha/actions/workflows/balena-tag-release.yml)

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
  - WiFi Connect: <http://grauna.local:8080>
  - Nginx Proxy Manager: <http://grauna.local:8081>
  - Jellyfin: <http://grauna.local:8082>
  - Filebrowser: <http://grauna.local:8083>
  - Kolibri: <http://grauna.local:8084>
  - Kiwix: <http://grauna.local:8085>
  - MeTube: <http://grauna.local:8086>
  - Nextcloud: <http://grauna.local:8087>
  - Portal: <http://grauna.local:8088>
  - PiHole: <http://grauna.local:8089>
  - Visual Code Studio: <http://grauna.local:8090>
  - Calibre: <http://grauna.local:8091>
  - Resilio-Sync: <http://grauna.local:8092>


  Create mappings using Nginx Proxy Manager to have custom domains. Ex.: jellyfin.grauna.local

  Connect to a HDMI source to use the browser kiosk.

## Configurando

## WiFi Connect

Quando ligar sem conexão de internet por cabo, Grauninha vai criar um WiFi. Conectando no WiFi você pode conecta-lo
a uma rede WiFi pelo: http://grauna.local:8080

## Passar pelo wizzard

Você deve configurar cada um dos seguintes aplicativos manualmente:

Jellyfin, Kolibri, Resilio-Sync, Nextcloud

## Jellyfin

Como usuário admin crie um novo usuário sem senha e desmarque a opção "Ocultar este usuário das telas de login" para que exista um usuário aberto para a comunidade.

## Kiwix

O serviço so nicia quando encontra arquivos zim. Passe a variável `DOWNLOAD` com a url de algum arquivo zim. Ex.: `https://download.kiwix.org/zim/wikiversity/wikiversity_pt_all_maxi_2022-01.zim`

Ou adicione na pasta manualmente pela linha de comando de um drive externo.

### Nginx Proxy Manager

Email:    admin@example.com
Password: changeme

Nas configurações modifique a página padrão (Default Site) para que seja o portal. Adicione os domínios em "Add Proxy Host".

> Dica para LibreRouter / LibreMesh

Para uma melhor experiência adicione crie um arquivo `.conf` novo em `etc/config/dnsmasq.d/` com uma máscara de domínio para o ip do Grauninha:

```
address=/comunidade.app/10.147.143.9
```
### Filebrowser

Usuário: `admin`
Senha: `admin`

Criei novo usuário com idioma em português.


### MeTube

Usando o serviço "FIlebrowser" crie duas pastas novas: `metube-audio` e `metube-video`.
### Calibre

Usuário: `admin`
Senha: `admin123`
Configdb: `/books/` (precisa ter arquivos metadata.db gerado pelo Calibre)

Logado como usuário administrador mude o idioma para português, habilite navegação anônima e uploads.
Edite o usuário Guest para que possa fazer upload e ver todas secções.
Também pode mudar o título do serviço em configurações de UI.

### PiHole

Senha definida pela variável `WEBPASSWORD` do dispositivo, padrão: `grauna`

Você pode ter que modificar a variável `INTERFACE` para estar de acordo com a interface do seu dispotivo. Use `ip link show` para ver a interface de ethernet correta.

### Code

Senha definida pela variável `PASSWORD` do dispositivo, padrão: `grauna`

### ZeroTier

1. Add your ZeroTier network ID as a "Device Service Variable" named ZT_NETWORK
2. Host system preparation : SSH into the host system and execute zerotier-host-setup.sh. For increased control, you can also type the 8 commands manually. You can use `curl -o /tmp/zerotier-host-setup.sh https://raw.githubusercontent.com/synapzlu/balena-zerotier/master/scripts/zerotier-host-setup.sh && sh /tmp/zerotier-host-setup.sh` to download and execute.
3. Unpin the device release and monitor container download and startup
4. After a couple of minutes, a new "Not Authorized" member should appear in your ZeroTier dashboard.
5. Before authorizing this new member, be sure to tick "Allow Bridging" and "Do Not Auto Assign IPs". This last option will let your local DHCP assign an IP to your container's ZeroTier interface.
6. Use any mobile or device not connected to your LAN, install ZeroTier client, connect to the same network ID, authorize this member WITHOUT "Allow Bridging" and "Do Not Auto Assign IPs" features. They must stay UNticked.

## Contributing

Please open an issue or submit a pull request with any features, fixes, or changes.

Use `balena push nupef/grauninha --draft --release-tag "feature-name-test"` to publish draft releases.

Use `balena push nupef/grauninha --release-tag "feature-name"` to publish a release.

## TODO

- Fix auto-mount usb
- Add smart auto-syncing from usb
- Add [scp server](https://github.com/synapzlu/balena-scpserver)
- Best way to use ZeroTier