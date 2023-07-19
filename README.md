# homebridge-hubitat-makerapi

[![npm version](https://badge.fury.io/js/homebridge-hubitat-mediainputsource.svg)](https://badge.fury.io/js/homebridge-hubitat-mediainputsource)
![NPM Downloads](https://img.shields.io/npm/dw/:homebridge-hubitat-mediainputsource)

[![Packaging status](https://repology.org/badge/vertical-allrepos/homebridge-hubitat-mediainputsource.svg)](https://repology.org/project/homebridge-hubitat-mediainputsource/versions)

My Hubitat driver for an HDMI switch (https://github.com/joelwetzel/Hubitat-4KMX42-H2A) implements Hubitat's "MediaInputSource" capability.  This capability allows for switching between two different inputs.

Unfortunately, it's not well supported yet.  I don't think it's used very often.  I use this HomeBridge plugin to connect my Hubitat to HomeKit:  https://github.com/danTapps/homebridge-hubitat-makerapi.  Unfortunately, it does not support "MediaInputSource".

However, I used it as a base to make my own HomeBridge plugin.  My plugin is here: 

The plugin is also registered with NPM, so you can add it to any HomeBridge by searching for and installing homebridge-hubitat-mediainputsource.  A valid config for the plugin will look like:

> {
> 
>     "platform": "Hubitat-MakerAPI-HDMI-Switch",
> 
>     "name": "Hubitat-MakerAPI-HDMI-Switch",
> 
>     "app_url": "http://192.168.1.113/apps/api/2/",
> 
>     "access_token": "REDACTED"
> 
> }

My plugin queries Hubitat just like danTapps's plugin, but it ONLY looks for Hubitat devices with the MediaInputSource capability. It translates it into an appropriate accessory type in HomeKit.  In HomeKit, the accessory has a category of TELEVISION, and has 3 services:  Television, InputSource, and Switch.  In the HomeApp, this renders it as a screen with a power button and an input selector.

Extra installation step:  Television devices have to be published as an "external accessory" in homebridge.  This means they won't be included by default when adding the HomeBridge to your Home app.  The television device has to be added separately.

You'll need to open your HomeBridge Status page.  When you restart the HomeBridge, you'll see log lines like:
>[18/07/2023, 13:23:58] Family Room HDMI Switch D6F0 is running on port 38779.
>
>[18/07/2023, 13:23:58] Please add [Family Room HDMI Switch D6F0] manually in Home app. Setup Code: 786-74-406

You can then add the accessory in the home app using that setup code.

Issue:  The Home app on iPhone has a UI bug involving television pickers.  Sometimes, when you turn the power on, the input selector becomes deactivated, and if you oscillate power on and off, the input selector's activation status will always be the opposite of what it should be.  Therefore, I don't really use it directly.  I use the Scenes to control everything.



