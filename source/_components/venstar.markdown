---
layout: page
title: "Venstar Thermostat"
description: "Instructions for how to integrate Venstar WiFi thermostats within Home Assistant."
date: 2018-01-14 00:04
sidebar: true
comments: false
sharing: true
footer: true
logo: venstar.png
ha_category:
  - Climate
ha_release: 0.62
ha_iot_class: Local Polling
redirect_from:
 - /components/climate.venstar/
---


The `venstar` climate platform allows you to control [Venstar](http://www.venstar.com) thermostats from Home Assistant.
Venstar thermostats feature a local API that allows for automation without the need for a cloud service.

Currently supported and tested thermostats:

- Color Touch T7900

Currently supported functionality:
- Setting heat/cool temperature when the thermostat is in the appropriate mode.
- Changing the operation mode of the thermostat (heat/cool/off/auto)
- Turning the fan on/off
- Reading and setting the humidity level and limits
- Turning on away preset
- Turning on hold mode preset

The following values are supported for the hold_mode state attribute:
- `off`: *Enables* the scheduling functionality.
- `temperature`: *Disables* the schedule and holds the set temperature indefinitely.

Note - Please ensure you update your thermostat to the latest firmware. Currently tested on firmware 5.10.

To set it up, add the following information to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
climate:
  - platform: venstar
    host: IP_OR_HOSTNAME_OF_THERMOSTAT
```

{% configuration %}
host:
  description: Address of your thermostat, e.g., 192.168.1.32.
  required: true
  type: string
username:
  description: Username for the thermostat.
  required: false
  type: string
password:
  description:  Password for the thermostat.
  required: false
  type: string
ssl:
  description: Whether to use SSL or not when communicating.
  required: false
  type: boolean
  default: false
timeout:
  description: Number of seconds for API timeout.
  required: false
  type: integer
  default: 5
humidifier:
  description: Report humidity and expose humidifier setpoints.
  required: false
  type: boolean
  default: true
{% endconfiguration %}

## Full configuration sample

```yaml
# Example configuration.yaml entry
climate:
  - platform: venstar
    host: IP_OR_HOSTNAME_OF_THERMOSTAT
    ssl: true
    username: OPTIONAL_AUTH_USER_HERE
    password: OPTIONAL_AUTH_PASS_HERE
    timeout: 5
    humidifier: false
```
