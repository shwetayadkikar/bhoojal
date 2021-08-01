# Bhoojal - Ground Water Monitoring and Regulation with Azure

## Contents
- [Problem Statement](#problem-statement)
- [Proposed Solution](#proposed-solution)
  - [Outlet Monitoring](#outlet-monitoring)
  - [Data Pipelines](#data-pipelines)
  - [Dashboard](#dashboard)

## Problem Statement
- Ground Water is an invaluable and exhaustible resource
- Regulation of Ground Water consumption is becoming a priority for every regional governing body
- Ground Water resources are dependent on numerous factors such rain, geographical conditions, soil and terrain

### Proposed Solution
- Regulate and monitor ground water consumption against quantity and quality metrics
- Utilize Ground Penetration Radar data to observe Ground Water levels and establish quotas
- Augment weather data such as rainfall information with Ground Water data to establish tolerable consumption trends
- Send out email notifications to consumers when consumption or quality metrics need attention

![Architecture](https://user-images.githubusercontent.com/1644919/125955312-6f38bc15-0b27-49f9-9353-bfd4334c0c5b.png)
##### Architecture implemented on Azure

#### Outlet Monitoring
We utilize IOT Hub to fetch data from outlets registered on the Bhoojal platform. Outlets seed data in related to consumption and quality of the water from the registered outlet. Quality data is processed via a Stream Analytics job and alerts are raised through a Cosmos DB entry that further triggers an email notification to the outlet owner through an Azure Function. Dummy device [/device](/device) and Stream Analytics query [stream-analytics/ProcessAlerts](stream-analytics/ProcessAlerts) can be found here.

#### Data Pipelines
GPR and Historical weather data is aggregated on the platform to score outlets based on their quality and quantity health. Notebooks that are part of this pipeline are located at [/notebooks](/notebooks).
![image](https://user-images.githubusercontent.com/1644919/125954427-51a321cf-3527-4c63-83da-2150158e1d33.png)

##### Ground Penetration Radar (GPR)
Ground Penetration Radar (GPR) are radars that can identify ground characteristics and highlight the presence of materials such as minerals and water under the ground surface. The GPR data can prove to be highly useful to monitor health of under ground aquifiers.
![Ground Penetration Radar Sample](https://user-images.githubusercontent.com/1644919/125952299-a7f6db7d-776e-4d49-8b19-816c73d7f6f0.png)
##### Source: Aleksandr Pivtorak

#### Dashboard
GPR heatmaps and outlet data processed through Stream Analytics and Databricks notebooks is made available via a CDN hosted dashboard. The static files are hosted on a storage account that is connected to a CDN profile for optimized access for citizens and administrators. VueJS app can be found here [/web](/web) along with APIs hosted on Azure functions [/bhoojal-api](/bhoojal-api).
