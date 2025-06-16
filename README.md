# TP-Serveur-TCP-IP-simple
Axel Pedrero / Simon Lours

## 2.1 Cohérence concurrente et synchronisation

**— Quels types de problèmes de concurrence peuvent apparaître dans ce système multi-clients ?**  
Deux clients modifient un même canal en même temps. Résultat possible : perte de données, état incohérent.

**— Que peut-il arriver si deux clients rejoignent ou quittent un canal en même temps ?**  
Si les deux rejoignent : un des deux peut ne pas être ajouté correctement.  
S’ils quittent : possible que le dernier utilisateur reste enregistré ou que le canal ne soit pas mis à jour.

**— Votre système est-il vulnérable aux incohérences d’état ou aux conditions de course ? Comment s’en prémunir ?**  
Oui, sans verrou ça serait dangereux. Mais y’a un `threading.Lock`, donc les accès concurrents sont protégés si c’est bien utilisé.

---

## 2.2 Modularité et séparation des responsabilités

**— Quelles sont les grandes responsabilités fonctionnelles de votre application serveur (gestion client, traitement commande, envoi message, logs, persistance…) ?**  
Oui, tout ça : gestion des clients, des pseudos, des canaux, des messages, des logs, et sauvegarde JSON.

**— Peut-on tracer une frontière claire entre logique métier et logique d’entrée/sortie réseau ?**  
Non. Tout est mélangé dans les méthodes du handler. Commandes, accès à l’état, logs, tout dans les mêmes fonctions.

**— En cas d’erreur dans une commande, quelle couche doit réagir ?**  
C’est le handler qui réagit direct. Soit il écrit un message d’erreur, soit il ignore. Y’a pas de couche dédiée pour ça.


