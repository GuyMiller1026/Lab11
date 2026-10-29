# Error table

One row per failure. Fill in every column. You need at least eight rows.

| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Fleet file does not exist | `load_fleet` | `Err(DataError::Io(..))` (kind `NotFound`) | _(example: your row goes here)_ |
|Missing Fleet file|mv data/fleet.txt data/fleet.bak|load_fleet|Err(DataError::Io(..))|
|Folder given as fleet path|set fleet path to data|load_fleet|Err(DataError::Io(..))|
|Fleet file with only comments|set the fleet path to data/fleet_empty.txt| load_fleet  |Err(DataError::NoShips("data/fleet_empty.txt"))|
|Fleet file where every line is bad|Fleet path to "data/fleet_all_bad.txt"| load_fleet|Err(DataError::NoShips("data/fleet_all_bad.txt"))|
|Board file with nine rows| Set practice path to data/boards/broken_rows.txt and then choose practice| parse_board|Err(DataError::Board(BoardError::WrongRowCount(9)))|
|Board file with a bad character| set the practice path again to data/boards/broken_char.txt and then choose practice| Parse_board|Err(DataError::Board(BoardError::BadChar { line: 6, ch: 'x' }))|
|Missing scores file| delete data/scores.txt| load_scores|Ok(vec![])|
|Scores file can’t be written| Set the scores path to data and then win a game|append_score|Err(DataError::Io(..))|
|K11|I typed K11 in practice mode|parse_coord|Err(CoordError::ColumnOutOfRange('K'))|

Scenarios to cover (add more if you find them):

- fleet file missing
- a directory given as the fleet path
- fleet file with only comments
- fleet file where every line is bad
- board file with nine rows
- board file with a bad character
- scores file missing
- scores file that cannot be written
- `K11` typed at the prompt
