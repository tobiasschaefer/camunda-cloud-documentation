---
id: flags
title: Flags
description: "Flags allow you to control the availability of certain features within Desktop Modeler."
---

Flags allow you to control the availability of certain features within Desktop Modeler.

## Configuring Flags

You may configure flags in a `flags.json` file or pass them via CLI.

### Configure in `flags.json`

Place a `flags.json` file inside the `resources` folder of your local [`{USER_DATA}`](../search-paths#user-data-directory) or [`{APP_DATA_DIRECTORY}`](../search-paths#app-data-directory) directory to persist them.

### Configure via CLI

Pass flags via the command line when starting the application.

```
camunda-modeler --disable-plugins
```

Flags passed as command line arguments take precedence over those configured via a configuration file.

## Available Flags

| flag                                                       | default value                       |
| ---------------------------------------------------------- | ----------------------------------- |
| ["disable-plugins"](#disable-plug-ins)                     | false                               |
| "disable-adjust-origin"                                    | false                               |
| "disable-cmmn"                                             | true                                |
| "disable-dmn"                                              | false                               |
| "disable-form"                                             | false                               |
| ["disable-httl-hint"](#disable-history-time-to-live-hint)  | false                               |
| ["default-httl"](#default-history-time-to-live)            | false                               |
| "disable-platform"                                         | false                               |
| "disable-zeebe"                                            | false                               |
| "disable-remote-interaction"                               | false                               |
| "single-instance"                                          | false                               |
| "user-data-dir"                                            | [Electron default](../search-paths) |
| ["display-version"](#custom-display-version-label)         | `undefined`                         |
| ["zeebe-ssl-certificate"](#zeebe-ssl-certificate)          | `undefined`                         |
| ["c7-engine-version"](#default-execution-platform-version) | `undefined`                         |
| ["c8-engine-version"](#default-execution-platform-version) | `undefined`                         |

## Examples

### Disable Plug-ins

Start the modeler without activating installed plug-ins. This is useful to debug modeler errors.

### BPMN-only Mode

To disable the DMN and FORM editing capabilities of the App, configure your `flags.json` like this:

```js
{
    "disable-dmn": true,
    "disable-form": true
}
```

As a result, the app will only allow users to model BPMN diagrams.

![BPMN only mode](./img/bpmn-only.png)

### Disable `history-time-to-live` hint

<span class="badge badge--platform">Camunda 7 only</span>

To disable the [history time to live hint](../../reference/modeling-guidance/rules/history-time-to-live.md) in scenarios where the engine configures HTTL, configure `flags.json`:

```js
{
    "disable-httl-hint": true
}
```

### Default `history-time-to-live`

<span class="badge badge--platform">Camunda 7 only</span>

To set a default [history time to live](../../reference/modeling-guidance/rules/history-time-to-live.md) value to be used in newly created models, configure `flags.json`:

```js
{
    "default-httl": 30
}
```

### Custom `display-version` label

To display a custom version information in the status bar of the app, configure `flags.json`:

```js
{
    "display-version": "1.2.3"
}
```

![Custom version info](./img/display-version.png)

### Zeebe SSL certificate

<span class="badge badge--cloud">Camunda 8 only</span>

> :information_source: Modeler will read trusted certificates from your operating system's trust store.

Provide additional certificates to validate secured connections to a Camunda 8 installation.

Configure your `flags.json`:

```js
{
    "zeebe-ssl-certificate": "C:\\path\\to\\certs\\trusted-custom-roots.pem"
}
```

Additional information adapted from the [upstream documentation](https://nodejs.org/docs/latest/api/tls.html#tlscreatesecurecontextoptions):

> The peer (Camunda 8) certificate must be chainable to a CA trusted by the app for the connection to be authenticated. When using certificates that are not chainable to a well-known CA, the certificate's CA must be explicitly specified as trusted or the connection will fail to authenticate. If the peer uses a certificate that doesn't match or chain to one of the default CAs, provide a CA certificate that the peer's certificate can match or chain to. For self-signed certificates, the certificate is its own CA, and must be provided.

### Default execution platform version

To change default execution platform version, configure your `flags.json` as follows:

```json
{
  "c7-engine-version": "7.18.0",
  "c8-engine-version": "8.0.0"
}
```

New diagrams created in Desktop Modeler will use the configured version instead of the latest stable version.
