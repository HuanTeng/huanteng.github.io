`门磁`

```
{
  "type": "DoorSensorsChanged-v2-1462353745",
  "content": {
    "door_sensor_id": 1126,
    "is_open": false,
    "alert_mode": 0,
    "alert_status": 1,
    "behaviors": [{
      "action": "close",
      "timestamp": 1462934721000
    }]
  }
}
```

`开关量采集器`

```
{
  "type": "IoDetectorChanged-v1-#{user.user_uniq_id}",
  "content": {
    "device_identifier": "K1",
    "io_detector_id": 1,
    "state": true
  }
}
```

`设备在线离线状态改变`

```
{
  "type": "DeviceConnectivity-v1-#{u.user_uniq_id}",
  "content": {
      "device_identifier": "B293",
      "connectivity_string": "离线",
      "reason": "",
      "connectivity": 2
  }
}
```

`灯泡状态改变`

```
{
  "type": "BulbsChanged-v2-#{u.user_uniq_id}",
  "content": {
      "device_identifier": "B293",
      "bulb_id: 2491,
      "wall_switch_id": 83,
      "channel": 1
      "hue": 0.0,
      "brightness": 0.0,
      "turned_on": false,
      "script_end_time":
  }
}
```

`红外`

```
{
  "type": "InfraredSensorsChanged-v1-#{u.user_uniq_id}",
  "content": {
      "infrared_sensor_id": 1,
      "channel": 7,
      "active": ,
      "time": ,
      "cfg_parameters_7": {
        "wait": 600,
        "ratio": 4,
        "count": 2
      },
      "version": 0
  }
}
```

`随心开关`

```
{
  "type": "SwitchesChanged-v1-#{u.user_uniq_id}",
  "content": {
    "switch_id": 118
  }
}
```

`墙壁开关长按`

```
{
  "type": "WallSwitchPressed-v1-#{u.user_uniq_id}",
  "content": {
    "type": ,
    "channel": ,
    "switch_id":
  }
}
```

`随心开关长按`

```
{
  "type": "SwitchPressed-v1-#{u.user_uniq_id}",
  "content": {
    "type": ,
    "switch_id":
  }
}
```

`墙壁开关`

```
{
  "type": "WallSwitchesChanged-v1-#{u.user_uniq_id}",
  "content": {
    "wall_switch_id": ,
    "device_identifier":,
    "status": ,
    "change_mask":
  }
}
```
