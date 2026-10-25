# Packet Gate — Firewall and Monitoring Lab

A browser-based cybersecurity learning project for exploring firewall policy rules, simulated traffic, deterministic attack scenarios, and read-only network-monitoring log imports.

> **Safety and scope:** Packet Gate is an educational simulator. It does not capture live packets, enforce operating-system firewall rules, execute generated `iptables` commands, or connect directly to a running Suricata/Zeek sensor. Imported monitoring logs are read locally by the browser.

## Features

- Ordered firewall rules using **first-match-wins** evaluation.
- IPv4/CIDR source and destination matching, protocol, destination port, and simplified connection-state labels.
- Default allow/block policy and illustrative packet tests.
- Repeatable, deterministic attack scenarios: port scan, SSH brute force, database probe, ICMP burst, and HTTP traffic spike.
- Simulated monitoring dashboard and heuristic alerts.
- Read-only import of Suricata EVE JSON and Zeek `conn.log` data.
- JSON rule import/export, CSV alert export, and reviewed `iptables` text generation.
- Responsive single-page app; no build step is required.

## Run the application

1. Download or clone this repository.
2. Open `index.html` in a modern browser (Chrome, Firefox, Edge, or Safari).
3. Configure rules, run packet tests, or start a deterministic attack scenario.
4. To inspect monitoring data, use the read-only log-import section and select a local Suricata EVE JSON or Zeek connection log file.

No server is required for the core demo. Web fonts may be requested from Google Fonts when internet access is available; system fallbacks are included.

## Run automated tests

Requires Node.js 18 or later. From the repository root:

```bash
npm test
```

The tests use Node's built-in test runner and do not require third-party packages. They cover IPv4/CIDR validation, rule matching and order, destination/port/protocol/state handling, deterministic event fixtures, Suricata and Zeek parsing, sample fixtures, and malformed Suricata JSON.

## Monitoring-log examples

Sample files are in `tests/fixtures/`: `sample-suricata-eve.json` and `sample-zeek-conn.log`. Only import real sensor data you are authorized to access. This is file-based ingestion, not a live sensor integration. Imported records are observations and must not be interpreted as proof of firewall enforcement.

## Architecture

```text
Browser UI
  ├── Rule editor and ordered policy evaluator
  ├── Packet test cases
  ├── Deterministic synthetic event generators
  ├── Heuristic alerting and event display
  ├── Local file parser ── Suricata EVE JSON / Zeek conn.log
  └── JSON / CSV / iptables-text export

Node.js test runner ── tests selected functions from index.html
```

## Security limitations

- Connection state is a simplified event label, not kernel conntrack or full TCP session tracking.
- The simulator is IPv4-focused and does not model every real firewall feature (for example NAT, interface rules, IPv6, fragmentation, or application payload inspection).
- Heuristic alerting can produce false positives or miss activity.
- Exported firewall commands are text only. Review and test them in an isolated lab with a rollback plan; never apply unreviewed output to production systems.
- Do not use generated events as evidence of a real attack.

## Portfolio summary

**Packet Gate — Firewall and Monitoring Lab** demonstrates firewall policy design, first-match rule evaluation, least-privilege thinking, repeatable attack simulation, basic alert triage, and read-only monitoring-log parsing. It explicitly distinguishes a browser-based teaching tool from real firewall enforcement and IDS/IPS operations.

## License

MIT. See [LICENSE](LICENSE).
