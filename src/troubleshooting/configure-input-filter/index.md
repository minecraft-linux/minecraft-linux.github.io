# Configure the Input Filter

You can force your input device and override the behavior like this

- Press the pencil icon to edit your profile

<img width="752" alt="Image" src="https://github.com/user-attachments/assets/e5aed881-38e8-4d70-bdd2-57f1f64b594f" />

- Press expand advanced

<img width="752" alt="Image" src="https://github.com/user-attachments/assets/77a4fb0b-7a09-40b3-972d-3af8aa98e1e5" />

- Scroll down to Environment Variables and Click "Add new Variable"

<img width="752" alt="Image" src="https://github.com/user-attachments/assets/bf6d70c7-2360-4de6-badd-af74d51eef8f" />

- Enter Key `MCPELAUNCHER_CLIENT_FORCED_INPUT_MODE` and value `2` (Gamepad Only) (`0` Touch Only, `1` Mouse + Keyboard Only) then press Save like this

<img width="752" alt="Image" src="https://github.com/user-attachments/assets/8ca89f21-db97-4809-a0a0-e320ff3b18ad" />

The launcher would now refuse to recognize any mouse, keyboard, touch input events that your drivers seem to randomly send to the launcher this confuses the game so the launcher filters them and not all software devices work well with it.


If you don't like the input filter and think the game don't get confused you use this Key `MCPELAUNCHER_CLIENT_RAW_INPUT` with value `1`
