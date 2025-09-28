
-----

# High-Rounds Tracker Script (GSC)

This GSC (Game Scripting Language) script module is designed to track, load, save, and announce high-round records for different player counts across various maps in a round-based survival/Zombies environment.

## 🌟 Features

  * **Persistent Records:** High-round records are loaded from and saved to a file (`scriptdata/highrounds.txt`), ensuring they persist across server restarts.
  * **Per-Map & Per-Player Count Tracking:** Records are tracked separately for each map and for player counts of 1, 2, 3, and 4.
  * **Automatic Record Monitoring:** The script starts a monitor thread (`MonitorForNewHighRounds`) that listens for the `"between_round_over"` notify to check if the current round beats a standing record.
  * **In-Game Announcements:**
      * Announces all current map records on map load.
      * Announces records to players as they connect (`AnnounceRecordsOnJoin`).
      * Broadcasts a celebratory message when a new high-round is broken.

-----


## 🗃️ Data and File Structure

### In-Game Data (`level.highRoundsByMap`)

Records are stored in a nested structure on the `level` entity.

| Structure Key | Description |
| :--- | :--- |
| `mapname` (string) | The key for the outer array (e.g., "zm\_mapname"). |
| `playerCount` (1-4) | The index for the inner array (e.g., `level.highRoundsByMap[mapname][2]` for 2-Player). |
| `.round` (integer) | The high round number achieved. |
| `.players` (array) | An array of player names (strings) who achieved the record. |

### Persistent File Format (`scriptdata/highrounds.txt`)

The script reads and writes records in a simple, pipe-delimited format, with each record on a new line:

**Format:**
`[mapname]|[playerCount]|[playerNames]|[round]`

**Example Line:**

```
zm_my_map|2|PlayerOne;PlayerTwo|85
```

  * Player names are separated by a **semicolon (`;`)**.
  * If no players are recorded (e.g., round 0), the player name field will be the string **`None`**.


Thanks To - Aymoss + HGM






