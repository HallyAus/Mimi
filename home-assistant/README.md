# Home Assistant Automations

Collection of Home Assistant automation scripts for solar power management and smart home control.

## Structure

```
home-assistant/
├── automations/     # Automation YAML files
├── helpers/         # Input helpers (input_number, input_boolean, etc.)
└── README.md
```

## Automations

### Tapo Solar Control (`automations/tapo_solar_control.yaml`)

Automatically controls a Tapo smart plug based on solar inverter power output.

**Features:**
- Turns ON plug when solar power exceeds threshold (default: 4000W)
- Turns OFF plug after sustained low power (default: 3 consecutive checks below 3500W)
- Hysteresis prevents rapid on/off cycling during fluctuating power
- Daily notification limit (one notification per day)
- Configurable thresholds via UI helpers

**Required Entities:**
- `sensor.solar_inverter_inverter_active_power` - Your solar inverter power sensor
- `switch.dan_smart_plug` - The Tapo smart plug to control
- `notify.mobile_app_daniel` - Mobile app notification service

**Setup:**
1. Create the helpers from `helpers/tapo_solar_helpers.yaml`
2. Copy the automation from `automations/tapo_solar_control.yaml`
3. Adjust entity names to match your setup

## Installation

### Via UI (Recommended)
1. Create helpers: Settings → Devices & Services → Helpers
2. Create automation: Settings → Automations → Create Automation → Edit in YAML

### Via configuration.yaml
```yaml
# Include helpers
input_number: !include helpers/tapo_solar_helpers.yaml
input_boolean: !include helpers/tapo_solar_helpers.yaml

# Include automations
automation: !include_dir_merge_list automations/
```
