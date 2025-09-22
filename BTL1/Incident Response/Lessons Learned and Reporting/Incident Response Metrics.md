Metrics are numerical values used for quantitative assessment, allowing us to assess, compare, and track performance. Regarding incident response, it can highlight areas where the team has responded efficiently or ineffectively. These metrics can also help to identify trends in incidents that the organization is facing so they can be addressed, using metrics to support a business case to receive more budget or personnel.

There are many different options for using metrics to summarise the response to an incident and compare it to previous and future incidents. In this lesson, we will cover several common metrics that can be used for reporting purposes, allowing security teams to highlight their strengths and weaknesses, and use them to support business decisions such as increased headcount or budget.

**Please note that different organizations will use different metrics, this is aimed to give you a general idea of what metrics can be recorded.**

---

# Impact Metrics

- **Service Level Agreement (SLA) –** SLAs are an agreement between an organization and its customer that determines expectations for things such as uptime, responsiveness, and responsibilities of both parties.  This is often calculated using percentages with two of the most common ones being 99% and 99.9%.

- **Service Level Objective (SLO)** – SLOs are an agreement that exists within the SLA that determines that specific metric being measured, such as the uptime of a critical virtual machine.  Measuring these objectives can hold both the organization and potentially the client liable in the case that the objective is not met.

- **Escalation Rate** – This metric will measure how often alerts in your SIEM are being assigned to the correct security team member.  This can help prevent a brand-new analyst from receiving an alert for a sophisticated ransomware attack and dismissing it or taking it on themselves, rather than escalating the alert, to a more senior level analyst who has handled this ransomware before and knows the signs of a breach.

---

# Time-Based Metrics

- **Mean Time to Detect (MTTD)** **–** Also known as the meantime to acknowledge (MTTA), this is the average amount of time it takes for the security team to notice that a security incident has occurred.  Measuring this metric is important because it can help increase the effectiveness of alerts sent to a SIEM or another logging platform.

- **Mean Time to Response (MTTR) –** Also known as the meantime to repair, resolve or recover, this is the time from when something is detected, and when the security team can take action to address it.  This is often one of the most important metrics to track because it can show how efficient the team was when responding to the incident and can help identify key areas where the response time could improve.

- **Incidents Over Time –** This metric looks at the average number of incidents over a period of time to determine whether there is an increase or decrease of incidents. This metric helps determine whether changes need to be made to allow for more security to prevent incidents or to determine if the lower incident count is correlating to another event.

- **Remediation Time –** How long did it take the incident responders and appropriate stakeholders to remediate the situation (recovering all affected systems and returning to production status)?

---

# Incident Type Metrics

- **Cumulative Number of Incidents Per Types –** by categorizing incidents based on their type and comparing the total number of each incident category, this can provide security teams with an overview of where improvements need to be made. For example, if an organization had a high number of incidents caused by attackers exploiting vulnerabilities in internet-facing systems, then the organization would see they need to perform the vulnerability management process to patch these systems and apply mitigating controls such as web application firewalls and proxies.

- **Alerts Created per Incident –** This metric will help analyze how many alerts were created for the specific incident.  For example, in an incident did the EDR send out an alert that a malicious file has been downloaded, but did your O365 environment not generate an alert as well?  This metric can help see where in the Cyber Kill Chain process, you can improve your defenses, and, in this example, help prevent the malware from being downloaded in the first place.

- **Cost per Incident (CPI)** – This metric analyzes the perceived cost of the incident at the affected company and could be analyzed in a few different ways.  One way would be to analyze the duration of the incident and multiply it by the cost of the security team and/or team members that worked on and resolved the case.  Another way is calculated by analyzing the impact that the incident had on the business, such as a loss of sales made, productivity lost, or destruction of equipment or computers.  This metric can be most useful when a business impact analysis (BIA) has already been conducted with the client to establish the base costs of their organization.