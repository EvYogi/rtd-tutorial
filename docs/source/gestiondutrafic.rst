Info trafic
======================



Délai entre événement grave et message par la radio 107.7
----------------------------------------------------------

Enjeux
  Sécurité des usagers.

Description
  L’indicateur permet de mesurer le temps que met ATMB à signaler aux usagers un événement grave sur son réseau par radio 107.7. 
  
  Sont considérés comme événements graves mettant en cause la sécurité des usagers ceux se produisant sur section courante, bretelles et plate-formes de péage. Ils consistent notamment en accident, contresens, véhicules en feu, piétons, animaux, objets sur chaussée et véhicules arrêtés.

Périmètre de mesure
  L'ensemble du réseau d'AXXX, en permanence. La mesure s’effectue à partir du moment où un événement grave mettant en cause la sécurité des usagers sur le réseau est localisé et confirmé. 
  
  Un inventaire permanent des événements graves est tenu à jour par AXXX, permettant une exploitation statistique annuelle établissant les pourcentages d'événements se situant dans les seuils correspondants aux objectifs.

Méthode de calcul 
  Pour calculer le délai entre événement grave et message sur les antennes de la radio 107.7, vous devez vous connecter à l’interface 107.7 (INSERER LE LIEN), sélectionner une plage de dates et exécuter la requête. 
   
   Après avoir sélectionné la plage de dates, les indicateurs sont calculés automatiquement :
   
  - ``Evènements diffusés dans les 4 minutes suivant la déclaration`` : affiche le nombre et pourcentage d’événements transmis et diffusés dans les 4 minutes après leur enregistrement dans SIERRA.
  - ``Evènements diffusés dans les 8 minutes suivant la déclaration`` : affiche le nombre et pourcentage d’événements transmis et diffusés dans les 8 minutes après leur enregistrement dans SIERRA.

  Les données brutes sont affichées plus loin et vous pouvez les exporter dans un fichier Excel à l’aide du bouton « Export Excel ».

  L'indicateur calcule la durée comprise entre la réception de cette information au niveau du PC et sa diffusion sur les antennes radio de 107.7. 
  
.. prompt::
  'DELAI_TOTAL' = 'DELAI_ENVOI' + 'DELAI_DIFFUSION'
  'DELAI_ENVOI' = 'DATE_ENVOI' - 'DATE_EVENEMENT'
  'DELAI_DIFFUSION' = 'DATE_DIFFUSION' - 'DATE_ENVOI'
  
  INSERER LA FORMULE PPOUR CALCULER LE POURCENTAGE   
    
.. figure:: /docs/source/duree_107.png
 :width: 80%
 :align: center
 :alt: Schema 107.7

Règles métier / Exceptions
  L'indicateur doit **prendre en compte** les événements de type ``TYPE_EVENEMENT`` :
  
    - ``ACCIDENT``, 
    - ``OBSTACLE SUR LA CHAUSSEE``, 
    - ``PANNE``, 
    - ``ANIMAL ERRANT``, 
    - ``CONTRE SENS``, 
    - ``ANIMAL CHAUSSEE``,
    - ``VEHICULE EN FEU``, 
    - ``PIETON SUR LA CHAUSSEE``. 
  
  L'indicateur doit **exclure** les événements produits sur une aire de service (champ ``AIRE_SERVICE = 0``). 
  
  *ATTENTION: ce champ n'est pas disponible dans les données affichées. Ce critère est pris en compte au moment de l'extraction des événements depuis SIERRA avant de les insérer dans la base de données 107.7.*

En cas d'anomalie / asence de données
  Spécifier le traitement à appliquer. 
       
Objectif
  L’indicateur est assorti d’un double objectif de résultat par mode de transmission à l’usager:
  
  Pour une diffusion sur la radio 107.7 :
  
    - seuil 1 : délai de moins de 4 min dans au moins 90% des cas 
    - seuil 2 : délai de moins de 8 min dans au moins de 98% des cas

Mécathisme de pénalité
  Appliquée en cas de non-respect des seuils. 
  
