Alerts trigger when search results meet specific conditions, allowing us to monitor and detect particular activity, such as a user failing to log in, or an external IP scanning the organization. Alerts are triggered and are then typically investigated by human analysts, who will perform the initial triage of the event, and escalate it to senior analysts if required. 

This is the main role of SOC analysts, to triage and investigate SIEM alerts, while senior analysts may also be responsible for developing new detection rules, as well as tuning existing rules to reduce noise and make them more effective.

## Alerting Process

The process of creating alerts can be split into four main steps:

1. **Search Query**
2. **Search Timing**
3. **Alert Triggers**
4. **Alert Actions**

We will cover each of these steps in more detail below.

### 1 – Search Query

The first task is to decide what activity we want to generate an alert. Is it an external IP trying to SSH into a corporate server? Is it a user account that is having a high number of login failures? Is it local administrator account usage? Rules in Splunk essentially search queries, so we need to work out what activity we want to detect, and how to write a search query that will identify it.
### 2 – Search Timing

Now that we have an alert with a search query, we need to set how often Splunk is going to run the search query to look for any activity that makes the alert conditions. Primarily we’ll use one of the two options:

- Continuously run this search query to look for related activity in real-time (the majority of SIEM rules)
- Run this search query on a set schedule (typically used to identify changes from baselines and behavioral profiles)
## 3 – Alert Trigger

If we have a rule that is looking for account logon failures, having it alert every time one logon failure event is generated in the environment, the SIEM is going to get smashed with tons of alerts. To combat this, we can create thresholds within the alert. For example, everyone gets their password wrong sometimes – but getting your password wrong 5, 6 times in a row isn’t normal behavior. We can create an alert that is looking for login failures from Windows domain controllers using Windows Event logs and set a threshold of 6 per user. Now when an account hits 6 login failures, an alert will generate. We can also combine thresholds with time ranges, so if an account fails to login 6 times within 5 minutes, generate an alert.
### 4 – Alert Action

This is where we determine what actually happens when an alert triggers. Some of the default actions include:

- Sending an email notification (typically used for high-profile events that need an immediate response from senior analysts)
- Adding an alert to the list of recently triggered alerts (this is how analysts can identify alerts and work to investigate them)
- Log and index searchable alert events (this actually allows analysts to quickly view all the information related to the alert that trigged)

Splunk also has the ability to allow administrators to write their own custom actions using webhooks, so messages can be created in their own applications, such as a mobile app that informs analysts when a new alert has been triggered and needs to be investigated.

## Creating Your Own Rules

First, we need a search query. Once we’ve written it, we can click on **‘Save As’** and then **‘Alert’**.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f9bb0872a6d528e774b778ef35402490765936ddcec7b6b5ac3d1e6e5de1002f58e8cf03d356f2af1b50e69f951b.png)

Then the following windows will be displayed:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/14908579c7c8c1168b4fe335f1c68fafe291a60bb3c601bd5e30d2aa9ae42d6bc4dff619ff4dd571763d13e395e5.png)

Give the alert a title and description.

**Permissions**

- **Private –** Only you can access, edit, and view triggered alerts.
- **Shared in App –** All users of the app can view triggered alerts, by default, everyone has read access and power user has write access to the alert.

**Alert type:**

Here we tell Splunk how to search for these events that match our alert.  
 
- Scheduled alerts, will search at a defined interval and evaluate trigger conditions when the search completes.
- Real-time alerts, run constantly in the background and evaluate trigger conditions within a window of time based on the conditions you define.

Lastly, **trigger actions:**

Here we tell Splunk actions to take when an alert is generated, as mentioned it can do the following; trigger alerts, log the event, output results to lookup file, and run a script or output results to an endpoint so it can get the attention of a SOC analyst.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e76ad60bef8ab534265dc32a9a85eb57806717fa85e5fc8b34c2aceb9d7712041e5ac9a15c2dd4d57244202c3169.png)

---