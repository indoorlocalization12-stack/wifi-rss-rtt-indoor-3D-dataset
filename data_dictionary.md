# Data dictionary

The dataset contains RSS measurements, RTT application measurements, training reference-point floor mappings, and test-point floor mappings. The tables describe the CSV fields and their meanings. RSS and RTT measurements use separate application schemas and logging conventions.

## RSS-only measurements (customized WiFiAnalyzer)

| Column | Meaning |
| --- | --- |
| `Time Stamp` | Timestamp recorded by the RSS application |
| `apId` | Consistently pseudonymized WiFi access point identifier (`AP_####`) |
| `Strength` | Received signal strength in dBm |
| `Primary Frequency` | WiFi primary channel frequency in MHz |

## RTT application measurements (custom native Android app)

| Column | Meaning |
| --- | --- |
| `timestamp` | Timestamp recorded by the RTT application |
| `landmark` | Reference-point or test-point label recorded by the RTT application |
| `apId` | Consistently pseudonymized WiFi access point identifier (`AP_####`) |
| `distance_mm` | Ranging-derived distance estimate in millimeters; `-1` observed for unavailable/failed ranging |
| `stddev_mm` | App-reported ranging distance standard deviation in millimeters; `-1` observed when unavailable |
| `rssi_dbm` | Received signal strength in dBm |
| `success_frames` | App-reported count of successful ranging frames |
| `attempt_frames` | App-reported count of attempted ranging frames |
| `type` | Observation/status category, including `RSS_ONLY`, `RSS_PRE_RTT`, `RTT+RSS`, and `RTT_FAILED` |

Do not treat every RTT-app row as a successful RTT measurement. Check `type`, distance validity, and frame counts before analysis.

## Training reference-point floor mappings

Files: `floor3_floor_mapping.csv`, `floor4_floor_mapping.csv`, `floor5_floor_mapping.csv`.

| Column | Meaning |
| --- | --- |
| `RP_ID` | Training reference-point identifier, e.g., `RP_301` |
| `floor` | Integer floor label (3, 4, or 5, corresponding to the file) |

| File | Data records |
| --- | ---: |
| `floor3_floor_mapping.csv` | 87 |
| `floor4_floor_mapping.csv` | 105 |
| `floor5_floor_mapping.csv` | 105 |


## Test-point floor mappings

Files: `floor3_test_floor_mapping.csv`, `floor4_test_floor_mapping.csv`, `floor5_test_floor_mapping.csv`.

| Column | Meaning |
| --- | --- |
| `rp_id` | Test-point identifier; note the lowercase column name |
| `floor` | Integer floor label (3, 4, or 5, corresponding to the file) |

| File | Data records |
| --- | ---: |
| `floor3_test_floor_mapping.csv` | 21 |
| `floor4_test_floor_mapping.csv` | 21 |
| `floor5_test_floor_mapping.csv` | 21 |


## Notes on matching

Training measurement filenames identify reference points; capitalization and separators differ between RSS and RTT application outputs (for example, `RP_301` versus `rp301`). Test measurement filenames and RTT `landmark` values may also use different conventions. Training mapping files use `RP_ID`, while test mapping files use `rp_id`. Normalize identifiers before joining records across files; raw strings are not necessarily interchangeable.

