# Last-artwork-sensor-for-home-assistant
Using for remember artwork from last play in media player so card still show picture after stop play


Can use this for calling sensor.

entity_picture: >
 [[[
   return states['sensor.last_album_art'].state;
 ]]]

 or
 
background-image: >
  url('[[[ return states["sensor.last_album_art"].state ]]]')
