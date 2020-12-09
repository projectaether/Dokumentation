# API Dokumentation

[Was ist **ProjectAether**?](https://projectaether.github.io/)

## Get Started

Bei der API handelt es sich um eine REST-API.  
Das bedeutet, dass Anfragen per GET-Parameter getätigt werden und somit jede Programmiersprache ohne Client-Library genutzt werden kann.  
Beispiele sind unten zu finden.  

Basis-URL: ```https://api.hgg.zusor.io/```

## Richtlinien
⚠️ Namen von Klassen werden *immer* **klein** geschrieben ⚠️

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
**GET** ```/classes/${KlassName}/raw```  
Vertretungsplan - HTML für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [PlanWeekObject Reference](#planweekobject)
```json
{
    "internalID": "c00001",
    "name": "5a",
    "available": true,
    "weeks": [ PlanWeekObject ]
}
```

### 🆕 Class Subjects List   
**GET** ```/classes/${KlassName}/subjects```  
Alle Fächer als Array für die mit ```${KlassName}``` angegebene Klasse.
```json
[ string ]
```

### 🆕 Class Timetable  
**GET** ```/classes/${KlassName}/timetable```   
Stundenplan als spezielles JSON für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [UntisWeekObject Reference](#untisweekobject)
```json
[ UntisWeekObject ]
```

### Parsed Class HTML
**GET** ```/classes/${KlassName}/parsed```  
**GET** ```/classes/${KlassName}/parsed?filter=${filter}``` 🆕 [New Filter Reference](https://projectaether.github.io/Dokumentation/Filter)   
Vertretungsplan als spezielles JSON für alle angezeigten Wochen für die mit ```${KlassName}``` angegebene Klasse. [UntisWeekObject Reference](#untisweekobject)
```json
[ UntisWeekObject ]
```

## Objects
### PlanObject
[PlanWeekObject Reference](#PlanWeekObject)
```ts
{
    name: string;                   // Klassen-Name Bsp: "5a"
    internalID: string;             // Bsp: "c00001"
    available: boolean;             // Wenn "true" ist der Plan per API verfügbar
    lastFetched?: number;           // Die API arbeitet mit einer Version, die zu diesem Zeitpunkt vom HGG-Server geladen wurde
    lastChanged?: number;           // Letzte Änderung der neusten Woche
    teacher?: string;               // Klassenlehrer
    weeks?: PlanWeek[];             // Die nächsten 4 Wochen
}
```
### PlanWeekObject
```ts
{
    html: string;                   // HTML, dass den Vertretungsplan darstellt
    weekNumber: number;             // Wochen-Nummer
    lastChanged: number;            // Die letzte erkannte Änderung
    startDate: Date;                // Datum der Woche (Montag)
    debug?: string;                 // ⛔ Reserviert
}
```
---
### UntisWeekObject
```ts
{
    startDate: Date;                // Datum der Woche (Montag)
    days: Array<UnitsDay>;          // Alle Tage der Woche
    weekNumber: number;             // Wochen-Nummer
    lastChanged: number;            // Die letzte erkannte Änderung
}
```
### UntisDayObject
[UntisLessonObject Reference](#UntisLessonObject)
```ts
{
    date: Date;                     // Datum des Tages
    lessons: Array<UntisLesson>;    // Alle Stunden des Tages (Index entspricht der Reihenfolge (1. Stunde, 2. Stunde, ...))
}
```
### UntisLessonObject
[UntisSubjectObject Reference](#UntisSubjectObject)
```ts
{
    subjects: Array<UntisSubject>;  // Alle Fächer in dieser Stunde
}
```
### UntisSubjectObject
```ts
{
    name: string;                   // Name des Fachs z.B. "De"
    room?: string;                  // Raum z.B. "Aula"
    teacher?: string;               // 🆕 Zeigt den Lehrer für diese Fach
    changed?: boolean;              // Sind für diese Stunde Änderungen vorgenommen? (Rot im Vertretungsplan) ( ⚠️ Ist bei allen Fächern in einer Stunde gleich! ⚠️ )
    special?: boolean;              // Ist das kein normaler Unterricht z.B. "Schulgottesdienst"
    isCoop?: boolean;               // Sind in diesem Fach mehrere Klassen zusammen z.B. Religion / Ethik bzw. sind mehrere Lehrer für dieses Fach zuständig z.B. Sport (+ Schwimmen)
}
```
