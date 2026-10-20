# WordMaster V2 API (JSON statique pour FlutterFlow)

Ce dépôt contient les données de départ pour WordMaster : 30 mots anglais, 30 allemands et 30 japonais.

## Fichiers
- `categories.json` : les huit catégories de l'application.
- `data/en.json`, `data/de.json`, `data/ja.json` : 30 mots par langue.
- `audio/en/`, `audio/de/`, `audio/ja/` : emplacements pour les fichiers MP3 de prononciation.
- `images/` : emplacement facultatif pour les images.

## Champs de chaque mot
`id`, `word`, `translation`, `definition`, `example`, `level`, `category`, `language`, `reading`, `imageUrl`, `audioUrl`.

`reading` est utilisé pour la lecture/romanisation du japonais. Les champs `imageUrl` sont vides tant que les images ne sont pas ajoutées. Les champs `audioUrl` pointent vers les chemins MP3 attendus dans ce dépôt, mais les MP3 ne sont pas fournis : ajoute les fichiers audio correspondants avant de publier l'application.

## Important sur les sons
Un champ `audioUrl` ne crée pas le son à lui seul. Pour que le bouton audio fonctionne, il faut placer un MP3 réel à chaque chemin référencé, par exemple `audio/en/en_001.mp3`. Tu peux créer les fichiers avec un service Text-to-Speech (TTS) en choisissant une voix anglaise, allemande ou japonaise. Vérifie la licence et les conditions du service choisi. Utilise une voix japonaise pour les mots japonais. Après ajout des fichiers, teste chaque URL brute GitHub dans le navigateur.

## Publier le dépôt
1. Crée un dépôt public `wordmaster-v2-api` sous le compte GitHub `ranimaziza`.
2. Téléverse tous les fichiers de cette archive à la racine du dépôt, sans mettre tout le dossier dans un sous-dossier supplémentaire.
3. Va dans `Settings > Pages`, choisis la branche `main` et le dossier `/ (root)`, puis enregistre.
4. Teste :
   - `https://ranimaziza.github.io/wordmaster-v2-api/categories.json`
   - `https://ranimaziza.github.io/wordmaster-v2-api/data/en.json`
   - `https://ranimaziza.github.io/wordmaster-v2-api/data/de.json`
   - `https://ranimaziza.github.io/wordmaster-v2-api/data/ja.json`

Les URLs `raw.githubusercontent.com` inscrites dans `audioUrl` sont les chemins attendus pour les fichiers MP3 après leur ajout. Pour les API Calls FlutterFlow, préfère les URLs GitHub Pages ci-dessus pour les JSON.

## FlutterFlow - connexion JSON
1. Ouvre `API Calls` > `+ Add API Call`.
2. Nom : `GetEnglishWords`; méthode `GET`; URL `https://ranimaziza.github.io/wordmaster-v2-api/data/en.json`.
3. Clique `Test API Call`. Configure la réponse comme une liste JSON (JSONPath racine `$`).
4. Répète pour allemand (`GetGermanWords`) et japonais (`GetJapaneseWords`) avec les chemins correspondants.
5. Pour l'affichage, connecte le résultat à une `ListView` dynamique et utilise les champs de chaque élément.
6. Pour les catégories et les niveaux, filtre la liste côté FlutterFlow au départ. Si la liste grandit, passe à une vraie API avec endpoints de filtrage.
7. Ajoute un lecteur audio à l'interface et fais-lui lire `audioUrl` (par exemple avec l'action audio/Play Sound disponible dans ton projet FlutterFlow). Le MP3 doit être accessible en HTTPS.

## Remarques
- Ce projet est une base de départ, pas un dictionnaire complet validé professionnellement.
- Les champs `imageUrl` sont vides : ajoute des URLs d'images accessibles et autorisées.
- Les niveaux CECRL sont des indications pédagogiques initiales, à réviser.
- Les traductions japonaises en français peuvent avoir plusieurs équivalents selon le contexte.
