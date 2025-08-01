# Editing a Package

## Development Setup

Once you've created your package, go to an instance of Unity with Airship installed. To set up your package for development:

1. In the toolbar, go to Airship -> Airship Packages.
2. Click on the Create New Package section.
3. In the Package ID field, paste in the full Package ID from the website, e.g. `@YourOrg/PackageName`.
4. Click on Create Package.

This will create a new directory, e.g. `Assets/AirshipPackages/@YourOrg/PackageName`. Anything in this directory pertains to your package.

## First Publish

When you're ready to publish, go back to the Airship Packages window. Find your package and click Publish All. Do _not_ click on Publish Code, as this will not work for the first publish.

## Subsequent Publishes

If the only changes to your package are code (TypeScript files), then you may use the Publish Code button. This is much quicker than Publish All.

If your changes contain non-code assets (e.g. an image), you must publish with Publish All, or else the publish may skip over your non-code asset changes.

## Using the Package

Your package is now ready to be used by yourself or anyone else. If you open another Airship project, you can include your new package by going to the Airship Packages window -> Add Package, and putting in the full name of your package. Clicking Add Package will then download the latest version of the package.

{% hint style="info" %}
If you use the package in the same game in which it's developed, then the game will always be using the local version of the package, _not_ the published version. For this reason, it may be beneficial to have a separate project specifically for your package. This also gives you a dedicated project in which to test your package.
{% endhint %}
