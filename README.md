# Analyse Statique d’un APK Android (UnCrackable Level 1)

## Présentation

Ce projet présente une **analyse statique de sécurité** d’une application Android (APK) en utilisant des techniques de reverse engineering.
L’objectif est de comprendre la structure interne de l’application, identifier les vulnérabilités potentielles et évaluer les risques de sécurité.

## Objectifs

* Analyser la structure d’un fichier APK
* Effectuer du reverse engineering
* Identifier les informations sensibles
* Détecter des vulnérabilités
* Comparer différents outils de décompilation

## Outils utilisés
* JADX GUI
* dex2jar
* JD-GUI
* PowerShell (Windows)

## Étapes réalisées

### 🔹 Task 1 : Vérification de l’APK

* Vérification que l’APK est une archive valide (signature `PK`)
* Analyse de la structure :

  * `AndroidManifest.xml`
  * `classes.dex`
  * `res/`, `META-INF/`

### 🔹 Task 2 : Obtention de l’APK

* APK téléchargé depuis OWASP (UnCrackable Level 1)
* Vérification de l’intégrité et de la taille

### 🔹 Task 3 : Analyse avec JADX

* Décompilation de l’APK
* Identification des éléments principaux :

  * `MainActivity`
  * Détection du root
  * Détection du debug
  * Logique de vérification du secret

### 🔹 Task 4 : Recherche de données sensibles

* Recherche de mots-clés : `secret`, `debug`, `verify`
* Résultats :

  * Messages codés en dur
  * Fonction de validation (`a.a()`)
  * Utilisation de chiffrement AES

### 🔹 Task 5 : Conversion DEX → JAR

* Extraction de `classes.dex`
* Conversion en `app.jar` avec dex2jar

### 🔹 Task 6 : Comparaison JADX vs JD-GUI

| Critère         | JADX               | JD-GUI     |
| --------------- | ------------------ | ---------- |
| Support Android |  Complet           |  Limité   |
| Ressources      |  Oui               |  Non      |
| Lisibilité      |  Bonne             |  Moyenne |
| Obfuscation     |  Meilleure gestion |  Basique  |

---

## Vulnérabilités identifiées

###  1. Logique sensible exposée

* Vérification du secret réalisée côté client
* Accessible via reverse engineering

---

###  2. Chiffrement faible

* Utilisation de AES en mode ECB (non sécurisé)

---

###  3. Détection de debug

* Présente mais facilement contournable

---

###  4. Détection de root

* Implémentée mais insuffisante

---

##  Recommandations

* Déplacer la logique sensible côté serveur
* Utiliser un chiffrement sécurisé (AES-GCM)
* Renforcer l’obfuscation du code (ProGuard/R8)
* Améliorer les mécanismes anti-debug

---

##  Permissions

* `android.permission.INTERNET`
* `android.permission.ACCESS_NETWORK_STATE`


Fatimaezzahra Ennassiri

---

## 📅 Date

Avril 202
