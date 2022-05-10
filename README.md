# prime
# 

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

 

<table>
    <thead>
        <tr>
            <th>STEP</th>
            <th>API CALL</th>
            <th>REQUEST</th>
            <th>RESPONSE</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1. Get the Train Id associated to a ShortTrainId</td>
            <td>1</td>
            <td>https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765 12</td>
            <td>[

    {

        "trainId": 3485,

        "shortTrainId": "A98765 12",

        "customerTrainKey": {

            "scac": "CN",

            "section": "5",

            "trainSymbol": "A9876",

            "originDate": "2022-04-12"

        }

    }

]</td>
        </tr>
        <tr>
            <td>2. Get the train schedule info associated to a Train Id</td>
            <td>2</td>
            <td>https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule/train-id/3485</td>
            <td>[GETTrainScheduleResponse.json](/json/GETTrainSchedule.json) </td>
        </tr>
        <tr>
            <td>3. Get the location data associated to a station number (ORIGIN)</td>
            <td>3</td>
            <td>https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/8159448</td>
            <td>[GETOriginLocation.json](/json/GETStationName_1.json) </td>
        </tr>
         <tr>
            <td>4  Get the location data associated to a station number (DESTINATION)</td>
            <td>3</td>
            <td>https://devint.pds.dev.use.torq.dev/topology-lookup/station/id/71598</td>
            <td>[GETDestinationLocation.json](/json/GETStationName_2.json) </td>
        </tr>
    </tbody>
</table>

#### API Calls Examples - Create a Train Schedule attached to a Train Id

|STEP|API CALL|REQUEST|RESPONSE|
|----|--------|------|---------|
|1. Get the Train Id associated to a ShortTrainId|1|https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765%2011|{"status": 404,"errorCode": "ERR_0033","errorMessage": "Invalid short train id"}|
|2. Create a TrainId for a ShortTrainId|4|https://devint.pds.dev.use.torq.dev/train-management/train-id<br><br>{"scac":"CN","section":"5","trainSymbol":"A9876","originDate":"2022-04-14","trainSymbolWithSection":"A98765"} |3489|
|3. Validate the station name based on station number|5|https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/58H|[GETStationName_Response.json](/json/GETStationName.json) |
|4. Create Train Schedule attached to a Train Id|6|https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule <br><br>[POSTCreateTrainSchedule.json](/json/POSTCreateTrainSchedule.json) |HTTP CODE 201 |

 

#### API Calls Examples - Update a Train Schedule attached to a Train Id


<table>
    <thead>
        <tr>
            <th>STEP</th>
            <th>API CALL</th>
            <th>REQUEST</th>
            <th>RESPONSE</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1. Make an API call to Validate the ShortTrainID</td>
            <td>1</td>
            <td>https://devint.pds.dev.use.torq.dev/train-management/train-id/short-id/A98765 12
            </td>
            <td>[

    {

        "trainId": 3485,

        "shortTrainId": "A98765 12",

        "customerTrainKey": {

            "scac": "CN",

            "section": "5",

            "trainSymbol": "A9876",

            "originDate": "2022-04-12"

        }

    }

]</td>
        </tr>
        <tr>
            <td>3. Validate the station name based on station number</td>
            <td>5</td>
            <td>https://devint.pds.dev.use.torq.dev/topology-lookup/station/station-name-or-station-number/58H
            </td>
            <td> 
              [GETStationName_Response.json](/json/GETStationName.json) 
          </td>
        </tr>
        <tr>
            <td>4. Update Train Schedule attached to a Train Id</td>
            <td>6</td>
            <td>https://devint.pds.dev.use.torq.dev/train-schedule/train-schedule <br><br>[POSTCreateTrainSchedule.json](/json/POSTCreateTrainSchedule.json) 
            </td>
            <td> HTTP CODE 201           </td>
        </tr>
        <tr>
            <td>5. Refresh the Train Schedule data</td>
            <td colspan=3>CALL Show the Train Schedule attached to a Train Id</td>            
        </tr>
    </tbody>
</table>

