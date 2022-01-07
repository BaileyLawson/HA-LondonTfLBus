# HA-LondonTfL

WARNING: still under construction and subject to change often

![Departure details from Canning Town Station Platform 4](https://github.com/morosanmihail/HA-LondonTfL/blob/main/images/example_2.png?raw=true)

Simple Home Assistant sensor to retrieve departures from Transport for London stations.
Each station creates its own sensor.

Just drop into your `custom_components` folder.
After, of course, creating a new folder in there called `london_tfl`, where all the files in this repo will live in.

Sensor state is the next train departure time from the given station and platform (if set).
Attributes contain up to `max` departures.
Sensor name will change to the name of the first departure's destination station.
If you do not want this behaviour, you can change the name of the sensor manually.

You can add integration via the Integrations menu by searching for `London TfL`.
It will auto-populate the line list, then auto-populate the station list with all stations on that line.

Alternatively, you can set it up manually in your `configuration.yaml`, though this is no longer recommended, as getting a station's Naptan ID is not trivial.

Demo configuration:

```
sensor:
  - platform: london_tfl
    name: London TfL
    stops:
      - line: dlr  # Required
        station: 940GZZDLRVC  # Required
      - line: dlr
        station: 940GZZDLCGT
        platform: Platform 4  # Optional. All platforms by default
        max: 3  # Optional. 3 items by default
```


Also available is support for the Upcoming Media card.
Random, yes, but it works as a decent visualiser of all upcoming times.

![Example of Upcoming Media Card](https://github.com/morosanmihail/HA-LondonTfL/blob/main/images/upcoming_media_2.png?raw=true)

For reference, this also uses `card-mod` to make it look slightly nicer with the less information provided.

```
entity: sensor.dlr_from_royal_victoria_dlr_940gzzdlcgt
image_style: fanart
max: 3
title: TFL
type: custom:upcoming-media-card
clock: 24
box_shadows: false
border_color: none
title_size: small
line1_size: little
title_text: To $title
line1_text: at $time
line2_text: ' '
line3_text: ' '
line4_text: ' '
card_mod:
  style: |
    .type-custom-upcoming-media-card {
      background: none !important;
      box-shadow: none !important;
    }

    .type-custom-upcoming-media-card > div {
      padding: 0px !important;
    }

    .lond_fanart {
      border-radius: var(--ha-card-border-radius, 4px);
      background-color: rgb(100, 100, 100);
      background-blend-mode: multiply;
      height: 80px;
    }

    .lond_fan_fanart {
      background: none !important;
      box-shadow: none !important;
    }
```


TODO:
- Add support as a custom HACS repo
- Expand with `/Journey/JourneyResults` API
