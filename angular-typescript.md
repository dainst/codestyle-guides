# Angular/Typescript-Styleguide

Für Angular-/Typescript-Projekte, zurzeit ausschließlich idai-field.

## Zeilenlänge

Die Zeilenlänge sollte 120 Zeichen nicht überschreiten.

## Einrückung

Einrückung mit 4 Leerzeichen, sofern nicht anders (z.B. für eine Sprache oder ein Projekt) definiert.

## Leerzeichen

Jeweils ein Leerzeichen vor und nach allen Arten von Operatoren:

```typescript
this.foo = bar + 23;
```

Ein Leerzeichen nach if:

```typescript
if (foo == bar)
```

Ein Leerzeichen vor öffnenden geschweiften Klammern:

```typescript
if (foo == bar) {
```

Ein Leerzeichen nach Komma zur Trennung von Parametern:

```typescript
private doStuff(foo, bar, baz) {}
```

Mit Typisierung:

```typescript
private doStuff(foo: any, bar: any, baz: any): any {}
```

## Leerzeilen

Bei Funktionen:

```typescript
public a() {

    doThis();
    doThat();
}
```

## Klammerung

Öffnende geschweifte Klammern in der gleichen Zeile wie die zugehörige Anweisung (["Java-Style"](https://de.wikipedia.org/wiki/Einr%C3%BCckungsstil#Variation:_Java_.2F_Sun)).

## Typangabe bei Variablendeklaration

Typangabe bei Variablendeklaration mit einem Leerzeichen getrennt:

```typescript
private foo: Foo;
```

Optionale Semikola sollten immer angegeben werden.

## Arrays

Für Arrays aus TypeScript-Basistypen (string, number, boolean, any) wird die Schreibweise mit eckigen Klammern verwendet:
```
const values: string[] = ['A', 'B', 'C'];
```

Für alle anderen Arrays wird die Schreibweise mit spitzen Klammern verwendet:
```
const resources: Array<Resource> = [{ ... }, { ... }];
```

## Anführungszeichen

Wann immer möglich, einfache '' verwenden. Z.B.:

```typescript
const name = 'dai';
```

## Benennung und Kommentare

Bei der Benennung von Variablen, Konstanten, Funktionen usw. sollte auf Abkürzungen verzichtet werden. Es sollten möglichst sprechende Namen gewählt werden, sodass zusätzliche Kommentare nicht nötig sind. 

Kommentare können in folgenden Fällen gesetzt werden:

* Über eine Klasse oder ein Modul zur Erläuterung deren/dessen Aufgaben
* An allen Stellen, an denen die Funktionsweise von Codebestandteilen aus der Benennung der Variablen, Funktionen usw. nicht eindeutig hervorgeht (z.B. Code zur Behebung komplexerer Bugs)


## Promises

Bevorzugt async und await benutzen, um nach Möglichkeit auf Promise-Chaining (.then(() => {}).then...) verzichten zu können.

## Objekte - Felder vs. Hashes

Wenn wir z.B. im Interface Document das Feld resource definiert haben,

```typescript
interface Document {
  resource: any;
}
```

können wir bei Aufrufen dann schreiben:

```typescript
const document: Document = { resource: {} };
document.resource['filename'] = 'a.txt';
```

D. h. wir verwenden den keybasierten Access für Felder, die nicht definiert sind, und die Punktnotation für Felder, die definiert sind.

## Schleifen

* entweder *forEach* für Schleifen verwenden und mit Array-Funktionen (filter, map, reduce etc.) kombinieren oder *for .. of* verwenden
* *for mit i* nur in begründeten Ausnahmefällen verwenden

## let, const, var

Wann immer es geht, **const** verwenden. Wenn das nicht geht, **let** verwenden.
**var** wird grundsätzlich nicht verwendet.

Temporäre Variablen erst kurz vor Verwendung deklarieren.

## Importe

Importe werden in der folgenden Reihenfolge angegeben:

1. Externe Libraries (z.B. Angular)
2. Eigene Libraries (z.B. idai-field-core)
3. Module der aktuellen Codebasis

```
import { Component } from '@angular/core';
import { Datastore, ProjectConfiguration } from 'idai-field-core';
import { Messages } from '../messages/messages';
```


## Parameter-Side-Effects

Grundsätzlich gilt:
Eine Methode mit Rückgabewert sollte ohne Parameter-Side-Effects auskommen. Negativbeispiel:
```
public manipulate(a: string[]): string[] {
    a.splice(0, 1);
    return a;
}
```
Der Caller von manipulate weiß beim Aufruf der Methode nicht, dass sich der Parameter a ändert. Durch die Angabe des Rückgabewertes wird fälschlicherweise suggeriert, dass das bestehende Array nicht geändert, sondern ein Neues zurückgegeben wird.

In Methoden ohne Rückgabewert, bei denen die Manipulation eines Parameters aus dem Namen ausreichend hervorgeht, können Parameter-Side-Effects unter Umständen sinnvoll sein. Möglich wären also die beiden folgenden Varianten:
```
public manipulate(a: string[]) {
    a.splice(0, 1);
}
```

```
public manipulate(a: string[]): string[] {
    return a.slice(1);
}
```

## Access modifiers in Components

*public* wird ausgeschrieben, auch wenn es bei Typescript der Default-Modifier ist.

*public* wird immer verwendet, wenn die Methoden von anderen Klassen aufgerufen werden. Zugriffe aus Templates gelten dabei als public access.

*public* wird nur bei von Angular-Interfaces abgeleiteten Klassen für die Interface-Methoden weggelassen, z.B. ngOnInit oder ngOnChanges.

*private* bzw. *protected* für alles andere.


## Static methods

Bei private methods sollte **static** verwendet werden, wann immer es möglich ist. Dadurch ist bei diesen Methoden auf den ersten Blick ersichtlich, dass keine Felder des Objekts manipuliert werden.

Public static methods werden selten verwendet, da sie aus Templates nicht aufgerufen werden können. Utility-Funktionen werden nicht als public static methods innerhalb von Klassen definiert, sondern einzeln exportiert, sodass sie zur Verwendung unabhängig voneinander importiert werden können.


## Reihenfolge von Feldern und Methoden in Klassen

1. Fields
2. Constructor
3. Public methods
3. Public static methods
4. Protected methods 
5. Private methods
6. Private static methods


## HTML/CSS

### Einrückung
Einrückungen sollten grundsätzlich mit 4 Leerzeichen vorgenommen werden. Auf Modularisierung (Ausgliedern in neue Angular-Components) sollte geachtet werden, sodass Templates nicht zu lang werden.

### CSS-Einbindung
Auf Style-Attribute sollte vollständig verzichtet werden. Stattdessen werden Klassen oder IDs verwendet.

### Hierarchie in SCSS-Files
Von der Möglichkeit der Hierarchiedarstellung in SCSS-Files sollte Gebrauch gemacht werden, um die tatsächliche Gliederung im DOM bzw. in der Component-Struktur annähernd widerzuspiegeln.
```
#resources {
  position: fixed;
  width: 100%;
  z-index: 1001;

  #search-bar-container {
    padding-right: 8px;

    #search-bar #filter-button {
      right: 5px;
    }
  }
}
```
