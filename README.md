# Test DISC — version française

Une application [Streamlit](https://streamlit.io) qui fait passer un test de personnalité
DISC (Dominance, Influence, Stabilité, Conformité) et restitue un profil détaillé,
avec sa marge d'incertitude plutôt que des chiffres présentés comme définitifs.

Pensée pour être envoyée à des stagiaires avant une formation (par exemple une
formation à la gestion du temps) : chacun passe le test depuis son navigateur,
télécharge son profil en PDF ou en JSON, et peut vous l'envoyer avant la session.

```bash
pip install -r requirements.txt
streamlit run disc_style.py
```

Python 3.10 ou plus récent. Aucun compte, aucun serveur, aucune base de données.

## Ce que ça fait

- 40 affirmations, tirées au hasard dans une banque de 264, réparties équitablement
  entre les quatre dimensions et mélangeant des formulations positives et négatives
  (pour repérer les réponses données au hasard).
- Un profil DISC complet : dimension dominante, mélange des deux dimensions les
  plus fortes, angle mort, environnement de travail où la personne est la plus
  efficace, sources de friction avec les autres profils, conseils de communication.
- Un indice de confiance sur la cohérence des réponses (élevée / modérée / faible),
  avec les raisons quand la confiance est faible.
- Un export PDF et un export JSON (le JSON permet de reprendre le test plus tard,
  ou de comparer un nouveau passage à un ancien).
- Rien n'est envoyé à un serveur : tout le calcul se fait dans la session
  Streamlit de la personne qui passe le test.

## Pourquoi seulement le module DISC ?

Le projet d'origine ([dzyla/disc-personality-assessment](https://github.com/dzyla/disc-personality-assessment),
licence MIT) proposait aussi des modules « forces », « sous pression » et
« motivateurs ». Le module « forces » reprend le référentiel des 34 thèmes
CliftonStrengths de Gallup, qui est une évaluation commerciale déposée — ce
n'est donc pas un contenu à diffuser librement. Cette version française ne
conserve que le module DISC, dont le contenu (les 264 affirmations et les
descriptions de profils) est original et n'appartient à aucun test propriétaire
(le modèle DISC lui-même, issu des travaux de William Marston, est dans le
domaine public ; ce qui est protégé, ce sont des formulations commerciales
précises comme le « DISC Classic »® que ce projet n'utilise pas).

Le code des modules retirés reste dans `assessment/scoring/` et
`data/*.json` au cas où on voudrait un jour les réactiver avec un contenu
maison — voir le commentaire dans `assessment/registry.py`.

## Déployer gratuitement, sans serveur (Streamlit Community Cloud)

1. Créez un compte sur [share.streamlit.io](https://share.streamlit.io) (gratuit,
   connexion avec votre compte GitHub).
2. Poussez ce dépôt sur votre propre compte GitHub (voir plus bas).
3. Sur Streamlit Community Cloud, cliquez sur **New app**, choisissez votre
   dépôt, la branche `main`, et indiquez `disc_style.py` comme fichier
   principal.
4. Streamlit installe automatiquement les dépendances (`requirements.txt`) et
   vous donne une URL publique du type `https://<nom>.streamlit.app` — c'est
   ce lien que vous envoyez à vos stagiaires avant la formation.

Chaque mise à jour poussée sur GitHub redéploie automatiquement l'application.

## Mettre le dépôt sur votre GitHub

```bash
git init -b main
git add -A
git commit -m "Test DISC en français pour les formations"
git remote add origin https://github.com/<votre-compte>/<nom-du-depot>.git
git push -u origin main
```

(Si le dossier est déjà un dépôt git, remplacez les deux premières lignes par
`git add -A` et `git commit -m "..."`.)

## Tests

```bash
pip install -r requirements.txt
pytest
```

La suite couvre le tirage des questions, le calcul des scores, la génération
du rapport et du PDF, et le parcours complet de l'application (via le module
de test headless de Streamlit).

## Licence et origine

Ce projet est une adaptation française, pour Eric Falcon Formation, du projet
[dzyla/disc-personality-assessment](https://github.com/dzyla/disc-personality-assessment)
de Dawid Zyla, sous licence MIT (voir `LICENSE`). Le code de calcul et
l'architecture Streamlit viennent du projet d'origine ; les questions, les
descriptions de profils et l'interface ont été traduites et adaptées en
français, et les modules non liés au DISC ont été retirés (voir plus haut).

Ce test est un instrument d'auto-évaluation, pas un outil clinique ni de
recrutement : il mesure comment une personne se décrit elle-même à un instant
donné, ce qui est utile à connaître mais ne remplace pas un échange direct.
