# websocket api example

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

<details>

<summary>PUB smartylighting/streetlights/1/0/event/{streetlightId}/lighting/measured Operation</summary>

* Operation ID: `dimLight`

#### Parameters

#### `fdsfkafka` Operation specific information

#### Message Dim light `dimLight`

_Command a particular streetlight to dim the lights._

**Headers**

Examples of headers _(generated)_

```json
{
  "my-app-header": 0
}
```

**Payload**

Examples of payload _(generated)_

```json
{
  "percentage": 0,
  "sentAt": "2019-08-24T14:15:22Z"
}
```

</details>
