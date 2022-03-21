---
title: Updater
description: Detecting when Home Assistant updates are available.
ha_category:
  - Binary Sensor
ha_release: 0.8
ha_iot_class: Cloud Polling
ha_quality_scale: internal
ha_codeowners:
  - '@home-assistant/core'
ha_domain: updater
ha_platforms:
  - binary_sensor
---

<div class='note warning'>

This integration is deprecated and will be removed in Home Assistant Core 2022.5.
Please check the [breaking changes](https://www.home-assistant.io/blog/2022/03/02/release-20223/#breaking-changes) section of the release [2022.3.5](https://www.home-assistant.io/blog/2022/03/02/release-20223/#release-202235---march-15) for more information.

</div>

The `updater` binary sensor will check daily for new releases of the Home
Assistant Core. The state will be "on" when an update is available. Otherwise,
the state will be "off". The newer version, as well as the link to the release
notes, are attributes of the updater.

## Configuration

```yaml
# Example configuration.yaml entry
updater:
```

## Notification

For an added bonus, an automation integration can be created to send a message with a notifier when that state of this component's entity changes.

{% raw %}

```yaml
# Example configuration.yaml entry
automation:
  - alias: "Update Available Notification"
    trigger:
      - platform: state
        entity_id: binary_sensor.updater
        from: "off"
        to: "on"
    action:
      - service: notify.notify
        data:
          message: "Home Assistant {{ state_attr('binary_sensor.updater', 'newest_version') }} is available."
```

{% endraw %}
