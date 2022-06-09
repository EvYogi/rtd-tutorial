Info trafic
======================



Délai événement grave et message par la radio 107.7
-----------------------------------------------------

Enjeux
  Sécurité des usagers.

Description
  L’indicateur permet de mesurer le temps que met ATMB à signaler aux usagers un événement grave sur son réseau par radio 107.7. 
  
  Sont considérés comme événements graves mettant en cause la sécurité des usagers ceux se produisant sur section courante, bretelles et plate-formes de péage. Ils consistent notamment en accident, contresens, véhicules en feu, piétons, animaux, objets sur chaussée et véhicules arrêtés.

Périmètre de mesure
  L'ensemble du réseau d'AXXX, en permanence. La mesure s’effectue à partir du moment où un événement grave mettant en cause la sécurité des usagers sur le réseau est localisé et confirmé. 
  
  Un inventaire permanent des événements graves est tenu à jour par AXXX, permettant une exploitation statistique annuelle établissant les pourcentages d'événements se situant dans les seuils correspondants aux objectifs.

Méthode de calcul 
  L'indicateur calcule la durée comprise entre la réception de cette information au niveau du PC et sa diffusion sur les antennes radio de 107.7. 
  
.. prompt::
  'DELAI_TOTAL' = 'DELAI_ENVOI' + 'DELAI_DIFFUSION'
  'DELAI_ENVOI' = 'DATE_ENVOI' - 'DATE_EVENEMENT'
  'DELAI_DIFFUSION' = 'DATE_DIFFUSION' - 'DATE_ENVOI'
    
    
.. figure:: /docs/source/duree_107.png
 :width: 80%
 :align: center
 :alt: Schema 107.7

Règles métier / Exceptions
  L'indicateur doit **prendre en compte** les événements de type : ``TYPE_EVENEMENT`` = ``ACCIDENT``, ``OBSTACLE SUR LA CHAUSSEE``, ``PANNE``, ``ANIMAL ERRANT``, ``CONTRE SENS``, ``ANIMAL CHAUSSEE``, ``VEHICULE EN FEU``, ``PIETON SUR LA CHAUSSEE``. 
  
  L'indicateur doit **exclure** les événements produits sur une aire de service (champ ``AIRE_SERVICE = 0``).
       
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
  
  
  
Délai événement grave et message par PMV
----------------------------------------------

Enjeux
  Sécurité des usagers.

Description
  L’indicateur permet de mesurer le temps que met ATMB à signaler aux usagers un événement grave sur son réseau par panneaux à Messages Variable (PMV).
  
  Sont considérés comme événements graves mettant en cause la sécurité des usagers ceux se produisant sur section courante, bretelles et plate-formes de péage. Ils consistent notamment en accident, contresens, véhicules en feu, piétons, animaux, objets sur chaussée et véhicules arrêtés.

Périmètre de mesure
  L'ensemble du réseau d'AXXX, en permanence. Pour les PMV cela s'entend "hors PMV non gérés par la société". 

Méthode de calcul 
  L'indicateur calcule la durée comprise entre la réception de cette information au niveau du PC et son signalement par ATMB sur les PMV est enregistrée.
  
  Pour les PMV, en cas d’événements simultanés, seul l’élément prioritaire est pris en compte dans le calcul. 
    
  Un inventaire permanent des événements graves est tenu à jour par ATMB, permettant une exploitation statistique annuelle établissant les pourcentages d’événements se situant dans les seuils correspondants aux objectifs.    
  

Méthode de calcul
  Les événements considérés comme grave : ``TYPE_EVENEMENT`` = ``ACCIDENT``, ``OBSTACLE SUR LA CHAUSSEE``, ``PANNE``, ``CONTRE SENS``, ``ANIMAL SUR LA CHAUSSEE`` où la variable ``ANIMAL ERRANT = OUI``, ``OBJETS SUR LA CHAUSSEE`` (hors BAU), ``PRODUIT SUR LA CHAUSSEE``, ``VEHICULE EN FEU``, ``PIETON SUR LA CHAUSSEE``. 
  
  On distingue deux cas d'affichage possibles : via PAC et ???? .  
  
  Si l'événement a été affiché via PAC, alors la date de début et la date de fin d'action sont renseignées. Le délai est la différence entre la ``Date_debut_ac`` et la ``date_debut_evt``. 
  
  Si l'événement n'a pas été affiché via PAC, le champ ``FIE = NULL`` et le champ ``Evts sans affichage PMV via PAC = NONaffichage". Dans ce cas de figure, le délai est calculé à partir de ... A COMPLETER.
  
  L'indicateur doit **exclure** les événements produits sur une aire de service (la variable ``Presence_Aire_Service = Non ou Nan``).
  
  Voici les restrictions :
  -	Exclure tous les événements Z-test ; Annulé ; Hors Concession
  -	Exclure tous les événements sur les Aires et sur les Lit d’arret
  -	Exclure tous les événements 
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
  Sierra
  
