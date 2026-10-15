# 💰 Mon Budget

Petite application personnelle (iPhone + ordinateur) qui reprend le fonctionnement du classeur **Budget 2026.xlsx** :

- **Mois** : les lignes du budget rangées comme dans l'Excel — *Salaire, Aide, Charges fixes, Épargne* (à gauche) et *Sorties / Activités, Exceptionnel* (à droite sur ordinateur).
  Chaque ligne : motif, montant **en F ou en €** (converti avec le taux, 120 par défaut), jour du mois, compte (Banque Pop, BNC, BNC Prélèvement, Espèce, Revolut, BCI…) et une **case à cocher** quand c'est passé (le « x » de l'Excel).
- **Synthèse** (à droite de l'écran sur ordinateur) : mêmes calculs que l'Excel
  - Total restant mensuel = Salaire + Aide + Charges fixes + Épargne + Sorties
  - Soit par semaine (÷ 4) et par jour (÷ 7)
  - Total restant avec l'exceptionnel
  - Total réel = seulement les lignes cochées
  - Totaux par compte (prévu et réel)
- **Nouveau mois** : flèche › puis « Créer … à partir de … » : les lignes du mois précédent sont recopiées, cases décochées (tu choisis les catégories à reprendre).
- **Épargne** : l'onglet Épargne de l'Excel, avec le solde qui se cumule ligne après ligne.
- **Année** : bilan mois par mois (rentrées, sorties, restant).
- **Import Excel** (Réglages) : reprend tous les onglets de mois (« 06-26_JUIN »…) et l'onglet Épargne. Le fichier est lu sur l'appareil, il n'est envoyé nulle part.

## 🔒 Sécurité (même principe que Ma Maison)

- L'**application** (le code) est publique sur GitHub Pages : elle ne contient **aucune donnée**.
- Tes **données** sont dans un **dépôt privé** séparé, dans un fichier `budget.enc.json`, **chiffré avec ton mot de passe** (AES-256-GCM, PBKDF2-SHA256 310 000 itérations) **sur le téléphone, avant l'envoi**.
- Ton mot de passe n'est jamais envoyé ni stocké en clair. « Rester connecté » fonctionne comme dans Ma Maison (clé propre à l'appareil, le bouton 🔒 déconnecte).
- Les réglages de Mon Budget sont séparés de ceux de Ma Maison (même adresse `github.io`, mais stockage distinct).
- ⚠️ **Mot de passe oublié = données perdues.** Fais de temps en temps Réglages → Exporter, et garde le fichier en lieu sûr.

---

## Installation (≈ 10 min, une seule fois)

### 1. Dépôt de l'application (public)
1. github.com → **New repository** → nom : `mon-budget` → **Public** → *Create*.
2. *Add file → Upload files* → dépose les fichiers : `index.html`, `sw.js`, `manifest.webmanifest`, `icon-180.png`, `icon-192.png`, `icon-512.png`, `README.md` → *Commit*.
3. *Settings → Pages* → Source : **Deploy from a branch** → `main` / `(root)` → *Save*.
4. Après 1–2 minutes : `https://flonewcal988.github.io/mon-budget/`

### 2. Dépôt des données (privé)
**New repository** → nom : `mon-budget-donnees` → **Private** → coche **Add a README file** → *Create*.

### 3. Jeton d'accès (limité à ce seul dépôt)
1. Photo de profil → *Settings → Developer settings → Personal access tokens → Fine-grained tokens* → *Generate new token*.
2. Nom : `Mon Budget` · Expiration : 1 an.
3. **Repository access → Only select repositories →** `mon-budget-donnees`.
4. **Permissions → Contents : Read and write** (rien d'autre) → *Generate token* → copie le `github_pat_…`.

> Astuce : tu peux aussi modifier le jeton de Ma Maison pour lui ajouter `mon-budget-donnees`, mais un jeton séparé est plus propre.

### 4. Premier lancement
1. Ouvre `https://flonewcal988.github.io/mon-budget/`
2. Pseudo et dépôt sont pré-remplis ; colle le jeton et **choisis un mot de passe** (8 caractères min.).
3. Réglages (⚙️) → **Importer mon fichier Excel** → choisis `Budget_2026.xlsx`.

### 5. Sur iPhone
Safari → bouton **Partager** → **Sur l'écran d'accueil**. Sur un autre appareil (ordinateur), refais l'étape 4 avec **le même mot de passe**.

## Bon à savoir
- Les montants en € sont convertis avec **un seul taux** (Réglages). Ton onglet Épargne utilisait 119,33 pour « Epargne actuelle » : l'app affiche donc 729 480 F au lieu de 725 417 F pour cette ligne — saisis-la en F si tu veux le montant exact.
- Hors ligne : l'app fonctionne, les modifications partent sur GitHub au retour du réseau.
- Jeton expiré : écran de verrouillage → *Réinitialiser cet appareil* → reconnecte-toi avec le nouveau jeton et le même mot de passe.
