# Consommation d'antibiotiques et microbiologie en milieu hospitalier

Étude exploratoire et prédictive sur MIMIC-IV demo (100 patients) : prescriptions
d'antibiotiques, administrations en réanimation et résultats de microbiologie.

## Données
- MIMIC-IV Clinical Database Demo (PhysioNet), accès libre.
- Tables utilisées : patients, admissions, icustays, prescriptions, inputevents,
  d_items, microbiologyevents. Schéma : `docs/schema.md`.
- Les données ne sont pas dans le dépôt.

## Pile technique
BigQuery (sandbox) pour l'extraction SQL, Python (Colab) pour l'analyse et le ML, Git.

## Reproduire
1. Télécharger le demo depuis PhysioNet.
2. Charger chaque CSV dans un dataset BigQuery, **toutes colonnes en STRING**
   (la détection automatique échoue sur certaines tables), puis convertir
   avec SAFE_CAST dans les requêtes.
3. Renseigner l'ID du projet et du dataset (voir `.env.example`).
4. Exécuter les requêtes de `sql/` depuis les notebooks.

## Structure
repo/
├─ README.md
├─ requirements.txt
├─ .gitignore
├─ .env.example        # modèle de configuration, sans valeur secrète
├─ docs/
│  └─ schema.md        # schéma de relations
├─ sql/                # une requête = un fichier .sql
├─ src/                # code Python réutilisable (client BigQuery, chargement CSV, nettoyage)
├─ notebooks/          # EDA et ML
└─ exports/            # petits agrégats pour Tableau 

## Limites
Échantillon de 100 patients, dates décalées par patient (pas de dates absolues).
