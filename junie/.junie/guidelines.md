# Project Guidelines

## Repository Purpose

- This repository stores and documents AI rules for building node.js applications.
- The rules are **not** intended to be used directly in this repository.

## Rule Versioning Policy

### On every rule update:
1. Increment the `version` field in the rule's YAML header (e.g., `1.0.0` → `1.1.0`).
2. Update the `timestamp` field to the current date and time (format: `YYYY-MM-DD HH:MM`).

### On changes affecting multiple rules:
1. Find the highest version number currently in use across the affected rules.
2. Set **all** affected rules to that next highest version.
3. Update the `timestamp` field in all affected rules.

### YAML Header Format (required on every rule file):
```yaml
---
version: X.Y.Z
timestamp: YYYY-MM-DD HH:MM
---
```
