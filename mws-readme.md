---
layout: default
title: Documentation - Mini Web Server Pro
---
# Mini Web Server — Android
### by [Taysir Digital Group (TDG)](https://taysirdigitalgroup.github.io) · Aliou Mbengue, PDG/CEO

<p align="center">
  <img src="assets/icon.png" width="96" alt="Mini Web Server icon"/>
</p>

<p align="center">
  <b>Apache 2.4 · MariaDB 10.11 · PHP 8.3 · phpMyAdmin 5.2 · FTP intégré</b><br/>
  Le serveur web complet dans votre poche — 100 % natif ARM64, aucune dépendance externe.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Android-7%2B%20(API%2024%2B)-brightgreen?logo=android"/>
  <img src="https://img.shields.io/badge/Flutter-3-blue?logo=flutter"/>
  <img src="https://img.shields.io/badge/Apache-2.4%20ARM64-orange"/>
  <img src="https://img.shields.io/badge/PHP-8.3-purple"/>
  <img src="https://img.shields.io/badge/MariaDB-10.11-teal"/>
  <img src="https://img.shields.io/badge/licence-propriétaire-lightgrey"/>
</p>

---

## Présentation

**Mini Web Server** transforme votre smartphone Android en serveur web complet.  
Développez, testez et hébergez vos sites PHP/MySQL directement depuis votre appareil — sans PC, sans connexion internet, sans configuration fastidieuse.

Idéal pour :
- Les développeurs web qui veulent tester leurs projets en mobilité
- Les formateurs qui animent des ateliers sans infrastructure réseau
- Les entrepreneurs qui veulent présenter une démo offline
- Toute personne souhaitant héberger un site en réseau local

---

## Fonctionnalités

### 🌐 Serveur Apache 2.4 (ARM64 natif)
- Démarrage/arrêt en un tap
- Port configurable (défaut : 8080)
- Dossier racine `htdocs` personnalisable
- `mod_rewrite` activé (URL propres, `.htaccess`)
- Support MIME audio/vidéo + `Accept-Ranges`
- **PHP 8.3.11** intégré avec extensions : `gd`, `zip`, `exif`, `intl`, `sodium`, `xsl`, `calendar`, `pdo_sqlite`, `mysqli`, `openssl`, `curl`, `mbstring`, `json`, `opcache`…
- Gestion dynamique des extensions PHP (activer/désactiver sans recompiler)
- Sélecteur de version PHP (8.3 / 7.4 — legacy)

### 🗄️ MariaDB 10.11
- Démarrage automatique avec Apache (ou indépendant)
- Accès **phpMyAdmin 5.2** depuis le navigateur
- Identifiants par défaut : `root` / `root` (modifiables via phpMyAdmin)

### 📂 Serveur FTP intégré
- Serveur FTP passif natif (port 2221 par défaut)
- Authentification configurable (user/password)
- Compatible avec FileZilla, Cyberduck, et tout client FTP standard
- **Gestionnaire de fichiers intégré** (sans client FTP externe) :
  - Parcourir l'arborescence `htdocs` avec fil d'Ariane
  - Téléverser des fichiers depuis le stockage ou apps externes
  - Créer des dossiers
  - Renommer · **Déplacer** · **Copier** · Supprimer
  - Éditeur de texte intégré (`.php`, `.html`, `.js`, `.css`, `.json`, `.sql`, `.env`…)

### 💻 Console Termux
- Terminal intégré (nécessite Termux)
- Commandes rapides préconfigurées : `pkg update`, `apachectl`, `mysqld`, `php -v`, `netstat`, `df -h`, `free -h`
- Saisie libre de commandes bash

### 📋 Journaux en temps réel
- Logs Apache, MariaDB et FTP dans un seul flux
- Badges colorés par source (`SRV` bleu · `FTP` teal)
- Codes couleur : vert (succès) · orange (arrêt) · rouge (erreur)
- Copie et export du journal

### 🌍 Interface bilingue EN / FR
- Détection automatique de la langue du téléphone
- Changement manuel depuis l'AppBar (dropdown 🇬🇧 / 🇫🇷)
- Toutes les pages et messages localisés

### 📣 Publicité
- **Start.io** actif (v1 release — ne nécessite pas de store officiel)
- **AdMob** intégré et commenté — réactivation après publication Play Store / App Store

