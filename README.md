# eglise-maison-lumiere.github.io
🏛️ Ministère Maison de Lumière — Application de Gestion
Application web complète pour la gestion des programmes de cultes, des membres et l'exportation PDF du Ministère Maison de Lumière.

📋 Table des matières
•	Aperçu
•	Fonctionnalités
•	Technologies utilisées
•	Installation et configuration
•	Configuration Supabase
•	Structure du projet
•	Utilisation
•	Export PDF
•	Sauvegarde des données

🌟 Aperçu
Application single-page (fichier HTML unique) permettant à l'équipe du ministère de :
•	Planifier et gérer les programmes de cultes
•	Gérer la liste des membres et leurs responsabilités
•	Visualiser les programmes dans un calendrier mensuel
•	Exporter les programmes en PDF
•	Synchroniser toutes les données dans le cloud via Supabase

✅ Fonctionnalités
Tableau de bord
•	Vue générale des statistiques (total programmes, programmes du mois, programmes à venir, membres)
•	Liste des 5 programmes les plus récents avec aperçu rapide
Programmes des cultes
•	Créer, modifier et supprimer des programmes
•	Filtrage par mois, année et type de culte
•	Types supportés :
•	Culte d'Adoration
•	Culte de Prière
•	Culte Spécial
•	Service de Sainte Cène
•	Enseignement Biblique
•	École Dominicale
Vue Calendrier
•	Navigation mensuelle (mois précédent / suivant)
•	Filtrage par type de culte avec badges cliquables
•	Export PDF du mois complet ou filtré par type
Membres & Rôles
•	Ajouter, modifier et supprimer des membres
•	Responsabilités disponibles : Pasteur/Orateur, Modérateur/trice, Lecteur/trice, Intercesseur/se, Chant spécial, Présentation des visiteurs, Musicien/ne, Diacre/Diaconesse, Psalmiste, Enseignant/e, Usher, Autre
Sauvegarde
•	Export JSON de toutes les données
•	Import JSON (fusion avec les données existantes)
•	Réinitialisation complète
•	Synchronisation cloud automatique via Supabase

🛠️ Technologies utilisées
Technologie	Rôle
HTML5 / CSS3 / JavaScript	Frontend (application single-page)
Supabase
Base de données PostgreSQL cloud (gratuit)
jsPDF
Génération de fichiers PDF
LocalStorage	Cache local pour affichage instantané

🚀 Installation et configuration
Prérequis
•	Un navigateur web moderne (Chrome, Firefox, Edge, Safari)
•	Un compte Supabase (gratuit, sans carte bancaire)
Étapes
1. Cloner le dépôt
git clone https://github.com/votre-utilisateur/maison-de-lumiere.git
cd maison-de-lumiere

2. Ouvrir le fichier
Double-cliquez sur maison-de-lumiere-supabase.html dans votre explorateur de fichiers,
ou ouvrez-le avec votre navigateur :
# Sur Mac
open maison-de-lumiere-supabase.html

# Sur Linux
xdg-open maison-de-lumiere-supabase.html

# Sur Windows
start maison-de-lumiere-supabase.html


🗄️ Configuration Supabase
1. Créer un projet Supabase
1. Allez sur supabase.com → "New project"
2. Nommez le projet maison-de-lumiere
3. Choisissez un mot de passe et une région
2. Créer les tables (SQL Editor)
Dans Supabase → SQL Editor → New query, exécutez :
-- Table des programmes
CREATE TABLE programmes (
  id    BIGSERIAL PRIMARY KEY,
  date  TEXT, type TEXT, hd TEXT, hf TEXT,
  mod   TEXT, lec  TEXT, pri TEXT, cha TEXT,
  vis   TEXT, ora  TEXT, tex TEXT, them TEXT, notes TEXT
);

-- Table des membres
CREATE TABLE membres (
  id    BIGSERIAL PRIMARY KEY,
  nom   TEXT, titre TEXT, resp TEXT
);

-- Politiques d'accès public
ALTER TABLE programmes ENABLE ROW LEVEL SECURITY;
ALTER TABLE membres    ENABLE ROW LEVEL SECURITY;
CREATE POLICY "public_all" ON programmes FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "public_all" ON membres    FOR ALL USING (true) WITH CHECK (true);

3. Récupérer vos clés API
Dans Supabase → Project Settings → API :
•	Copiez le Project URL → https://xxxxxxxxxx.supabase.co
•	Copiez la clé anon public
4. Configurer le fichier HTML
Ouvrez maison-de-lumiere-supabase.html et remplacez en haut du script :
var SUPABASE_URL = 'https://xxxxxxxxxx.supabase.co'; // ← votre URL
var SUPABASE_KEY = 'eyJhbGci...';                    // ← votre clé anon


📁 Structure du projet
maison-de-lumiere/
│
└── maison-de-lumiere-supabase.html   # Application complète (fichier unique)

L'application est entièrement contenue dans un seul fichier HTML.
Aucune dépendance locale, aucun serveur requis.

📖 Utilisation
Créer un programme
1. Cliquez sur "+ Nouveau programme" (barre du haut ou menu)
2. Remplissez les informations du culte (date, type, modérateur, orateur, texte biblique...)
3. Cliquez "Enregistrer" → les données sont automatiquement sauvegardées dans Supabase
Gérer les membres
1. Allez dans Membres & Rôles
2. Cliquez "+ Ajouter un membre"
3. Renseignez le nom, titre et responsabilité principale
4. Cliquez "Enregistrer"
Calendrier avec filtre
1. Allez dans Vue Calendrier
2. Naviguez avec les boutons Précédent / Suivant
3. Utilisez le menu déroulant pour filtrer par type de culte
4. Cliquez sur un badge de type pour filtrage rapide
5. Cliquez "📄 PDF filtré" pour exporter uniquement les programmes affichés

📄 Export PDF
Trois modes d'export disponibles :
Mode	Description
Programme individuel	Export d'un seul programme depuis la liste ou l'aperçu
PDF du mois	Tous les programmes du mois affiché dans le calendrier
PDF filtré	Programmes du mois filtrés par type de culte
PDF par type	Tous les programmes d'un type donné (section Sauvegarde)

💾 Sauvegarde des données
Action	Description
Export JSON	Télécharge un fichier de sauvegarde complet
Import JSON	Fusionne un fichier de sauvegarde avec les données existantes
Réinitialiser	Supprime toutes les données (irréversible)
Les données sont synchronisées en temps réel avec Supabase.
Un cache local (localStorage) garantit un affichage instantané même sans connexion.

👥 Équipe
Développé pour le Ministère Maison de Lumière.

📝 Licence
Ce projet est à usage interne du Ministère Maison de Lumière.
