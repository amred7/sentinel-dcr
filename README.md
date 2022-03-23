Documentation pour le nouveau data collector utilisant les Data collection Rule : https://docs.microsoft.com/en-us/azure/azure-monitor/logs/custom-logs-overview

# tutorial 
https://docs.microsoft.com/en-us/azure/azure-monitor/logs/tutorial-custom-logs

## description des etapes a haut niveau 
ce scenario se base sur le tutorial cite plus haut

    1 Il faut creer une app registrations avec son client secrets
    2 Creer un data collection endpoint dans azure monitor, il doit etre dans le meme region que le LAW
    3 lancer le script qui generera un fichier json conforme a partir de votre fichier source de journaux. la commande est : .\LogGenerator.ps1 -Log "sample_access.log" -Type "file" -Output "data_sample.json"
    4 cree une custome log table (DCR-Based) avec son Data Collection Rule et l associe au data collection endpoint creer precedement
    5 creer la structure de la table. soit automatiquement en important un jeu de donnee ou manuellement en definissant tout les champs
    6 eventuellement completer la definition afin de faire de la transformation tel que l affection de la valeur timegernerat a partir d un champs present dans le jeu de donnee
    8 Assigner des permissions au DCR afin que app registration puisse utiliser le role Microsoft.Insights/Telemetry/Write
    9 envoyer les donnees en roulant le script avec la commande suivante : .\LogGenerator.ps1 -Log "sample_access.log" -Type "API" -Table "ApacheAccess_CL" -DcrImmutableId <immutable ID> -DceUri <data collection endpoint URL>

## authentification flow 
https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow


## script 
.\LogGenerator.ps1 -Log "sample_access.log" -Type "file" -Output "data_sample.json"