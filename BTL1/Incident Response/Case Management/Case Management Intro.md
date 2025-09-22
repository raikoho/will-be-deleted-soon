Typically, Security Operations Centres will utilize a case management solution to record their investigations when responding to security alerts or incidents. This tool is key for both compliance and operations, allowing analysts to correlate details between cases, ensure their work is documented, and allow for collaboration between analysts working on the same investigation.

A range of solutions can be used for this purpose, and real-world security teams use tools such as ServiceNow, IBM Resilient, Jira Service Management, and TheHive. In these next few lessons, we'll focus on the open-source tool TheHive, specifically designed as an incident response case management solution.

To best explain how case management tools function, we'll take a quick look at IBM Resilient to show you the functionality that is available in this tool.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8ad735f2eff8e28b7e0327389655877ebc02f4d7ab1fec07355d5048d5b5b25c5b96fbb3ba0e2d2abc2dc64662c3.jpg)

This is a screenshot of IBM's Resilient that shows a phishing-related case that has been created. This view is the Tasks page, where analysts will click into a task to add notes about what they have done, and mark them as complete. We can see that these sections are loosely based on the PICERL incident response lifecycle, with discovery and identification being first, then enrichment and validation, followed by containment and remediation.

On the right-hand section of the screenshot, we can see the ‘People’ heading, where the current owner of this case is the ‘Tier 1 Analysts’ group of users.

Below that we have Related Incidents. Resilient offers powerful functionality where analysts can add values to an ‘Indicators’ page, such as IP addresses, email addresses, URLs, file names, hashes, and more. These are correlated between cases and provides the related incidents section. The cases that are displayed here have some similarity with this current case - a great way to identify emerging threats or trends.

Next we have the Attachments section where analysts can upload files that are attached to this case. This can be used to attach log files, email files, PCAPs, memory dumps, or anything else that is deemed relevant to the investigation.

And finally, we have the Newsfeed section that provides a timeline of changes that have been made to the case, such as new notes being added, tasks being marked as complete, files being attached, new members being assigned, and more.

Hopefully this gives you a quick insight into what these types of platforms are used for, and how they assist security teams with formally documenting their investigations to provide accountability and meet compliance requirements.