# 🧪 OPR Coding Lab zur Vertiefung von Kovarianz und Kontravarianz in Java (mit Generics)

## 🎯 Ziel
Du lernst:
- den Unterschied zwischen **Kovarianz (`? extends`)** und **Kontravarianz (`? super`)**.
- wann und warum man welche Variante einsetzen sollte.
- wie man Generics sicher verwendet, ohne `ClassCastException`.

---

## 🧰 Vorbereitung (gleich wie im Coding Lab)

```java
class Tier {
    public void gibLaut() {
        System.out.println("Ein Tier macht ein Geräusch.");
    }
}

class Hund extends Tier {
    @Override
    public void gibLaut() {
        System.out.println("Wuff!");
    }
}

class Katze extends Tier {
    @Override
    public void gibLaut() {
        System.out.println("Miau!");
    }
}
```

---

## 🧩 **Lösung zu Übung 1: Kovarianz (`? extends`)**

```java
public static void gibTierLaute(List<? extends Tier> tiere) {
    for (Tier t : tiere) {
        t.gibLaut();
    }
}

// Anwendung:
List<Hund> hunde = Arrays.asList(new Hund(), new Hund());
List<Katze> katzen = Arrays.asList(new Katze(), new Katze());

gibTierLaute(hunde);
gibTierLaute(katzen);
```

❗ **Warum kein Hinzufügen erlaubt ist:**  
Weil der Compiler nicht weiß, ob die Liste z. B. `List<Hund>` oder `List<Katze>` ist – daher darf man keine `Tier`-Objekte hinzufügen (Typunsicherheit).

---

## 🧩 **Lösung zu Übung 2: Kontravarianz (`? super`)**

```java
public static void fuegeHundHinzu(List<? super Hund> liste) {
    liste.add(new Hund());
}
```

### Anwendung:

```java
List<Tier> tiere = new ArrayList<>();
List<Object> objekte = new ArrayList<>();

fuegeHundHinzu(tiere);
fuegeHundHinzu(objekte);
```

❗ **Warum kein sicheres Zurückgeben möglich ist:**  
Man weiß nicht, welcher Typ in der Liste gespeichert ist → Rückgabe als `Object`, nicht als `Hund`.

---

## ✅ Bonusidee: `? super Tier`

```java
public static void akzeptiereTiere(List<? super Tier> liste) {
    liste.add(new Hund());
    liste.add(new Katze());
    // Rückgabe nur als Object möglich
}
```

### Anwendung:

```java
List<Object> objekte = new ArrayList<>();
akzeptiereTiere(objekte);
```
