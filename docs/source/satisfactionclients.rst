Satisfaction des usagers
=========================

.. target to paragraph:

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
  
Objectif
  L’indicateur est assorti d’un double objectif de résultat :
    
    - **Seuil 1** : au moins de 90% de réponses en 10 jours ouvrés au plus;
    - **Seuil 2** : au moins 98,5% de réponses en un mois calendaire au plus. 
    
  Une exception est constituée pour les événements exceptionnels générant des réclamations de masse (plus de 100 réclamations liées à un même événement).  

Méthode de calcul
  Avant de calculer le délai de réponse, vous devez faire une extraction de données à l'aide de Power Automate. 
  
    *Power Automate est un outil permettant d'automatiser des extractions de données depuis Dynamics. Un mini ETL a été conçu spécifiquement pour l'indicateur sur le délai de réponse qui est détaillé plus loin.*
  
  Après avoir extrait les données, vous devez prendre en compte un ensemble de règles métier qui permettent de qualifier les sollicitations écrites. 
  
  L'indicateur doit **prendre en compte** les règles suivantes : 
  
  - Prendre en compte les incidents au statut ``Résolu`` et ``Actif``;
  - Prendre en compte les incidents dont la variable ``Origine``:
  
    - ``Web``,
    - ``Formulaire contact (Web)``,
    - ``Courrier libre``, 
    - ``E-mail``, 
    - ``Carte "Parcours le plus long``,
    - ``Content / Pas content``.

  L'indicateur doit **exclure** les incidents suivants: 
  
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
  - Exclure les incidents dont la ``date de réception`` est enregistrée en année précédente (N-1). *Par exemple, si vous calculez l'indicateur pour l'année 2021, ne pas prendre en compte les incidents avec la date de réception en 2020.* 
  - Exclure les incidents "enfant" où la variable ``Incident parent`` fait référence à un autre incident pour ne pas comptabiliser deux fois la même sollicitation.
  
  Le premier objectif de l'indicateur est exprimé en jours ouvrés, ce qui signifie qu'il faut exclure les week-ends et tous les jours fériés de l'année en cours d'étude. Le second objectif est exprimé en jours calendaires, donc comprend les week-ends et les jours fériés. En fonction de votre outil de calcul (Python, Excel), vous devez spécifier les jours fériés pour l'année en cours d'étude. 

.. code-block:: python
  
    class FrBusinessCalendar(AbstractHolidayCalendar):
      """ Custom Holiday calendar for France based on https://en.wikipedia.org/wiki/Public_holidays_in_France
        - 1 January: New Year's Day
        - Moveable: Easter Monday (Monday after Easter Sunday)
        - 1 May: Labour Day
        - 8 May: Victory in Europe Day
        - Moveable Ascension Day (Thursday, 39 days after Easter Sunday)
        - Moveable Pentecôte Day (Mondayn 49 days after Easter Sunday)
        - 14 July: Bastille Day
        - 15 August: Assumption of Mary to Heaven
        - 1 November: All Saints' Day
        - 11 November: Armistice Day
        - 25 December: Christmas Day
      """
        rules = [
        Holiday('New Years Day', month=1, day=1),
        EasterMonday,
        Holiday('Labour Day', month=5, day=1),
        Holiday('Victory in Europe Day', month=5, day=8),
        Holiday('Ascension Day', month=1, day=1, offset=[Easter(), Day(39)]),
        Holiday('Pentecote Day', month=1, day=1, offset=[Easter(), Day(49)]),
        Holiday('Bastille Day', month=7, day=14),
        Holiday('Assumption of Mary to Heaven', month=8, day=15),
        Holiday('All Saints Day', month=11, day=1),
        Holiday('Armistice Day', month=11, day=11),
        Holiday('Christmas Day', month=12, day=25)
    ]

Une fois que vous avez préparé le dataset de référence intégrant toutes les règles mentionnées plus haut, vous devez créer deux nouvelles variables :

    ``delai_calendaire`` = ``Première réponse d'ici`` - ``date de réception`` 
    
    ``delai_jours_ouvres`` = ``Première réponse d'ici`` - ``date de réception`` | *sans week-ends / jours fériés*

.. code-block:: python
    
    # Délai de réponse en jours calendaire
    df['delai_calendaire'] = df['Première réponse d\'ici'] - df['Date de réception']
    
        
    # Créer les limites calendaires, par exemple pour l'année 2021. 
    from datetime import date

    year = 2021
    start = date(year, 1, 1)
    end = start + pd.offsets.MonthEnd(12)

    # Instancier le calendtrier des jours fériés en France
    cal = FrBusinessCalendar()
    
    # Lister les jours fériés entre deux dates
    holidays_fr = cal.holidays(start=start, end=end)
    
    # Définir les variables de calcul
    A = [d.date() for d in df['Date de réception']] 
    B = [d.date() for d in df['Première réponse d\'ici']]
    
    # Calculer le délai de réponse pour chaque incident en excluant les week-end et les jours fériés.
    df['delai_jours_ouvres'] = np.busday_count(A, B, holidays=holidays_fr) 
    
