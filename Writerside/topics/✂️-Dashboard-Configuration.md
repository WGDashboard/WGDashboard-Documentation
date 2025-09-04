# ✂️ Configure

## Configuration File

Since version 2.0, WGDashboard will be using a configuration file called `wg-dashboard.ini`, (It will generate automatically after first time running the dashboard). More options will include in future versions, and for now it included the following configurations:

### `[Account]`

Configurations on how to sign in to WGDashboard

#### `username`

Username to sign in. 

Default: `admin`

#### `password`

Password to sign in, and is hashed with `bcrypt.hashpw(value, bcrypt.gensalt())`. 

Default: `bcrypt.hashpw("admin", bcrypt.gensalt())`

#### `enable_totp`

Boolean to indicate if TOTP is enabled. 

Default: `false`

#### `totp_verified`

Boolean to indicate if TOTP is verified

Default: `false`

#### `totp_key`

The **key** to generate TOTP

Default: `pyotp.random_base32()`

### `[Server]`

Configuration on WGDashboard

#### `wg_conf_path`

The path of all the WireGuard configurations

Default: `/etc/wireguard`

#### `awg_conf_path`

The path of all the AmneziaWG configurations

Default: `/etc/amnezia/amneziawg`

#### `app_prefix`

**Will deprecate in future release, please review [](Add-URL-Prefix-to-WGDashboard.md)**

Prefix before each path

Default: `(blank)`

#### `app_ip`

The IP address WGDashboard will bind on

Default: `0.0.0.0`

#### `app_port`

The port WGDashboard will listen on

Default: `10086`

#### `auth_req`

Does the dashboard need authentication to access, if `auth_req = false` , user will not be access the **Setting** tab due to security consideration. **User can only edit the file directly in system**.

Default: `true`

#### `version`

Dashboard Version

#### `dashboard_refresh_interval`

How frequent the dashboard will refresh on the configuration page, the value is in milliseconds.

Default: `60000`

#### `dashboard_sort`

How Peers are sorting.

Default: `status`

#### `dashboard_theme`

WGDashboard's theme

Default: `dark`

#### `dashboard_api_key`

Boolean to indicate if API Key is enabled

Default: `false`

#### `dashboard_language`

Language displaying on the UI of WGDashboard. Please visit [](Change-Language.md) for languages is available

Default: `en-US` (English)

### `[Peers]`

Default Settings on a new peer

#### `peer_global_dns`

DNS Server

Default: `1.1.1.1`

#### `peer_endpoint_allowed_ip`

Endpoint Allowed IP

Default: `0.0.0.0/0`

#### `remote_endpoint`

Remote Endpoint (i.e where your peers will connect to)

Default: WGDashboard will retrieve the IP address of your system's default network interface.

#### `peer_mtu`

Maximum Transmit Unit

Default: `1420`

#### `peer_keep_alive`

Persistent Keepalive

Default: `21`

#### `peer_display_mode`

How peer will display

Default: `grid`

### `[Other]`

For some other usages, no need to edit manually

#### `welcome_session`

Indicator if welcome session is finished for a freshly installed WGDashboard

Default: `false`

### `[Database]`

Configuration of database. Currently, you will need to manually edit this file to configure database, before making changes, please stop WGDashboard first.

#### `type`

Which type of database is currently using. WGDashboard is available to use different types of database **since v4.3.0**. The available types are `sqlite`, `postgresql` and `mysql`

Default: `sqlite`

> All 4 fields below are required when `type` set to `postgrsql` or `mysql`

#### `host`

Database server's IP address to domain.

#### `port`

Database server's port.

#### `username` {id="database_username"}

Username used to connect database server.

> Please ensure your username is permission to **create databases**

#### `password` {id="database_password"}

Password of the username above


### `[Email]`

Configurations for WGDashboard's SMTP service.

> All fields in this section are default in **blank**

#### `server` {id="email_server"}

Domain or IP address of the SMTP server you wish to use

#### `port` {id="email_port"}

Port of the SMTP server you wish to use

#### `encryption`

This field can be set to **blank** or `STARTTLS` if you wish to use TLS with SMTP

#### `username` {id="email_username"}

The username used to sign in to the SMTP server

#### `email_password`

Password of the username above to sign in to the SMTP server

#### `send_from`

This is sender's name to display on the email you sent out. It can be only email or name with email, for example:

`onboarding@wgdashboard.dev` or `WGDashboard <onboarding@wgdashboard.dev>`

#### `email_template`

This is the template you can set and will apply when you want to sent out an configuration. The template is enabled with Jinja template, for more information: [](Email-Service.md)

### `[WireGuardConfiguration]`

Settings for WireGuard configurations

#### `autostart`

A pipeline separated list of configuration names that WGDashboard will toggle when start up.


## Generating QR code and peer configuration file (.conf)

Starting version 2.2, dashboard can now generate QR code and configuration file for each peer. Here is a template of what each QR code encoded with and the same content will be inside the file:

```ini
[Interface]
PrivateKey = QWERTYUIOPO234567890YUSDAKFH10E1B12JE129U21=
Address = 0.0.0.0/32
DNS = 1.1.1.1

[Peer]
PublicKey = QWERTYUIOPO234567890YUSDAKFH10E1B12JE129U21=
AllowedIPs = 0.0.0.0/0
Endpoint = 0.0.0.0:51820
PresharedKey = QWERTYUIOPO234567890YUSDAKFH10E1B12JE129U21=
```

|                   | Description                                                                                            | Default Value                                                                                   | Available in Peer setting |
|-------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------|
| **`[Interface]`** |                                                                                                        |                                                                                                 |                           |
| `PrivateKey`      | The private key of this peer                                                                           | Private key generated by WireGuard (`wg genkey`) or provided by user                            | Yes                       |
| `Address`         | The `allowed_ips` of your peer                                                                         | N/A                                                                                             | Yes                       |
| `DNS`             | The DNS server your peer will use                                                                      | `1.1.1.1` - Cloud flare DNS, you can change it when you adding the peer or in the peer setting. | Yes                       |
| **`[Peer]`**      |                                                                                                        |                                                                                                 |                           |
| `PublicKey`       | The public key of your server                                                                          | N/A                                                                                             | No                        |
| `AllowedIPs`      | IP ranges for which a peer will route traffic                                                          | `0.0.0.0/0` - Indicated a default route to send all internet and VPN traffic through that peer. | Yes                       |
| `Endpoint`        | Your wireguard server ip and port, the dashboard will search for your server's default interface's ip. | `<your server default interface ip>:<listen port>`                                              | Yes                       |
| `PresharedKey`    | The Pre-Shared Key of this peer _(if available)_                                                       | N/A                                                                                             | Yes                       |
