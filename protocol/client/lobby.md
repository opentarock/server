Lobby client protocol
======

#### Create room

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.room.create* |  |
| name | Room name | A non-empty string representing room's name. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.room.create* |  |
| room | `Room` | Created room info. |

#### List rooms

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.room.list* |  |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.room.list* |  |
| rooms | `Room` array | List of currently active rooms. |

#### Join room

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.room.join* |  |
| room_id | The room ID | Identifies the room the user is trying to join. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.room.join* |  |
| room | `Room` | Joined room info. |

##### Event:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *lobby.room.join* |  |
| player | `Player` | A player that joined the room. |
| timestamp | *unix timestamp* | Unix timestamp of latest room state change in nanoseconds. |

#### Leave room

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.room.leave* |  |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.room.leave* |  |

##### Event:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *lobby.room.leave* |  |
| player | `Player` | A player that left the room. |
| timestamp | *unix timestamp* | Unix timestamp of latest room state change in nanoseconds. |

#### Room info

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.room.info* |  |
| room_id | The room ID | Identifies the room that the user wants additional information for. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.room.info* |  |
| room | `Room` | Room info for the requested room. |

#### Start game

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.game.start* |  |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.game.start* |  |

##### Event:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *lobby.game.start* |  |
| room_id | The room ID | Identifies the room that the user has joined and the has has been started in. |
| state | Any string | A random string of characters that the player sends as part of player ready message. |

### Player ready

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *lobby.player.ready* |  |
| state | Any string | A string received in the game start event message when lobby game is started by the owner. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *lobby.player.ready* |  |

##### Event:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *lobby.player.ready* |  |
| user_id | The user ID | The user that has become ready. |

### Common

#### Player

| Parameter | Values | Description |
| --- | --- | ---|
| id | The user ID | The unique identifier of a user. |
| nickname | User nickname | The chosen nickname of a user. |

#### Room

| Parameter | Values | Description |
| --- | --- | ---|
| id | The room ID | The unique identifier for a room. |
| name | Room name | Chosen room name. |
| owner | `Player` | Owner's player info. |
| players | `Player` array | List of non-owner players in the room. |
