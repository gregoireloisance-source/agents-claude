---
description: Brief, brainstorming des questions, cadrage, recherche d'experts, revue puis export Excel et Word
---

Tu m'aides à préparer une série d'expert calls pour une phase de due diligence. Procède dans l'ordre, sans sauter d'étape.

## Temps 1 : Formulaire

N'effectue aucune recherche à ce stade. Affiche exactement le formulaire ci-dessous, pré-rempli avec ce que j'ai déjà écrit après la commande : $ARGUMENTS. Demande-moi de le compléter en une seule réponse. Les champs marqués (optionnel) peuvent rester vides.

FORMULAIRE
1. Nom de la société cible :
2. Site web :
3. Questions principales (important) : les 3 à 8 questions auxquelles je veux répondre grâce à ces expert calls (ex. : le client est-il satisfait et renouvelle-t-il ? le prix est-il défendable face aux concurrents ? quelle est la menace principale ?)
4. Marchés et segments (optionnel) : secteurs, produits, types de clients, pays
5. Concurrents connus (optionnel) :
6. Partenaires connus (optionnel) : intégrateurs, éditeurs, distributeurs
7. Contexte supplémentaire (optionnel) : teaser, présentation, infos publiques partageables, et/ou un guide d'entretien d'un projet précédent à prendre comme modèle de style (colle le texte)
8. Géographie : France et Europe par défaut
9. Nombre de contacts visés : 30 par défaut, entre 10 et 40

Rappelle-moi de ne saisir aucune information confidentielle et de ne pas viser de salariés actuels de la cible. Si je n'ai pas renseigné au moins deux questions principales, demande-les avant de continuer.

## Temps 2 : Brainstorming des questions

Toujours sans recherche web. À partir de mes questions :
1. Reformule-les de façon précise et testable auprès d'un expert, et signale en une ligne celles qui sont vagues, trop larges, orientées ou impossibles à trancher par un expert.
2. Challenge-moi : indique les angles importants que mes questions ne couvrent pas. Propose au maximum 3 à 5 questions complémentaires, chacune avec une ligne expliquant pourquoi elle compte. N'en ajoute pas pour le plaisir : seulement celles qui changeraient réellement ma vision de l'investissement.
3. Demande-moi lesquelles garder, modifier ou écarter.

Sois concis et constructif. Un seul aller-retour, sauf si je veux continuer à discuter. Termine par la liste finale numérotée de 5 à 8 questions retenues.

## Temps 3 : Cadrage

Écris un résumé court : la cible, le périmètre, la liste finale des questions, les catégories d'experts que tu comptes viser, la grille de notation proposée (3 à 6 critères notés de 1 à 5, tirés des facteurs clés de succès du secteur, identiques pour tous les experts afin de pouvoir comparer leurs notes) et les informations manquantes. Si la société ou le site manque, redemande-les. Termine par « Valides-tu ce cadrage et cette grille de notation ? » et attends mon accord explicite avant de lancer quoi que ce soit.

## Temps 4 : Lancement d'un lot

Seulement après ma validation, lance l'agent expert-calls-prep (dans un plugin, il peut apparaître sous le nom expert-calls:expert-calls-prep) pour un lot de 10 contacts maximum. Transmets-lui le brief complet : cible, site, marchés, concurrents, partenaires, contexte, géographie, nombre total visé, la liste finale des questions validées (numérotées), la grille de notation validée, le guide d'entretien modèle si je t'en ai fourni un, la liste des personnes et entreprises déjà proposées à exclure (vide au premier lot), et la consigne que le cadrage est déjà fait.

## Temps 5 : Restitution et revue (en texte, dans le terminal)

Présente d'abord le résultat du lot en texte, tel que l'agent l'a produit : tableaux des experts, messages d'approche, guides de 45 minutes, pistes. Ne génère aucun fichier à ce stade.

