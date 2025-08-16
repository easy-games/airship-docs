# Installing Airship

## Prerequisites

1. Install the "LTS" version of [Nodejs](https://nodejs.org/en)
2. Install [Unity Hub](https://unity.com/download)
3. Recommended: install [VSCode](https://code.visualstudio.com/) for script editing

### Download from Github

[Click here to download the Starter Template](https://github.com/easy-games/airship-template/archive/refs/heads/main.zip).

This project has everything prepared to start building a game on Airship.

* Make sure to unzip after downloading.
* After unzipping, **rename the airship-template-main folder** to the name of your project.\\

### Open in Unity Hub

1.  Add -> Add project from disk.\\

    <figure><img src="../.gitbook/assets/Screenshot 2024-03-12 at 7.42.06 AM.png" alt=""><figcaption></figcaption></figure>
2. Select the unzipped (and renamed!) Starter Template folder.
3. You will be prompted to install a recommended version of Unity for the project. Press yes.

### Opening Unity for the First Time

* You will be prompted to download the Unity Editor. Press yes.
  * Make sure to install the required modules:
    * Android Build Support
    * iOS Build Support
    * Linux Build Support (IL2CPP)
    * Windows Build Support (IL2CPP)

<div align="left"><figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption></figcaption></figure></div>

{% hint style="info" %}
Airship will start downloading required asset packages. This may take a few minutes.
{% endhint %}

If you see an LTS error you may need to restart Unity Hub. Close Unity, and Unity Hub and then reopen Unity Hub and your template project.

<figure><img src="../.gitbook/assets/image (108).png" alt="" width="287"><figcaption></figcaption></figure>

{% hint style="warning" %}
Unity hub may still be open in your system tray. Right click on the unity icon and select "Quit Unity Hub" to fully close it.

<img src="../.gitbook/assets/image (107).png" alt="" data-size="original">
{% endhint %}

### Play the Game

You're now ready to play the game. Click the play button in Unity.\
You should see a character spawn on an empty floor:

<figure><img src="../.gitbook/assets/Screenshot 2024-08-16 at 3.35.32 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If your editor is stuck in an "Untitled Scene", search for "DefaultScene" in the project tab and open it.
{% endhint %}