Finalement, vous devez compter **le pourcentage d'incidents ayant reçu une réponse dans le délai de moins de 10 jours ouvrés** (réf. à la variable ``delai_jours_ouvres``) par rapport au nombre total d'incidents et **le pourcentage d'incidents ayant reçu une réponse en moins de 30 jours calendaires** (réf. à la variable ``delai_calendaire``) par rapport au nombre total d'incidents. 

Mécathisme de pénalité
  Appliqué en cas de non-respect du deuxième seuil (30 jours calendaires).

Propriétaire de données
  Direction Clientèle / Pôle Relation Client.

Source de données
  Dynamics + Power Automate. La spécification de l'ETL est disponible dans le document (A COMPLETER).

Rapport BO
  Non disponible.



Histogramme de délais de réponse aux sollicitations d'usagers (%)
-------------------------------------------------------------------

Enjeux
  Services aux usagers / respect des usagers.
  
Description
  Tracer l'histogramme des délais de réponse qui fait apparaître le pourcentage de réponses jour par jour à partir du 11ème jour.

Méthode de calcul
  Pour tracer l'histogramme, récupérer les données issues de l'indicateurs :ref:`Délai de réponse aux sollicitations écrites d'usagers <target to paragraph>`, notamment les délais de réponse et le nombre d'incidents associé. Calculer le nombre d'incidents cumulé et le pourcentage de réponses pour chaque délai puis tracer l'histogramme jour par jour à partir du 11ème jour. 
 
.. figure:: /docs/source/Annotation_tableau.png
   :width: 40%
   :align: center
   :alt: Données de calcul pour l'histogramme. 

*Données de calcul pour l'histogramme.*

.. figure:: /docs/source/Annotation_histo.png
   :width: 80%
   :align: center
   :alt: Histogramme 
    
 *Histogramme: "% de réponses apportés en 2021"*

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
  Le bilan des réclamations met en lumière les motifs de réclamation qui ont poussé les usagers à écrire à ATMB. 
  
Périmètre mesuré
  L'ensemble des réclamations adressées à ATMB. Dans le bilan des réclamations on distingue deux types de sollicitation :
  
  - Réclamations : addréssées par les usagers à ATMB, ce sont les incidents de type RECLAMATION (la variable ``Niveau 1 = RECLAMATIONS``). Pour compter les réclamations, récupérer les données issues de l'indicateurs :ref:`Délai de réponse aux sollicitations écrites d'usagers`.
  - Régularisations : les transactions effectuées entre les SCA. Tous les mois les SCA envoient un fichier Excel comprenant toutes les régularisations faites pour le compte ATMB. Le service de facturation d'ATMB transmet également les régularisations passées.  

Méthode de calcul
  Pour chaque niveau, comptabiliser le nombre d'incidents selon sa classification  les règles métier suivantes:
  
  - Prendre en compte les incidents dont ``Niveau 1 = RECLAMATION`` au statut ``Résolu`` et ``Actif``.
  - Prendre en compte toutes les réclamations dont la date de réception se situe entre le 1 janvier et le 31 décembre inclus de l'année analysée. 
  - Prendre en compte uniquement les incidents "parent" et les incidents "enfants" à condiction que l'incident "enfant" est ``Niveau 1 = DEMANDE``. 
  - Prendre en compte uniquement les réclamations localisées sur le réseau d'ATMB (cf. liste spécifié dans l'annexe).
  
  - Exclure les réclamations de type ``Avis de paiement``
  - Exclure les réclamations de type ``Ticket perdu ou égaré``.
  - Exclure les réclamations de type ``CNP``.

Le bilan des réclamations classe les réclamations par type : 
  - ``Niveau 2`` = ``PEAGE``, ``OFFRE DE PEAGE``, ``ACCUEIL & ASSISTANCE``, ``CONDITIONS CIRCULATION``, ``INFRASTRUCTUREs``, ``DEGÂTS A VEHICULE``, ``DEPANNAGE``;
  - ``Niveau 3`` = ``passage``, ``paiement``, ``politique tarifaire``, ``disponibilité du personnel``, ``attitude du personnel``, ``disponibilité outils relations client``, ``facturation``, ``politique commerciale``, ``badge``, ``gestion du trafic``, ``signalisation``, ``information trafic``, ``dégâts à véhicule``, ``dépannage``, ``état patrimoine``, ``environnement``, ``sécurité``, ``accès PMR``, ``aires``. 
  -  ``Niveau 4`` = ...
  
  Le template du bilan des réclamations est annexé au rapport d'exécution de la concession au format Excel.. 

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

  - Nombre de réclamations = nombre total de réclamations selon :doc:`Bilan des réclamations`.
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
