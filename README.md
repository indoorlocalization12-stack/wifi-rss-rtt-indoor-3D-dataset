# Anonymized Indoor WiFi RSS and RTT Measurements

This repository contains anonymized WiFi received signal strength (RSS) and WiFi round-trip-time (RTT) ranging observations collected on three floors of an indoor environment. It accompanies a research submission to SenSys 2027.

## Collection

RSS-only observations were recorded with a customized version of WiFiAnalyzer. RTT observations were recorded with a separate custom native Android application, which also logged RSS and ranging status. These applications have different schemas and logging behavior; their timestamps should **not** be assumed to be synchronized.

`distance_mm` is an app-reported ranging-derived distance estimate in millimeters, **not** raw round-trip time. A value of `-1` is present in unsuccessful or unavailable ranging observations; use the `type` field when interpreting each record.

## Contents


| Folder or file | Contents |
| --- | --- |
| `RSS_floor_3_github/` | Floor 3 training RSS (87 files) |
| `RSS_Floor_4_github/` | Floor 4 training RSS (100 files) |
| `RSS_Floor_5_github/` | Floor 5 training RSS (105 files) |
| `RTT_floor_3_github/` | Floor 3 training RTT (87 files) |
| `RTT_floor_4_github/` | Floor 4 training RTT (105 files) |
| `RTT_floor_5_github/` | Floor 5 training RTT (105 files) |
| `test_points_floor_3_RSS_RTT/` | Floor 3 test observations (25 files) |
| `test_points_floor_4_RSS_RTT/` | Floor 4 test observations (37 files) |
| `test_points_floor_5_RSS_RTT/` | Floor 5 test observations (42 files) |
| `floor3_floor_mapping.csv` | Floor 3 training RP identifiers and floor labels (87 records) |
| `floor4_floor_mapping.csv` | Floor 4 training RP identifiers and floor labels (105 records) |
| `floor5_floor_mapping.csv` | Floor 5 training RP identifiers and floor labels (105 records) |
| `floor3_test_floor_mapping.csv` | Floor 3 test identifiers and floor labels (21 records) |
| `floor4_test_floor_mapping.csv` | Floor 4 test identifiers and floor labels (21 records) |
| `floor5_test_floor_mapping.csv` | Floor 5 test identifiers and floor labels (21 records) |

## Floor-mapping convention

The six floor-mapping files associate a location identifier with a floor number (3, 4, or 5). Training files use the columns `RP_ID,floor`; test files use `rp_id,floor`. Identifier capitalization and naming conventions vary, so joins should be checked carefully.


## Anonymization

WiFi BSSIDs have been consistently pseudonymized as `AP_0001`, `AP_0002`, etc., across the previously documented release. SSIDs and AP coordinate columns were removed. Timestamps and application-specific fields are retained. Pseudonymization does not guarantee complete anonymity: release should follow a final review of filenames, metadata, timestamp privacy, and publication permissions.


See [data_dictionary.md](data_dictionary.md) for column definitions.

## License and citation

A license and formal citation will be added after confirming release permissions and the submission's anonymity requirements. Do not infer a license from the presence of these files.
