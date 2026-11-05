# Data dictionary

The dataset contains three CSV schemas. Fields below describe their apparent meaning based on the observed headers and sample values; details of application implementation have not been independently verified.

## RSS-only measurements (customized WiFiAnalyzer)

| Column | Meaning |
| --- | --- |
| `Time Stamp` | Timestamp as recorded by the RSS application; representation and timezone should be verified against the app |
| `apId` | Consistently pseudonymized WiFi access point identifier (`AP_####`) |
| `Strength` | Received signal strength, generally expressed in dBm; confirm app configuration |
| `Primary Frequency` | WiFi primary channel frequency, generally in MHz; confirm app configuration |

## RTT application measurements (custom native Android app)

| Column | Meaning |
| --- | --- |
| `timestamp` | App-recorded timestamp; samples resemble Unix epoch milliseconds, but confirm implementation |
| `landmark` | App-recorded reference/test-point label; compare with filename where applicable |
| `apId` | Consistently pseudonymized WiFi access point identifier (`AP_####`) |
| `distance_mm` | Ranging-derived distance estimate in millimeters; `-1` observed for unavailable/failed ranging |
| `stddev_mm` | App-reported ranging distance standard deviation in millimeters; `-1` observed when unavailable |
| `rssi_dbm` | Received signal strength in dBm |
| `success_frames` | App-reported count of successful ranging frames |
| `attempt_frames` | App-reported count of attempted ranging frames |
| `type` | Observation/status category, including `RSS_ONLY`, `RSS_PRE_RTT`, `RTT+RSS`, and `RTT_FAILED` |

Do not treat every RTT-app row as a successful RTT measurement. Check `type`, distance validity, and frame counts before analysis.

## Training reference-point coordinates

| Column | Meaning |
| --- | --- |
| `RP_ID` | Reference-point identifier, such as `RP_301` |
| `x_floor` | Local horizontal coordinate in feet |
| `y_floor` | Local vertical coordinate in feet |

The coordinates refer to training reference points only. Test-point ground-truth coordinates are not included.

## Notes on matching

Training measurement filenames identify reference points; capitalization and separators differ between the RSS and RTT application outputs (for example, `RP_301` versus `rp301`). Test measurement filenames and RTT `landmark` values also use different conventions. Normalize carefully rather than assuming raw strings match.

## Known exclusions

The prepared release excludes one Floor 3 RTT training file with no corresponding reference-point coordinate and 18 zero-row RTT test files. Original files should be retained privately for provenance.
