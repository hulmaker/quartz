# Communication

Document provides overal description of communication between parts of the system.


|  Sender             |  Direction | Receiver      | What                           |
| ------------------- | -----------| ------------- | -------------------------------|
| Cloud               | asks       | Monitoring    | for images from sensors        |
| Cloud               | sends      | SMPT server   |  PDF reports via email         |
| ?? Cloud            | sends      | CityLight     | new image to be shown          |
| CityLight           | sends      | ?? Monitoring | alive                          | 
| Monitoring          | asks       | Sensor        | for sensor configuration       |
| Monitoring          | sends      | Sensor        | sensor new configuration       |
| Monitoring          | sends      | Sensor        | management commands            |
| Sensor              | sends      | Cloud         | data [format V2 (cloud)]       |
| Sensor              | sends      | Monitoring    | data [format V2 (monitoring)]  |
| Customer(s) servers | asks       | Cloud         | for report data via API        |

[format V2 (cloud)]: Data/footfall-data-format.md#V2-format-definition-for-ic-cloud
[format V2 (monitoring)]: Data/footfall-data-format.md#V2-format-for-ic-monitoring
