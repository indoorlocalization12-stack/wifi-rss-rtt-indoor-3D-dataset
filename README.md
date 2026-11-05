# Anonymized Indoor WiFi RSS and RTT Measurements

This repository contains anonymized WiFi received signal strength (RSS) and WiFi round-trip-time (RTT) ranging observations collected on three floors of an indoor environment. It accompanies a research submission to SenSys 2027.

## Collection

RSS-only observations were recorded with a customized version of WiFiAnalyzer. RTT observations were recorded with a separate custom native Android application, which also logged RSS and ranging status. These applications have different schemas and logging behavior; their timestamps should **not** be assumed to be synchronized.

`distance_mm` is an app-reported ranging-derived distance estimate in millimeters, **not** raw round-trip time. A value of `-1` is present in unsuccessful or unavailable ranging observations; use the `type` field when interpreting each record.

## Contents

The prepared release has 696 CSV files: 292 training RSS files, 297 training RTT files, 104 nonempty test measurement files (61 RSS and 43 RTT), and three training coordinate files.

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
| `floor3_coordinates.csv` | Floor 3 training reference points (87) |
| `floor4_coordinates.csv` | Floor 4 training reference points (105) |
| `floor5_coordinates.csv` | Floor 5 training reference points (105) |

## Coordinate convention

Training reference-point coordinates (`x_floor`, `y_floor`) are local, two-dimensional coordinates in feet, obtained from a scaled floor-plan representation using its bottom-left corner as the origin. They are **not** geographic coordinates. Coordinates for independent test points are not included.

## Anonymization

WiFi BSSIDs have been consistently pseudonymized as `AP_0001`, `AP_0002`, etc., across the released files. SSIDs and AP coordinate columns were removed. Timestamps and application-specific fields are retained. Pseudonymization does not guarantee complete anonymity: release should follow a final review of filenames, metadata, timestamp privacy, and publication permissions.

## Limitations

- The public release does not include test-point ground-truth coordinates, so the reported localization errors cannot be independently recalculated using this release alone.
- RSS and RTT collection methods differ, and rows should not be assumed to correspond one-to-one.
- Some RTT test locations have no recorded observations; empty CSV files were excluded from this prepared release.
- One unmatched Floor 3 training RTT file (`rp312`) was excluded because no matching training coordinate was available.
- Failed RTT attempts and RSS-only records may occur in RTT application logs.

See [data_dictionary.md](data_dictionary.md) for column definitions.

## License and citation

A license and formal citation will be added after confirming release permissions and the submission's anonymity requirements. Do not infer a license from the presence of these files.
