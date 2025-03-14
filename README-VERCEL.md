# Déploiement sur Vercel

Ce guide explique comment déployer l'application Joe's Robot Shop sur Vercel.

## Prérequis

1. Un compte [Vercel](https://vercel.com)
2. [Git](https://git-scm.com/) installé sur votre machine
3. [Node.js](https://nodejs.org/) version LTS recommandée

## Configuration du projet

### 1. Préparation du frontend (Angular)

1. Modifiez le fichier `src/environments/environment.prod.ts` pour pointer vers votre API :
```typescript
export const environment = {
  production: true,
  apiUrl: 'VOTRE_URL_API' // L'URL de votre API déployée
};
```

2. Créez un fichier `vercel.json` à la racine du projet :
```json
{
  "version": 2,
  "builds": [
    {
      "src": "package.json",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "dist/joes-robot-shop"
      }
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/index.html"
    }
  ]
}
```

### 2. Déploiement du backend (API)

1. Dans le dossier `api-server`, créez un fichier `vercel.json` :
```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/index.js"
    }
  ]
}
```

## Étapes de déploiement

### Déployer l'API

1. Créez un nouveau projet sur Vercel
2. Connectez votre dépôt Git
3. Pour le dossier `api-server` :
   ```bash
   cd api-server
   vercel
   ```
4. Notez l'URL de l'API déployée

### Déployer le frontend

1. Mettez à jour l'URL de l'API dans `environment.prod.ts`
2. À la racine du projet :
   ```bash
   vercel
   ```

## Variables d'environnement

Dans les paramètres du projet Vercel, configurez les variables d'environnement nécessaires :

- `NODE_ENV`: `production`
- `PORT`: `8081` (pour l'API)

## Vérification du déploiement

1. Accédez à votre URL Vercel du frontend
2. Vérifiez que l'application se charge correctement
3. Testez les fonctionnalités qui utilisent l'API

## Dépannage

- Si vous rencontrez des erreurs CORS, vérifiez la configuration CORS dans `api-server/index.js`
- Pour les problèmes de build, consultez les logs dans le dashboard Vercel
- Pour les problèmes d'API, vérifiez les variables d'environnement dans le dashboard Vercel

## Support

Pour plus d'aide :
- [Documentation Vercel](https://vercel.com/docs)
- [Documentation Angular](https://angular.io/guide/deployment) 