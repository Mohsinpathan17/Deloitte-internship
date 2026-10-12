<div align="center">

# ◈ Deloitte Internship Coding Task
### Industrial Device Data Normalization • Python • JSON • Unit Testing

**Transform two device telemetry formats into one consistent, application-ready structure.**

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![JSON](https://img.shields.io/badge/Data-JSON-0D1B2A?style=for-the-badge)](https://www.json.org/)
[![Tests](https://img.shields.io/badge/Testing-unittest-15A86D?style=for-the-badge)](https://docs.python.org/3/library/unittest.html)
[![Portfolio](https://img.shields.io/badge/Portfolio-Mohsin%20Pathan-06B6D4?style=for-the-badge)](https://mohsinpathan.vercel.app)

</div>

---

## Overview

This repository contains a **Deloitte internship coding task** implemented in Python. Two source JSON files represent industrial device telemetry in different structures. The program detects the incoming format and converts the data into a **shared normalized schema**, making downstream processing more consistent.

The existing solution lives in [`main.py`](main.py), with expected output in [`data-result.json`](data-result.json).

> **Note:** This repository documents a coding exercise. It does not, by itself, establish employment with Deloitte or deployment in a production factory.

## How it works

```text
           Input device telemetry
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   Format 1                 Format 2
 Flat device fields     Nested device object
 Slash-separated        ISO timestamp
 location               Separate location fields
          │                     │
          ▼                     ▼
 convertFromFormat1()   convertFromFormat2()
          │                     │
          └──────────┬──────────┘
                     ▼
           Normalized JSON object
                     │
                     ▼
              unittest checks
```

### Format handling

| Concern | Format 1 | Format 2 | Normalized output |
|---|---|---|---|
| Device identity | `deviceID`, `deviceType` | `device.id`, `device.type` | `deviceID`, `deviceType` |
| Timestamp | Existing numeric timestamp | ISO date-time string | Millisecond timestamp |
| Location | Slash-delimited string | Individual fields | Nested country, city, area, factory, section |
| Device readings | `operationStatus`, `temp` | Existing `data` object | `data.status`, `data.temperature` |

### Example normalized result

```json
{
  "deviceID": "dh28dslkja",
  "deviceType": "LaserCutter",
  "timestamp": 1624445837783,
  "location": {
    "country": "japan",
    "city": "tokyo",
    "area": "keiyō-industrial-zone",
    "factory": "daikibo-factory-meiyo",
    "section": "section-1"
  },
  "data": {
    "status": "healthy",
    "temperature": 22
  }
}
```

## Running the solution

Use **Python 3**. Only Python standard-library modules (`json`, `datetime`, and `unittest`) are used in the current code.

```bash
git clone https://github.com/Mohsinpathan17/Deloitte-internship.git
cd Deloitte-internship
python main.py
```

The script expects these files in the repository root: `data-1.json`, `data-2.json`, and `data-result.json`. It tests both conversions against the expected result.

The repository has not been independently verified in this README update; run the command above to confirm all fixtures and tests are available and passing.

## Engineering concepts demonstrated

- **Data normalization:** Transform heterogeneous JSON payloads into a predictable structure.
- **Schema mapping:** Extract nested and flat fields without changing the intended output contract.
- **Timestamp conversion:** Parse an ISO-format time and represent it as Unix milliseconds.
- **Automated validation:** Use `unittest` to check both input formats against the same expected output.

## Limitations and improvements

The current implementation assumes expected keys are present and that the slash-separated location contains five segments. More robust input validation and clearer errors would be suitable improvements for a production implementation. Timestamp parsing also expects a particular ISO string format.

---

<div align="center">

**Developed by [Mohsin Pathan](https://github.com/Mohsinpathan17)**

[GitHub profile](https://github.com/Mohsinpathan17) · [Live portfolio](https://mohsinpathan.vercel.app) · [NEXYRAL](https://nexyral.online)

</div>
