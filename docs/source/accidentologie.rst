Accidentologie
===============


Taux d'accidentalité
-----------------------

Enjeux
  Sécurité routière des usagers. 

Description
  L'indicateur permet de mesurer le taux d'accidentalité sur le réseau.
  
Méthode de calcul
   Pour calculer le taux d'accidentalité, vous devez vous connecter à l'interface de Business Objects et sélectionner le rapport ``ListeEvenements``. Vous pouvez sélectionner une plage de dates dans la barre à filtres à gauche et exécuter la requête. 
  
  Dans l'onglet ``XXX`` vous trouvez le nombre d'accidents présenté par type :``ACCROCHAGE``, ``ACCIDENT MATERIEL``, ``ACCIDENT CORPOREL``. 
  
  Le taux d'accidents est le quotient entre le nombre d'accidents (materiels et corporels) et le nombre de kilomètres parcourus.  

Règles métier / Exception
  L'indicateur exclut les accidents de type ``ACCROCHAGE``.

Objectif
  Non défini. 

Mécathisme de pénalité
  Non défini.

Propriétaire de données 
  Direction Réseau Environnement.

Source de données
  SIERRA + données venant de la gendarmerie.

Rapport BO
  Le rapport ``ListeEvenements``.
  
   
  
Bilan de la sécurité routière
-------------------------------

Enjeux
  Le bilan annuel a pour but de faire connaître l’accidentalité pour en comprendre les mécanismes, à travers notamment des analyses thématiques. 
  
Description
  ATMB établit un bilan annuel de sécurité routière, aussi bien quantitatif que qualitatif. Tous les accidents (matériels et corporels) sont recensés et font l’objet d’un suivi statistique annuel (taux d’accidents, taux de blessés légers, graves, tués). 

Méthode de calcul
  A noter qu’à partir de janvier 2020 ATMB avons deux méthodes de recensement de nos données accidents corporels :
  
  - Données accidents ATMB :
  
    - Accident Corporel si intervention des pompiers (le(s) client(s) sera(ont) considéré(s) comme victime dès lors que les pompiers l’on (les ont) pris en charge.
    - Accident Matériel si intervention du dépanneur ou/et dégât au domaine.
    - Sinon c'est un Accrochage.
    
  - Données accidents croisés avec la GND concernant les accidents corporels (Accident Corporel si le(s) blessé(s)  nécessite(nt) des soins hospitaliers le blessé sera considéré comme HO s’il a un ITT, sinon il sera considéré comme blessé NHO). ::

.. code-block:: text
  
  *Rappel définitions*
  
  - Blessés Non Hospitalisés : victimes ayant fait l’objet de soins médicaux mais n’ayant pas été admises comme patients à l’hôpital plus de 24 heures.
  - Blessés Hospitalisés : victimes admises comme patients dans un hôpital plus de 24 heures.
  - Tués : toutes personnes qui décèdent sur le coup ou dans les trente jours qui suivent l’accident.


Cartographie des accidents
----------------------------

Enjeux
  Sécurité routière. 
  
Description
  Positionner les accidents produits sur la carte du résea d'ATMB permet de mieux comprendre les zones à risque et de décider des aménagements à apporter. 
  
Méthode de calcul
  Tout accident fait l'objet d'une intervention et est localisé sur le réseau. Les coordonnées de localisation sont importé dans l'outil ArcGIS pour positionner les accidents sur la carte.
  
Source de données
  SIERRA et ArcGis

Rapport BO
  Le rapport ``ListeEvenements`` 


Cartographies des trafics
--------------------------
Enjeux
  Sécuritè routière. 
  
Description
  La cartographie permet de visualiser des trafics sur le réseau d'ATMB.
  
Méthode de calcul
  Au niveau chaque section d'autoroute préciser le volume du trafic dans deux sens à l'aide de l'outil ArcGIS. 

Source de données
    SIERRA et ArcGIS
    
Rapport BO
  Non disponible.


Bilan des collisions animales
-------------------------------

Enjeux
  Sécurité routière / Protection de la faune.  
  
Description
  Faire un bilan des collisions animales produites sur le réseau.  
  
Méthode de calcul
  Pour faire le bilan, vous devez vous connecter à l'interface de BusinessObjects et sélectionner le rapport ``ListeEvenements``. Sélectionner une plage de dates dans la barre à filtres à gauche et exécuter la requête. 
  
  Dans l'onglet " xxx " vous pouvez visualiser le tableau comprenant les collisions animales. 
  
  Pour compter le nombre de collisions, il faut filter les événements en sélectionnant ``Typ_evt = Animal sur chaussée``. 
  
Règles métier / Exceptions
  Quid ``Animal errant`` ? 
 
Source de données
  SIERRA

Rapport BO
  Le rapport ``ListeEvenements``. 
