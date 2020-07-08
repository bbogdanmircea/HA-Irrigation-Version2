https://www.domoticadiy.it/2020/06/irrigazione-smart-my-garden-irrigation-home-assistant/ is a good reference if you can read italian

1. Install HACS and all components listed in prerequisites.md
    browser_mod (https://github.com/thomasloven/hass-browser_mod) --> configuration.yaml needs edit according to component help
    lovelace_gen (https://github.com/thomasloven/hass-lovelace_gen) --> configuration.yaml needs edit according to component help
    card-mod (https://github.com/thomasloven/lovelace-card-mod)
    hui-element (https://github.com/thomasloven/lovelace-hui-element)
    button-card (https://github.com/custom-cards/button-card)
    config-template-card (https://github.com/iantrich/config-template-card)
    mini-graph-card (https://github.com/kalkih/mini-graph-card)
    layout-card (https://github.com/thomasloven/lovelace-layout-card)
    state-switch (https://github.com/thomasloven/lovelace-state-switch)
    time-picker-card (https://github.com/GeorgeSG/lovelace-time-picker-card)
    
2. Copy/Clone repository locally

3. Create folder packages in the homeassistant configuration folder, insert the following lines in configuration.yaml:
homeassistant:
  packages: !include_dir_named packages
  
4. Copy the lovelace folder in the same config folder where configuration.yaml is

sudo cp -r lovelace /usr/share/hassio/homeassistant

5. Copy the package folder in the config/packages folder

sudo cp -r package /usr/share/hassio/homeassistant/packages/

6. Add a time sensor in configuration.yaml if already not existing in the section sensors:

- platform: time_date
  display_options:
    - 'time'
    - 'date'
    
7. Create a file irrigation.yaml :

title: Irrigation
views:
  - !include lovelace/view_garden_version2.yaml
  
8. Modify configuration.yaml to have main dashboard as storage, and dashboard Irrigation as yaml:

lovelace_gen:

lovelace:
  mode: storage
  dashboards:
    lovelace-irrigation:
      mode: yaml
      title: Irrigation
      icon: mdi:flower
      show_in_sidebar: true
      filename: irrigation.yaml

9. Add the 2 fonts, 
a.If the main dashboard is yaml, then you need to add it to the hacs configuration file:

(notare il percorso /hacsfiles/… in quanto sto utilizzando hassio)

lovelace:
  mode: yaml
  resources:
    - type: module
      url: browser_mod.js
    - type: module
      url: /hacsfiles/mini-graph-card/mini-graph-card-bundle.js
    - type: module
      url: /hacsfiles/lovelace-card-mod/card-mod.js
    - type: module
      url: /hacsfiles/button-card/button-card.js
    - type: module
      url: /hacsfiles/config-template-card/config-template-card.js
    - type: module
      url: /hacsfiles/lovelace-layout-card/layout-card.js
    - type: module
      url: /hacsfiles/lovelace-state-switch/state-switch.js
    - type: module
      url: /hacsfiles/lovelace-hui-element/hui-element.js
    - type: module
      url: /hacsfiles/lovelace-time-picker-card/time-picker-card.js
    - url: https://fonts.googleapis.com/css?family=Oswald
      type: css
    - url: https://fonts.googleapis.com/css?family=Dosis
      type: css
  
  b.If the main dashboard is storage, then you need to add them in Configuration/Dashboard/Resources, add the urls of the 2 fonts as Stylesheets
  
10. If you installed the dark theme, then you need to edit configuration.yaml

frontend:
  themes: !include_dir_merge_named themes
  
11. Restart HA and check the Irrigation dashboard
      