Rapport BO
  Le rapport ``délai_AFFICHAGE_PMV_- _V10-4sma``.
  


Histogramme annuel des durées des coupures
--------------------------------------------

Enjeux
  Sécurité routière.

Description
  Tracer l'histogramme des durées des coupures produites au cours de l'année.
  
Méthode de calcul
  Parmi les événements de type ``Type_evt = Coupure``, calculer la durée de chaque coupure entre ``Date_debut`` et ``Date_fin`` en heure puis repartir les durées par 
  
  Règles de gestion :

    1. Ne pas prendre en compte le plan d'intervention de déclenchements des avalanches (PIDA) dans ``Nom_Mesure = PIDA`` ( A CONFIRMER)

Source de données
  Sierra

Rapport BO
  Le rapport ``Liste Coupures``.



Déclenchement de Plan de Gestion de Trafic (h)
-----------------------------------------------

Enjeux
  Sécurité routière.

Description
  Calculer la durée des PGT declenchés au cours de l'année.
  
Méthode de calcul
  Parmi les événements de type ``Type_evt = Mesure``, calculer la durée de chaque PGT entre ``Date_debut`` et ``Date_fin`` en heure puis additionner les durées.
  
  Règles de gestion :
    1. Ne pas prendre en compte le plan d'intervention de déclenchements des avalanches (PIDA) dans ``Nom_Mesure = PIDA`` ( A CONFIRMER)

Base de données
  Sierra

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



Gêne au péage
--------------

Enjeux
  Service aux usagers - Rapidité et fiabilité du trajet.

Description
  la réflexion est engagée pour aboutir sur la durée du contrat d'entreprise à mettre en place plusieurs critères de qualité objectifs, dont les principes sont suivants :
  
  Critère 1. disponibilité des voies de passage.
  
  Ce critère vise à évaluer le niveau de service de l'ensemble des équipements indispensables de la chaîne de traitement du péage (et notamment ceux qui sont utilisés pour la détection de l'usager, la transaction, et la libération de la voie de péage). 
  
  Critère 2. délai global de traitement d'exploitation en voie de péage, dans lequel peuvent apparaître deux sous-critères :
  
    - le délai entre la détection de l'événement et sa prise de connaissance par AXXXX;
    - le délai entre la prise de connaissance d'un événement par AXXX et la libération de la voie de péage (possibilité de redémarrage effectif de l'usager). 
  
  Critère 3. optimisation de l'ordonnancement des voies à travers la bonne utilisation de la débrayabilité des voies TSA.
  
  Ces critères permettront de définir des indicateurs de synthèse qui seront utilisés pour mesurer la performance d'AXXX au travers d'objectifs à fixer. 

Méthode 
  Le détail des critères 1 et 2 et les indicateurs de synthèse associés, ainsi que les méthodes de mesure et de calcul devront être élaborés par AXXX pour être finalisés en accord avec le concédant pour la fin d'année qui suit celle de signature du contrat.
  
  Des chroniques de ces critères ainsi que des premiers calculs des indicateurs de synthèse seront alors réalisées sur les 2 années suivantes (mise en place progressive des systèmes de mesure).
  
  Le critère 3 fera l'objet d'échanges entre le concédant et AXXX afin d'aboutir à une méthode de mesure à la fin du contrat d'entreprise.
  
Périmètre mesuré
  Les barrières et gares de l'ensemble du réseau en entrée et en sortie. 

Objectif
  Les objectifs de performance à atteindre seront définis en accord avec le concédant avant la fin du premier trimestre de la dernière année du contrat d'entreprise.
  
Pénalité
  Sera ppliquée en cas de non-respect des seuils qui restent à fixer.
  
Responsable
  Direction Réseau Environnement.

Source de données
  Non dispoible.

Rapport BO
  Non dispobible. 
