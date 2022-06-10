Satisfaction des usagers
=========================

Délais de réponse aux sollicitations écrites d'usagers
--------------------------------------------------------

Enjeux
  Services aux usagers / respect des usagers.


Description
  L’indicateur permet d’évaluer la réactivité de ATMB dans ses réponses aux sollicitations des clients – mails, courrriers et contact web. 

  La mesure s’effectue entre la date de réception par ATMB du courrier client (papier ou électronique) et la date de réponse des services ATMB (papier ou électronique).
  
  La réponse considérée est la 1ère réponse sur le fond et non une réponse d’attente. Un suivi permanent des réponses est effectué par ATMB qui calcule les pourcentages de réponses se situant dans les seuls admissibles.

Périmètre mesuré
  L'ensemble des sollicitations écrites pour ATMB. 

Méthode de calcul
  Avant de calculer le délai de réponse, vous devez faire une extraction de données réalisée par Power Automate. 
  
    *Power Automate est un outil permettant d'automatiser des extractions de données (un mini ETL) depuis Dynamics. L'extraction de données conçue spécifiquement pour l'indicateur sur le délai de réponse est détaillée plus loin.*
  
  Après avoir extrait les données, vous devez prendre en compte un ensemble de règles métier qui permettent de qualifier les sollicitations écrites. L'indicateur doit prendre en compte les règles suivantes : 
  
  - Prendre en compte les incidents au statut ``Résolu`` et ``Actif``;
  - Prendre en compte les incidents dont la variable ``Origine``:
  
    - ``Web``,
    - ``Formulaire contact (Web)``,
    - ``Courrier libre``, 
    - ``E-mail``, 
    - ``Carte "Parcours le plus long``,
    - ``Content / Pas content``.

  L'indicateur doit exclure les incidents suivants: 
  
  - Exclure les incidents au statut ``Annulé``,
  - Exclure les incidents dont la variable ``Origine``:
  
    - ``téléphone``, 
    - ``visite``, 
    - ``Facebook``, 
    - ``IoT``, 
    - ``Twitter``, 
    - ``péage``.
  - Exclure les incidents de type ``Niveau 1 = DEMANDE`` et ``Niveau 2 = SAV`` où ``Niveau 4`` :
  
      - ``changement de coordonnées``, 
      - ``changement DA/DM``, 
      - ``matérialisé/dématérialisé``, 
      - ``rejet CB``, 
      - ``rejet prélèvement``.
    - Exclure les incidents de type ``Niveau 1 = AUTRES`` sauf les incidents où ``Niveau 2 = "Autres" ou NULL``.
    - Exclure les incidents dont la ``date de réception`` est enregistrée en année précédente (N-1). Par exemple, si vous calculez l'indicateur pour l'année 2021, ne pas prendre en compte 
    - Exclure les incidents "enfant" où la variable ``Incident parent`` fait référence à un autre incident pour ne pas comptabiliser deux fois la même sollicitation.

Objectif
  L’indicateur est assorti d’un double objectif de résultat :
  
  * **Seuil 1** : au moins de 90% de réponses en 10 jours ouvrés au plus;
  * **Seuil 2** : au moins 98,5% de réponses en un mois calendaire au plus. 
    
  Une exception est constituée pour les événements exceptionnels générant des réclamations de masse (plus de 100 réclamations liées à un même événement).  

Mécathisme de pénalité
  Appliqué en cas de non-respect du deuxième seuil (30 jours calendaires).

Propriétaire de données
  Direction Clientèle

Source de données
  Dynamics. L'extraction de données est faite à partir de l'ETL de Power Automate. La spécification de l'ETL est disponible dans le document (A COMPLETER).

Rapport BO
  Non disponible.



Histogramme de délais de réponse aux sollicitations d'usagers (%)
-------------------------------------------------------------------

Enjeux
  Services aux usagers / respect des usagers.
  
Description
  Tracer l'histogramme des délais de réponse qui fait apparaître le pourcentage de réponses jour par jour à partir du 11ème jour.

Méthode de calcul
  Pour tracer l'histogramme, récupérer les données issues de l'indicateurs :doc:`Délai de réponse aux sollicitations écrites d'usagers`, notamment les délais de réponse et le nombre d'incidents associé. Calculer le pourcentage de réponses jour par jour à partir du 11ème jour de manière suivante :
   
