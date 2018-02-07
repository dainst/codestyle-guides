// TODO Compiler-Settings (no implicit any usw.)
// TODO Lamba-Notation (this-Pointer und implizites Return)


# Angular-Styleguide

* für Angular / Typescript Projekte
* idai-field-client
* idai-components-2

## Zeilenlänge
Die Zeilenlänge sollte 110 Zeichen nicht überschreiten.

## Einrückung

Einrückung mit 4 Leerzeichen, sofern nicht anders (z.B. für eine Sprache oder ein Projekt) definiert

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
private doStuff(foo, bar, baz) { }
```

Mit Typisierung:

```typescript
private doStuff(foo: any, bar: any, baz: any): any { }
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

Öffnende geschweifte Klammern in der gleichen Zeile wie die zugehörige Anweisung ("Java-Style":https://de.wikipedia.org/wiki/Einr%C3%BCckungsstil#Variation:_Java_.2F_Sun)

## Typangabe bei Variablendeklaration

Typangabe bei Variablendeklaration mit einem Leerzeichen getrennt:

```typescript
private foo: Foo;
```

Optionale Semikola sollten immer angegeben werden.

## Anführungszeichen

Wann immer möglich, einfache '' verwenden. Z.B.:

```typescript
const name = 'dai';
```

Doppelte "" dann verwenden, wenn man etwas innerhalb des Strings replacen möchte.

Das Verhalten von IntelliJ (https://stackoverflow.com/questions/39779272/webstorm-phpstorm-double-quotes-in-typescript-auto-import) sollte umgestellt werden, das bei *organize imports* auch einfache Anführungszeichen generiert werden.

```typescript
import {MapState} from './map/map-state';
```

## Temporäre Variablen

... erst kurz vor Verwendung deklarieren. Am besten ganz vermeiden.


## Promises

Bevorzugt async und await benutzen, um nach Möglichkeit auf Promise-Chaining (.then(() => {}).then...) verzichten zu können.

## Objekte - Felder vs. Hashes.

Dank Typescript können wir ja Klassen definieren. Wenn wir z.B. in der Klasse Document das Feld resource definiert haben,

```typescript
class Doc {
  resource: any
}
```

können wir bei Aufrufen dann schreiben

```typescript
const doc: Doc = { resource: { } };
doc.resource['filename'] = 'a.txt';
```

D.h. wir verwenden den keybasierten Access für Felder die nicht definiert sind, und die Punktnotation für Felder die definiert sind.

## Schleifen

* bevorzugt *forEach* für Schleifen verwenden und mit Array-Funktionen (filter, map, includes, reduce etc.) kombinieren
* nur wenn nötig *for .. of* verwenden
* *for mit i* nur in begründeten Ausnahmefällen verwenden

## let, const, var

Wann immer es geht, **const** verwenden. Wenn das nicht geht, **let** verwenden.
**var** wird grundsätzlich nicht verwendet.

## Parameter-Sideeffects

Grundsätzlich gilt:
Eine Methode mit Rückgabewert sollte ohne Parameter-Sideeffects auskommen. Negativbeispiel:
```
public manipulate(a: string[]): string[] {
    a.splice(0, 1);
    return a;
}
```
Der Caller von manipulate weiß beim Aufruf der Methode nicht, dass sich der Parameter a ändert. Durch die Angabe des Rückgabewertes wird zusätzlich fälschlicherweise suggeriert, dass das bestehende Array nicht geändert, sondern ein neues zurückgegeben wird.

In Methoden ohne Rückgabewert, bei denen die Manipulation eines Parameters aus dem Namen ausreichend hervorgeht, können Parameter-Sideeffects unter Umständen sinnvoll sein.
```
public manipulate(a: string[]) {
    a.splice(0, 1);
}
```

Nach Möglichkeit sollte allerdings ganz auf Parameter-Sideeffects verzichtet werden.
```
public manipulate(a: string[]): string[] {
    return a.slice(1);
}
```

## Access modifiers in Components

*public* wird ausgeschrieben, auch wenn es bei Typescript der Default-Modifier ist.

*public* wird immer verwendet, wenn die Methoden von anderen Klassen aufgerufen werden. Zugriffe aus Templates gelten dabei als public access.

Diese Regel wurde eingeführt, weil der Typescript-Compiler Zugriffe auf Methoden aus Templates nicht erkennt und die IDE diese Methoden fälschlicherweise als unused markiert.

*public* wird nur bei von Angular-Interfaces abgeleiteten Klassen für die Interface-Methoden weggelassen, z.B. ngOnInit oder ngOnChanges.

*private* bzw. *protected* für alles andere.


## Static methods

Bei private methods sollte **static** verwendet werden, wann immer es möglich ist. Dadurch ist bei diesen Methoden auf den ersten Blick ersichtlich, dass keine Felder des Objekts manipuliert werden. Feldzugriffe sollten generell möglichst nah an den Einstiegspunkten in die Klasse (public methods) stattfinden.

Public static methods werden selten verwendet, da sie aus Templates nicht aufgerufen werden können. Bei Utility-Klassen sollten statt public static methods direkt Funktionen exportiert werden.


## Reihenfolge von Feldern und Methoden in Klassen

1. Fields
2. Constructor
3. Public methods
3. Public static methods
4. Protected methods 
5. Private methods
6. Private static methods

Diese Reihenfolge soll u. a. erreichen, dass sich Methoden, die Felder manipulieren, möglichst weit oben in der Datei befinden.


## HTML/CSS

### Einrückung
Einrückungen sollten grundsätzlich mit 4 Leerzeichen eingerückt werden. Auf Modularisierung (Ausgliedern in neue Angular-Components) sollte geachtet werden, sodass Templates nicht zu lang werden.

### CSS-Einbindung
Auf Style-Attribute sollte vollständig verzichtet werden. Stattdessen werden Klassen oder IDs verwendet.

### Hierarchie in SCSS-Files
Von der Möglichkeit der Hierarchiedarstellung in SCSS-Files sollte Gebrauch gemacht werden:
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
