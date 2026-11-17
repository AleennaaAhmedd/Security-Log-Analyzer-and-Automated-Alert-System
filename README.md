# Security Log Analyzer and Automated Alert System

A Python-based, rule-driven security log analyzer that reads authentication and system logs, detects suspicious patterns using transparent rules, and generates evidence-backed alerts for an analyst to review.

> **Project status: In development.** This is a semester project for the Cyber Security course (BS Cyber Security, University of Management and Technology, Lahore). The features listed below are the planned scope. This README will be updated as each part is implemented and tested.

---

## Project Overview

Operating systems, servers, and applications produce large volumes of logs. Reviewing them manually is slow and suspicious activity is easy to miss. This tool ingests synthetic (or authorized) log data, normalizes the records into a common structure, applies configurable detection rules, and produces alerts that include severity, timestamp, rule name, affected entity, and supporting evidence.

This is an educational prototype. It is not a replacement for a production SIEM, and an alert is an indicator that needs investigation, not proof of an attack.

## Planned Features

- Import a log file in a documented CSV format
- Validate records and handle malformed or incomplete lines without crashing
- Normalize fields: timestamp, source, event type, username, source IP, message
- Six rule-based detections with configurable thresholds and time windows
- Evidence-rich alerts (alert ID, rule, severity, affected entity, reason, supporting events)
- Persistent storage of events and alerts in SQLite, with JSON/CSV export
- Summary report: events processed, alerts generated, counts by rule and severity
- Command-line interface, with an optional Streamlit dashboard
- Labelled synthetic dataset and repeatable tests
- Evaluation: precision, recall, F1-score, false-positive rate, and processing time

## Detection Rules

| ID | Rule | Idea |
|----|------|------|
| R1 | Repeated failed logins | Many failed logins for one account or source within a time window |
| R2 | Successful login after failures | A successful login follows repeated failures for the same account or source |
| R3 | Privileged account change | Account creation, privilege change, or admin group membership |
| R4 | Unusual activity volume | Event count from one source exceeds a threshold in a time window |
| R5 | Repeated access denied | Multiple access-denied events in a short period |
| R6 | Off-hours login | Successful login outside normal hours |

All thresholds and time windows will be configurable through a configuration file.

## System Architecture

```
Log File -> Parser -> Normalizer -> Rule Engine -> Alert Generator -> SQLite / JSON / CSV -> Summary and Evaluation
```

## Technologies

- Python 3
- csv, json, re, datetime, sqlite3 (standard library)
- pytest (testing)
- Streamlit (optional dashboard)
- Git and GitHub (version control)

## Planned Repository Structure

```
config/        rule thresholds and settings
data/          synthetic dataset, labels, data dictionary
src/           parser, rules, engine, alerts, storage, evaluation, CLI
tests/         unit, boundary, malformed-input, and integration tests
docs/          architecture diagram, weekly log, screenshots
dashboard/     optional Streamlit dashboard
```

## Installation and Usage

Setup and usage instructions will be added when the first working version is ready.

## Ethics, Privacy and Limitations

- Only synthetic, public, or explicitly authorized logs are used. No real personal or confidential logs are included.
- No secrets or credentials are stored in the repository.
- The tool does not block accounts or take automated response actions.
- Results on a small synthetic dataset do not represent real-world detection accuracy.
- Rule-based detection can miss low-and-slow attacks and can produce false positives.

## Author

Aleena Ahmed
BS Cyber Security, University of Management and Technology (UMT), Lahore
GitHub: [AleennaaAhmedd](https://github.com/AleennaaAhmedd)

## Acknowledgements and References

Python documentation, SQLite documentation, MITRE ATT&CK, and NIST SP 800-61 are used as reference material. A full reference list will be added in the project report.
