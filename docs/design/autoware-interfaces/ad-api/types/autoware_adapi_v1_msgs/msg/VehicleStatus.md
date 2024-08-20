---
# This file is generated by tools/autoware-interfaces/generate.py
title: autoware_adapi_v1_msgs/msg/VehicleStatus
uses:
  - autoware_adapi_v1_msgs/msg/Gear
  - autoware_adapi_v1_msgs/msg/HazardLights
  - autoware_adapi_v1_msgs/msg/TurnIndicators
---

{% extends 'design/autoware-interfaces/templates/autoware-data-type.jinja2' %}
{% block definition %}

```txt
builtin_interfaces/Time stamp
autoware_adapi_v1_msgs/Gear gear
autoware_adapi_v1_msgs/TurnIndicators turn_indicators
autoware_adapi_v1_msgs/HazardLights hazard_lights
float64 steering_tire_angle
```

{% endblock %}