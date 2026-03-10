# Typescript Overview

In Airship, you write code using TypeScript instead of C#.

&#x20;Most Unity APIs are available. If something is missing ask in our [Discord](https://discord.gg/YqrmGwSg7z) — we'll add it for you.&#x20;

* You do not use C# for any game scripts (only advanced editor scripts)
* TypeScript allows you to instantly update your game on all platforms

## Opening in VSCode

In [VSCode](https://code.visualstudio.com/) choose `File > Open Folder` and select the Assets folder in your project. This will give you proper syntax highlighting and import suggestions. &#x20;

{% hint style="info" %}
It's important to open the "Assets" folder and not the root folder.
{% endhint %}

## Creating Scripts

To create a new script open the `Project` tab and navigate to the `Assets/Code` folder. In here you can see the scripts that control the template.

<img src="../.gitbook/assets/Screenshot 2024-08-16 at 3.51.56 PM.png" alt="" data-size="original">

In the folder you can create a new script by right clicking and selecting:\
`Create > Airship > Typescript File`

## Important Globals

Useful Airship services can be found under the `Game` `Airship` and `Platform` globals.

## Important Considerations

Airship uses the [Luau Runtime](https://github.com/luau-lang/luau) to run scripts from the cloud. This means all TypeScript files are compiled to Luau instead of JavaScript and there are a few gotcha's when expecting a JavaScript function or library to exist. [Check this page for more information.](https://docs.airship.gg/other/javascript-greater-than-luau)