Propriétaire de données
  Direction Réseau Environnement
  
Source de données
  Interface 107.7. L'application permet d'accéder et d'extraire les données brutes depuis l'interface au format Excel. 
  
Rapport BO
  Non disponible. 
  
  
  
Délai événement entre grave et message par PMV
-------------------------------------------------

Enjeux
  Sécurité des usagers.

Description
  L’indicateur permet de mesurer le temps que met ATMB à signaler aux usagers un événement grave sur son réseau par panneaux à Messages Variable (PMV).
  
  Il s'agit de calculer la durée comprise entre la réception de cette information au niveau du PC et son signalement par ATMB sur les PMV est enregistrée. En cas d’événements simultanés, seul l’élément prioritaire est pris en compte dans le calcul. 
    
  Un inventaire permanent des événements graves est tenu à jour par ATMB, permettant une exploitation statistique annuelle établissant les pourcentages d’événements se situant dans les seuils correspondants aux objectifs. 

Périmètre de mesure
  L'ensemble du réseau d'AXXX, en permanence. Pour les PMV cela s'entend "hors PMV non gérés par la société" => besoin de précision (!) 
  
Méthode de calcul
  Pour calculer le délai entre événement grave et message PMV, vous devez vous connecter à l’interface de BusinessObjects et sélectionner le rapport ``délai_AFFICHAGE_PMV_- _V10-4sma``. 
  
  Sélectionner une plage de dates dans la barre de filtres à gauche et choisir l’onglet « XXX » pour afficher le délai d’affichage PMV.
  
    - ``% evt <3min (tout evt)`` : affiche le pourcentage d’événements transmis et diffusés dans les 3 minutes après leur enregistrement dans SIERRA.
    - ``% evt <6min (tous evts)`` : affiche le pourcentage d’événements transmis et diffusés dans les 6 minutes après leur enregistrement dans SIERRA.
    
  Les événements considérés comme grave où la variable ``Type_evt =`` :
  
    - ``ACCIDENT``, 
    - ``OBSTACLE SUR LA CHAUSSEE``, 
    - ``PANNE``, 
    - ``CONTRE SENS``, 
    - ``ANIMAL SUR LA CHAUSSEE`` où la variable ``ANIMAL ERRANT = OUI``, 
    - ``OBJETS SUR LA CHAUSSEE`` (hors BAU), 
    - ``PRODUIT SUR LA CHAUSSEE``, 
    - ``VEHICULE EN FEU``, 
    - ``PIETON SUR LA CHAUSSEE``. 
  
  On distingue deux cas d'affichage possibles : via PAC et ??? 
  
    1. Si l'événement a été affiché via PAC, alors la date de début et la date de fin d'action sont renseignées. Le délai est la différence entre la ``Date_debut_ac`` et la ``date_debut_evt``.  
  
.. prompt::
  ``délai``= ``Date_debut_ac`` - ``date_debut_evt``

   2.  Si l'événement n'a pas été affiché via PAC, le champ ``FIE = NULL`` et le champ ``Evts sans affichage PMV via PAC = NONaffichage". Dans ce cas de figure, le délai est calculé à partir de ... A COMPLETER.

Les données brutes sont accessibles dans l’onglet ``XXX `` et vous pouvez les exporter dans un fichier Excel. 
  
