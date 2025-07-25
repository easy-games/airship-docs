# Publishing with API Key

{% hint style="info" %}
If you signed up with Google for your Airship account the steps to publish are [here](../publishing/publish-game.md).
{% endhint %}

If you aren't signed into editor you can still publish your game using API keys.

### Registering an API Key

1. Go to your [organization's API keys dashboard](https://create.airship.gg/dashboard/organization/api-keys) and click `Create Key` .&#x20;
2. Give your key permission to publish to the game you want to deploy to.
3. In Unity Editor go to `Airship > Configuration` and paste the key in `Airship API Key`

<div align="center" data-full-width="false"><figure><img src="../.gitbook/assets/Screenshot 2025-07-24 at 5.50.20 PM.png" alt="" width="116"><figcaption></figcaption></figure></div>

### Setting Up Your Publish Target

1. Grab your game id from your [create dashboard](https://create.airship.gg/dashboard).

<div data-full-width="false"><figure><img src="../.gitbook/assets/Screenshot 2025-07-24 at 5.45.13 PM.png" alt="" width="375"><figcaption></figcaption></figure></div>

2. Go to your game config

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 5.26.58 PM.png" alt="" width="176"><figcaption></figcaption></figure>

3. Paste in your game id to `Target game id` and click `Submit`

<figure><img src="../.gitbook/assets/Screenshot 2025-07-24 at 6.01.48 PM.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="success" %}
If your game names shows up next to "Publish target" you are ready to deploy!
{% endhint %}
