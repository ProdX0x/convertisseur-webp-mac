# POUR MAC CONVERTISSEUR IMAGE PNG-JPEG --> 👉 WEBP 
Un script simple pour convertir des images (Midjourney ou autres) PNG/JPEG en WebP sur Mac

---

```markdown
# 🧠 Convertisseur WebP pour Mac — Simple et pédagogique

Ce projet t'apprend à créer **un petit script sur ton Mac** pour **convertir des images PNG ou JPEG en WebP** (un format plus léger pour le web et les apps mobiles).

---

## 🎯 Objectif

- 📂 Tu places des images `.png`, `.jpg`, ou `.jpeg` dans un dossier `originals`
- 🧠 Tu exécutes un script très simple
- 🖼️ Les images converties `.webp` apparaissent dans un dossier `webp`

---

## 👶 Pour qui ?

Ce projet est fait pour :

- Un enfant curieux 🧒
- Une personne qui débute avec le Mac ou le Terminal 💡
- Quelqu’un qui aime automatiser des tâches simples et utiles ⚙️

---

## 📦 Ce qu’il te faut

- ✅ Un **Mac**
- ✅ L’application **Terminal** (déjà installée sur ton Mac)
- ✅ Une **connexion Internet** pour la 1re installation

---

## 📁 Étape 1 — Préparer les dossiers

1. Ouvre le **Finder**
2. Va dans le dossier **Téléchargements**
3. Crée un dossier appelé **ImagesMidjourney**
4. Dans ce dossier, crée 2 sous-dossiers :

---

ImagesMidjourney/
├── originals   ← Tu mets ici tes images PNG ou JPG
└── webp        ← Les images converties apparaîtront ici

---

---

## 🛠️ Étape 2 — Installer l'outil de conversion

Dans le Terminal, tape :

```
brew install webp
```

🔍 Cela installe l’outil `cwebp` (fourni par Google) qui permet de convertir les images.  
Tu ne fais cette étape **qu’une seule fois**.

---

## 🧠 Étape 3 — Savoir si tu es en `zsh` ou `bash`

Tape cette commande dans le Terminal :

```
echo \$SHELL
```

Tu verras l’un des deux :

- `/bin/zsh` → tu es en **ZSH** ✅ *(par défaut depuis macOS Catalina)*
- `/bin/bash` → tu es en **BASH**

---

## 📜 Étape 4 — Créer le script de conversion

Dans tous les cas, commence par taper :

```
nano \~/Downloads/ImagesMidjourney/convert\_images.sh
````

Puis colle **le bon script selon ton cas** 👇

---

### ✅ Si tu es en ZSH (Terminal moderne – macOS récent – macOS Catalina et versions récentes)

```
#!/bin/zsh

setopt null_glob

ORIGINALS_DIR="$HOME/Downloads/ImagesMidjourney/originals"
WEBP_DIR="$HOME/Downloads/ImagesMidjourney/webp"

mkdir -p "$WEBP_DIR"

echo "🧹 Nettoyage..."
find "$WEBP_DIR" -name '*.webp' -delete

echo "🌀 Conversion PNG/JPG vers WebP..."
count=0

for img in "$ORIGINALS_DIR"/*.{png,jpg,jpeg}; do
  [ -e "$img" ] || continue
  base=$(basename "$img")
  base="${base%.*}.webp"
  /opt/homebrew/bin/cwebp -quiet "$img" -o "$WEBP_DIR/$base"
  echo "✅ $(basename "$img") → $base"
  ((count++))
done

echo "🎉 $count image(s) convertie(s) avec succès."
open "$WEBP_DIR"
````

---

### ✅ Si tu es en BASH (anciens macOS ou Terminal modifié)

```
#!/bin/bash

ORIGINALS_DIR="$HOME/Downloads/ImagesMidjourney/originals"
WEBP_DIR="$HOME/Downloads/ImagesMidjourney/webp"

mkdir -p "$WEBP_DIR"

echo "🧹 Nettoyage..."
find "$WEBP_DIR" -name '*.webp' -delete

echo "🌀 Conversion PNG/JPG vers WebP..."
count=0

for img in "$ORIGINALS_DIR"/*.{png,jpg,jpeg}; do
  [ -e "$img" ] || continue
  base=$(basename "$img")
  base="${base%.*}.webp"
  cwebp -quiet "$img" -o "$WEBP_DIR/$base"
  echo "✅ $(basename "$img") → $base"
  ((count++))
done

echo "🎉 $count image(s) convertie(s) avec succès."
open "$WEBP_DIR"
```

---

### 💾 Pour enregistrer et quitter :

* `CTRL + O` → puis `Entrée` pour sauvegarder
* `CTRL + X` → pour quitter l’éditeur

---

## 🔓 Étape 5 — Rendre le script exécutable

Tape ceci dans le Terminal :

```
chmod +x ~/Downloads/ImagesMidjourney/convert_images.sh
```

---

## 🚀 Étape 6 — Utiliser le script

1. Glisse des images `.png`, `.jpg`, ou `.jpeg` dans le dossier `originals`
2. Lance le script avec :

```
~/Downloads/ImagesMidjourney/convert_images.sh
```

✅ Les images `.webp` apparaîtront dans le dossier `webp`

---

## ✅ Résultat attendu

* Tes images originales restent dans `originals`
* Les images converties `.webp` vont dans `webp`
* Elles prennent **moins de place**, avec une qualité toujours bonne
* Tu peux lancer le script **quand tu veux**

---

## 🌟 Bonus

Tu peux aller plus loin :

* Créer un **raccourci Automator** pour lancer le script en un clic
* L’intégrer dans une app Mac avec **Swift / SwiftUI**
* Ou même dans une app iPhone si tu apprends à coder

---

## 👋 Auteur

Amusez-vous !

---

