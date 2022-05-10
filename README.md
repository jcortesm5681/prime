
## Approvals
|Approved|Role|Assignee|Approved|Role|Assignee|
|--------|----|--------|--------|----|:------:|
|.       |    |        |        |    |        |


## Version
			

|Revision|Date      |Author             |Changes       |
|--------|----------|-------------------|:------------:|
|1.0     |04/26/2022|Jose Gonzalez      | Created      | 


## Target Audience

For HLD:  Business users , general users, Testing group

For LLD:  Technical users, Testing group


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
 


|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|
|------|------------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Get the Train Id associated to a ShortTrainId|
|2|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|GET|https://devint.pds.dev.use.torq.dev/train-schedule/train-id/{trainId}|Get the train schedule info associated to a Train Id|
|3|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/name/{stationNumber}|Get the location data associated to a station number|

#### API CALL SEQUENCE
To get the Train Schedule data :

a) Get the TrainId associated to a ShortTrainId calling to API ID 1



b) Take the Traind  FIELD from the JSON response from API ID 1 and call API ID 2 to get the train schedule info



c) Take the StationNumber FIELD from the JSON response from API ID 2 and call API ID 3 to get the StaitonName ( Must be invoked 2 times for Origin and Destination)



Watch the Request/Response Message Examples on _**Step By Step - Show the Train Schedule attached to a Train Id**_
 

#### Create a Train Schedule attached to a Train Id

|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|
|------|------------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Validate a Train Id associated to a ShortTrainId|
|4|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|POST|https://devint.pds.dev.use.torq.dev/train-management/train-id|Create a TrainId for a ShortTrainId|
|5|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/|Validate the station name based on station number|
|6|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|POST|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule|Create Train Schedule attached to a Train Id|

 

#### API CALL SEQUENCE
To create a Train Schedule:

a) Get the TrainId associated to a ShortTrainId calling API ID 1 to validate IF EXISTS



b)  IF NOT EXISTS, call API ID 4 to create a TrainId



c) To add Station Train Schedule, call API ID 5 to validSCate the Station Number. Add 2 to n rows based one the business scenario



d)  Call the API ID 6 to create a schedule



Watch the Request/Response Message Examples on _**Step By Step - Create a Train Schedule attached to a Train Id**_


#### Update a Train Schedule attached to a Train Id

|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|
|------|------------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `TrainManagement`|GET|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/{shortTrainID}|Validate a Train Id associated to a ShortTrainId|
|5|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `Topology`|GET|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/|Validate the station name based on station number|
|6|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `TrainSchedule`|POST|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule|Create Train Schedule attached to a Train Id|

 

#### API CALL SEQUENCE

 

To Update a Train Schedule:

a) Get the TrainId associated to a ShortTrainId calling to API ID 1



b) Update values based on business scenario

c) To update a Station Train Schedule, call API ID 5 to validate the Station Number. Add 2 to n rows based one the business scenario



d)  Call the API ID 6 to update the schedule



Watch the Request/Response Message Examples on _**Step By Step - Create a Train Schedule attached to a Train Id**_

 

#### API Calls Examples - Show the Train Schedule attached to a Train Id

