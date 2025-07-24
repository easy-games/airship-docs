---
description: Quickly run code from the chat window
---

# Chat Commands

Airship has a built in command system. The API is exposed so you can register your own chat commands.

## Chat Command Structure

All commands are run with the / character followed by the command keyword, then parameters separated by spaces:

```
/mycommand 12 secondParam
```

## Example Command

```typescript
import { Airship } from "@Easy/Core/Shared/Airship";
import { ChatCommand } from "@Easy/Core/Shared/Commands/ChatCommand";
import { Player } from "@Easy/Core/Shared/Player/Player";

export class MyCommand extends ChatCommand {
	constructor() {
		// command name, alias, usage hints, and description
		super("mycommand", ["c"], "[string] (optional)", "Print a message");
	}

	// Player that sent the command and the variables passed through as string arguments
	public Execute(player: Player, args: string[]): void {

		// Get the parameter if it was sent
		let firstParameter = ""
		if(args.size() > 0){
			firstParameter = args[0];
		}
		
		// Create a log message
		const logMessage = "Client sent message: " + firstParameter;

		// Log to console on server
		print(logMessage);

		// Send the results to every clients chat window
		Airship.Chat.BroadcastMessage(logMessage);
	}
}
```

You must register the command on the server. Do this from some AirshipBehaviour that lives in your scene:

```typescript
import { Airship } from "@Easy/Core/Shared/Airship";
import { Game } from "@Easy/Core/Shared/Game";
import MyCommand from "./MyCommand";

export default class CommandManager extends AirshipBehaviour {
	override Start() {
		if (Game.IsServer()) {
			Airship.Chat.RegisterCommand(new MyCommand());
		}
	}
}
```

