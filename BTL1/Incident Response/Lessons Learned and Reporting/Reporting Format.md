The first thing we want to state is that **there is no standard format for incidents reports**. Unfortunately there’s not a magical template that will work for all security teams across every organization in the world. However, it’s common to see 4 main sections of a report, which we’ll cover in more depth below:

- **Executive Summary**
- **Incident** **Timeline**
- **Incident Investigation**
- **Appendix**

---

# Executive Summary

This is typically where the high-level overview of the incident will go, using non-technical terms to clearly state the business impact. Executives are very busy so it’s our job to ensure that this section is easily readable and contains information that is important to this specific audience.

The executive summary should ideally be one page and focus on areas such as business risks, financial costs, and damage that occurred and prevented. This is a great place to really highlight the work of the security team and how they have prevented more damage and costs from happening (by containing an incident, preventing data exfiltration, catching an insider threat, etc). Doing this will show the executives that the cost of running the security team is less than suffering successful incidents, showing the value in maintaining (and potentially even growing) the team.

---

# Incident Timeline

The timeline will provide the date, time, and short descriptions of all key events throughout the incident. This can either be in the order these actions were taken or discovered, or re-ordered to be in chronological order to make it easier to read exactly what has happened from start to finish. It is common to see security teams use either their local timezone (provided the incident has only affected one geographic location) or Universal Time Coordinated (UTC) if the incident affects users or systems across multiple timezones. Converting multiple timezones to a single one ensures that the timeline is kept neat and easy to read and refer to.

---

# Incident Investigation

This will be the main bulk of the report, providing step-by-step documentation of actions that were conducted and the associated findings of the incident responders. All stages of the incident response lifecycle should be considered and reported on, with the exception of preparation:

- **Detection and Analysis** – How was the incident discovered? Was it a SIEM alert? A threat hunt? A user or system admin that reported something unusual? How was this activity triaged to ensure it was an incident and not a false positive? Were any checks conducted on the affected system(s) or was network traffic collected and analyzed? Screenshots should be used to show exactly what actions were taken, and what the investigating responders saw when performing analysis.

- **Containment, Eradication, and Recovery** – How was the incident scoped? Remember, this is arguably the most important part of a response, we need to ensure we’ve found all affected systems to prevent reinfection at a later date. How did the security team remove the actor(s) from the networks? Were systems restored from known-safe backups? Was anti-virus used to scan all systems, along with manual checks via an EDR solution? Were systems completely decommissioned? And what was the root cause? Correctly identifying this would allow us, as defenders, to address the issue and ensure that a similar incident doesn’t occur again.

- **Post-Incident Activity** – What could have been done better? Maybe the security team needs more personnel, additional tools, or more visibility into networks and systems. This should all be explained here to help drive decision-making to help prevent or allow the team to better respond to future incidents. Anything major should be included in the executive summary to ensure that it is seen by the top-level business decision-makers.

---

# Report Appendix

The appendix is used as storage for the report, and will typically include images or figures (graphs, tables) that will be referenced in the main body of the report. An example of content that could be included in this section includes a long list of IP addresses that were scanned to look for malicious indicators. This list or table would be included here as this would take up a lot of space in the ‘incident investigation’ report.

---

# Report Templates

We can’t stress this enough – one template will not work for everyone. It will vary between organizations, depending on what information is most important to them. However, the sections we have mentioned above are the common ones that are likely to be present in most incident reports.