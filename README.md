# coinflip.aleo

## NOTE: Different function executions require different keys (player 1, player 2, multisig keys). For testing purposes, you can run the below to switch execution keys.

```
echo "
NETWORK=testnet3
PRIVATE_KEY={MS_PK || P1_PK | P2_PK}
" > .env
```

## Functions

### propose_game

`propose_game` to create a game with a friend.

Function:
```rust
propose_game(
    private ms_seed: field,
    private game_address: address,
    private opponent: address,
    private wager: puzzle_token.leo/Puzz.record,
    private wager_amount: u64,
    private player_one_answer: field,
    private sig: signature,
    private m_of_n: u8,
    private nonce: field
)
```

Example Command:
```
leo run propose_game 12312412field aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww "{
  owner: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  amount: 1u64.private,
  _nonce: 3208710856480263791337381472273621837437204638140170253923868382800284202059group.public
}" 1u64 1field sign1qnhgv5vd5xrjvend63pgw2qj8f6zxhz5yk36r3nsxkgjz6285cp9gz332p7uyu6upujg0f4qf4cyqqamp5hh6kfg2nxhyfkk3lkrvpxlam644zwcpzuhnjsc08k76c40xc23gzdpsx8fkzgz6c02qs89q93j76sqw5svpfpe4yqtpa9g6zwsqs6y3r5pfamwk89hjveu44mqzxzltvg 1field 1u8 1field
```
### player_one_renege_proposal

`propose_game` to create a game with a friend.

Function:
```rust
player_one_renege_proposal(
    private game_record: Game,
    private ms_rules: puzzle_account.leo/OwnerRules.record,
    private token_owner_rules: puzzle_token.leo/TokenOwnerRules.record,
    private player_one_claim_record: puzzle_token.leo/PuzzClaim.record,
    private puzz_record: puzzle_token.leo/Puzz.record,
    private amount: u64,
    private sig: signature, // player 1 sig
    private msg: field, // msg generated on propose_game with nonce
)
```

### submit_wager

`propose_game` to create a game with a friend.

Function:
```rust
submit_wager(
    private game_address: address,
    private opponent: address,
    private wager: puzzle_token.leo/Puzz.record,
    private wager_amount: u64,
    private nonce: field,
    private msg: field,
    private sig: signature,
)
```

```
leo run submit_wager aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u "{
  owner: aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww.private,
  amount: 1u64.private,
  _nonce: 7701257160296569907737636443563584249648223084591824301557650023481162448786group.public
}" 1u64 sign1qnhgv5vd5xrjvend63pgw2qj8f6zxhz5yk36r3nsxkgjz6285cp9gz332p7uyu6upujg0f4qf4cyqqamp5hh6kfg2nxhyfkk3lkrvpxlam644zwcpzuhnjsc08k76c40xc23gzdpsx8fkzgz6c02qs89q93j76sqw5svpfpe4yqtpa9g6zwsqs6y3r5pfamwk89hjveu44mqzxzltvg
```

### player_two_renege_proposal

Function:
```rust
player_two_renege_proposal (
    private game_record: Game,
    private puzz_record: puzzle_token.leo/Puzz.record,
    private amount: u64,
)
```

```
leo run player_two_renege_proposal "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  player_one_comm: 5722488078224404519904990561561967723774900188856745391253581068668871700882field.private,
  player_two_answer: 1field.private,
  total_pot: 1u64.private,
  player_one_address: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  player_two_address: aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww.private,
  game_state: 0field.private,
  _nonce: 1296315430263074257232864498293672966286835343348148902391724199988062350962group.public
}" "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  amount: 1u64.private,
  _nonce: 4523450399236952519907142286677160238720523714834464784249135179526188829220group.public
}" 1u64
```

## accept_game
```rust
accept_game (
  private game_record: Game,
  private player_two_answer: field,
)
```

```
leo run accept_game "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  player_one_comm: 5722488078224404519904990561561967723774900188856745391253581068668871700882field.private,
  player_two_answer: 1field.private,
  total_pot: 1u64.private,
  player_one_address: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  player_two_address: aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww.private,
  game_state: 0field.private,
  _nonce: 1296315430263074257232864498293672966286835343348148902391724199988062350962group.public
}" 1field
```

### reveal_answer

`reveal_answer` to reveal answer record to prove player 1 won or lost.

Function:
```rust
reveal_answer(
    private answer_record: Answer,
    private game_address: address,
    private opponent_address: address,
)
```

Example Command:
(current version immediately below):
```
leo run reveal_answer "{                                                                         system
  owner: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  game_address: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  nonce: 1field.private,
  answer: 1field.private,
  _nonce: 7009801456707050578336701579084302465418736038255959066582797292369873303448group.public
}" aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww
```

(later version):
```
leo run reveal_answer "{
  owner: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  game_address: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  nonce: 1field.private,
  answer: 1field.private,
  _nonce: 3758214225201963159322315890422876208404622381900552146703962096804019801163group.public
}" aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww
```

### finish_game

`finish_game` to finish game

Function:
```rust
finish_game (
    private game_record: Game,
    private revealed_answer_record: RevealedAnswer,
    private puzz_record: puzzle_token.leo/Puzz.record,
)
```

```
leo run finish_game "{                                                                           system
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  player_one_comm: 5722488078224404519904990561561967723774900188856745391253581068668871700882field.private,
  player_two_answer: 1field.private,
  total_pot: 1u64.private,
  player_one_address: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  player_two_address: aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww.private,
  game_state: 1field.private,
  _nonce: 3553610906097706365741456401130919249613155723801620547652734147524726606202group.public
}" "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  answer: 1field.private,
  nonce: 1field.private,
  _nonce: 4664029747950624586742729197884948830947232283053549771820864082582580731401group.public
}" "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  amount: 2u64.private,
  _nonce: 4523450399236952519907142286677160238720523714834464784249135179526188829220group.public
}"
```

### claim_total_pot

`claim_total_pot` to claim total pot (if p1 does not reveal answer)

Function:
```rust
claim_total_pot (
    private game_record: Game,
    private revealed_answer_record: RevealedAnswer,
    private puzz_record: puzzle_token.leo/Puzz.record,
)
```


```
leo run claim_total_pot "{                                                                       system
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  player_one_comm: 5722488078224404519904990561561967723774900188856745391253581068668871700882field.private,
  player_two_answer: 1field.private,
  total_pot: 1u64.private,
  player_one_address: aleo1ml2xr6fawppd6uaf8gn95uy2fpqqg8gk74k0lu8na7uvayk64v8qu8hw5u.private,
  player_two_address: aleo1muq22xpnzgaeqez0mgkdcau6kcjpk6ztey0u8yv34zcupk3hpczsmxeaww.private,
  game_state: 1field.private,
  _nonce: 3553610906097706365741456401130919249613155723801620547652734147524726606202group.public
}" "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  answer: 1field.private,
  nonce: 1field.private,
  _nonce: 4664029747950624586742729197884948830947232283053549771820864082582580731401group.public
}" "{
  owner: aleo1eqkje8cvr0twm07w4m5n356pju7njtfx75xp5zzvpg8yhgrnr58snq9kyu.private,
  amount: 2u64.private,
  _nonce: 4523450399236952519907142286677160238720523714834464784249135179526188829220group.public
}"
```