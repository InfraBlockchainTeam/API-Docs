# Socket.IO chat demo service 1.0.0 documentation

Socket.IO chat demo service

&#x20;

1.0.0

### Servers

* socketio-chat-h9jt.herokuapp.com/socket.iowssdemo

### Operations

*   #### PUB /

    Accepts **one of** the following messages:

    *   **Examples**

        string

        **This example has been generated automatically.**
    * **Examples**
    * **Examples**
    *   \#3add user

        Additional properties are allowed.

        **Examples**

        string

        **This example has been generated automatically.**
*   #### SUB /

    Accepts **one of** the following messages:

    *   \#0new message

        Additional properties are allowed.

        **Examples**

        ```
        {
          "username": "string",
          "message": "string"
        }
        ```

        **This example has been generated automatically.**
    *   \#1typing

        Additional properties are allowed.

        **Examples**

        **This example has been generated automatically.**
    *   \#2stop typing

        Additional properties are allowed.

        **Examples**

        **This example has been generated automatically.**
    *   \#3user joined

        Additional properties are allowed.

        **Examples**

        ```
        {
          "username": "string",
          "numUsers": 0
        }
        ```

        **This example has been generated automatically.**
    *   \#4user left

        Additional properties are allowed.

        **Examples**

        ```
        {
          "username": "string",
          "numUsers": 0
        }
        ```

        **This example has been generated automatically.**
    *   \#5login

        Additional properties are allowed.

        **Examples**

        **This example has been generated automatically.**
*   #### SUB /admin

    Additional properties are allowed.

    Accepts the following message:

    server metric

    Additional properties are allowed.

    **Examples**

    ```
    {
      "name": "string",
      "value": 0
    }
    ```

    **This example has been generated automatically.**

### Messages

*
*
*
*   \#4add user

    Additional properties are allowed.
*   \#5new message

    Additional properties are allowed.
*   \#6typing

    Additional properties are allowed.
*   \#7stop typing

    Additional properties are allowed.
*   \#8user joined

    Additional properties are allowed.
*   \#9user left

    Additional properties are allowed.
*   \#10login

    Additional properties are allowed.
*   \#11server metric

    Additional properties are allowed.