---

## Les 4 pages de l'application

| Page | Icône | Contenu |
|------|-------|---------|
| **Serveurs** | `dns` | Contrôle Apache · MariaDB · FTP · ports · racine · phpMyAdmin · FTP Manager |
| **Console** | `terminal` | Terminal Termux + commandes rapides préconfigurées |
| **Journaux** | `article` | Logs temps réel avec badges source, couleurs et export |
| **Infos** | `info` | À propos · Développeur · Contacts · Stack technique · Nous soutenir |

---

## Utilisation

### Démarrer les serveurs

1. Ouvrir l'app → onglet **Serveurs**
2. Appuyer sur le toggle **Apache** → `✓ Démarré sur :8080`
3. (Optionnel) Appuyer sur le toggle **MariaDB** → `✓ Démarré`
4. Votre site est accessible depuis n'importe quel appareil du réseau local à :  
   `http://<IP_WiFi>:8080`

### Accéder à phpMyAdmin

- Apache + MariaDB démarrés → appuyer sur le lien **Admin** dans la carte MariaDB  
- URL : `http://<IP_WiFi>:8080/pma`  
- Identifiants : `root` / `root`

### Déposer des fichiers via FTP

1. Démarrer le serveur **FTP** (onglet Serveurs)
2. **Option A** — Client FTP externe (FileZilla, etc.) :
   - Hôte : `<IP_WiFi>` · Port : `2221` · User : `admin` · Pass : `admin`
3. **Option B** — Gestionnaire intégré :
   - Appuyer sur le lien `IP:port` → bouton **Gérer** → naviguer et gérer les fichiers

### Changer la version PHP

- Carte Apache → ligne **PHP** → appuyer sur la version affichée
- Sélectionner `8.3` ou `7.4` → Apache recharge sans couper les connexions (graceful restart)

### Activer/désactiver les extensions PHP

- Carte Apache → ligne **PHP** → bouton **Extensions**
- Cocher/décocher les extensions dynamiques → **Appliquer**

---

## Architecture technique

```
Mini Web Server
├── lib/
│   ├── l10n/
│   │   └── app_strings.dart       Localisation EN/FR (InheritedWidget)
│   ├── pages/
│   │   ├── home_page.dart         AppBar + TabBar (4 onglets)
│   │   ├── dashboard_page.dart    Contrôle serveurs + FTP
│   │   ├── ftp_manager_page.dart  Gestionnaire de fichiers FTP
│   │   ├── console_page.dart      Terminal Termux
│   │   ├── logs_page.dart         Journaux temps réel
│   │   ├── info_page.dart         À propos + contacts
│   │   └── vhost_dashboard_screen.dart  Liste des sites hébergés
│   ├── services/
│   │   ├── native_server_service.dart   Apache + MariaDB (JNI)
│   │   ├── ftp_server_service.dart      Serveur FTP passif (dart:io)
│   │   ├── server_state.dart            État global (ChangeNotifier)
│   │   ├── network_service.dart         Détection IP WiFi
│   │   └── notification_service.dart    Notification persistante
│   └── widgets/
│       ├── server_card.dart
│       ├── php_version_selector.dart
│       ├── extension_manager_sheet.dart
│       └── password_info_dialog.dart
├── android/app/src/main/jniLibs/arm64-v8a/
│   ├── libnative_httpd.so         Apache 2.4 ARM64
│   ├── libnative_mysqld.so        MariaDB 10.11 ARM64
│   ├── libnative_libphp83.so      PHP 8.3.11 ARM64
│   └── libnative_libphp74.so      PHP 7.4.33 ARM64 (⏳)
└── assets/
    ├── php_extensions/            Extensions PHP dynamiques (.so)
    └── phpmyadmin.zip             phpMyAdmin 5.2
```

### Stack ARM64

| Composant | Version | Build |
|-----------|---------|-------|
| Apache httpd | 2.4 | `build_apache_only.sh v4` |
| PHP | 8.3.11 | `build_php_only83.sh v56` |
| MariaDB | 10.11.9 | `build_mariadb_ndk.sh` |
| phpMyAdmin | 5.2.1 | `build_assets.sh` |
| ICU | 74.2 | compilé avec PHP |
| OpenSSL | 3.3.1 | `build_prereqs_only.sh` |
| NDK | r26d | `aarch64-linux-android21-clang` |

