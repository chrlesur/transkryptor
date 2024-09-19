# Transkryptor

## Table des matières
- [Transkryptor](#transkryptor)
  - [Table des matières](#table-des-matières)
  - [Introduction](#introduction)
  - [Fonctionnalités](#fonctionnalités)
  - [Architecture technique](#architecture-technique)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [APIs externes](#apis-externes)
    - [Architecture des fichiers](#architecture-des-fichiers)
  - [Installation](#installation)
  - [Configuration](#configuration)
    - [Clés API](#clés-api)
    - [Configuration du serveur](#configuration-du-serveur)
  - [Utilisation](#utilisation)
  - [API](#api)
    - [GET /](#get-)
    - [POST /test-keys](#post-test-keys)
    - [POST /analyze](#post-analyze)
  - [Gestion des erreurs et journalisation](#gestion-des-erreurs-et-journalisation)
  - [Considérations de sécurité](#considérations-de-sécurité)
  - [Performances et optimisation](#performances-et-optimisation)
  - [Dépannage](#dépannage)
  - [Contributions](#contributions)
  - [Feuille de route](#feuille-de-route)

## Introduction

Transkryptor est une application web sophistiquée conçue pour faciliter la transcription de fichiers audio, l'analyse des transcriptions, et la génération de synthèses. En tirant parti des capacités avancées des API OpenAI et Anthropic, Transkryptor offre une solution complète pour le traitement et l'analyse de contenu audio.

## Fonctionnalités

- **Transcription audio**: 
  - Support des fichiers au format M4A
  - Transcription automatique utilisant des modèles de reconnaissance vocale avancés

- **Analyse de transcription**: 
  - Analyse approfondie du contenu transcrit
  - Extraction de concepts clés, de sentiments, et d'autres informations pertinentes

- **Génération de synthèse**: 
  - Création de résumés concis et informatifs basés sur l'analyse

- **Validation des clés API**: 
  - Test des clés API OpenAI et Anthropic pour assurer leur validité

- **Suivi de progression**: 
  - Affichage en temps réel de la progression globale et par lot des opérations

- **Options de téléchargement**: 
  - Possibilité de télécharger les transcriptions, analyses, et synthèses au format texte

## Architecture technique

### Frontend
- HTML5 pour la structure
- CSS3 pour le style (framework CSS non spécifié dans le code fourni)
- JavaScript vanilla pour l'interactivité côté client

### Backend
- Node.js comme environnement d'exécution
- Express.js comme framework web
- Modules npm supplémentaires :
  - `cors` pour la gestion des requêtes cross-origin
  - `axios` pour les requêtes HTTP
  - `gpt-3-encoder` pour le comptage des tokens
  - `path` pour la gestion des chemins de fichiers

### APIs externes
- OpenAI API pour la transcription (non implémentée dans le code fourni, mais mentionnée dans l'interface)
- Anthropic API (modèle Claude 3.5 Sonnet) pour l'analyse et la synthèse

### Architecture des fichiers
- `server.js`: Serveur backend Express
- `public/index.html`: Interface utilisateur frontend
- `public/`: Dossier contenant tous les fichiers statiques (CSS, JS, etc.)

## Installation

1. Clonez le dépôt :
   ```
   git clone https://github.com/chrlesur/transkryptor.git
   cd transkryptor
   ```

2. Installez les dépendances :
   ```
   npm install
   ```

3. Configurez les variables d'environnement (optionnel) :
   ```
   export PORT=3000
   ```

Note : Le port par défaut est 3000, mais vous pouvez le changer en définissant la variable d'environnement PORT.

4. Assurez-vous que votre structure de fichiers est correcte :
   ```
   transkryptor/
   │
   ├── public/
   │   ├── index.html
   │   ├── styles.css (si vous en avez un)
   │   └── script.js (si vous en avez un)
   │
   ├── server.js
   ├── package.json
   └── ... (autres fichiers et dossiers)
   ```

5. Lancez le serveur :
   ```
   node server.js
   ```

6. Ouvrez votre navigateur et accédez à `http://localhost:3000` (ou le port que vous avez configuré)

## Configuration

### Clés API
1. Obtenez une clé API OpenAI sur [https://platform.openai.com](https://platform.openai.com)
2. Obtenez une clé API Anthropic sur [https://www.anthropic.com](https://www.anthropic.com)
3. Entrez ces clés dans l'interface utilisateur de Transkryptor

### Configuration du serveur
Le serveur utilise les variables d'environnement suivantes :
- `PORT`: Le port sur lequel le serveur écoute (par défaut : 3000)

## Utilisation

1. Ouvrez votre navigateur et accédez à `http://localhost:3000` (ou l'ip et le port que vous avez configuré)
2. **Configuration des clés API**
   - Entrez vos clés API OpenAI et Anthropic dans les champs correspondants
   - Cliquez sur "Tester les clés API" pour valider vos clés

3. **Transcription**
   - Cliquez sur "Fichier audio (M4A)" pour sélectionner un fichier audio
   - Appuyez sur "Transcrire" pour lancer la transcription
   - Suivez la progression dans les barres de progression

4. **Analyse**
   - Une fois la transcription terminée, cliquez sur "Analyser la transcription"
   - L'analyse apparaîtra dans la section "Analyse"

5. **Synthèse**
   - Après l'analyse, cliquez sur "Synthétiser l'analyse"
   - La synthèse sera affichée dans la section "Synthèse"

6. **Téléchargement**
   - Utilisez les boutons "Télécharger" pour sauvegarder la transcription, l'analyse ou la synthèse

## API

### GET /
Sert la page d'accueil de l'application (index.html).

### POST /test-keys
Teste la validité des clés API fournies.

**Payload**:
```json
{
  "openaiKey": "votre-clé-openai",
  "anthropicKey": "votre-clé-anthropic"
}
```

**Réponse réussie**:
```json
{
  "status": "OK",
  "message": "Les deux clés API sont valides"
}
```

### POST /analyze
Envoie une requête d'analyse à l'API Anthropic.

**Payload**:
```json
{
  "prompt": "Votre texte à analyser",
  "apiKey": "votre-clé-anthropic"
}
```

**Réponse réussie**:
```json
{
  "content": [
    {
      "text": "Réponse de l'analyse"
    }
  ],
  "tokenCount": 123,
  "responseTokenCount": 456
}
```

## Gestion des erreurs et journalisation

Le serveur utilise un système de journalisation personnalisé qui enregistre les événements importants et les erreurs dans la console. Chaque entrée de journal inclut un horodatage précis.

Exemple de journal :
```
[2024-09-15 14:30:25] Test des clés API en cours...
[2024-09-15 14:30:26] Test de la clé OpenAI réussi
[2024-09-15 14:30:27] Test de la clé Anthropic réussi
[2024-09-15 14:30:27] Test des clés API terminé avec succès
```

En cas d'erreur, le serveur renvoie des réponses JSON détaillées, incluant un message d'erreur et, si disponible, des détails supplémentaires.

## Considérations de sécurité

- Les clés API sont actuellement gérées côté client et envoyées avec chaque requête. Dans un environnement de production, il est recommandé de mettre en place un système d'authentification utilisateur et de stocker les clés API de manière sécurisée côté serveur.
- L'application utilise CORS (Cross-Origin Resource Sharing). Assurez-vous de configurer correctement les paramètres CORS pour votre environnement de production afin de limiter les requêtes aux origines autorisées.
- Implémentez des mécanismes de rate limiting pour prévenir les abus d'API.

## Performances et optimisation

- L'application utilise `gpt-3-encoder` pour compter les tokens, ce qui permet d'optimiser l'utilisation des API en évitant les dépassements de limites.
- Le traitement par lots (visible dans la barre de progression par lot) permet de gérer efficacement les fichiers volumineux.

## Dépannage

- Si l'application ne se charge pas dans le navigateur, assurez-vous que le serveur est en cours d'exécution et que vous accédez à la bonne adresse (http://localhost:3000 par défaut).
- Vérifiez que tous les fichiers statiques (HTML, CSS, JS) sont correctement placés dans le dossier `public/`.
- Si les clés API échouent au test, vérifiez qu'elles sont correctement copiées et qu'elles n'ont pas expiré.
- En cas d'erreur lors de la transcription ou de l'analyse, consultez les journaux du serveur pour plus de détails.
- Si le serveur ne démarre pas, assurez-vous qu'aucune autre application n'utilise le port spécifié.
- Si vous changez le port via la variable d'environnement PORT, assurez-vous de redémarrer le serveur pour que les changements prennent effet.
- Vérifiez que le port affiché dans la console du serveur correspond à celui que vous utilisez pour accéder à l'application dans votre navigateur.

## Contributions

Les contributions à Transkryptor sont les bienvenues. Voici comment vous pouvez contribuer :

1. Forkez le projet
2. Créez votre branche de fonctionnalité (`git checkout -b feature/AmazingFeature`)
3. Committez vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Poussez vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## Feuille de route

Fonctionnalités futures envisagées :

- Support de formats audio supplémentaires (WAV, MP3, etc.)
- Interface utilisateur améliorée avec un framework moderne (React, Vue.js)
- Système d'authentification utilisateur
- Stockage des transcriptions et analyses dans une base de données
- Fonctionnalités d'édition de transcription
- Support multilingue pour la transcription et l'analyse
- Optimisation des performances pour le traitement de fichiers volumineux