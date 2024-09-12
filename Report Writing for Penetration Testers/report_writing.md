# Penetration Testing Deliverables
## Report Writing for Penetration Testers
**January 08, 2024**

### Adaptability in Penetration Testing
"No plan survives first contact with the enemy" – This highlights that specific activities planned during the engagement may not always occur as expected due to the unpredictability of the testing environment. Key points to ensure:
- Penetration tests (PT) can be repeated to confirm if an issue is real.
- Penetration tests can be conducted post-remediation to verify the fix.
- If a system failure occurs, the tester and the client can determine if the test was the cause.

---

## Rules of Engagement (RoE)
The rules of engagement (RoE) ensure that all parties respect the agreed-upon guidelines. 

### Note Portability
It's crucial to write in a concise and coherent manner. Portability is particularly important if a PT has to leave the engagement due to illness or other issues. A shared understanding of note-taking ensures consistency across the PT team.

---

## The General Structure of Penetration Testing Notes
### Key Principles:
- Instead of taking general notes assuming we’ll remember how to replicate actions, we must document exactly what was done.
- Every command typed or action taken should be noted so it can be reproduced.
- If the notes don't help in remembering actions later, they won't be useful.
- To write a convincing and substantiated technical report, sufficient details are required.

### Important Considerations:
- Notes should be structured and detailed to avoid ambiguity.
- Coherent and thorough documentation ensures others can repeat the tests and achieve the same results.

---

## Recommended Note Structure for Penetration Testing
While personal preferences are allowed, notes should remind us of what occurred and enable issue replication. For example, in a web app:
- **Application Name**
- **URL**
- **Request Type** (GET, POST, OPTIONS, etc.)
- **Issue Detail**: Overview of the triggered vulnerability.
- **Proof of Concept (PoC) Payload**: String or code block that triggers the issue.

---

## Choosing the Right Note-Taking Tool
### Requirements:
- **Screenshots**: Essential for illustrating issues.
- **Code Blocks**: Proper formatting for commands and scripts.
- **Portability**: Cross-platform compatibility.
- **Directory Structure**: Clear and coherent organization.

---

## Taking Screenshots
Screenshots are vital for both note-taking and technical reporting. A well-captured screenshot can communicate an issue more effectively than text.

---

## Purpose of a Technical Report
A penetration test's value is largely delivered through the report. It is the primary means by which the client takes action. Finding vulnerabilities holds little business impact if they aren’t presented clearly with recommendations. Key points for report preparation:
- Understand the purpose of the report.
- Present the collected information in a way the audience can easily understand.

---

## Tailoring the Report Content
Deliver content appropriate to the audience's skill level. Key strategy:
- Structure content with appropriate sections and subsections.
- Two main audiences:
  - **C-Level Executives** (CISO, CSO, CFO, etc.) or department heads.
  - **Technical Teams** (IT/security staff).

---

## Executive Summary
The executive summary helps senior management understand the scope and outcomes of the testing. It should:
- Provide a high-level overview of the engagement.
- Clearly outline the scope of the test and the value provided.
- Support decision-making for remediation.

---

## Testing Environment Considerations
The report should begin with any issues that affected the testing process, as transparency is essential. Even if issues are known to those involved, documenting them ensures clarity.

### Possible Outcomes:
- **Positive Outcome**: Engagement proceeded smoothly without limitations.
- **Neutral Outcome**: For example, no credentials were provided, reducing the attack surface but not impacting the test significantly.
- **Negative Outcome**: Insufficient time or scope expansion hindered a comprehensive review.

---

## Technical Summary
The technical summary lists the key findings in the report, along with recommendations aimed at technical readers. Topics might include:
- User and privilege management
- System architecture
- Authorization and authentication
- Patch management
- Access control
- Audit logs and monitoring
- Data encryption
- Security misconfigurations

---

## Technical Findings and Recommendations
Present technical findings in a tabulated format, including:
- **Issue Description**
- **Implication**
- **Recommendation**

---

## Appendices, Further Information, and References
Include any additional information or references in the appendices. This section may contain further reading, technical solutions, or practical implementations that aren't necessary for the main body of the report.
