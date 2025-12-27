# Features

Footfall application provides several more or less independent informations to the customers, which might be separated to features.

## List of features

Each feature is in some phase from idea to real usage by customers. 

| Feature Status     | Description                                                                 | Production ready |
| -------------------| --------------------------------------------------------------------------- | ---------------- |
| Idea               | Investors or customers wisch.                                               | No               |
| PoC                | Proof of Concept. Dev team tries if it even possible.                       | No               |
| Implementation     | Feature is in development right now.                                        | No               |
| Testing            | Implementation is finished and feature is tested.                           | No (!)           |
| First delivery     | Internal testing is finished and feature is in testing run in one customer. | No (!)           |
| Production         | Feature can be presented to customers                                       | Yes              |


### CV features

CV features represents features which requires computer vision techniques which are detected/counted on sensor itself.

| CV Features               | Status        |
| ------------------------- | ------------- |
| Footfall                  | Production    |
| Gender detection          | Production    |
| Group detection           | Production    |
| Age detection             | Testing       |
| Stroller detection        | ???           |
| Heatmaps                  | First delivery |
| Multi-Target Multi-Camera Tracking  | PoC/Implementation |
| Foodcort pickup/order     | PoC/Implementation |
| Stroller                  | ???           |

### Data aggregation

Data aggregation features represents raw data post processing techniques which are done on Cloud.

| Data aggregation             | Status        |
| -------------------------    | ------------- |
| Entrance Groups              | Production    | 
| Occupancy                    | ???           |
| Dwelling time                | ???           |
| Comparison of 2 date periods | Production    |
| Monthly summary report       | Production    |
| Weekly summary report        | Production    |  

### Data presentation

Data presentation features represents way how the data (raw or aggregated) are delivered to customer.

| Data presentation         | Status        |
| ------------------------- | ------------- |
| Web application (Cloud)   | Production    |
| Reporting by email        | Production    |
| Data in Excel             | Production    |
| Data via API              | Production    |