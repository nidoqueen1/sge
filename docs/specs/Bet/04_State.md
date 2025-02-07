# **State**


## **KVStore**
State in bet module is defined by its KVStore. This KVStore has only a single partitions:

1. A partition for all bets

The bet model in the Proto files is as below:

```
message Bet {

  // uid is the unique uuid assigned to bet
  string uid = 1 [(gogoproto.customname) = "UID" ,(gogoproto.jsontag) = "uid", json_name = "uid"];

  // sport_event_uid is the unique uuid of te sportevent on which bet is placed
  string sport_event_uid = 2 [(gogoproto.customname) = "SportEventUID" ,(gogoproto.jsontag) = "sport_event_uid", json_name = "sport_event_uid"];

  // odds_uid is the unique uuid of the odds on which bet is placed
  string odds_uid = 3 [(gogoproto.customname) = "OddsUID" ,(gogoproto.jsontag) = "odds_uid", json_name = "odds_uid"];

  // odds_value is the odds on which bet is placed
  string odds_value = 4[
    (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Dec",
    (gogoproto.nullable)   = false];

  // amount is the wagger amount deducted by betting fee
  string amount = 5[
    (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
    (gogoproto.nullable)   = false];

  // betFee is the betting fee
  cosmos.base.v1beta1.Coin bet_fee = 6[
    (gogoproto.castrepeated) = "github.com/cosmos/cosmos-sdk/types.Coin",
    (gogoproto.nullable) = false];


  // status is the status of the bet, such as `pending` or `settled`
  Status status = 7;

  // result is the result of bet, sunch as `won` or `lost`
  Result result = 8;

  // verified shows bet is verified or not
  bool verified = 9;

  // ticket is a signed string containing important info such as `oddsValue`
  string ticket = 10;

  // creator is the bettor address
  string creator = 11;

  //Status of the Bet.
  enum Status {

    //the unknown status
    STATUS_INVALID = 0;

    //placed bet placed and waiting for result
    STATUS_PLACED = 1;

    //canceled by Bettor
    STATUS_CANCELLED = 2;

    //there was an abort because of force like match canceled or system.
    STATUS_ABORTED = 3;

    //pending for any reason like DVM , see BetEventStatus on this case.
    STATUS_PENDING = 4;

    //the result of the bet is decelerated.
    STATUS_RESULT_DECLARED = 5;

    //the bet is settled.
    STATUS_SETTLED = 6;
  }

  //Result of the bet.
  enum Result {

    //the invalid or unknown
    RESULT_INVALID = 0;

    // the result is not decelerated yet.
    RESULT_PENDING = 1;

    // bet is won
    RESULT_WON = 2;

    // bet is lost
    RESULT_LOST = 3;

    // bet is draw
    RESULT_DRAW = 4;

    // bet is aborted
    RESULT_ABORTED = 5;
  }
```
