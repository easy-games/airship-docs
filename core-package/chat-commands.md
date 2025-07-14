---
description: Quickly run code from the chat window
---

# Chat Commands

Setting up a chat command lets you link code to keywords. Type the keyword in chat on your client and the code will be run on the Server.&#x20;



## Chat Command Structure

All commands are run with the / character followed by the command keyword, then parameters separated by spaces:

```
/mycommand 12 secondParam
```

{% hint style="info" %}
You can use the / key to open the chat window with the / character already entered
{% endhint %}





## Create your own Chat Command

1. Create a new TS file and name MyCommand.ts
2. Create a class that extends "ChatCommand"

```typescript
export class MyCommand extends ChatCommand {
```

3. Setup the core variables in the constructor

```typescript
constructor() {
	super("mycommand", ["c"], "[string] (optional)", "Print a message");
}
```

4. Implement the Execute function which fires on the server when a client types the command

```typescript
//Player that sent the command and the variables passed through as string arguments
public Execute(player: Player, args: string[]): void {

	//Get the parameter if it was sent
	let firstParameter = ""
	if(args.size() > 0){
		firstParameter = args[0];
	}
	
	//Create a log message
	const logMessage = "Client sent message: " + firstParameter;

	//Log to console on server
	print(logMessage);

	//Send the results to every clients chat window
	Airship.Chat.BroadcastMessage(logMessage);
}
```

5. Register the command somewhere in your games code through Airship.Chat

```typescript
Airship.Chat.RegisterCommand(new MyCommand());
```

6. You can now run your command in the chat by typing&#x20;

```
/mycommand hello
```





## The Full Script

```typescript
import { Airship } from "@Easy/Core/Shared/Airship";
import { ChatCommand } from "@Easy/Core/Shared/Commands/ChatCommand";
import { Player } from "@Easy/Core/Shared/Player/Player";


export class MyCommand extends ChatCommand {
	constructor() {
		super("mycommand", ["c"], "[string] (optional)", "Print a message");
	}

	//Player that sent the command and the variables passed through as string arguments
	public Execute(player: Player, args: string[]): void {

		//Get the parameter if it was sent
		let firstParameter = ""
		if(args.size() > 0){
			firstParameter = args[0];
		}
		
		//Create a log message
		const logMessage = "Client sent message: " + firstParameter;

		//Log to console on server
		print(logMessage);

		//Send the results to every clients chat window
		Airship.Chat.BroadcastMessage(logMessage);
	}
}
```



