---
layout: page
title: "Sensibo A/C controller"
description: "Instructions on how to integrate Sensibo A/C controller into Home Assistant."
date: 2017-04-01 15:00 +0200
sidebar: true
comments: false
sharing: true
footer: true
logo: sensibo.png
ha_category:
  - Climate
ha_release: 0.44
ha_iot_class: Cloud Polling
redirect_from:
 - /components/climate.sensibo/
---

Integrates [Sensibo](https://sensibo.com) Air Conditioning controller into Home Assistant.

To enable this platform, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
climate:
  - platform: sensibo
    api_key: YOUR_API_KEY
```

{% configuration %}
api_key:
  description: Your Sensibo API key (To get your API key visit <https://home.sensibo.com/me/api>).
  required: true
  type: string
id:
  description: A unit ID or a list of IDs. If none specified then all units accessible by the `api_key` will be used.
  required: false
  type: string
{% endconfiguration %}

<p class="note">
If you create the API key using a dedicated user (and not your main user),
then in the Sensibo app log you will be able to distinguish between actions
done in the app and actions done by Home Assistant.
</p>

### Full config example
```yaml
climate:
  - platform: sensibo
    api_key: YOUR_API_KEY
    id:
      - id1
      - id2
```

### Adding a quick switch example

If you want a "Quick Switch" to turn your AC On / Off, you can do that using the following `Switch Template`:

{% raw %}
```yaml
switch:
  - platform: template
    switches:
      ac:
        friendly_name: "AC"
        value_template: "{{ is_state('climate.ac', 'cool') or is_state('climate.ac', 'heat') or is_state('climate.ac', 'dry') or is_state('climate.ac', 'heat')}}"
        turn_on:
          service: climate.set_havc_mode
          data:
            entity_id: climate.ac
            hvac_mode: off
        turn_off:
          service: climate.set_havc_mode
          data:
            entity_id: climate.ac
            hvac_mode: 
```
{% endraw %}
