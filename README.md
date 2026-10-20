# Expert calls : préparation de recherches d'experts en due diligence

> [!NOTE]
> **Prototype de démonstration.** Cet outil illustre une façon de structurer la préparation d'expert calls : cadrage, sourcing, guides d'entretien, suivi. Ce n'est pas un produit fini. Réalisé dans le cadre d'un processus de recrutement, pour montrer une démarche plutôt que livrer un outil de production.
>
> **Non connecté à ce stade.** L'agent travaille uniquement à partir de sources publiques et de ce que l'utilisateur saisit. Il n'a accès à aucun CRM, réseau d'experts, messagerie ou base de données financières, et n'utilise aucune donnée interne.
>
> **Ce que changerait un branchement aux outils d'une équipe d'investissement :**
> - **CRM et base de relations** (par exemple Affinity, DealCloud, Salesforce) : repérer les **introductions chaleureuses** (qui, dans l'équipe, connaît déjà l'expert ou son entreprise), éviter de recontacter une personne déjà sollicitée et reprendre l'historique des échanges.
> - **Réseaux d'experts** (par exemple GLG, AlphaSights, Third Bridge) : proposer des profils déjà qualifiés là où les sources publiques atteignent leurs limites, notamment pour les anciens clients et anciens salariés.
> - **Données de marché** (par exemple PitchBook, Capital IQ, Pappers) : enrichir les fiches et recouper les informations.
> - **Messagerie et agenda** : envoyer les messages après validation et planifier les calls.
> - **Liste de restrictions et conformité** : bloquer automatiquement les contacts interdits.
>
> Le prototype montre la logique et les garde-fous : aucune invention, sources vérifiables, validation humaine avant tout envoi.

Agent et commande pour Claude Code qui aident à préparer une série d'expert calls : cadrage des questions d'investissement, identification d'experts à partir de sources publiques, brouillons de messages d'approche, guides d'entretien de 45 minutes et export Excel.

> Les messages sont des brouillons : rien n'est envoyé automatiquement. Les sources sont publiques uniquement.

## Ce que fait l'outil

1. **Formulaire** : société cible, site, questions principales, marchés, concurrents, partenaires, géographie, nombre de contacts visés. Un guide d'entretien d'un projet précédent peut être fourni comme modèle de style.
2. **Brainstorming** : l'outil reformule les questions et propose quelques angles complémentaires, que l'utilisateur garde ou écarte.
3. **Cadrage** : résumé du périmètre et grille de notation de 1 à 5 (3 à 6 critères, identiques pour tous les experts pour pouvoir comparer), à valider avant toute recherche.
4. **Recherche par lots de 10 contacts maximum** : clients et partenaires cités publiquement, anciens salariés, consultants.
5. **Pour chaque expert** : un message d'approche et un guide de discussion de 45 minutes.
6. **Revue** : le résultat s'affiche d'abord en texte dans le terminal. L'utilisateur commente, demande un lot supplémentaire ou exporte.
7. **Export Excel** : classeur avec les onglets Synthèse, Questions, Experts A, Pistes B, Messages, Guides et Sources.

### Deux niveaux de résultats

- **Niveau A** : experts nommés, avec au moins une source publique vérifiable et un niveau de confiance (haute, moyenne, faible).
- **Niveau B** : pistes sans nom, de la forme « entreprise + fonction à rechercher », avec des liens de recherche LinkedIn et Google préremplis. Ces liens ouvrent une recherche dans le navigateur : le tri et la vérification des profils restent manuels.

### Guides d'entretien de 45 minutes

