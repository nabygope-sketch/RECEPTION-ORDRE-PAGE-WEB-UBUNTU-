# 🔘 Projet ESP32 - Commande à distance (LED & Buzzer)

## Objectif

Créer une interface web permettant de **contrôler une LED et un buzzer** connectés à une ESP32 via des boutons sur une page web.

---

## Étape 1 : Ajout des boutons dans `data.php`

Modifier le fichier :

```bash
/var/www/html/btsciel/data.php
```

### Code à ajouter dans `<body>`

```html
<h1>Commande ESP32</h1>

<button onclick="fetch('http://IP_ESP32/son')">
Allumer
</button>

<button onclick="fetch('http://IP_ESP32/led')">
Éteindre
</button>
```

---

### Résultat attendu

* Un bouton **Allumer** → active le buzzer
* Un bouton **Allumer** → contrôle la LED
* Interaction via requêtes HTTP envoyées à l’ESP32

---

## Étape 2 : Ajout des actionneurs sur l’ESP32

### Matériel nécessaire

* ESP32
* Grove Buzzer
* LED
* Résistance **220 Ω**
* Breadboard

---

## 🔊 1. Test Buzzer

### Branchement

* VCC → 3.3V
* GND → GND
* SIG → GPIO 26

### Code Arduino

```cpp
const int buzzer = 23;

void setup() {
  ledcAttach(buzzer, 2000, 8);
}

void loop() {
  ledcWriteTone(buzzer, 262); // Do
  delay(300);

  ledcWriteTone(buzzer, 294); // Ré
  delay(300);

  ledcWriteTone(buzzer, 330); // Mi
  delay(300);

  ledcWriteTone(buzzer, 0); // stop
  delay(1000);
}
```

### Résultat attendu

Le buzzer joue une séquence de notes (Do, Ré, Mi).

---

## 💡 2. LED

### Branchement

* LED connectée sur **GPIO 23**
* Résistance : **220 Ω**

### ❓ Questions

* **Broche utilisée** : GPIO 23
* **Valeur résistance** : 220 Ω

---

### 💻 Code Arduino

```cpp
const int led = 23;

void setup() {
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH); // allumer
  delay(2000);

  digitalWrite(led, LOW); // éteindre
  delay(2000);
}
```

---

### ✅ Résultat attendu

* LED s’allume pendant 2 secondes
* Puis s’éteint pendant 2 secondes

---

## ✔️ Validation

* Tester les boutons depuis la page web
* Vérifier le fonctionnement du buzzer et de la LED
* Faire valider le montage par le professeur

---

## 📌 Remarques

* Vérifier que l’ESP32 est accessible via son IP
* S’assurer que le serveur web et l’ESP32 sont sur le même réseau
* Adapter les broches GPIO si nécessaire

---
