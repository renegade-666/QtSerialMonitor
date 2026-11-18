Fork of QtSerialMonitor project. 
https://github.com/mich-w/QtSerialMonitor/tree/master/src

Altered by ChatGPT to route gyroscope and accelerometer data into separate charts.

## Configuring separate charts

The application supports multiple independent time-series charts. Channel-to-chart assignments and chart captions are read from `charts.json`, located beside the executable. The default configuration routes the gyroscope channels to the first chart and the accelerometer channels to the second chart. No sensor channel names are hardcoded in the chart-routing implementation.

Example:

```json
{
  "charts": [
    {
      "name": "Gyroscope",
      "yAxisLabel": "Angular velocity",
      "channels": ["gx", "gy", "gz"]
    },
    {
      "name": "Accelerometer",
      "yAxisLabel": "Acceleration",
      "channels": ["ax", "ay", "az"]
    }
  ]
}
```

The order of entries determines the chart order: the first entry configures the original chart widget and each subsequent entry creates another chart. Change the `channels` arrays to match the labels emitted by your device. Labels not assigned to either chart are still parsed and remain available to the application's other data consumers, but are not plotted. Add or remove entries in the `charts` array to choose the number of charts (at least one).

CMake copies the default `charts.json` beside the built executable. If you edit the file after building, edit the copy beside the executable so the application loads your changes.
