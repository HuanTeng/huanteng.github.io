`门磁`

```
{
  type: "DoorSensorsChanged-v1-#{u.user_uniq_id}",
  content: {
    door_sensor_id: ,
    alert_status: ,
    alert_mode: ,
    is_open:
  }
}
```

`开关量采集器`

```
{
  type: "IoDetectorChanged-v1-#{user.user_uniq_id}",
  content: {
    device_identifier: ,
    io_detector_id: ,
    state:
  }
}
```

`设备在线离线状态改变`

```
{
  type: "DeviceConnectivity-v1-#{u.user_uniq_id}",
  content: {
      device_identifier: ,
      connectivity_string: ,
      reason: ,
      connectivity:
  }
}
```

`灯泡状态改变`

```
{
  type: "BulbsChanged-v2-#{u.user_uniq_id}",
  content: {
    device_identifier: ,
    bulb_id: ,
    wall_switch_id: ,
    channel: ,
    hue: ,
    brightness: ,
    turned_on: ,
    script_end_time:
  }
}
```

`红外`

```
{
  type: "InfraredSensorsChanged-v1-#{u.user_uniq_id}",
  content: {
    infrared_sensor_id: ,
    channel: ,
    active: ,
    time: ,
    cfg_parameters_7: ,
    version:
  }
}
```

`随心开关`

```
{
  type: "SwitchesChanged-v1-#{u.user_uniq_id}",
  content: {
    switch_id:
  }
}
```

`墙壁开关长按`

```
{
  type: "WallSwitchPressed-v1-#{u.user_uniq_id}",
  content: {
    type: ,
    channel: ,
    switch_id:
  }
}
```

`随心开关长按`

```
{
  type: "SwitchPressed-v1-#{u.user_uniq_id}",
  content: {
    type: ,
    switch_id:
  }
}
```

`墙壁开关发生变化`

```
{
  type: "WallSwitchesChanged-v1-#{u.user_uniq_id}",
  content: {
    wall_switch_id: ,
    device_identifier: ,
    status: ,
    change_mask:
  }
}
```

`创建灯组`

```
{
  type: "GroupCreated-v1-#{user.user_uniq_id}",
  content: {
      group_id: ,
      bulb_ids:
  }
}
```

`安防模式变化`

```
{
  type: "SecurityPatternsChanged-v1-#{u.user_uniq_id}",
  content: {
    id: ,
    state: ,
    state_summary: ,
  }
}
```

`通用模块发生变化`

```
{
  type: ,
  content:
}
```

`用户离家回家`

```
{
  "type": "UserEvent-v1-#{user.user_uniq_id}",
  "content": {
    "user_uniq_id": xx,
    "event": enum["back", "leave"],
    "distance": distance(int)
  }
}
```