---

## Build (développeurs)

### Prérequis système (Linux Mint 22 / Ubuntu)

```bash
sudo apt update
sudo apt install -y build-essential cmake ninja-build pkg-config \
  autoconf automake libtool wget curl git bison re2c \
  libssl-dev libxml2-dev zlib1g-dev libncurses-dev \
  libpcre2-dev libonig-dev libcurl4-openssl-dev
```

### Flutter

```bash
sudo snap install flutter --classic
flutter doctor
```

### Compiler les binaires natifs ARM64

```bash
cd mini_web_server_v3/scripts

# 1. Dépendances (OpenSSL, PCRE2, APR, libxml2…) — ~20 min
bash build_prereqs_only.sh

# 2. Apache — ~10 min
bash build_apache_only.sh

# 3. PHP 8.3 — ~40 min
bash build_php_only83.sh

# 4. MariaDB (via Termux)
bash build_mariadb_ndk.sh

# 5. Assets (phpMyAdmin + configs)
bash build_assets.sh
```

> ⚠️ `build_native.sh` est archivé — ne plus utiliser (écrase PHP avec ancienne version).

### Compiler l'APK

```bash
cd mini_web_server_v3
flutter pub get
flutter build apk --release
# APK : build/app/outputs/flutter-apk/app-release.apk
```

### Installer sur Android

```bash
# ⚠️ Obligatoire en développement avant chaque réinstallation
adb shell pm clear com.serveurlocal.app

adb install build/app/outputs/flutter-apk/app-release.apk
```

### Android SDK (si absent)

```bash
mkdir -p ~/android-sdk/cmdline-tools
cd ~/android-sdk/cmdline-tools
wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
unzip commandlinetools-linux-*.zip && mv cmdline-tools latest

echo 'export ANDROID_HOME=$HOME/android-sdk' >> ~/.bashrc
echo 'export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools' >> ~/.bashrc
source ~/.bashrc

sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"
sdkmanager --licenses
flutter config --android-sdk $HOME/android-sdk
```

---

## Console Termux

La page **Console** fonctionne avec ou sans Termux :

| Mode | Comportement |
|------|-------------|
| Sans Termux | Affichage en lecture seule · bouton Ouvrir Termux |
| Avec Termux | Terminal complet · commandes rapides préconfigurées |

**Activer Termux :**
1. Installer [Termux depuis F-Droid](https://f-droid.org/packages/com.termux/) (⚠️ pas depuis Play Store)
2. Dans Termux : `Paramètres → Autoriser l'exécution de commandes externes`

---

## Réactiver AdMob (après publication store)

**`lib/main.dart`** — décommenter :
```dart
await MobileAds.instance.initialize();
```

**`lib/pages/dashboard_page.dart`** — remplacer les blocs Start.io par les blocs AdMob commentés.

**`android/app/src/main/AndroidManifest.xml`** — remplacer les IDs de test :
```xml
<meta-data android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-XXXXXXXXXXXXXXXX~NNNNNNNNNN"/>
```

---

## Contacts & Support

| | |
|---|---|
| **Organisation** | Taysir Digital Group (TDG) |
| **PDG / CEO** | Aliou Mbengue |
| **Téléphone** | +221 76 455 03 58 |
| **Email** | taysirdigitalgroup@gmail.com |
| **Site web** | [taysirdigitalgroup.github.io](https://taysirdigitalgroup.github.io) |
| **Devise** | *« Vos rêves, nos défis »* |

**Soutenir le projet :**
- 💳 PayPal : [paypal.me/MBENGUE28](https://paypal.me/MBENGUE28)
- 🌊 Wave : [pay.wave.com · Taysir Digital Group](https://pay.wave.com/m/M_sn_DoZfd98ruV_6/c/sn/) · `+221 76 455 03 58`
- 🟠 Orange Money : `+221 77 664 70 80`

---

## Licence

© 2025 Taysir Digital Group (TDG) — Tous droits réservés.  
Mini Web Server est un logiciel propriétaire. Toute reproduction ou distribution sans autorisation est interdite.
