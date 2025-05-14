# 🧪 OPR Coding Lab zur Vertiefung von Kovarianz und Kontravarianz in Java (mit Generics)

## 🎯 Ziel
Du lernst:
- den Unterschied zwischen **Kovarianz (`? extends`)** und **Kontravarianz (`? super`)**.
- wann und warum man welche Variante einsetzen sollte.
- wie man Generics sicher verwendet, ohne `ClassCastException`.

---

## 🧰 Vorbereitung

Lege folgende Klassenstruktur an:

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

## 🧩 **Übung 1: Kovarianz (`? extends`)**

```java
public static void gibTierLaute(List<? extends Tier> tiere) {
    for (Tier t : tiere) {
        t.gibLaut();
    }
}
```

### Aufgaben:
1. Erstelle eine `List<Hund>` und eine `List<Katze>`.
2. Übergib beide Listen an `gibTierLaute(...)`.
3. Erkläre, warum man in der Methode keine Elemente zur Liste hinzufügen darf.

---

## 🧩 **Übung 2: Kontravarianz (`? super`)**

```java
public static void fuegeHundHinzu(List<? super Hund> liste) {
    liste.add(new Hund());
}
```

### Aufgaben:
1. Übergib eine `List<Tier>` an `fuegeHundHinzu(...)`.
2. Was passiert, wenn du `List<Hund>` oder `List<Object>` übergibst?
3. Warum kannst du keine Elemente aus `liste` zurückgeben als `Hund`?

---

## ✅ Bonusidee

- Schreibe eine Methode, die mit `<? super Tier>` arbeitet und sowohl `Tier`, `Hund`, als auch `Object` akzeptiert.
