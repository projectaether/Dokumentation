# Endpoints

## Class List
**GET** ```/classes```  
Liste aller Klassen am HGG. [PlanObject Reference](/TypeDefinitions#planobject)
```json
{
    "classes": [ PlanObject ]
}
```

## Parsed Class HTML
**GET** ```/classes/${KlassName}/parsed```  
**GET** ```/classes/${KlassName}/parsed?filter=${filter}``` [Filter Reference](/Filter)   
Vertretungsplan als spezielles JSON für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [UntisWeekObject Reference](#untisweekobject)
```json
[ UntisWeekObject ]
```

## Raw Class HTML
**GET** ```/classes/${KlassName}/raw```  
Vertretungsplan - HTML für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [PlanWeekObject Reference](/TypeDefinitions#planweekobject)
```json
{
    "internalID": "c00001",
    "name": "5a",
    "available": true,
    "weeks": [ PlanWeekObject ]
}
```

## Class Subjects List   
**GET** ```/classes/${KlassName}/subjects```  
Alle Fächer als Array für die mit ```${KlassName}``` angegebene Klasse.
```json
[ string ]
```

## Class Timetable  
**GET** ```/classes/${KlassName}/timetable```   
Stundenplan als spezielles JSON für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [UntisWeekObject Reference](/TypeDefinitions#untisweekobject)
```json
[ UntisWeekObject ]
```

<hr/>

## News Feed
**GET** ```/feed/hgg/news```   
News der HGG Seite in übersichtlichem JSON. [JoomlaFeedEntry Reference](/TypeDefinitions#joomlafeedentry)
```json
[ JoomlaFeedEntry ]
```