STEP|API CALL|REQUEST|RESPONSE|
|----|--------|------|---------|
|1. Get the Train Id associated to a ShortTrainId|1|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|2. Get the train schedule info associated to a Train Id|2|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule/train-id/3485|```json{  "trainId": 3489,  "scac": "CN",  "section": "5",  "trainSymbol": "A9876",  "originDate": [    2022,    4,    11  ],  "trainCategory": "1",  "trainGroup": "FRT",  "reportType": null,  "activities": [    {     "stationSequenceNum": 1,      "station": {        "id": 8159448,        "name": "Talley GA"      },      "sta": "2022-04-11T22:53:56-05:00[US/Central]",      "std": "2022-04-11T22:53:56-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S1",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    },    {      "stationSequenceNum": 2,      "station": {        "id": 71598,        "name": "Reeves GA"      },      "sta": "2022-04-12T22:57:28-05:00[US/Central]",      "std": "2022-04-12T22:57:28-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S2",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    }  ]}``` |
|3. Get the location data associated to a station number (ORIGIN)|3|https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/8159448|```json{  "topoOperationalTEType": "STATION",  "id": 8159448,  "physicalControlPointId": 8159450,  "containsTrack": true,  "stationNumber": "58H",  "stationName": "Talley GA",  "ambigousStationName": "Talley",  "boundaryId": 1374763500806619600,  "reportingTimeZone": "US/Eastern",  "namedBoundaryName": [    "Atlanta North"  ],  "stationLocation": [    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159690      ],      "id": 8159690,      "offset": 1.265,      "lowOffset": 1.265,      "highOffset": 1.265,      "segmentLength": 44.275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159692      ],      "id": 8159692,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159688      ],      "id": 8159688,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "SIDING"    }  ],  "trackEntityType": "STATION",  "authoritySiding": false,  "wye": false,  "timeZoneBoundary": false,  "authorityEnable": true,  "displayEnable": false,  "cutOver": true,  "trackLimits": [    1374763500806619600  ],  "ABAuthorityStation": false,  "CTCAuthorityStation": true,  "COTAuthorityStation": false,  "TWCAuthorityStation": false}```|
|4  Get the location data associated to a station number (DESTINATION)|3|https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/71598|```json{  "topoOperationalTEType": "STATION",  "id": 8159448,  "physicalControlPointId": 8159450,  "containsTrack": true,  "stationNumber": "58H",  "stationName": "Talley GA",  "ambigousStationName": "Talley",  "boundaryId": 1374763500806619600,  "reportingTimeZone": "US/Eastern",  "namedBoundaryName": [    "Atlanta North"  ],  "stationLocation": [    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159690      ],      "id": 8159690,      "offset": 1.265,      "lowOffset": 1.265,      "highOffset": 1.265,      "segmentLength": 44.275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159692      ],      "id": 8159692,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159688      ],      "id": 8159688,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "SIDING"    }  ],  "trackEntityType": "STATION",  "authoritySiding": false,  "wye": false,  "timeZoneBoundary": false,  "authorityEnable": true,  "displayEnable": false,  "cutOver": true,  "trackLimits": [    1374763500806619600  ],  "ABAuthorityStation": false,  "CTCAuthorityStation": true,  "COTAuthorityStation": false,  "TWCAuthorityStation": false}```|



 

#### API Calls Examples - Create a Train Schedule attached to a Train Id

|STEP|API CALL|REQUEST|RESPONSE|
|----|--------|------|---------|
|1. Get the Train Id associated to a ShortTrainId|1|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%2011|```json{"status": 404,"errorCode": "ERR_0033","errorMessage": "Invalid short train id"}```|
|2. Create a TrainId for a ShortTrainId|4|https://devint.pds.dev.use.torq.dev/train-management/train-id<br><br>```json{"scac":"CN","section":"5","trainSymbol":"A9876","originDate":"2022-04-14","trainSymbolWithSection":"A98765"}``` |```3489```|
|3. Validate the station name based on station number|5|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/58H|```json{  "topoOperationalTEType": "STATION",  "id": 8159448,  "physicalControlPointId": 8159450,  "containsTrack": true,  "stationNumber": "58H",  "stationName": "Talley GA",  "ambigousStationName": "Talley",  "boundaryId": 1374763500806619600,  "reportingTimeZone": "US/Eastern",  "namedBoundaryName": [    "Atlanta North"  ],  "stationLocation": [    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159690      ],      "id": 8159690,      "offset": 1.265,      "lowOffset": 1.265,      "highOffset": 1.265,      "segmentLength": 44.275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159692      ],      "id": 8159692,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159688      ],      "id": 8159688,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "SIDING"    }  ],  "trackEntityType": "STATION",  "authoritySiding": false,  "wye": false,  "timeZoneBoundary": false,  "authorityEnable": true,  "displayEnable": false,  "cutOver": true,  "trackLimits": [    1374763500806619600  ],  "ABAuthorityStation": false,  "CTCAuthorityStation": true,  "COTAuthorityStation": false,  "TWCAuthorityStation": false}``` |
|4. Create Train Schedule attached to a Train Id|6|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule <br><br>```json{  "trainId": 3489,  "scac": "CN",  "section": "5",  "trainSymbol": "A9876",  "originDate": [    2022,    4,    11  ],  "trainCategory": "1",  "trainGroup": "FRT",  "reportType": null,  "activities": [    {      "stationSequenceNum": 1,      "station": {        "id": 8159448,        "name": "Talley GA"      },      "sta": "2022-04-11T22:53:56-05:00[US/Central]",      "std": "2022-04-11T22:53:56-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S1",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    },    {      "stationSequenceNum": 2,      "station": {        "id": 71598,        "name": "Reeves GA"      },      "sta": "2022-04-12T22:57:28-05:00[US/Central]",      "std": "2022-04-12T22:57:28-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S2",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    }  ]}``` |```HTTP CODE 201``` |


 

