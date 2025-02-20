---
layout: page
title: "Jewish Calendar"
description: "Instructions on how to integrate the Jewish Calendar sensor within Home Assistant."
date: 2018-09-09 00:00
sidebar: true
comments: false
sharing: true
footer: true
ha_category:
  - Calendar
ha_iot_class: Local Polling
ha_release: 0.79
redirect_from:
 - /components/sensor.jewish_calendar/
---

The Jewish Calendar (`jewish_calendar`) sensor platform displays a variety of information related to the Jewish Calendar as a variety of sensors.

## Configuration

To enable this sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: jewish_calendar
```

{% configuration %}
language:
  required: false
  default: english
  description: Whether to represent the sensors in Hebrew (א' תשרי תשע"ט) or English characters (1 Tishrei 5779). Valid options are 'english' and 'hebrew'.
  type: string
latitude:
  required: false
  description: Latitude for time calculations of the sensor.
  default: Home Assistant location
  type: integer
longitude:
  required: false
  description: Longitude for time calculations of the sensor.
  default: Home Assistant location
  type: integer
diaspora:
  required: false
  description: Consider the location as diaspora or not for calculation of the weekly portion and holidays.
  default: false
  type: string
candle_lighting_minutes_before_sunset:
  required: false
  description: Number of minutes before sunset to report as candle lighting time.
  default: 18
  type: integer
havdalah_minutes_after_sunset:
  required: false
  description: Number of minutes after sunset to report as havdalah time. If this is set to 0, uses the time that the sun is 8.5 degrees below the horizon (same as the 'three_stars' sensor). If non-zero, this value is added as an offset to the time of sunset to report havdalah.
  default: 0
  type: integer
sensors:
  required: false
  default: date
  description: List of available sensors.
  keys:
    date:
      description: Show the hebrew date for today.
    weekly_portion:
      description: Show the weekly portion (parshat hashavu'a).
    holiday_name:
      description: If it is a holiday, show the name of the holiday.
    holyness:
      description: On a scale of 1 to 9 show the level of holyness _(see below)_.
    first_light:
      description: First light of dawn (Alot Hashachar - עלות השחר).
    gra_end_shma:
      description: Last time for reading of the Shma according to the GR"A.
    mga_end_shma:
      description: Last time for reading of the Shma according to the MG"A.
    plag_mincha:
      description: Time of the Plag Hamincha.
    first_stars:
      description: Time at which the first stars are visible (Tset Hakochavim - צאת הכוכבים).
    upcoming_shabbat_candle_lighting:
      description: The time of candle lighting for either the current Shabbat (if it is currently Shabbat) or the immediately upcoming Shabbat.
    upcoming_shabbat_havdalah:
      description: The time of havdalah for either the current Shabbat (if it is currently Shabbat) or the immediately upcoming Shabbat. If it is currently a three-day holiday, this value *could* be None (i.e. if holiday is Sat./Sun./Mon. and it's Saturday, there will be no shabbat_havdalah value. See comments in hdate library for details.)
    upcoming_candle_lighting:
      description: The time of candle lighting for either the current Shabbat OR Yom Tov, or the immediately upcoming Shabbat OR Yom Tov. If, for example, today is Sunday, and Rosh Hashana is Monday night through Wednesday night, this reports the candle lighting for Rosh Hashana on Monday night. This avoids a situation of triggering pre-candle-lighting automations while it is currently Yom Tov. To always get the Shabbat times, use the upcoming_shabbat_candle_lighting sensor.
    upcoming_havdalah:
      description: The time of havdalah for either the current Shabbat OR Yom Tov, or the immediately upcoming Shabbat OR Yom Tov. If, for example, today is Sunday, and Rosh Hashana is Monday night through Wednesday night, this reports the havdalah for Rosh Hashana on Wednesday night. To always get the Shabbat times, use the upcoming_shabbat_havdalah sensor.
    issur_melacha_in_effect:
      description: A boolean sensor indicating if melacha is currently not permitted. The value is true when it is currently Shabbat or Yom Tov and false otherwise.
    omer_count:
      description: An integer sensor indicating the day of the Omer (1-49) or 0 if it is not currently the Omer.

{% endconfiguration %}

### Holyness levels

1. Mido'rayta - by Torah ordination (Rosh Hashana, Yom Kippur, Pesach, Shavuot, Sukkot)
2. Erev Yom Tov
3. Hol Hamo'ed
4. Hanukka and Purim
5. Fast days
6. Modern holidays, e.g. Yom Yerushalayim and Yom Haatsmaut
7. Minor holidays, e.g. Lag ba'omer and Tu bishvat
8. Memorial days: yom hazikaron and yom hashoah
9. Days mentioned by the Israeli parliament: Rabin memorial day, Ze'ev Zhabotinsky day, etc.

## Full configuration sample

```yaml
# Example configuration.yaml entry
sensor:
  - platform: jewish_calendar
    language: english
    diaspora: true
    havdalah_minutes_after_sunset: 50
    sensors:
      - date
      - weekly_portion
      - holiday_name
      - holyness
      - first_light
      - gra_end_shma
      - mga_end_shma
      - plag_mincha
      - first_stars
      - upcoming_candle_lighting
      - upcoming_havdalah
```
