# Footfall data format

Historically footfall was  V1 and V1.5 format. ( not used anymore )

## V2 format definition for iC Cloud

- JSON format
- Currently used by all sensors.

```rust
#[derive(Default, Debug, Clone, PartialEq, Serialize, ToSchema, Deserialize)]
pub struct FootfallDataV2 {
    /// Not send from footfall
    /// Added on icclient side -> hostname 
    #[serde(skip_serializing_if = "Option::is_none")]
    pub name: Option<String>,
    pub ent_in: i32,
    pub time_in: String,
    pub ent_out: i32,
    pub time_out: String,
    #[serde(skip_serializing_if = "Vec::is_empty")]
    #[serde(default)]
    pub detections: Vec<DetectionV2>,
    #[serde(skip_serializing_if = "Vec::is_empty")]
    #[serde(default)]
    pub features: Vec<Feature>,
    #[serde(skip_serializing_if = "Option::is_none")]   
    #[serde(default)]
    pub group_id: Option<i32>,
}

#[derive(Default, Debug, Clone, PartialEq, ToSchema, Serialize, Deserialize)]
pub struct DetectionV2 {
    pub x: f32,
    pub y: f32,
    pub t: String,
    #[serde(skip_serializing_if = "Option::is_none")]
    pub ix: Option<i32>,
    #[serde(skip_serializing_if = "Option::is_none")]
    pub iy: Option<i32>,
}
```

### Example data for unittesting

- [Full version: footfall_traffic_v2-full.json](footfall_traffic_v2-full.json)
- [Minimal version:footfall_traffic_v2-min.json](footfall_traffic_v2-min.json)

## V2 format for iC Monitoring

- binary gRPC format 
- Used by all sensors

```proto
message Traffic {
    /// UUID of device
    string device_id = 1;
    /// entrance id / from
    int32 ent_in = 2;
    /// entrance id / to
    int32 ent_out = 3;
    /// Enter timestamptz with microseconds with timezone ( 5 min precision )
    int64 time_in = 4;
    /// Leave timestamptz with microseconds with timezone ( 5 min precision )
    int64 time_out = 5;
}
```


