sequenceDiagram
User->>Shortcut: Click to run.
Shortcut->>VTCGame: call VTCGame.
VTCGame->>VTCLauncher: call VTCLauncher.
VTCLauncher-->>User: show GUI.
User->>VTCLauncher: Choose game and play.
VTCLauncher-->>User: Require login.
User->>VTCLauncher: Login.
VTCLauncher->>VTCServer: Require authen user.
VTCServer-->>VTCLauncher: Return user info.
VTCLauncher->>Game: Call game with user info.
Game->>VTCServer: Get user detail info.
VTCServer-->>Game: Return user detail info.
Game-->>User: Allow user play game.
User->>Game: Play game.

