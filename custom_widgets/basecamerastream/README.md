# A Camera Stream widget for HADashboard.

!!! This widget has been updated to work with Appdaemon version 4.

To use this widget, you need to:
1. Copy the basecamerastream folder to your custom_widgets folder. Your custom_widgets folder should be in your Appdaemon conf directory      and need to be created if it does not exist.
2. copy the camerastream.yaml file from the custom_widgets folder to your custom_widgets folder.
   After copying the above, your custom_widgets folder should have the following structure:
````yaml
   custom_widgets
     camerastream.yaml 
     basecamerastream
       basecamerastream.html
       basecamerastream.js
       basecamerastream.css  
````
   Make sure the folders and files are readable by the user account under which Appdaemon is running.
   
3. Configure a widget:

   Example widget configuration in a .dash file:

````yaml
my_camera:
  widget_type: camerastream
  entity: camera.my_camera
  title: My Camera
  base_url: "http://my_home_assistant_ip:my_ha_port"  
  # e.g. "https://my_duck_dns_domain.duckdns.org:8123" or "http://192.168.1.20:8123"
  log: 1  # optional. Will print some log info in the console for debugging purposes if set to 1.
  
layout:
  - my_camera(4x3)
  ````
  
  The widget just sets the ````src```` of an ````img```` element to:
  ````javascript
  base_url + "/api/camera_proxy_stream/" + name_of_entity + "?token=" + current_camera_token
  ````
  and updates the token when it changes which happens roughly every 5 minutes.
  The token is an attribute of the camera entity, it is not a long-lived access token.
