---
# This file is generated by tools/autoware-interfaces/generate.py
title: autoware_adapi_v1_msgs/srv/SetDoorCommand
uses:
  - autoware_adapi_v1_msgs/msg/DoorCommand
  - autoware_adapi_v1_msgs/msg/ResponseStatus
---

{% extends 'design/autoware-interfaces/templates/autoware-data-type.jinja2' %}
{% block definition %}

```txt
autoware_adapi_v1_msgs/DoorCommand[] doors
---
autoware_adapi_v1_msgs/ResponseStatus status
```

{% endblock %}