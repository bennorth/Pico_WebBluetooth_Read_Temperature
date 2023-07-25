 * Load webpage
 * Click `Connect`, choose Pico, let a few readings come in.
 * Click `Disconnect`, wait a couple of seconds.
 * Click `Connect`, choose Pico, let a few readings come in.

Expected behaviour: On the second connect, a *new* event listener
should be attached, with the id value `5002`.  So I was expecting all
readings which came in after the second `Connect` to log the id
`5002`.

Actual behaviour:

Without the `stopNotifications()` call:

```
2023-07-25T07:28:51.108Z : discoverDevices
2023-07-25T07:28:53.499Z : > Name:Pico D8:3A:DD:1C:56:86
2023-07-25T07:28:53.499Z : > Id:9hrRyLa5+61tGqegjjEm5g==
2023-07-25T07:28:53.499Z : [object BluetoothDevice]
2023-07-25T07:28:53.499Z : Connecting to GATT Server...
2023-07-25T07:28:54.569Z : Getting Service...
2023-07-25T07:28:55.280Z : Getting Temperature Characteristic...
2023-07-25T07:28:55.280Z : Stopping notifications
2023-07-25T07:28:55.280Z : making event listener with id 5001
2023-07-25T07:28:55.281Z : Adding event listener with handlerClosureId 5001
2023-07-25T07:28:55.281Z : Enabling notifications...
2023-07-25T07:28:55.282Z : Connected to Pico D8:3A:DD:1C:56:86
2023-07-25T07:28:55.282Z : Notifications have been started.
2023-07-25T07:28:55.470Z : Got temp: 18.61781 / 5001
2023-07-25T07:28:55.969Z : Got temp: 19.08595 / 5001
2023-07-25T07:28:56.470Z : Got temp: 18.61781 / 5001
2023-07-25T07:28:56.969Z : Got temp: 18.61781 / 5001
2023-07-25T07:28:57.469Z : Got temp: 18.61781 / 5001
2023-07-25T07:28:57.801Z : Device Pico D8:3A:DD:1C:56:86 is disconnected.
2023-07-25T07:29:05.305Z : discoverDevices
2023-07-25T07:29:07.792Z : > Name:Pico D8:3A:DD:1C:56:86
2023-07-25T07:29:07.792Z : > Id:9hrRyLa5+61tGqegjjEm5g==
2023-07-25T07:29:07.792Z : [object BluetoothDevice]
2023-07-25T07:29:07.793Z : Connecting to GATT Server...
2023-07-25T07:29:08.919Z : Getting Service...
2023-07-25T07:29:09.121Z : Got temp: 19.08595 / 5001
2023-07-25T07:29:09.569Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:09.632Z : Getting Temperature Characteristic...
2023-07-25T07:29:09.633Z : Stopping notifications
2023-07-25T07:29:09.633Z : making event listener with id 5002
2023-07-25T07:29:09.633Z : Adding event listener with handlerClosureId 5002
2023-07-25T07:29:09.633Z : Enabling notifications...
2023-07-25T07:29:09.635Z : Connected to Pico D8:3A:DD:1C:56:86
2023-07-25T07:29:09.635Z : Notifications have been started.
2023-07-25T07:29:10.069Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:10.569Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:11.068Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:11.570Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:12.070Z : Got temp: 18.61781 / 5001
2023-07-25T07:29:12.372Z : Device Pico D8:3A:DD:1C:56:86 is disconnected.
```

We never see any output from the closure with id `5002`.

With the `stopNotifications()` call:

```
2023-07-25T07:30:14.967Z : discoverDevices
2023-07-25T07:30:16.745Z : > Name:MPY BTSTACK
2023-07-25T07:30:16.745Z : > Id:9hrRyLa5+61tGqegjjEm5g==
2023-07-25T07:30:16.745Z : [object BluetoothDevice]
2023-07-25T07:30:16.745Z : Connecting to GATT Server...
2023-07-25T07:30:17.818Z : Getting Service...
2023-07-25T07:30:18.530Z : Getting Temperature Characteristic...
2023-07-25T07:30:18.530Z : Stopping notifications
2023-07-25T07:30:18.532Z : making event listener with id 5001
2023-07-25T07:30:18.532Z : Adding event listener with handlerClosureId 5001
2023-07-25T07:30:18.532Z : Enabling notifications...
2023-07-25T07:30:18.534Z : Connected to MPY BTSTACK
2023-07-25T07:30:18.535Z : Notifications have been started.
2023-07-25T07:30:19.020Z : Got temp: 19.08595 / 5001
2023-07-25T07:30:19.520Z : Got temp: 19.08595 / 5001
2023-07-25T07:30:20.020Z : Got temp: 18.61781 / 5001
2023-07-25T07:30:20.520Z : Got temp: 19.08595 / 5001
2023-07-25T07:30:21.019Z : Got temp: 18.61781 / 5001
2023-07-25T07:30:21.519Z : Got temp: 19.08595 / 5001
2023-07-25T07:30:21.937Z : Device MPY BTSTACK is disconnected.
2023-07-25T07:30:24.927Z : discoverDevices
2023-07-25T07:30:26.964Z : > Name:MPY BTSTACK
2023-07-25T07:30:26.964Z : > Id:9hrRyLa5+61tGqegjjEm5g==
2023-07-25T07:30:26.964Z : [object BluetoothDevice]
2023-07-25T07:30:26.964Z : Connecting to GATT Server...
2023-07-25T07:30:28.819Z : Getting Service...
2023-07-25T07:30:29.070Z : Got temp: 19.08595 / 5001
2023-07-25T07:30:29.530Z : Getting Temperature Characteristic...
2023-07-25T07:30:29.530Z : Stopping notifications
2023-07-25T07:30:29.532Z : making event listener with id 5002
2023-07-25T07:30:29.532Z : Adding event listener with handlerClosureId 5002
2023-07-25T07:30:29.532Z : Enabling notifications...
2023-07-25T07:30:29.719Z : Connected to MPY BTSTACK
2023-07-25T07:30:29.719Z : Notifications have been started.
2023-07-25T07:30:29.719Z : Got temp: 18.61781 / 5002
2023-07-25T07:30:30.069Z : Got temp: 19.08595 / 5002
2023-07-25T07:30:30.620Z : Got temp: 19.08595 / 5002
2023-07-25T07:30:31.120Z : Got temp: 19.08595 / 5002
2023-07-25T07:30:31.604Z : Device MPY BTSTACK is disconnected.
```

We still get a stray invocation of the `5001` closure in the second
connection, but this now mostly works.
