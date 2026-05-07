# AI-Augmented Pen Test Triage: Claude Code Skill

> A Claude Code skill that augments penetration testing and vulnerability assessment workflows in regulated environments. Built and maintained by a senior information security professional with 20 years of GRC and security management experience across financial services, healthcare, and real estate.

---

## What This Does

Security assessments generate noise. Regulated environments generate liability. This skill bridges both.

It augments the **triage and documentation phase** of penetration test and vulnerability assessment workflows by:

- **Classifying findings** by severity and regulatory exposure: HIPAA, PCI-DSS, NYDFS, GDPR, CPRA, SOX, NIST CSF
- **Evaluating false-positive risk** based on system context, business criticality, and compensating controls
- **Generating chain-of-custody-aware documentation** suitable for regulated-environment audit trails
- **Translating technical findings** into risk language for business stakeholders, compliance audiences, and executive reporting
- **Flagging remediation vs. risk-acceptance decisions** based on regulatory requirements and business constraints

---

## Why It Exists

Standard pen test reports are written for engineers. They get handed to compliance teams, business leaders, and auditors who need to make risk decisions, fast, in language they can act on.

After 11 years managing GRC programs across industries where a misclassified finding can mean a HIPAA violation or a PCI audit failure, I built this skill to do what I was doing manually: translate technical security findings into business risk language without losing the technical accuracy that makes the translation credible.

It also addresses a gap I kept hitting in regulated environments: **most AI-assisted security tools have no concept of chain-of-custody**. When a finding is used in an audit response, a board presentation, or a regulatory submission, the trail from raw scanner output to final risk position needs to be defensible. This skill documents that trail.

---

## Regulated Environment Considerations

This skill was designed with three regulated-environment constraints that most security tooling ignores:

### 1. False-Positive Risk
In regulated environments, a false positive isn't just wasted time. It can trigger unnecessary remediation spend, create misleading audit artifacts, or generate erroneous risk exceptions that become permanent record. The skill prompts explicit false-positive evaluation before any finding is documented as confirmed.

### 2. Chain-of-Custody Documentation
Any finding that may surface in an audit response, regulatory submission, or board-level risk report needs a clear record of: who assessed it, what context was applied, what compensating controls were considered, and what the final risk position is. The skill produces output structured for this trail.

### 3. Business-Constraint Remediation
Many findings in production regulated environments **cannot be remediated in isolation.** A vulnerability in a critical-care device, a legacy system under a multi-year vendor contract, or an integration that a business unit depends on for revenue falls into this category. The skill handles the risk-acceptance workflow, not just the remediation workflow.

---

## Skill Structure

```
pen-test-triage/
├── SKILL.md                          # Claude Code skill instructions (the core prompt)
├── README.md                         # This file
├── templates/
│   ├── finding-triage-template.md    # Structured triage output format
│   ├── chain-of-custody-log.md       # Audit-trail documentation template
│   └── risk-acceptance-memo.md       # Risk acceptance record for regulated environments
├── examples/
│   ├── sample-web-app-triage.md      # Example: web application vulnerability triage
│   ├── sample-network-triage.md      # Example: network infrastructure finding
│   └── sample-hipaa-context.md       # Example: HIPAA-regulated environment classification
└── docs/
    ├── regulatory-mapping.md         # Finding severity → regulatory exposure mapping
    └── usage-guide.md               # How to use the skill effectively
```

---

## How to Use

### Prerequisites
- [Claude Code](https://docs.claude.ai/en/docs/claude-code/getting-started) installed
- Basic familiarity with running skills in Claude Code

### Installation

```bash
# Clone the repository
git clone https://github.com/CavenderProjects/pen-test-triage.git

# Copy the skill into your Claude Code skills directory
cp -r pen-test-triage/SKILL.md ~/.claude/skills/pen-test-triage/

# Or on Windows (PowerShell):
Copy-Item -Recurse pen-test-triage\SKILL.md "$env:APPDATA\Claude\skills\pen-test-triage\"
```

### Invoking the Skill

In Claude Code, trigger the skill with:

```
/pen-test-triage
```

Then provide:
1. The raw finding text (from scanner output, manual test notes, or a prior report)
2. System context (what the system does, who uses it, what data it handles)
3. Regulatory environment (HIPAA, PCI, NYDFS, etc., or "general corporate")
4. Business constraint context (any known constraints on remediation)

### Example Input

```
Finding: Outdated TLS version (TLS 1.0) detected on payment processing endpoint.
System: Legacy order management system integrated with payment gateway. Cannot be
        updated until contract renewal in Q3 2027.
Regulatory environment: PCI-DSS 4.0, SOX-adjacent financial controls
Business constraint: Vendor dependency; unilateral update not possible
```

### Example Output Structure

The skill produces a structured triage record including:
- **Confirmed/False Positive determination** with reasoning
- **Severity classification** (Critical/High/Medium/Low) with regulatory exposure context
- **Remediation options** ranked by feasibility given stated constraints
- **Risk acceptance documentation** if remediation is not feasible
- **Audit-ready language** for compliance reporting

---

## Limitations and Honest Caveats

This is a **workflow augmentation tool**, not an autonomous security assessment engine.

- It does not perform scanning, probing, or discovery. It assists with the triage and documentation of findings already identified by the assessor
- Output requires review by a qualified security professional before use in any regulatory or audit context
- False-positive evaluation is only as good as the context provided (garbage in, garbage out)
- It does not replace legal review for risk acceptance decisions with significant regulatory exposure

---

## Part of a Broader AI Governance Practice Portfolio

This skill is the first published artifact in a broader AI governance project portfolio being built in 2026.

| Artifact | Status | Description |
|----------|--------|-------------|
| **Pen Test Triage Skill** (this repo) | Live | Claude Code skill for regulated-environment security assessment augmentation |
| **AI Risk Assessment Template** | In progress | Maps NIST AI RMF + ISO 42001 controls to GRC framework language enterprises already use |
| **AI Vendor Risk Questionnaire** | In progress | 25-question due diligence framework for evaluating third-party AI vendors; fills the gap left by pre-2023 contracts with no AI clause |

The larger project addresses a specific gap: most AI governance content is written for either AI engineers (too technical for GRC teams) or compliance audiences (too theoretical for practitioners). These tools are built for the people who have to operationalize AI governance inside real organizations with real regulatory exposure.

---

## Background

**Christopher Cavender, CISSP, CCSP | IAPP AIGP (in progress)**

20 years in information security and GRC. Former Business Information Security Officer at Anywhere Real Estate (Fortune 500); 11 years managing security programs across financial services, healthcare, and real estate. Currently Information Systems Security Manager at Tripoint Solutions. NJ/NYC.

This skill emerged from a practical problem encountered repeatedly across regulated environments: AI tools being adopted into security workflows with no framework for evaluating false-positive risk, chain-of-custody implications, or regulatory exposure. Rather than write another policy about it, I built the tool.

**Connect:** [LinkedIn](https://linkedin.com/in/christopher-cavender-cissp) · [AI Risk Assessment Template repo](https://github.com/CavenderProjects/ai-risk-assessment-template) *(coming)*

---

## Contributing

Contributions welcome, especially from practitioners working in regulated environments with specific HIPAA, NYDFS, PCI, or EU AI Act context to add. Open an issue or submit a PR.

---

## License

MIT License. Use freely. Attribution appreciated but not required.

If you use this in a regulated environment and find something that needs fixing, please open an issue; that feedback directly improves the tool.

---

*Built May 2026 · Part of an active AI governance practice portfolio*
