# Last-artwork-sensor-for-home-assistant
Using for remember artwork from last play in media player so card still show picture after stop play
Inspiration from this topic https://community.home-assistant.io/t/getting-the-entity-picture-of-last-active-media-player/483119/2


Add code to configuration.yaml

Can use this for calling sensor.

entity_picture: >
 [[[
   return states['sensor.last_album_art'].state;
 ]]]

 or
 
background-image: >
  url('[[[ return states["sensor.last_album_art"].state ]]]')
