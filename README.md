# My Home Assistant Blueprints

## Notify everybody at home

Easily create scripts that allow you to notify everybody who is currently at home. Requires that you use the person component with presence detection, and have at least some notify services that target a specific person. Tested with the mobile app on Android only.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fcrnh%2Fhome-assistant-blueprints%2Fblob%2Fmain%2Fnotify_everybody_at_home.yaml)

This blueprint creates a script which can be used like most `notify` services. When you call the script, it checks if the person is at home; if so, the notification is sent.

### Configuration

In order to create the script, you need to supply a mapping of person names with their corresponding notify services. Say you've got two persons, Lisa and John, resulting in two `person` entities: `person.lisa` and `person.john`. For Lisa, you want to send a notification to `notify.lisa`, and for John, you want to send a notification to `notify.mobile_app_john`. The mapping will then look like this:

```yaml
lisa: notify.lisa
john: notify.mobile_app_john
```

### Usage

The blueprint will create a script, e.g. `script.notify_everybody_at_home`, which you can supply with a number of parameters. These are documented in the script and shown in the service developer tools.

[![Open your Home Assistant instance and show your service developer tools with a specific service selected.](https://my.home-assistant.io/badges/developer_call_service.svg)](https://my.home-assistant.io/redirect/developer_call_service/?service=script.notify_everybody_at_home)

The following parameters can be specified:

- `message`: Notification text.
- `title`: Notification title.
- `data`: Notification data, depends on the platform used to send the notification.
- `persons`: List of persons you want to notify, useful if you want to send the notification only to a specific set of people. If not specified, all persons configured in the blueprint are notified.

The `message`, `title` and `data` parameters are passed directly to the configured `notify` services.

### Limitations

The script calls all the notification services with the same data object (if supplied). It may therefore not work if you are using different notification platforms, e.g. the Android app and Pushbullet. In some cases, you can solve this kind of problems by creating a notify group. 