Termine par un court point à trois volets, que je peux traiter en une seule réponse :
1. Ce lot me convient-il ? J'ai des commentaires à intégrer (questions, profils, ton des messages, contenu des guides) ?
2. Veux-tu un lot supplémentaire ? Indique combien de contacts nous avons et combien il en reste pour atteindre l'objectif (40 maximum).
3. Veux-tu exporter en Excel (classeur complet) et/ou en Word (guides d'entretien) ?

Intègre mes commentaires avant tout export : modifie toi-même les messages et guides si c'est mineur, relance l'agent si je demande de nouveaux profils. Pour un lot supplémentaire, relance l'agent en lui transmettant les personnes et entreprises déjà proposées (à exclure), la grille de notation validée et les questions les moins couvertes en priorité.

## Temps 6 : Export, uniquement si je le demande

N'exporte que les formats que j'ai demandés. À chaque export, utilise tous les lots validés jusqu'ici.

1. Dossier de sortie : ~/Documents/expert-calls-output/ (crée-le s'il n'existe pas). N'écris jamais de résultat dans le dépôt agents-claude ni dans le dossier courant s'il s'agit d'un dépôt git.
2. Nom des fichiers : [société en minuscules sans espaces]_expert-calls_[AAAA-MM-JJ], avec les extensions .json, .xlsx et .docx.
3. Compile un fichier JSON avec le schéma ci-dessous. Reprends uniquement ce qui a été produit et validé dans la conversation : n'invente rien, laisse vide (chaîne vide ou liste vide) ce qui manque.

{
  "target": "", "website": "", "date": "JJ/MM/AAAA", "geography": "", "scope": "", "competitors": "", "partners": "",
  "questions": [{"id": 1, "question": "", "why": "", "expert_types": "", "experts": "A1, A2", "coverage": "Bonne | Partielle | Insuffisante", "gap": ""}],
  "experts_a": [{
    "id": "A1", "name": "", "role": "", "company": "", "category": "", "relevance": "", "questions": "1, 3",
    "priority": "Haute | Moyenne | Basse", "confidence": "Haute | Moyenne | Faible",
    "sources": [{"url": "", "note": "ce que la source établit"}],
    "message": {"language": "FR | EN", "subject": "", "body": ""},
    "guide": [{"block": "", "question": "", "followups": "", "serves": "1, 2"}]
  }],
  "leads_b": [{"id": "B1", "profile_type": "", "company": "", "function": "", "reason": "", "questions": "", "keywords": "", "sources": [{"url": "", "note": ""}]}],
  "templates_b": [{"profile_type": "", "language": "FR | EN", "subject": "", "message": "", "guide": [{"block": "", "question": "", "followups": "", "serves": ""}]}],
  "market_sources": [{"url": "", "note": ""}]
}

Pour les guides, reprends fidèlement les blocs et les questions produits par l'agent. Libellés de bloc : « Introduction (0-5 min) », « Bloc 1 : [thème] (5-13 min) » et les blocs suivants avec leurs horaires, « Notation et synthèse (35-42 min) », « Clôture (42-45 min) », et « À faire préciser » pour les chiffres et exemples à obtenir. Conserve au début du texte de chaque question le préfixe « ★ » (prioritaire) ou « ○ » (si le temps le permet), ainsi que « [Note 1-5] » pour les questions de notation. La couverture de chaque question d'investissement (Bonne, Partielle ou Insuffisante) est ton évaluation d'après les experts identifiés, avec les profils complémentaires à chercher dans « gap ».

4. Génère les fichiers demandés. Les scripts se trouvent dans le dossier scripts de ce plugin : ${CLAUDE_PLUGIN_ROOT}/scripts/. Si cette variable n'est pas disponible, cherche build_excel.py avec la commande find dans ~/.claude/plugins. Utilise ~/.venvs/expert-calls/bin/python si ce dossier existe, sinon python3.
   - Excel : python build_excel.py [fichier.json] [fichier.xlsx]
   - Word : python build_word.py [fichier.json] [fichier.docx]
   Si build_word.py n'existe pas, dis-moi que l'export Word n'est pas encore disponible et propose l'Excel seul. Si une bibliothèque manque (openpyxl, python-docx), dis-le-moi au lieu de l'installer toi-même.
5. Indique les chemins des fichiers créés, puis rappelle : brouillons à relire avant tout envoi, validation compliance, et conservation des fichiers (qui contiennent des noms de personnes) sur un espace autorisé par ma banque.

À la fin, si des questions restent mal couvertes, propose les profils complémentaires à chercher dans un lot supplémentaire.