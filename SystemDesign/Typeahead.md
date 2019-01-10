##Type Ahead

![TypeAhead](../image/TypeAhead.png)

Google suggestion:
Prefix -> top n hot key Words
Twitter typeahead:
Suggestion + user + hashtag

###Scenario
- DAU = 500M
- SEARCH 4 * 6 * 500 = 12B every user searches 6 times and types 4 letters
- QPS = 12b / 86400 = 138k
- Peak QPS = 300k

###Service
![typeaheadService](../image/typeaheadService.png)

![typeAheadQuery](../image/typeAheadQuery.png)

typeAheadQuery

###Storage

###Scale
