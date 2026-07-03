# Security Policy

Ailur Labs takes the security of our software, infrastructure, and the data of our enterprise clients seriously. Because our MCP servers and Wasm-native engines often operate at the core of enterprise data pipelines, we adhere to strict security practices and responsible disclosure protocols.

## 🛡️ Reporting a Vulnerability

**DO NOT open a public GitHub Issue for security vulnerabilities.** Public disclosure of unpatched vulnerabilities can put our users and enterprise clients at risk.

### How to Report
Please report security vulnerabilities using one of the following secure channels:

1. **GitHub Private Vulnerability Reporting**: Use the [GitHub Security Advisories](https://github.com/ailurlabs/.github/security/advisories) feature to report a vulnerability privately.
2. **Email**: Send a detailed report to **[team@ailur.ai](mailto:team@ailur.ai)**. (Please encrypt sensitive payloads using our PGP key if requested).

### What to Include
To help us triage and resolve the issue quickly, please include:
*   **Description**: A clear explanation of the vulnerability.
*   **Reproduction Steps**: Detailed steps or a minimal proof-of-concept (PoC) code.
*   **Affected Component**: The specific repository, package, or version (e.g., `wawk-core`, `wawk-mcpd`).
*   **Impact**: The potential impact on confidentiality, integrity, or availability.

### Our Commitment (SLA)
*   **Acknowledgment**: We will acknowledge receipt of your report within **48 hours**.
*   **Triage & Assessment**: We will provide an initial assessment and severity rating within **5 business days**.
*   **Resolution**: For critical vulnerabilities, we aim to release a patch or mitigation strategy within **30 days**.
*   **Credit**: With your permission, we will publicly acknowledge your contribution in our security advisories and release notes.

---

## 🔒 Security Architecture & Controls

Our core infrastructure is built on a **Wasm-native, zero-OS-dependency architecture**. This design inherently mitigates entire classes of vulnerabilities (e.g., RCE, privilege escalation). 

For our enterprise-grade components (such as the `wawk` engine family), we enforce the following strict security controls:

| Control Category | Implementation Details |
| :--- | :--- |
| **Sandboxing & Isolation** | **No OS Access**: `system()` calls are strictly blocked. `ENVIRON` is empty. No direct file I/O or network access is permitted from within the execution sandbox. |
| **Denial of Service (DoS) Prevention** | **Fuel Limits**: Execution is capped at 10 million fuel units per plugin call, mathematically preventing infinite loops and CPU exhaustion. |
| **Memory Safety** | **Memory Caps**: Linear memory is strictly capped at 10 MB per plugin instance, preventing Out-Of-Memory (OOM) crashes and heap exhaustion. |
| **Input Validation** | **Path Traversal Protection**: All file paths are canonicalized and strictly validated against a designated base directory. |
| **Payload Limits** | **Request Size**: HTTP body limits are enforced (e.g., 1 MB max) to prevent payload-based DoS attacks. |

---

##  Compliance Mapping

Our security controls and development lifecycle are designed to align with major enterprise compliance frameworks. While formal certification for specific frameworks depends on the deployment environment, our architecture natively supports:

*   **SOC 2**: DoS prevention, strict data isolation, and audit logging capabilities.
*   **ISO 27001**: Secure development lifecycle, code analysis (Clippy, cargo audit), and dependency management.
*   **HIPAA**: Strict access control and data minimization via Wasm sandboxing.
*   **GDPR**: Data minimization and the ability to deploy entirely on-premise or in isolated VPCs.
*   **FedRAMP**: Supply chain security via automated SBOM (Software Bill of Materials) generation and dependency auditing (`cargo deny`).

---

##  Security Updates & Advisories

To stay informed about security updates, please:
1.  **Watch this Repository**: Enable "Security" notifications on GitHub.
2.  **Check GitHub Security Advisories**: We publish detailed CVEs and mitigation steps via [GitHub Security Advisories](https://github.com/ailurlabs/.github/security/advisories).
3.  **Update Dependencies**: We recommend using automated dependency update tools (e.g., Dependabot, Renovate) to ensure you are always running the latest patched versions.

## 📦 Supported Versions

We provide security updates for the **latest major release** of our software. If you are using an older version, we strongly recommend upgrading to the latest stable release to ensure you receive critical security patches.

---

*Thank you for helping us keep Ailur Labs and our enterprise clients secure.*
