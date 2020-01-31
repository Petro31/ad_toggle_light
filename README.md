# Home Assistant Light Toggle Automation for Appdaemon

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)
<br><a href="https://www.buymeacoffee.com/Petro31" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-black.png" width="150px" height="35px" alt="Buy Me A Coffee" style="height: 35px !important;width: 150px !important;" ></a>

_Toggle Light Automation app for AppDaemon._

Simply toggles a light based on another light.  You can set the light service data.

## Installation

Download the `toggle_light` directory from inside the `apps` directory to your local `apps` directory, then add the configuration to enable the `hacs` module.

## Example App configuration

#### Simple switch
```yaml
office_toggle:
  module: toggle_light
  class: ToggleLight
  entity: switch.office_switch
  entities:
    - switch.office_outlet
```

#### Turn on light when TV turns on, only at night.
```yaml
tv_toggle:
  module: toggle_light
  class: ToggleLight
  entity: remote.tv
  turn_off: false
  sundown: true
  entities:
    - light.living_room
```

#### Advanced 
```yaml
office_toggle
  module: toggle_light
  class: ToggleLight
  entity: switch.office_switch
  entities:
  - switch.office_outlet
  - entity: light.office_lamp
    service_data:
      brightness: 100
      kelvin: 2700
  - entity: light.office_mood
    service_data:
      brightness: 130
      rgb_color: [255,0,0]
  log_level: INFO
```

#### App Configuration
key | optional | type | default | description
-- | -- | -- | -- | --
`module` | False | string | `toggle_light` | The module name of the app.
`class` | False | string | `ToggleLight` | The name of the Class.
`entity` | False | string | | entity_id of light/switch/sensor etc.
`entities`| False | list | | A list of entity_id's or entity objects.
`turn_on` | False | bool | `true` | enables/disables the turn_on command when `entity` is toggled.
`turn_off` | False | bool | `true` | enables/disables the turn_off command when `entity` is toggled.
`sundown` | False | bool | `false` | only allows the toggle to occur when the sun is down.
`log_level` | True | `'INFO'` &#124; `'DEBUG'` | `'INFO'` | Switches log level.

#### Entity Object Configuration
key | optional | type | default | description
-- | -- | -- | -- | --
`entity` | False | string | | The entity_id of the switch or light.
`service_data` | True | map | | Turn on service data.  Whenever the door turns on a light or switch, this data will be passed to the service data.  Warning: Use only valid combinations.  Light combinations are not validated and can cause errors in Home Assistant.