.. figure:: /docs/source/Annotation_histo.png
   :width: 80%
   :align: center
   :alt: Histogramme



.. figure:: /docs/source/Annotation_tableau.png
   :width: 40%
   :align: center
   :alt: Données de calcul pour l'histogramme. 
   

Objectif
  Non défini.

Mécathisme de pénalité
  Non défini.

Propriétaire de données
  Direction Clientèle / Pôle Relation Client.

Source de données
  Extraction de données sur l'indicateur "Délai de réponse aux sollicitations des usagers". Le template pour l'histogramme est disponible ici. 
  
Rapport BO
  Non disponible.

  

Bilan des réclamations
-----------------------

Enjeux
  Services aux usagers / qualité.

Description
  Le bilan des réclamations calcule le nombre de réclamations en les classant par type de niveau : 
  - ``Niveau 2`` = ``PEAGE``, ``OFFRE DE PEAGE``, ``ACCUEIL & ASSISTANCE``, ``CONDITIONS CIRCULATION``, ``INFRASTRUCTUREs``, ``DEGÂTS A VEHICULE``, ``DEPANNAGE``;
  - ``Niveau 3`` / ``Niveau 3`` = ``passage``, ``paiement``, ``politique tarifaire``, ``disponibilité du personnel``, ``attitude du personnel``, ``disponibilité outils relations client``, ``facturation``, ``politique commerciale``, ``badge``, ``gestion du trafic``, ``signalisation``, ``information trafic``, ``dégâts à véhicule``, ``dépannage``, ``état patrimoine``, ``environnement``, ``sécurité``, ``accès PMR``, ``aires``. 

Périmètre mesuré
  L'ensemble des réclamations adressées à ATMB.
  
  - Les réclamations sont les incidents du ``Niveau 1 = RECLAMATIONS``.
  - Les régularisations sont les transactions effectuées intersociétaires.

  
  Le bilan des réclamations est annexé au rapport d'exécution de la concession au format Excel (Annexe N°20). 

Méthode de calcul
  Pour chaque niveau, comptabiliser le nombre d'incidents selon sa classification selon les règles métier suivantes:
  
  - Prendre en compte les incidents dont ``Niveau 1 = RECLAMATION`` au statut ``Résolu`` et ``Actif``.
  - Prendre en compte toutes les réclamations dont la date de réception se situe entre le 1 janvier et le 31 décembre inclus de l'année analysée. 
  - Prendre en compte uniquement les incidents "parent" et les incidents "enfants" à condiction que l'incident "enfant" est ``Niveau 1 = DEMANDE``. 
  - Prendre en compte uniquement les réclamations localisées sur le réseau d'ATMB (cf. liste spécifié dans l'annexe).
  
  - Exclure les réclamations de type ``Avis de paiement``
  - Exclure les réclamations de type ``Ticket perdu ou égaré``.
  - Exclure les réclamations de type ``CNP``.

Objectif
  Non défini.

Mécanisme de pénalité 
  Non défini.

Propriétaire de donnnées
  Direction Clientèle / Pôle Relation Client.
  
Source de données 
  Dynamics. 
  
Rapport BO
  Non disponible. 



Taux de réclamations
----------------------

Enjeux
  Services aux usagers / respect des usagers.

Description
  L'indicateur exprime le niveau de réclamations enregistrées par le service Relation Clients, exprimés en milliard.
  
Méthode de calcul
  **Taux de réclamations** est égal au nombre de réclamations en année divisé par le nombre de km parcourus en année et multiplié par 1 000 000 000, où:

  - Nombre de réclamations = nombre total de réclamations selon :ref:`Bilan des réclamations`.
  - Nombre de kilomètre parcourus  = chercher la donnée dans le rapport BO ``aaaa_aaaa -1 KMP ouvert (BOTV) + fermé (BOPR) avec régul``. 
  
Objectif
  Non défini.

Mécathisme de pénalité
  Non défini.

Propriétaire de données
  Direction Clientèle

Source de données
  Dynamics

Rapport BO
  Pour récupérer le nombre de kilomètre parcourus, consulter le rapport ``aaaa_aaaa -1 KMP ouvert (BOTV) + fermé (BOPR) avec régul``. 
