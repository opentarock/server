Tarock client protocol
======

#### Deal

##### Event:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.deal* |  |
| hand | `Card` array | Created room info. |
| id | Player id | Id assigned to the player. |

#### Bidding

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *game.tarock.bid* |  |
| contract | `Game contract` | The contract name or `"pass"` to pass the bid. |

###### Errors:
* **invalid_contract** - The contract cannot be bid in this state.
* **must_bid** - The player trying to pass must bid (all other players passed).

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *game.tarock.bid* |  |

##### Events:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.bid.next* |  |
| player_id | Player id | The user that made the bid. |
| contract | `Game contract` | The contract that was bid by the player. |
| next_player | Player id | The player that should bid next. |
| valid_bids | `Game contract` array | Valid bids for the next player (only sent to the next player bidding) |

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.bid.winner* |  |
| player_id | Player id | The player that won the bidding. |
| contract | `Game contract` | The contract that was bid by the winning player. |

#### Calling a King

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *game.tarock.callking* |  |
| suit | `Card suit` | Suit of the called king. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *game.tarock.callking* |  |

##### Events:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.callking.start* |  |
| player_id | Player id | Player that is calling a king. |

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.callking.finished* |  |
| player_id | Player id | Player that has called the king. |
| suit | `Card` suit | Suit of the called king. |

#### Exchanging cards with the talon

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *game.tarock.exchange* |  |
| picked | `number` | The index of the card set picked. |
| cards | `Card` array | Cards to exchange. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *game.tarock.exchange* |  |

##### Errors:

* **invalid_pick** - Card set index is not correct.
* **invalid_card** - Card that is not allowed was discarded.

##### Events:

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.exchange.start* |  |
| player_id | Player id | Player that is exchanging cards with the talon. |
| invalid_cards | `Card` array | List of cards from player's hand that are not allowed to be exchanged. |

| Parameter | Values | Description |
| --- | --- | ---|
| event | *game.tarock.exchange.finished* |  |
| picked | `number` | The index of the card set picked. |
| discarded | `Card` array | Tarock cards that were discarded. |

#### Announcements

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *game.tarock.announce* |  |
| bonuses | `Bonus` array | Announced bonuses. |

##### Response:

| Parameter | Values | Description |
| --- | --- | ---|
| response | *game.tarock.announce* |  |

##### Errors:

* **invalid_bonus** - Bonus that could not be announced for player's cards was announced.

##### Events:

| Parameter | Values | Description |
| --- | --- | --- |
| event | *game.tarock.announce.next* |  |
| player_id | Player id | Player that has announced bonuses. |
| bonuses | `Bonus` array | The bonuses announced. |
| next_player | Player id | The player that should announce next. |
| valid_bonuses | `Bonus` array | List of bonuses that are valid to be declared (only sent to the next player announcing) |

| Parameter | Values | Description |
| --- | --- | --- |
| event | *game.tarock.accounce.finished* |  |

#### The Play

##### Request:

| Parameter | Values | Description |
| --- | --- | ---|
| command | *game.tarock.play* |  |
| card | `Card` | The played card. |

##### Response:

| Parameter | Values | Description |
| --- | --- | --- |
| response | *game.tarock.play* |  |

##### Errors:

* **invalid_card** - Card that is not valid for the current trick or is not in player's hand.

##### Events:

| Parameter | Values | Description |
| --- | --- | --- |
| event | *game.tarock.play.next* |  |
| player_id | Player id | Player that played the card. |
| card | `Card` | Played card. |
| trick_finished | *bool* | Is `true` if the played card finished the trick (default `false`). |
| next_player | Player id | The player that should play next. |

### Common

#### Cards

Cards are represented by a string started with uppercase letter indicating the
card suit followed by the card value.

##### Card suits:
* C (Clubs)
* S (Spades)
* H (Hearts)
* D (Diamonds)

Tarocks are represented the same way: T (Tarock)

##### Card values (in descending order):
* K (King)
* Q (Queen)
* N (Knight)
* J (Jack)

##### Only clubs and spades:
* 10 (Ten)
* 9 (Nine)
* 8 (Eight)
* 7 (Seven)

##### Only hearts and diamonds:
* 1 (One)
* 2 (Two)
* 3 (Three)
* 4 (Four)

##### Card values for tarocks:
Numbers of 1-21 and S (Skis).

#### Contracts

##### Values:
* klop
* three
* two
* one
* solo_three
* solo_two
* solo_one
* beggar
* solo_without
* open_beggar
* color_valat
* valat

#### Bonuses

##### Values:
* trula
* kings
* kings_ultimo
* pagat_ultimo
* valat
