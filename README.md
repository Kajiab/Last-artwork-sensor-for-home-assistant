📌 README.md – Last Artwork Sensor for Home Assistant
# 🖼️ Last Artwork Sensor for Home Assistant

Keep showing the artwork in Home Assistant even after the media player stops.

This repository provides a simple **template sensor** that stores the last artwork from your media player — so dashboards and cards can continue showing artwork even when playback is paused or stopped.

Inspired by a community discussion:  
https://community.home-assistant.io/t/getting-the-entity-picture-of-last-active-media-player/483119/2 :contentReference[oaicite:1]{index=1}

---

## 📦 Features

- 🧠 Remembers the **latest artwork** from a media player
- 📌 Works with any media player entity supported in Home Assistant
- 🎨 Allows use of the sensor’s state for `entity_picture` in cards
- 💡 Useful for Persistent UI and Background Artwork dashboards

---

## 🧰 How It Works

When a media player entity plays artwork with an image, this sensor copies the artwork URL.  
Even after the media ends, the sensor holds the last artwork URL so you can continue to display it.

This works by monitoring media player state updates and storing the artwork URL in a sensor using Home Assistant’s template sensor mechanism.

---

## 🛠️ Installation Instructions

### 1. Create Template Sensor

Copy this into your `configuration.yaml`:

```yaml
sensor:
  - platform: template
    sensors:
      last_album_art:
        friendly_name: "Last Album Art"
        attribute_templates:
          artwork: >-
            {% if states.media_player.your_player_entity.attributes.entity_picture %}
              {{ states.media_player.your_player_entity.attributes.entity_picture }}
            {% else %}
              {{ states.sensor.last_album_art.state }}
            {% endif %}
        value_template: >-
          {% if states.media_player.your_player_entity.attributes.entity_picture %}
            {{ states.media_player.your_player_entity.attributes.entity_picture }}
          {% else %}
            {{ states.sensor.last_album_art.state }}
          {% endif %}
```

Replace media_player.your_player_entity with your actual media player entity ID.

📌 Optional: Provide Fallback Artwork

If you want a fallback image when no artwork has been seen yet, create a folder:
```swift
/config/www/fallback_art/
```

Then refer to it in your card like:
```yaml
entity_picture: >-
  {% if states('sensor.last_album_art') %}
    {{ states('sensor.last_album_art') }}
  {% else %}
    /local/fallback_art/no_music.png
  {% endif %}
```

Use the sensor in cards or dashboards to show album art after playback ends.

📊 Example UI Usage
Picture Entity Card
```yaml
type: picture
entity: sensor.last_album_art
image: "{{ state_attr('sensor.last_album_art', 'artwork') }}"
```
Media Player Card with Last Artwork
```yaml
type: custom:mini-media-player
entity: media_player.your_player_entity
artwork: full-cover
```
💡 Notes

The sensor stores just the last artwork URL, so make sure the media_player entity supports entity_picture.

Works with audio and video players supported by Home Assistant.

Great for dashboards that show artwork persistently even when playback stops.

ℹ️ References

Community forum discussing how to display last artwork:
https://community.home-assistant.io/t/getting-the-entity-picture-of-last-active-media-player/483119/2

📜 License

This project is open source and available under the MIT License
.
