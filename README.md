# API Dokumentation

## Get Started

Bei der API handelt es sich um eine REST-API.  
Das bedeutet, dass Anfragen per GET-Parameter getätigt werden und somit jede Programmiersprache ohne Client-Library genutzt werden kann.  
Beispiele sind unten zu finden.  

Basis-URL: ```https://api.hgg.zusor.io/```

## Endpoints

### Class List
**GET** ```/classes```  
Liste aller Klassen am HGG. [PlanObject Reference](#planobject)
```json
{
    "classes": [ PlanObject ]
}
```

### Raw Class HTML
**GET** ```/classes/raw/${KlassName}```  
Vertretungsplan - HTML für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [PlanWeekObject Reference](#planweekobject)
```json
{
    "internalID": "c00001",
    "name": "5A",
    "available": true,
    "weeks": [ PlanWeekObject ]
}
```

### Parsed Class HTML
**GET** ```/classes/parsed/${KlassName}```  
Vertretungsplan als spezielles JSON für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [UntisWeekObject Reference](#UnitsWeekObject)
```json
[ UntisWeekObject ]
```

## Objects
### PlanObject
[PlanWeekObject Reference](#PlanWeekObject)
```ts
{
    name: string;
    internalID: string;
    available: boolean;
    lastFetched?: number;
    weeks?: PlanWeek[];
}
```
### PlanWeekObject
```ts
{
    html: string;
    weekNumber: number;
    lastChanged: number;
    debug?: string;
}
```
---
### UnitsWeekObject
[PlanWeekObject Reference](#PlanWeekObject)
```ts
{
    startDate: Date;
    days: Array<UnitsDay>;
    base: PlanWeek;
}
```
### UnitsDayObject
[UntisLessonObject Reference](#UntisLessonObject)
```ts
{
    date: Date;
    lessons: Array<UntisLesson>;
}
```
### UntisLessonObject
[UntisSubjectObject Reference](#UntisSubjectObject)
```ts
{
    subjects: Array<UntisSubject>;
}
```
### UntisSubjectObject
```ts
{
    name: string;
    room?: string;
    teacher?: string;
    changed?: boolean;
    special?: boolean;
    isCoop?: boolean;
}
```
