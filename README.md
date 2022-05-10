## Approvals
|Approved|Role|Assignee|Approved|Role|Assignee|
|--------|----|--------|--------|----|:------:|
|.       |    |        |        |    |        |


## Version
			

|Revision|Date      |Author             |Changes       |
|--------|----------|-------------------|:------------:|
|1.0     |04/26/2022|Jose Gonzalez      | Created      | 


## Target Audience

For HLD:  Business users , general users, Testing group

For LLD:  Technical users, Testing group


### Form goals


This form is used to:


* Show the Train Schedules attached to a Train Id
* Create a Train Schedule attached to a Train Id
  * Create Stations row
* Update Train Schedule data attached to a Train Id
* Delete (Not available)




### Fields form dependencies vs APIs
![This is a alt text.](/image/APIFlow.png "This is a sample image.")



### APIs
Show the Train Schedule attached to a Train Id
 


|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|REQUEST|RESPONSE|
|------|------------|------|------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Get the Train Id associated to a ShortTrainId|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|2|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|GET|https://devint.pds.dev.use.torq.dev/train-schedule/train-id/{trainId}|Get the train schedule info associated to a Train Id|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule/train-id/3485|[GETTrainScheduleResponse.json](/json/GETTrainSchedule.json) |
|3|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/name/{stationNumber}|Get the location data associated to a station number|https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/8159448|[GETOriginLocation.json](/json/GETStationName_1.json)|

#### API CALL SEQUENCE
To get the Train Schedule data :

a) Get the TrainId associated to a ShortTrainId calling to API ID 1



b) Take the Traind  FIELD from the JSON response from API ID 1 and call API ID 2 to get the train schedule info



c) Take the StationNumber FIELD from the JSON response from API ID 2 and call API ID 3 to get the StaitonName ( Must be invoked 2 times for Origin and Destination)



Watch the Request/Response Message Examples on _**Step By Step - Show the Train Schedule attached to a Train Id**_
 

#### Create a Train Schedule attached to a Train Id

|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|REQUEST|RESPONSE|
|------|------------|------|------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Validate a Train Id associated to a ShortTrainId|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|4|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|POST|https://devint.pds.dev.use.torq.dev/train-management/train-id|Create a TrainId for a ShortTrainId|https://devint.pds.dev.use.torq.dev/train-management/train-id<br><br>{"scac":"CN","section":"5","trainSymbol":"A9876","originDate":"2022-04-14","trainSymbolWithSection":"A98765"} |3489|
|5|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/|Validate the station name based on station number|https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/8159448|[GETOriginLocation.json](/json/GETStationName_1.json)|
|6|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|POST|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule|Create Train Schedule attached to a Train Id| [POSTCreateTrainSchedule.json](/json/POSTCreateTrainSchedule.json) |```HTTP CODE 201```   |
 

#### API CALL SEQUENCE
To create a Train Schedule:

a) Get the TrainId associated to a ShortTrainId calling API ID 1 to validate IF EXISTS



b)  IF NOT EXISTS, call API ID 4 to create a TrainId



c) To add Station Train Schedule, call API ID 5 to validSCate the Station Number. Add 2 to n rows based one the business scenario



d)  Call the API ID 6 to create a schedule



Watch the Request/Response Message Examples on _**Step By Step - Create a Train Schedule attached to a Train Id**_


#### Update a Train Schedule attached to a Train Id

|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|REQUEST|RESPONSE|
|------|------------|------|------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Validate a Train Id associated to a ShortTrainId|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|5|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/|Validate the station name based on station number|https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/8159448|[GETOriginLocation.json](/json/GETStationName_1.json)|
|6|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|POST|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule|Create Train Schedule attached to a Train Id| [POSTCreateTrainSchedule.json](/json/POSTCreateTrainSchedule.json) |```HTTP CODE 201```   |


 

#### API CALL SEQUENCE

 

To Update a Train Schedule:

a) Get the TrainId associated to a ShortTrainId calling to API ID 1



b) Update values based on business scenario

c) To update a Station Train Schedule, call API ID 5 to validate the Station Number. Add 2 to n rows based one the business scenario



d)  Call the API ID 6 to update the schedule



Watch the Request/Response Message Examples on _**Step By Step - Create a Train Schedule attached to a Train Id**_

 
 
