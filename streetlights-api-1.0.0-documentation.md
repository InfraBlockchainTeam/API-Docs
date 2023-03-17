# Streetlights API 1.0.0 documentation

* License: [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
* Default content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

The Smartylighting Streetlights API allows you to remotely manage the city lights.

### Check out its awesome features:

* Turn a specific streetlight on/off 🌃
* Dim a specific streetlight 😎
* Receive real-time information about environmental lighting conditions 📈

## Table of Contents

* [Servers](broken-reference)
  * [production](broken-reference)
* [Operations](broken-reference)
  * [PUB smartylighting/streetlights/1/0/event/{streetlightId}/lighting/measured](broken-reference)
  * [SUB smartylighting/streetlights/1/0/action/{streetlightId}/turn/on](broken-reference)
  * [SUB smartylighting/streetlights/1/0/action/{streetlightId}/turn/off](broken-reference)
  * [SUB smartylighting/streetlights/1/0/action/{streetlightId}/dim](broken-reference)

## Servers

### `production` Server

* URL: `test.mosquitto.org:{port}`
* Protocol: `mqtt`

Test broker

#### URL Variables

| Name | Description                                             | Default value | Allowed values |
| ---- | ------------------------------------------------------- | ------------- | -------------- |
| port | Secure connection (TLS) is available through port 8883. | `1883`        | `1883`, `8883` |

#### Security

**Security Requirement 1**

*   Type: `API key`

    * In: user

    Provide your API key as the user and leave the password empty.

**Security Requirement 2**

*   Type: `OAuth2`

    *   Flows:

        Required scopes: `streetlights:on`, `streetlights:off`, `streetlights:dim`

        | Flow               | Auth URL                                                           | Token URL                                                            | Refresh URL                                                              | Scopes                                                    |
        | ------------------ | ------------------------------------------------------------------ | -------------------------------------------------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------- |
        | Implicit           | [https://authserver.example/auth](https://authserver.example/auth) | -                                                                    | -                                                                        | `streetlights:on`, `streetlights:off`, `streetlights:dim` |
        | Password           | -                                                                  | [https://authserver.example/token](https://authserver.example/token) | -                                                                        | `streetlights:on`, `streetlights:off`, `streetlights:dim` |
        | Client credentials | -                                                                  | [https://authserver.example/token](https://authserver.example/token) | -                                                                        | `streetlights:on`, `streetlights:off`, `streetlights:dim` |
        | Authorization Code | [https://authserver.example/auth](https://authserver.example/auth) | [https://authserver.example/token](https://authserver.example/token) | [https://authserver.example/refresh](https://authserver.example/refresh) | `streetlights:on`, `streetlights:off`, `streetlights:dim` |

    Flows to support OAuth 2.0

**Security Requirement 3**

* Type: `Open ID`
  * OpenID Connect URL: [https://authserver.example/.well-known](https://authserver.example/.well-known)

## Operations

### PUB `smartylighting/streetlights/1/0/event/{streetlightId}/lighting/measured` Operation

_Inform about environmental lighting conditions of a particular streetlight._

* Operation ID: `receiveLightMeasurement`

The topic on which measured values may be produced and consumed.

#### Parameters

| Name          | Type   | Description                | Value | Constraints | Notes        |
| ------------- | ------ | -------------------------- | ----- | ----------- | ------------ |
| streetlightId | string | The ID of the streetlight. | -     | -           | **required** |

#### `kafka` Operation specific information

| Name     | Type | Description | Value         | Constraints | Notes |
| -------- | ---- | ----------- | ------------- | ----------- | ----- |
| clientId | -    | -           | `"my-app-id"` | -           | -     |

#### Message Light measured `lightMeasured`

_Inform about environmental lighting conditions of a particular streetlight._

* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

**Headers**

| Name          | Type    | Description | Value | Constraints   | Notes                                 |
| ------------- | ------- | ----------- | ----- | ------------- | ------------------------------------- |
| (root)        | object  | -           | -     | -             | **additional properties are allowed** |
| my-app-header | integer | -           | -     | \[ 0 .. 100 ] | -                                     |

> Examples of headers _(generated)_

```json
{
  "my-app-header": 0
}
```

**Payload**

| Name   | Type    | Description                              | Value | Constraints          | Notes                                 |
| ------ | ------- | ---------------------------------------- | ----- | -------------------- | ------------------------------------- |
| (root) | object  | -                                        | -     | -                    | **additional properties are allowed** |
| lumens | integer | Light intensity measured in lumens.      | -     | >= 0                 | -                                     |
| sentAt | string  | Date and time when the message was sent. | -     | format (`date-time`) | -                                     |

> Examples of payload _(generated)_

```json
{
  "lumens": 0,
  "sentAt": "2019-08-24T14:15:22Z"
}
```

### SUB `smartylighting/streetlights/1/0/action/{streetlightId}/turn/on` Operation

* Operation ID: `turnOn`

#### Parameters

| Name          | Type   | Description                | Value | Constraints | Notes        |
| ------------- | ------ | -------------------------- | ----- | ----------- | ------------ |
| streetlightId | string | The ID of the streetlight. | -     | -           | **required** |

#### `kafka` Operation specific information

| Name     | Type | Description | Value         | Constraints | Notes |
| -------- | ---- | ----------- | ------------- | ----------- | ----- |
| clientId | -    | -           | `"my-app-id"` | -           | -     |

#### Message Turn on/off `turnOnOff`

_Command a particular streetlight to turn the lights on or off._

**Headers**

| Name          | Type    | Description | Value | Constraints   | Notes                                 |
| ------------- | ------- | ----------- | ----- | ------------- | ------------------------------------- |
| (root)        | object  | -           | -     | -             | **additional properties are allowed** |
| my-app-header | integer | -           | -     | \[ 0 .. 100 ] | -                                     |

> Examples of headers _(generated)_

```json
{
  "my-app-header": 0
}
```

**Payload**

| Name    | Type   | Description                              | Value                     | Constraints          | Notes                                 |
| ------- | ------ | ---------------------------------------- | ------------------------- | -------------------- | ------------------------------------- |
| (root)  | object | -                                        | -                         | -                    | **additional properties are allowed** |
| command | string | Whether to turn on or off the light.     | allowed (`"on"`, `"off"`) | -                    | -                                     |
| sentAt  | string | Date and time when the message was sent. | -                         | format (`date-time`) | -                                     |

> Examples of payload _(generated)_

```json
{
  "command": "on",
  "sentAt": "2019-08-24T14:15:22Z"
}
```

### SUB `smartylighting/streetlights/1/0/action/{streetlightId}/turn/off` Operation

* Operation ID: `turnOff`

#### Parameters

| Name          | Type   | Description                | Value | Constraints | Notes        |
| ------------- | ------ | -------------------------- | ----- | ----------- | ------------ |
| streetlightId | string | The ID of the streetlight. | -     | -           | **required** |

#### `kafka` Operation specific information

| Name     | Type | Description | Value         | Constraints | Notes |
| -------- | ---- | ----------- | ------------- | ----------- | ----- |
| clientId | -    | -           | `"my-app-id"` | -           | -     |

#### Message Turn on/off `turnOnOff`

_Command a particular streetlight to turn the lights on or off._

**Headers**

| Name          | Type    | Description | Value | Constraints   | Notes                                 |
| ------------- | ------- | ----------- | ----- | ------------- | ------------------------------------- |
| (root)        | object  | -           | -     | -             | **additional properties are allowed** |
| my-app-header | integer | -           | -     | \[ 0 .. 100 ] | -                                     |

> Examples of headers _(generated)_

```json
{
  "my-app-header": 0
}
```

**Payload**

| Name    | Type   | Description                              | Value                     | Constraints          | Notes                                 |
| ------- | ------ | ---------------------------------------- | ------------------------- | -------------------- | ------------------------------------- |
| (root)  | object | -                                        | -                         | -                    | **additional properties are allowed** |
| command | string | Whether to turn on or off the light.     | allowed (`"on"`, `"off"`) | -                    | -                                     |
| sentAt  | string | Date and time when the message was sent. | -                         | format (`date-time`) | -                                     |

> Examples of payload _(generated)_

```json
{
  "command": "on",
  "sentAt": "2019-08-24T14:15:22Z"
}
```

### SUB `smartylighting/streetlights/1/0/action/{streetlightId}/dim` Operation

* Operation ID: `dimLight`

#### Parameters

| Name          | Type   | Description                | Value | Constraints | Notes        |
| ------------- | ------ | -------------------------- | ----- | ----------- | ------------ |
| streetlightId | string | The ID of the streetlight. | -     | -           | **required** |

#### `kafka` Operation specific information

| Name     | Type | Description | Value         | Constraints | Notes |
| -------- | ---- | ----------- | ------------- | ----------- | ----- |
| clientId | -    | -           | `"my-app-id"` | -           | -     |

#### Message Dim light `dimLight`

_Command a particular streetlight to dim the lights._

**Headers**

| Name          | Type    | Description | Value | Constraints   | Notes                                 |
| ------------- | ------- | ----------- | ----- | ------------- | ------------------------------------- |
| (root)        | object  | -           | -     | -             | **additional properties are allowed** |
| my-app-header | integer | -           | -     | \[ 0 .. 100 ] | -                                     |

> Examples of headers _(generated)_

```json
{
  "my-app-header": 0
}
```

**Payload**

| Name       | Type    | Description                                        | Value | Constraints          | Notes                                 |
| ---------- | ------- | -------------------------------------------------- | ----- | -------------------- | ------------------------------------- |
| (root)     | object  | -                                                  | -     | -                    | **additional properties are allowed** |
| percentage | integer | Percentage to which the light should be dimmed to. | -     | \[ 0 .. 100 ]        | -                                     |
| sentAt     | string  | Date and time when the message was sent.           | -     | format (`date-time`) | -                                     |

> Examples of payload _(generated)_

```json
{
  "percentage": 0,
  "sentAt": "2019-08-24T14:15:22Z"
}
```
