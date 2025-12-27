# Task Specification: 
## Create semi-automated approach for CARB monthly reporting
Creating epic for visibility on an item that has been communicated.

We will need by August 15, 2025, and on the 15th of each month thereafter, to send CARB a report reporting on RailState performance stats for all public and active sensors in California.

We have cancellation clauses if we fall below the following state:
- Locomotive ID Average accuracy is below 70% for 3 consecutive months (some force majeure items excluded)
- 5 or more incidents of sensors being inoperative for more than 15
 days within any 1 month period (some force majeure items excluded)
As such, we need a simple report by sensor (and summarized) indicating:
- Locomotive ID capture rate/accuracy
- Sensor uptime/downtime

### The report should contain:
2. Locomotive ID recognition – percent of human readable locomotive numbers captured and confidence level.
3. Locomotive Emissions Tier recognition – percent of locomotive ID with EPA emissions tier reported.
4. Railcar type recognition – percent of railcars with recognized car type (tank car, covered hopper, etc.).
5. Container type recognition – percent of containers with recognized container types (53 foot, 40 foot, 20 foot, other).

---

## Development Specifications
### Report Design
detailed per sensor (excel sheet with columns):
	- Locomotive ID accuracy: float
	- days inoperative: int
	- uptime: float
summary (numbers - single row):
- human readable Locomotive ID: float
- Emissions Tier recognition: float
- railcar type matching: float
- container type matching: float

## Task Breakdown

### 1. **Sensor Discovery and Data Pre-Fetching (SQL+API)**
- **T1.1** Fetch list of all active public sensors in California. (use sql)
- **T1.2** Fetch locomotive sightings from these sensors.  
- **T1.3** Fetch general sightings (cars and containers) for these sensors.  

- **T2.1** Get sensor availability/outage data.
- **T2.2** Get EPA emission tier per locomotive.
### 2. **Annotation Jobs**
- **T3.1** Create annotation jobs for locomotive ID. (per-sensor)
- **T3.2** Create annotation jobs for car and container types.  (uniform)
### 3. **Evaluation and Metric Calculation**
- **T4.1** Evaluate locomotive ID recognition accuracy.
- **T4.2** Calculate uptime and downtime.
- **T4.3** Evaluate emissions tier recognition rate for locomotives.
- **T4.4** Evaluate railcar type recognition accuracy.
- **T4.5** Evaluate container type recognition accuracy.
### 4. **Report Generation and Delivery**
- **T5.1** Generate per-sensor Excel sheet. (Columns: sensor ID, locomotive ID ACC, inoperative days, uptime.)
- **T5.2** Generate summary. (average values for each category)

- **T6.1** Compose email with summary and attach Excel report.
- **T6.2** Send report to CARB mailing list by the 15th of each month.

