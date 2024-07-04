# FTA analysis for planning module

## Definition of planning module(temp)

For the planning module, define nodes with "planning" as the namespace prefix at the beginning of their names.

| Node Name                                                                                |
| ---------------------------------------------------------------------------------------- |
| `/planning/mission_planning/mission_planner`                                             |
| `/planning/mission_planning/mission_planner_container`                                   |
| `/planning/mission_planning/route_selector`                                              |
| `/planning/planning_evaluator`                                                           |
| `/planning/planning_validator`                                                           |
| `/planning/scenario_planning/external_velocity_limit_selector`                           |
| `/planning/scenario_planning/lane_driving/behavior_planning/behavior_path_planner`       |
| `/planning/scenario_planning/lane_driving/behavior_planning/behavior_planning_container` |
| `/planning/scenario_planning/lane_driving/behavior_planning/behavior_velocity_planner`   |
| `/planning/scenario_planning/lane_driving/motion_planning/elastic_band_smoother`         |
| `/planning/scenario_planning/lane_driving/motion_planning/motion_planning_container`     |
| `/planning/scenario_planning/lane_driving/motion_planning/motion_velocity_planner`       |
| `/planning/scenario_planning/lane_driving/motion_planning/obstacle_cruise_planner`       |
| `/planning/scenario_planning/lane_driving/motion_planning/path_optimizer`                |
| `/planning/scenario_planning/lane_driving/motion_planning/surround_obstacle_checker`     |
| `/planning/scenario_planning/parking/costmap_generator`                                  |
| `/planning/scenario_planning/parking/freespace_planner`                                  |
| `/planning/scenario_planning/parking/parking_container`                                  |
| `/planning/scenario_planning/scenario_selector`                                          |
| `/planning/scenario_planning/velocity_smoother`                                          |
| `/planning/scenario_planning/velocity_smoother_container`                                |

## Input and output of planning module

Inputs will be topics that the planning module subscribes to from external modules.
Outputs will be topics that are published to the control module.
Summarizing based on [pilot-auto](https://github.com/tier4/pilot-auto) as of July 4, 2024

### Input

| topic name                                              | meaning                                                                                                                                                                                                                                                                                          | from         | to (omitted if there are many)                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------------------------------------------------------- |
| `/planning/scenario_planning/max_velocity_default`      | maximum velocity of the ego vehicle                                                                                                                                                                                                                                                              | api          | external_velocity_limit_selector behavior_velocity_planner |
| `/system/operation_mode/state`                          | operation mode about [operation mode](https://tier4.github.io/autoware-documentation/latest/design/autoware-interfaces/ad-api/features/operation_mode/) and [topic type](https://tier4.github.io/autoware-documentation/latest/design/autoware-interfaces/ad-api/list/api/operation_mode/state/) | system       | behavior_path_planner velocity_smoother                    |
| `/map/vector_map`                                       | lanelet information                                                                                                                                                                                                                                                                              | map          | -                                                          |
| `/localization/kinematic_state`                         | ego position                                                                                                                                                                                                                                                                                     | localization | -                                                          |
| `/localization/acceleration`                            | ego acceleration                                                                                                                                                                                                                                                                                 | localization | -                                                          |
| `/tf`                                                   | information for coordinate translation                                                                                                                                                                                                                                                           | localization | -                                                          |
| `/tf_static`                                            | broadcast viewer frames                                                                                                                                                                                                                                                                          | localization | -                                                          |
| `/perception/object_recognition/objects`                | dynamic objects                                                                                                                                                                                                                                                                                  | perception   | -                                                          |
| `/perception/occupancy_grid_map/map`                    | occupancy grid map                                                                                                                                                                                                                                                                               | perception   | -                                                          |
| `/perception/obstacle_segmentation/pointcloud`          | point cloud of obstacles which the ego-vehicle should stop or avoid                                                                                                                                                                                                                              | perception   | -                                                          |
| `/perception/traffic_light_recognition/traffic_signals` | traffic light information                                                                                                                                                                                                                                                                        | perception   | -                                                          |

For those inputs to the planning module where the subscribed nodes are essentially non-functional, categorize them in following table

| topic name                                                                                              | meaning                          | from       | to                        |
| ------------------------------------------------------------------------------------------------------- | -------------------------------- | ---------- | ------------------------- |
| `/perception/virtual_traffic_light_states`                                                              | virtual traffic light states     | perception | motion_velocity_planner   |
| `/awapi/tmp/virtual_traffic_light_states`                                                               | virtual traffic light states     | api        | behavior_velocity_planner |
| `/planning/scenario_planning/lane_driving/behavior_planning/behavior_path_planner/input/lateral_offset` | side shift request from operator | hmi        | behavior_path_planner     |

### Output

| topic name                               | meaning                   | from                  | to (omitted if there are many) |
| ---------------------------------------- | ------------------------- | --------------------- | ------------------------------ |
| `/planning/hazard_lights_cmd`            | hazard light              | behavior_path_planner | vehicle_cmd_gate               |
| `/planning/turn_indicators_cmd`          | turn indicator            | behavior_path_planner | vehicle_cmd_gate               |
| `/planning/mission_planning/route`       | route                     | mission_planning      | lane_departure_checker_node    |
| `/planning/scenario_planning/trajectory` | trajectory to be followed | planning              | -                              |

## Feature diagram

While some minor changes are necessary to align with the current implementation, the functional structure conforms to the current state.

![feature-diagram](image/planning-diagram-tmp.drawio-for-FTA.drawio.svg)
