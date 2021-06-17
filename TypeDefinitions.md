# Type Definitions
## PlanObject
[PlanWeekObject Reference](#planweekobject)
```ts
{
    name: string;                   // Klassen-Name Bsp: "5a"
    internalID: string;             // Bsp: "c00001"
    available: boolean;             // Wenn "true" ist der Plan per API verfügbar
    teacher?: string;               // Klassenlehrer
    weeks?: PlanWeek[];             // Die nächsten 4 Wochen
}
```
## PlanWeekObject
```ts
{
  weekNumber: number; // Wochen-Nummer
  lastChanged: number; // Die letzte erkannte Änderung
  startDate: DateTime; // Datum der Woche (Montag)
  html: string; // HTML, dass den Vertretungsplan darstellt
}
```

<br/>
<hr/>
<br/>

## UntisWeekObject
```ts
{
    startDate: Date;                // Datum der Woche (Montag)
    days: Array<UnitsDay>;          // Alle Tage der Woche
    weekNumber: number;             // Wochen-Nummer
    lastChanged: number;            // Die letzte erkannte Änderung
}
```
## UntisDayObject
[UntisLessonObject Reference](#untislessonobject)
```ts
{
  date: DateTime; // Datum des Tages
  lessons: Array<UntisLesson>; // Alle Stunden des Tages (Index entspricht der Reihenfolge (1. Stunde, 2. Stunde, ...))
  infos?: any; // 🆕 Infos für den Tag aus Ver-Kla-Dru
}
```
## UntisLessonObject
[UntisSubjectObject Reference](#untissubjectobject)
```ts
{
    subjects: Array<UntisSubject>;  // Alle Fächer in dieser Stunde
}
```
## UntisSubjectObject
```ts
{
  name: string; // Name des Fachs z.B. "De"
  room?: string; // Raum z.B. "Aula"
  teacher?: string; // 🆕 Zeigt den Lehrer für diese Fach
  changed?: boolean; // Sind für diese Stunde Änderungen vorgenommen? (Rot im Vertretungsplan) 🆕 Wird jetzt individuell angezeigt!
  special?: boolean; // Ist das kein normaler Unterricht z.B. "Schulgottesdienst"
  isCoop?: boolean; // Sind in diesem Fach mehrere Klassen zusammen z.B. Religion / Ethik bzw. sind mehrere Lehrer für dieses Fach zuständig z.B. Sport (+ Schwimmen)

  hasExtraInfo: boolean; // 🆕🆕 Gibt an, ob die nachfolgenden Infos verfügbar sind

  notice?: string; // Bemerkungen aus Ver-Kla-Dru
  changeType?: string; // Die Art der Änderung aus Ver-Kla-Dru
  isNew?: boolean; // 🆕 Zeigt an, ob dieser Eintrag seit dem letzten Update neu ist
  oldName?: string; // 🆕 Dieses Fach war hier früher mal
}
```

<br/>
<hr/>
<br/>

## SubjectInfo
```ts
  interface SubjectInfo {
    name: string; // Name wie auf dem Vertretungsplan
    fullName: string; // Langer Name (Beschreibung)
    teacher: string; // Lehrer, der dieses Fach Unterrichtet
    group: string; // Gruppe, zu dem dieses Fach gehört
  }
```

<br/>
<hr/>
<br/>

## JoomlaFeedEntry
[JoomlaFeedAuthor Definition](#joomlafeedauthor)
```ts
interface JoomlaFeedEntry {
  title: string; // Title der Ankündigung
  link: string; // Link zur HGG Seite
  html: string; // 🆕 Inhalt
  category: string; // Kathegorie
  author: JoomlaFeedAuthor; // Autor
  published: string; // 🆕 Veröffentlichungs Datum
  updated: string; // 🆕 Änderungs-Datum
}
```

## JoomlaFeedAuthor
```ts
interface JoomlaFeedAuthor {
  name: string; // Name des Autors
  email: string; // Email des Autors
}
```