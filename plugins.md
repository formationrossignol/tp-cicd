
## Étapes du TP

### Connexion Jenkins ↔ Gitea
- Ajouter le dépôt Gitea et les credentials dans Jenkins
- Créer un **webhook** pour déclencher les builds à chaque push

### Création du pipeline avec Blue Ocean
- Ouvrir **Blue Ocean → Create New Pipeline**
- Sélectionner le projet Gitea et la branche à builder
- Vérifier la détection automatique du **Jenkinsfile**

### Ajout des notifications Slack
- Configurer le **Webhook Slack** dans Jenkins
- Ajouter `slackSend` dans le Jenkinsfile pour succès/échec :

```groovy
pipeline {
    agent any
    stages {
        stage('Build') { steps { echo 'Building...' } }
        stage('Test') { steps { echo 'Testing...' } }
        stage('Deploy') { steps { echo 'Deploying...' } }
    }
    post {
        success { slackSend channel: '#dev-alerts', message: 'Build OK !' }
        failure { slackSend channel: '#dev-alerts', message: 'Build échoué !' }
    }
}
```

### Exécution et vérification
- Pousser un commit dans Gitea
- Observer la pipeline dans Blue Ocean
- Vérifier la notification dans Slack
- Contrôler les logs et le résultat de chaque stage

### Résultat attendu
- Build automatique déclenché par Gitea
- Pipeline visualisée dans Blue Ocean
- Notifications instantanées dans Slack
- Tous les stages passent avec succès ou affichent clairement les erreurs

