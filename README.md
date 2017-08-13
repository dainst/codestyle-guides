# angular-styleguide

## Zeilenlänge
Die Zeilenlänge sollte 80 Zeichen nicht überschreiten.

## Einrückung

Einrückung mit 4 Leerzeichen, sofern nicht anders (z.B. für eine Sprache oder ein Projekt) definiert

## Leerzeichen

Jeweils ein Leerzeichen vor und nach allen Arten von Operatoren (TODO klären, auch vor Doppelpunkten? nä oder?)

```javascript
  this.foo = bar + 23;
```

Ein Leerzeichen nach if

```javascript
if (foo == bar)
```

Ein Leerzeichen vor öffnenden geschweiften Klammern

```javascript
  if (foo == bar) {
```

Ein Leerzeichen nach Komma zur Trennung von Parametern

```
  doStuff(foo, bar, baz);
```

## Leerzeilen

Bei Funktionen

public a() {

    doThis();
    doThat();
}

## Klammerung

Öffnende geschweifte Klammern in der gleichen Zeile wie die zugehörige Anweisung ("Java-Style":https://de.wikipedia.org/wiki/Einr%C3%BCckungsstil#Variation:_Java_.2F_Sun)

## Typangabe bei Variablendeklaration

Typangabe bei Variablendeklaration mit einem Leerzeichen getrennt

```javascript
private foo: Foo;
```

Optionale Semikola sollten immer angegeben werden.

## Anführungszeichen

Wann immer möglich, einfache '' verwenden. Z.B.

```javascript
const name = 'dai';
```

Doppelte "" dann verwenden, wenn man etwas innerhalb des Strings replacen möchte.

Zu klären: Imports, organize Import in IntelliJ setzt immer doppelte Anführungzeichen

```javascript
import {MapState} from "./map/map-state";
```

## Promises

```javascript
return Promise.resolve()
      .then(() => this.doThis())
      .catch() => this.doThat())
      .this(() => {
      })
      .catch() => Promise.reject(undefined));
```

## Objekte - Felder vs. Hashes.

Dank Typescript können wir ja Klassen definieren. Wenn wir z.B. in der Klasse Document das Feld resource definiert haben,
können wir bei Aufrufen dann schreiben

```javascript
doc.resource['filename']
```

D.h. wir verwenden den keybasierten Access für Felder die nicht definiert sind, und die Punktnotation für Felder die definiert sind.

## access modifiers in components

*public* wird ausgeschrieben, auch wenn es default visibility ist

*public* wird immer verwendet, wenn die Methoden von anderen Klassen aufgerufen werden. Zugriffe aus Templates gelten dabei als public access.

Diese Regel wurde eingeführt, weil der Typescript-Compiler Zugriffe auf Methoden aus Templates nicht erkennt und die IDE diese Methoden fälschlicherweise als unused markiert.

*public* darf nur weggelassen werden bei von Angular Interfaces abgeleiteten Klassen für die Interfacemethoden, z.B. ngOnInit. Hier ist beides erlaubt: public ngOnInit {, aber auch ngOnInit {
*private* für alles andere.




