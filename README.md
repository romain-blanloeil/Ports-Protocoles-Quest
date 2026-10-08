# Ports & Protocoles — Quest

Quiz web pour réviser les **ports et protocoles réseau** vus en formation TSSR (Technicien Supérieur Systèmes et Réseaux) à l'ENI École Informatique, Nantes.

🔗 **Démo en ligne** : https://ports-protocoles-quest.blanloeil.com

## Fonctionnalités

- **4 modes de questions** (QCM à 4 choix) :
  - Port ➜ Protocole
  - Protocole ➜ Port
  - Définition ➜ Protocole
  - Mélangé
- **2 niveaux** :
  - **Rookie** : les 30 ports essentiels à connaître par cœur
  - **Expert** : la liste complète (67 lignes)
- **Nombre de questions au choix** (5, 10, 20 ou toutes) et **filtre par catégorie** (Network, Secure Remote, Identity, Transfert, Web & Database, Share & Storage, Monitoring, Messagerie)
- **Plusieurs bonnes réponses gérées** : le port 22 est partagé par SSH, SFTP et SCP, et le quiz n'en propose jamais deux comme bonnes réponses à la fois
- Explication affichée après chaque réponse : port, transport (TCP/UDP) et définition
- Fiche récapitulative consultable depuis le menu

## Structure du projet

| Fichier | Rôle |
|---|---|
| `index.html` | Page et logique du quiz (JavaScript sans framework) |
| `style.css` | Mise en forme |
| `ports_protocoles.csv` | Données : une ligne par couple port / protocole |

Aucune dépendance, aucune étape de build : c'est un site statique.

## Modifier les données

Les données sont dans `ports_protocoles.csv` (séparateur `;`, encodage UTF-8) :

```
Port;Transport;Service;Description;Categorie;Exemple;Note;Niveau
22;TCP;SSH;Accès distant sécurisé en ligne de commande, tunnel chiffré;Secure Remote;;;Rookie
```

- `Port` : numéro, ou `Aucun` pour les protocoles sans port (ICMP, ARP, FCoE)
- `Transport` : `TCP`, `UDP` ou `TCP/UDP`
- `Exemple` : commande d'exemple (facultatif, utile pour les protocoles sans port)
- `Note` : par exemple `Usage courant` pour un port qui n'est pas une attribution officielle
- `Niveau` : `Rookie` ou `Expert` (le niveau Expert inclut toutes les lignes)

Pour corriger ou ajouter un port, il suffit de modifier le CSV : le quiz se met à jour sans toucher au code.

## Lancer en local

Le CSV est chargé avec `fetch()`, ce qui est bloqué quand on ouvre `index.html` directement dans le navigateur. Il faut passer par un petit serveur :

```bash
python -m http.server 8000
```

Puis ouvrir http://localhost:8000.

## Déploiement

Hébergé sur **Vercel** : chaque `git push` sur la branche principale redéploie le site automatiquement. Le site est servi sur un sous-domaine personnalisé (enregistrement DNS CNAME) en HTTPS.

## Sources et limites

Les ports et protocoles proviennent du cours et de la fiche « 27 ports essentiels » de la formation. Certains ports sont des **usages courants** plutôt que des attributions officielles (indiqués dans le quiz). En cas de doute, le registre de l'IANA fait foi.

## Auteur

Romain Blanloeil — [romain.blanloeil.com](https://romain.blanloeil.com) · [GitHub](https://github.com/romain-blanloeil)
