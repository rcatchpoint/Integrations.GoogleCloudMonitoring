


  

# Catchpoint Google Stackdriver

  

####

## **Introduction**

  

Cloud Monitoring provides visibility into the performance, uptime, and overall health of applications. It collects metrics, events, and metadata from Google Cloud, Amazon Web Services, hosted uptime probes, application instrumentation, and a variety of common application components including Cassandra, Nginx, Apache Web Server, Elasticsearch, and many others. Operations ingests that data and generates insights via dashboards, charts, and alerts. Cloud Monitoring alerting helps you collaborate by integrating with Slack, PagerDuty, and more.

  

####

  
  

We will be looking at ingesting data from Catchpoint into Cloud Monitoring.

[https://cloud.google.com/monitoring](https://cloud.google.com/monitoring)

  
## **Prerequisites**

 - NodeJS


## **Installation &amp; Configuration**

  

 **Google cloud Setup**:

  
  

 **Enabling the Monitoring API**

  

1. Select the [project](https://console.cloud.google.com/apis/dashboard) you will use to access the API.

2.  Click the Enable APIs and Service button.

3. Search for &quot;Stackdriver&quot;.

4. In the search results, click through to &quot;Cloud Monitoring API&quot;.

5. If &quot;API enabled&quot; is displayed, then the API is already enabled. If not, click the Enable button.

  

**Install cloud SDK on your local machine**

  

1. Download the [Cloud SDK installer.](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe)

2. Launch the installer and follow the prompts. The installer is signed by Google LLC. Cloud SDK requires Python. Supported versions are 3.5 to 3.7, and 2.7.9 or higher. The installer will install all necessary dependencies, including the needed Python version.

3. After installation has completed, accept the following options:


- Start Cloud SDK Shell


  

The installer starts a terminal window and runs the gcloud init command.

  

  

**Clone the Repository to your local machine**

  

Clone this repository to your local machine.
In Catchpoint go to Settings>API:
[https://portal.catchpoint.com/ui/Content/Administration/ApiDetail.aspx](https://portal.catchpoint.com/ui/Content/Administration/ApiDetail.aspx)
In the “REST API” section click “Add Consumer” and assign a contact. Once saved you will be able to retrieve the consumer key and secret.


Navigate to the directory where the files were cloned.
update GoogleProjectId, CatchpointSecret, CatchpointSecret, CatchpointTestId under .env file


Now execute index.js file from the terminal. This will pull up last 15 minutes raw data for a given test and writes data to stackdriver monitoring (using Google API).
 ```bash
  node index.js
```
  

## **Results**

  

To use Cloud Monitoring, you must have a Google Cloud project with billing enabled. The project must also be associated with a Workspace. Cloud Monitoring uses Workspaces to organize monitored Google Cloud projects.

In the Google Cloud Console, go to Monitoring -\&gt; Overview this will create a workspace for you automatically for the first time.

  
To view the metrics for a monitored resource using Metrics Explorer, do the following:

 1. From the Google Cloud Console, go to Monitoring. [https://console.cloud.google.com/monitoring](https://console.cloud.google.com/monitoring)
 2. In the Monitoring navigation pane, click Metrics Explorer.
 3. Enter the monitored resource name in the Find resource type and metric text box.
Resource type -> global. 
All the Catchpoint specific metrics will have id’s in the following format. custom.googleapis.com/global/catchpoint_Connect
custom.googleapis.com/global/catchpoint_Dns
custom.googleapis.com/global/catchpoint_Load
 4. Metrics explorer also allows to filter data points using node name or test id.
 5. Add all the required metrics and this save the chart to a dashboard.
[https://cloud.google.com/monitoring/charts/metrics-explorer
](https://cloud.google.com/monitoring/charts/metrics-explorer
)
 6. Navigate to Monitoring->Dashboards to check out the metrics.


To check logs with the gcloud tool, use the logs read command:
This will which help in troubleshooting.
 ```bash
gcloud functions logs read
````

To view the logs for a specific function, provide the function name as an argument:

 ```bash
gcloud functions logs read catchpointSubscribe
````