| Temps | Bloc |
|---|---|
| 0-5 min | Introduction et qualification (rôle de l'expert, exposition à la cible) |
| 5-35 min | Trois ou quatre blocs thématiques (environ 8 min chacun), choisis selon le profil : client, ancien salarié de la cible, ancien salarié d'un concurrent, partenaire, consultant |
| 35-42 min | Notation de 1 à 5 sur la grille validée et question de synthèse |
| 42-45 min | Clôture : autres contacts, documents publics, suite |

- 15 à 20 questions au maximum, dont les prioritaires sont marquées **★** et les questions à poser si le temps le permet **○**.
- Questions ouvertes, neutres, avec une seule idée chacune. L'expert cite les acteurs avant que la cible soit nommée.
- Chaque question est reliée aux questions d'investissement qu'elle sert, avec une ou deux relances.

## Contenu du dépôt

```
.claude-plugin/
  marketplace.json               Marketplace : permet l'installation via /plugin
.claude/                         Le plugin expert-calls
  .claude-plugin/plugin.json     Manifeste du plugin (nom, version, description)
  agents/expert-calls-prep.md    Agent : recherche, sourcing, messages et guides
  commands/expert-calls.md       Commande /expert-calls : formulaire, revue, export
  scripts/build_excel.py         Génération du classeur Excel
.gitignore                       Exclut les fichiers générés (xlsx, docx)
README.md
```

## Installation

Prérequis : un compte Claude, Claude Code installé (voir la documentation officielle) et Python 3 avec openpyxl :

```
python3 -m pip install --user openpyxl
```

Dans Claude Code, ajouter la marketplace puis installer le plugin :

```
/plugin marketplace add gregoireloisance-source/agents-claude
/plugin install expert-calls@agents-claude
```

Redémarrer Claude Code si la commande n'apparaît pas. L'agent et la commande sont alors disponibles dans tous les dossiers.

### Alternative : depuis un clone du dépôt

```
gh repo clone gregoireloisance-source/agents-claude
cd agents-claude
claude
```

Dans ce dossier, l'agent et la commande sont chargés automatiquement, sans installation.

## Utilisation

Dans Claude Code, lancer :

```
/expert-calls [nom de la société]
```

Suivre ensuite le formulaire. Au moment de la revue, demander l'export Excel. Les fichiers sont créés dans `~/Documents/expert-calls-output/`, hors du dépôt.

## Règles de fonctionnement

- Aucune personne, source, citation ou adresse email n'est inventée. Si un lien avec la cible n'est pas vérifiable, l'outil le dit.
- Une liste courte et fiable passe avant une longue liste douteuse : le volume vient des pistes de niveau B.
- Aucune plateforme à accès restreint n'est contournée. LinkedIn n'est pas parcouru par l'outil.
- Une page LinkedIn que l'agent n'a pas pu lire ne compte pas comme source.
- Les messages ne nomment pas la cible et ne mentionnent aucune transaction.
- Ne jamais viser de salarié actuel de la cible.

## Précautions

- Ne saisir aucune information confidentielle (nom de code, chiffres non publics, document sous NDA).
- Faire valider l'approche par la compliance avant tout contact (informations privilégiées, RGPD, politique interne).
- Conserver les fichiers générés, qui contiennent des noms de personnes, sur un espace autorisé.
- Les recherches consomment le quota du compte Claude de chaque utilisateur.

## Limites connues

- Les experts nommés et sourcés restent peu nombreux : la plupart des profils pertinents ne sont pas publics.
- L'export Word des guides n'est pas encore inclus dans le dépôt.
- Le classeur est compilé par Claude à partir du texte affiché : contrôler les sources avant usage.
- L'outil n'a pas été testé à grande échelle : les résultats sont à relire.

## Mise à jour

```
/plugin marketplace update agents-claude
```

Ou `git pull` si vous utilisez un clone du dépôt.

## Pour la relecture

Les points sur lesquels un avis est utile :

1. Les questions de la phase de brainstorming sont-elles pertinentes et bien challengées ?
2. Les guides de 45 minutes sont-ils réalistes (nombre de questions, priorités, notations) ?
3. Les sources des experts sont-elles fiables et vérifiables ?
4. L'Excel est-il exploitable tel quel par une équipe d'investissement ?