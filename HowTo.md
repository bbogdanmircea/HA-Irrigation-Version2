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