#### API Calls Examples - Update a Train Schedule attached to a Train Id


STEP|API CALL|REQUEST|RESPONSE|
|----|--------|------|---------|
|1. Get the Train Id associated to a ShortTrainId|1|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|3. Validate the station name based on station number|5|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/58H|```json{  "topoOperationalTEType": "STATION",  "id": 8159448,  "physicalControlPointId": 8159450,  "containsTrack": true,  "stationNumber": "58H",  "stationName": "Talley GA",  "ambigousStationName": "Talley",  "boundaryId": 1374763500806619600,  "reportingTimeZone": "US/Eastern",  "namedBoundaryName": [    "Atlanta North"  ],  "stationLocation": [    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159690      ],      "id": 8159690,      "offset": 1.265,      "lowOffset": 1.265,      "highOffset": 1.265,      "segmentLength": 44.275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159692      ],      "id": 8159692,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "MAIN"    },    {      "topoOperationalTEType": "TopoLocationInfo",      "trackLimits": [        8159688      ],      "id": 8159688,      "offset": 358.6275,      "lowOffset": 358.6275,      "highOffset": 358.6275,      "segmentLength": 358.6275,      "direction": "UpBound",      "trackType": "SIDING"    }  ],  "trackEntityType": "STATION",  "authoritySiding": false,  "wye": false,  "timeZoneBoundary": false,  "authorityEnable": true,  "displayEnable": false,  "cutOver": true,  "trackLimits": [    1374763500806619600  ],  "ABAuthorityStation": false,  "CTCAuthorityStation": true,  "COTAuthorityStation": false,  "TWCAuthorityStation": false}```|
|4. Update Train Schedule attached to a Train Id|6|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule <br><br>```json{  "trainId": 3489,  "scac": "CN",  "section": "5",  "trainSymbol": "A9876",  "originDate": [    2022,    4,    11  ],  "trainCategory": "1",  "trainGroup": "FRT",  "reportType": null,  "activities": [    {      "stationSequenceNum": 1,      "station": {        "id": 8159448,        "name": "Talley GA"      },      "sta": "2022-04-11T22:53:56-05:00[US/Central]",      "std": "2022-04-11T22:53:56-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S1",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    },    {      "stationSequenceNum": 2,      "station": {        "id": 71598,        "name": "Reeves GA"      },      "sta": "2022-04-12T22:57:28-05:00[US/Central]",      "std": "2022-04-12T22:57:28-05:00[US/Central]",      "activityTypes": [],      "crewLineSegment": "S2",      "ptcTrainArrival": null,      "ptcTrainDeparture": null    }  ]}``` |```HTTP CODE 201```    |
|5. Refresh the Train Schedule data||CALL Show the Train Schedule attached to a Train Id|

 

