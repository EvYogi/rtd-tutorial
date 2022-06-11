Environnement
======================

Consommation d'eau (m3)
------------------------

Enjeux
  Préserver l'environnement. 
 
Description
   L'indicateur mesure le volume d'eau consommé par la société.

Méthode de calcul
  Prélevement des relevés depuis le compteur.

Objectif
  Afficher une baisse tendantielle dans la consommation d'eau.

Mécathisme de pénalité
  Non défini.

Propriétaire de données
  Direction Réseau Environnement / Centre d'exploitation. 

Source de données
  Fournisseur d'eau - factures.

Rapport BO
  Non disponible.



Tri des déchets
----------------

Enjeux
  Préserver l'environnement.

Description
  La mesure vise à équiper les centres d'explotation et les aires de repos avec un système de tri des déchets. 

Objectif / Résultats
  Equipement du parc :
  
  - Aires de repos et de service (%) : 100 % (14 sur 14 unités)
  - Centres d'exploitation (%) : 100 % (3 sur 3)
  
Propriétaire de données
  Direction Réseau Environnement / Responsable Environnement & Patrimoine.




Qualité de l'air
-----------------

Enjeux
  Préserver l'environnement.

Description
  Mesurer la durée et la longueur des bouchons (H.km) pour estimer la pollution de l'air engendrée : 
  
  - Les pollutions locales (particules, gaz toxiques) susceptibles d’entraîner des dommages immédiats dans une aire géographique donnée;
  - Les rejets de CO2 qui contribuent à l’effet de serre et posent un grave problème à l’échelle mondiale.

Méthode de calcul
  Les bouchons se quantifient en volume d’encombrement et s’expriment en heures.kilomètres (HKM). 

.. code-block:: text
  
  **Définitions**
  
  Le volume est calculé ainsi : produit de la durée du bouchon (exprimé en heures) par la longueur moyenne (exprimée en km) 
  ramené au nombre de voies.

Pour les événements de type ``Type event = "Bouchon"``:
  
  ``Bouchon H.km`` = (``Date_fin`` - ``Date_debut``) * max (``Longueur_queue``)/1000
   
Objectif
  Non défini.

Mécathisme de pénalité
  Non défini.

Propriétaire de données
  Direction Réseau Environnement
  
Source de données
  Sierra

Rapport BO
  Le rapport ``Bouchon OK``. 


Consommation de produits phytosanitaires (kg/km)
-------------------------------------------------

Enjeux
  Préserver l'environnement.

Description
 Depuis le 1er janvier 2017, la loi Labbé a interdit l’utilisation des produits phytosanitaires.

Objectif
  Consommation de produits phytosanitaires (kg/km) : 0 % 
  
  Depuis 2020, ATMB n'utilise plus les produits pour l'exploitation du réseau (0 %). 

Propriétaire de données
  Direction Réseau Environnement / Centres d'exploitation. 
  

