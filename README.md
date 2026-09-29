# SOC Lab 02: Threat Hunting with Splunk (BOTS)

A hands-on Blue Team lab using **Splunk** and the **Boss of the SOC (BOTS)** dataset to investigate a simulated security incident, the way a SOC analyst would.

![Focus](https://img.shields.io/badge/Focus-SOC_%7C_Threat_Hunting-blue?style=flat-square)
![Level](https://img.shields.io/badge/Level-Junior-green?style=flat-square)
![Tool](https://img.shields.io/badge/Tool-Splunk-000000?style=flat-square&logo=splunk&logoColor=white)

## About the Dataset

Boss of the SOC (BOTS) is a public blue team dataset and competition created by Splunk. It contains realistic security data from a simulated attack, which lets analysts practice investigation with SIEM searches.

- **Dataset version used:** `<BOTS v1 / v2 / v3>`
- **Source:** [Splunk Boss of the SOC](https://github.com/splunk/botsv1) *(adjust the link to the version you used)*

## Scenario

An organization suffered a security incident. Using only the collected logs in Splunk, the goal is to reconstruct what happened: how the attacker got in, what they did, and what evidence they left behind.

## Objectives

- Search and filter large volumes of log data with SPL
- Identify the attacker's activity and infrastructure
- Correlate events across different data sources
- Build an incident timeline
- Map findings to MITRE ATT&CK
- Recommend detection and prevention improvements

## Skills Demonstrated

- Splunk Search Processing Language (SPL)
- Threat hunting and log correlation
- Investigation across multiple data sources (web, network, endpoint)
- Indicator of Compromise (IOC) extraction
- Timeline reconstruction
- MITRE ATT&CK mapping
- Technical reporting

## Tools

- Splunk Enterprise
- BOTS dataset
- MITRE ATT&CK framework

## Data Sources Used

> Keep only the sourcetypes you actually searched.

| Sourcetype | Type of data | Used for |
|---|---|---|
| `<sourcetype>` | Web traffic | `<e.g., identifying scanning and attack attempts>` |
| `<sourcetype>` | IDS / network alerts | `<e.g., confirming malicious activity>` |
| `<sourcetype>` | Windows / endpoint logs | `<e.g., tracking process execution>` |
| `<sourcetype>` | DNS / proxy | `<e.g., finding malicious domains>` |

## Methodology

1. **Explore the data:** list available indexes and sourcetypes
2. **Identify the target:** find the affected asset or service
3. **Find the attacker:** look for anomalous source IPs and behavior
4. **Follow the activity:** pivot across sourcetypes to see each stage
5. **Extract IOCs:** IPs, domains, hashes, file names
6. **Build the timeline:** order events from first contact to impact
7. **Document and recommend:** report and detection ideas

### Example: listing available sourcetypes

```spl
index=* | stats count by sourcetype | sort - count
```

### Example: top source IPs hitting a web server

```spl
index=<index> sourcetype=<web_sourcetype> dest_ip=<target_ip>
| stats count by src_ip
| sort - count
| head 10
```

### Example: timeline of events from a suspicious IP

```spl
index=<index> src_ip=<attacker_ip>
| sort _time
| table _time sourcetype src_ip dest_ip uri_path status
```

## Key Findings

> Replace the `<...>` values with the results of your investigation.

| Item | Result |
|---|---|
| Target asset | `<hostname / website>` |
| Attacker IP(s) | `<IP>` |
| Attack type | `<e.g., scanning, brute force, exploitation>` |
| Initial access method | `<how they got in>` |
| Malicious domains / files | `<values>` |
| Impact | `<what happened>` |
| Severity | `<Low / Medium / High>` |

## Attack Timeline

| Time | Stage | Description |
|---|---|---|
| `<time>` | Reconnaissance | `<what happened>` |
| `<time>` | Initial access | `<what happened>` |
| `<time>` | Execution / persistence | `<what happened>` |
| `<time>` | Impact | `<what happened>` |

## Indicators of Compromise (IOCs)

| Type | Value |
|---|---|
| IP address | `<IP>` |
| Domain | `<domain>` |
| File name / hash | `<value>` |
| URL / URI pattern | `<value>` |

## MITRE ATT&CK Mapping

> Keep only the techniques that match what you found.

| Tactic | Technique | ID |
|---|---|---|
| Reconnaissance | Active Scanning | [T1595](https://attack.mitre.org/techniques/T1595/) |
| Initial Access | Exploit Public-Facing Application | [T1190](https://attack.mitre.org/techniques/T1190/) |
| Credential Access | Brute Force | [T1110](https://attack.mitre.org/techniques/T1110/) |
| Command and Control | Application Layer Protocol | [T1071](https://attack.mitre.org/techniques/T1071/) |
| Impact | Defacement | [T1491](https://attack.mitre.org/techniques/T1491/) |

## Detection and Prevention Recommendations

- Create Splunk alerts for repeated failed logins and for scanning behavior
- Monitor for unusual outbound connections and newly seen domains
- Block confirmed malicious IPs and domains
- Keep public-facing applications patched and behind a WAF
- Centralize logs and retain them long enough for investigations

## Project Structure

```text
soc-lab-02-splunk-bots/
├── README.md
├── docs/
│   ├── investigation.md
│   └── incident-report.md
├── queries/
│   └── spl-queries.md
└── evidence/
    └── (Splunk screenshots)
```

## Interview Questions This Lab Prepares For

- What is SPL, and how would you find the most active IPs in a dataset?
- How do you pivot from one indicator to related activity?
- What is the difference between an index and a sourcetype?
- How would you turn a hunting query into a scheduled alert?

## Author

**Nicolas Borges Ocampos**
Cybersecurity student | Aspiring SOC / Blue Team analyst
[LinkedIn](https://www.linkedin.com/in/nicolas-borges-512411402/)