Règles métier / Exceptions
  L'indicateur doit **exclure** :
  
    - tous les événements produits sur une aire de service (la variable ``Presence_Aire_Service = 'Non'`` ou vide).
    -	tous les événements Z-test ; Annulé ; Hors Concession
    -	tous les événements sur les Aires et sur les Lit d’arret
    -	tous les événements :
    
      - en bretelle entrée pour lesquels il n’y a pas de PIA (principalement RN205) ou PMV pour Bif
      
        - RN205

          - S1 : Bretelle entrée Vigie, Georgeanne, Aire Graviere, Bagna-Houches, Trabet, Fontaine, aire Chatelard, EDF et Chedde + Bretelle Sortie Vigie 
          - S2 : Bretelle entrée Bossons, Trabet, Georgeanne, Aire Graviere, Houches, fontaine, aire Chatelard, Servoz et Aire Chedde 

        - A40

          - S2 : BE Fayet
      - (provisoirement tant qu’on n’a pas le PIA TMB dans SIERRA) sur la RN205 dans le S1 du PK 0+000 au PK 4+100 
      - sur l’A40 dans le S2 entre le PMV de Chatillon (PK 102+500) et le PK 102+848
      - sur l’A41 dans le S2 entre le PMV de Bardonnex (PK 159+379) et le PK 160+029
      - sur l’A411 dans le S2 entre le PMV de Vallard (PK 1+350) et le PK 2+139
      - « Piétons sur la chaussée », « Animal sur chaussée », « Objets sur la chaussée », « Produit sur la chaussée » ayant une durée de vie de moins de 3 min


Objectif
  Pour une diffusion par PMV:
  
    - seuil 1 : délai de moins de 3 min dans 90% des cas
    - seuil 2 : délai de moins de 6 min dans 98% des cas

Mécathisme de pénalité
  Appliquée en cas de non-respect des seuils. 
  
Propriétaire de données
  Direction Réseau Environnement
  
Source de données
  SIERRA
  
Rapport BO
  Le rapport ``délai_AFFICHAGE_PMV_- _V10-4sma``.
  


Histogramme annuel des durées des coupures
--------------------------------------------

Enjeux
  Sécurité routière.

Description
  Tracer l'histogramme des durées des coupures produites au cours de l'année.
  
Méthode de calcul
  Pour tracer l'histogramme des coupures, vous devez vous connecter à l'interface de Business Objects et sélectionner le rapport ``Liste Coupures``. Puis préciser une plage de dates dans la barre à filtre à gauche et exécuter la requête. Choisir l'onglet "XXX" pour afficher la liste des événements (``Type_evt = Coupure``). 
  
  A partir de la liste affichée, la durée est calculée et renseignée dans la variable ``DUREE_EN_HEURE`` : différence entre``Date_debut`` et ``Date_fin`` convertie en heures pour chaque coupure. 
  
  Il est possible d'extraire la liste des événements au format Excel puis tracer l'histogramme en positionnant le nombre de coupures heure par heure. 

.. figure:: /docs/source/hist_coupure.png
 :width: 80%
 :align: center
 :alt: Histogramme des coupures

Règles métier/ Exceptions
    1. Exclure les coupures qui se sont produites sur les bretelles (la variable ``Bretelle`` doit être vide).

Source de données
  SIERRA

Rapport BO
  Le rapport ``Liste Coupures``.



Déclenchement de Plan de Gestion de Trafic (h)
-----------------------------------------------

Enjeux
  Sécurité routière.

Description
  Calculer la durée des PGT declenchés au cours de l'année.
  
Méthode de calcul
  Pour calculer la durée des PGT, vous devez vous connecter à l'interface de Business Objects et sélectionner le rapport ``Liste Mesures``. Puis préciser une plage de dates dans la barre à filtre à gauche et exécuter la requête. Choisir l'onglet "XXX" pour afficher la liste des événements (``Type_evt = Mesure``). 
  
  A partir de la liste affichée, la durée est calculée et renseignée dans la variable ``DUREE_EN_HEURE`` : différence entre``Date_debut`` et ``Date_fin`` convertie en heures pour chaque mesure.
  
  Il est possible d'extraire les données brutes à partir de l'onglet "Données brutes".

Règles de gestion / Exceptions
    1. Ne pas prendre en compte le plan d'intervention de déclenchements des avalanches (PIDA) dans ``Nom_Mesure = PIDA`` ( A CONFIRMER)

Base de données
  SIERRA

Rapport BO
  Le rapport ``Liste Mesures``.



Réseau couvert par les PGT (%)
-------------------------------

Enjeux
  Sécurité routière.

Objectif
  Couverture : 100%

Résultats ATMB
  Couverture actuelle : 100%

