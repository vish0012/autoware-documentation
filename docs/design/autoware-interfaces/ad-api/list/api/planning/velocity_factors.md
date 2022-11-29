<!-- This file is generated by a tool. Do not edit directly. -->

# /api/planning/velocity_factors

- Method: realtime stream
- Type: [autoware_adapi_v1_msgs/msg/VelocityFactorArray](../../../types/autoware_adapi_v1_msgs/msg/velocity_factor_array.md)

## Description

Get the velocity factors, sorted in ascending order of distance.
For details, see the [planning](./index.md).

## Message

| Name             | Type                   | Description                                        |
| ---------------- | ---------------------- | -------------------------------------------------- |
| factors.pose     | geometry_msgs/msg/Pose | The base link pose related to the velocity factor. |
| factors.distance | float32                | The distance from the base link to the above pose. |
| factors.type     | uint16                 | The type of the velocity factor.                   |
| factors.status   | uint16                 | The status of the velocity factor.                 |
| factors.detail   | string                 | The additional information of the velocity factor. |