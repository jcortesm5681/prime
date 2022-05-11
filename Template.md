## Approvals
|Approved|Role|Assignee|Approved|Role|Assignee|
|--------|----|--------|--------|----|:------:|
|.       |    |        |        |    |        |


## Version
			

|Revision|Date      |Author             |Changes       |
|--------|----------|-------------------|:------------:|
|1.0     |04/26/2022|John Doe           | Created      | 


## Target Audience

```
Describe the Target Audience for this document.
Example:
```

For Part 1:  Business users , general users, Testing group

For Part 2:  Technical users, Testing group


### Form goals
```
Describe the form objectives like Create, update, delete, etc.
Example:
```

This form is used to:

* Create a ...
* Update a ...
* Delete a ...




### Fields form dependencies vs APIs
```
Include a form image, like  : " ![This is a alt text.](/image/APIFlow.png "This is a sample image.") "
Highlighting the areas where the APIs interact.
Suggested colors:
```
![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) #8faadc

![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) #a9d18e

![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) #f8cbad

![#FFD966](https://via.placeholder.com/15/FFD966/000000?text=+) #FFD966

![#FF7575](https://via.placeholder.com/15/FF7575/000000?text=+) #FF7575

![#B685DB](https://via.placeholder.com/15/B685DB/000000?text=+) #B685DB

![#7576A3](https://via.placeholder.com/15/7576A3/000000?text=+) #7576A3


### APIs
```
For each form objective, must create a table that contains: 
the name, method, endpoint, request and response example message, of the APIs used.

You can use links to include long messages:
[POST_API2_Response.json](/json/linktoFile.json) 

The colors in the image above, must correspond to the colors in the table below.

Example: 
```
#### Update the ...
 

|API ID|SERVICE NAME|METHOD|ENDPOINT|SPECIFIC GOAL|REQUEST|RESPONSE|
|------|------------|------|------|------|------|:------------|
|1|![#8faadc](https://via.placeholder.com/15/8faadc/000000?text=+) `NAME1`|GET|https://devint.pds.dev.use.torq.dev/ServiceName1/short-id/{shortTrainID}|Get the field x and y|https://devint.pds.dev.use.torq.dev/ServiceName1/short-id/A98765%12|```json[	{		"trainId": 3485,		"shortTrainId": "A9876512",		"customerTrainKey": {			"scac": "CN",			"section": "5",			"trainSymbol": "A9876",			"originDate": "2022-04-12"		}	}] ``` |
|2|![#a9d18e](https://via.placeholder.com/15/a9d18e/000000?text=+) `NAME2`|POST|https://devint.pds.dev.use.torq.dev/ServiceName2|Update field z|https://devint.pds.dev.use.torq.dev/ServiceName2|[POST_API2_Response.json](/json/linktoFile.json) |
|3|![#f8cbad](https://via.placeholder.com/15/f8cbad/000000?text=+) `NAME3`|POST|https://devint.pds.dev.use.torq.dev/ServiceName2|Update and show ZZ|https://devint.pds.dev.use.torq.dev/ServiceName3| ```HTTP CODE 201```   | 

#### API CALL SEQUENCE
```
Here you can describe a Step By Step, to get the objective.
Any logic form should be described here.
```
To Update a ...

a) Get the X and y Field, calling to API ID 1



b) Take the X and Y  FIELD from the JSON response from API ID 1 and call API ID 2 to get the Z info



c) Take the Z FIELD from the JSON response from API ID 2 and call API ID 3 to update and show the ZZ Field


 
 
