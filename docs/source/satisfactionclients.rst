Satisfaction des clients
=========================

Délai de réponse aux sollicitations écrites d'usagers
--------------------------------------------------------

Enjeux
  Services aux usagers / respect des usagers.

Description
  L’indicateur permet d’évaluer la réactivité de ATMB dans ses réponses aux sollicitations des clients – mails, courrriers et contact web. 

Méthode
  La mesure s’effectue entre la date de réception par ATMB du courrier client (papier ou électronique) et la date de réponse des services ATMB (papier ou électronique). La réponse considérée est la 1ère réponse sur le fond et non une réponse d’attente. Un suivi permanent des réponses est effectué par ATMB qui calcule les pourcentages de réponses se situant dans les seuls admissibles.

Périmètre mesuré
  L'ensemble des sollicitations écrites pour ATMB. 

Objectif
  L’indicateur est assorti d’un double objectif de résultat :
  
    Seuil 1 : au moins de 90% de réponses en 10 jours ouvrés au plus
    
    Seuil 2 : au moins 98,5% de réponses en un mois calendaire au plus
    
  Une exception est constituée pour les événements exceptionnels générant des réclamations de masse (plus de 100 réclamations liées à un même événement).  

Méthode de calcul :

  Pour calculer l'indicateur, il faut prendre en compte les règles métier suivantes :
    - Prendre en compte les incidents au statut ``Résolu`` et ``Actif``.
    - Prendre en compte les incidents dont la variable ``Origine`` est égale à:
        - ``Web``, 
        - ``Formulaire contact (Web)``, 
        - ``Courrier libre``, 
        - ``E-mail``, 
        - ``Carte "Parcours le plus long``, 
        - ``Content / Pas content``.
    - Prendre en compte uniquement les incidents "parent" et non "enfant" pour ne pas comptabiliser deux fois la même demande. La variable ``Incident parent = NULL``.

  L'indicateur exclut les cas de figure suivants : 
    - Exclure les incidents au statut ``Annulé``.
    - Exclure les incidents dont la variable ``Origine`` est égale à :
        - ``téléphone``, 
        - ``visite``, 
        - ``Facebook``, 
        - ``IoT``, 
        - ``Twitter``, 
        - ``péage``.
    - Exclure les incidents de type ``Niveau 1 = DEMANDE`` et ``Niveau 2 = SAV`` où ``Niveau 4`` est égale
        - ``changement de coordonnées``, 
        - ``changement DA/DM``, 
        - ``matérialisé/dématérialisé``, 
        - ``rejet CB``, 
        - ``rejet prélèvement``.
    - Exclure les incidents du ``Niveau 1 = AUTRES`` sauf les incidents dont le ``Niveau 2 = "Autres" ou NULL``.
    - Exclure les incidents dont la ``date de réception`` est spécifié en année (N-1).
  

Mécathisme de pénalité
  Appliqué en cas de non-respect du deuxième seuil (30 jours calendaires).

Propriétaire de données
  Direction Clientèle

Source de données
  Dynamics. L'extraction de données est faite à partir de l'ETL de Power Automate. La spécification de l'ETL est disponible dans le document (A COMPLETER).

Rapport BO
  ``Non existant``

Histogramme de délais de réponse aux sollicitations de clients (%)
-------------------------------------------------------------------

Enjeux
  Services aux usagers / respect des usagers.
  
Description
  Tracer l'histogramme des délais de réponse qui fait apparaître le pourcentage de réponses jour par jour à partir du 11ème jour.

Méthode de calcul
  Pour tracer l'histogramme, récupérer les données issues de l'indicateurs "Délai de réponse aux sollicitations écrites de clients", notamment les délais de réponse et le nombre d'incidents associé. Calculer le pourcentage de réponses jour par jour à partir du 11ème jour de manière suivante ::
  
   1. Calculer une colonne "Nombre d'incidents cumulé"
   2. Pour calculer le délai de réponse en %, diviser le nombre d'incidents cumulé pour chaque durée (en jours) par le nombre total d'incidents.
   
Welcome!

.. figure:: docs/source/Annotation_histo.png
   :width: 80%
   :align: center
   :alt: Histogramme
   
Objectif
  NA

Mécathisme de pénalité
  NA

Propriétaire de données
  Direction Clientèle 

Source de données
  Extraction de données sur l'indicateur "Délai de réponse aux sollicitations des clients". 
  
Rapport BO
  ``Non existant``

  

Bilan des réclamations
-----------------------

Enjeux
  Services aux usagers / qualité.

Description
  Faire un bilan des réclamations réçues par ATMB: 
    
    Les réclamations sont les incidents du ``Niveau 1 = RECLAMATIONS``.
    
    Les régularisations sont les transactions effectuées intersociétaires.

Périmètre mesuré
  L'ensemble des réclamations pour ATMB (tous
  
  Le bilan des réclamations calcule le nombre de réclamations par type de niveau : ``péage / passage``, ``péage / paiement``, ``disponibilité du personnel``, ``attitude du personnel``, ``disponibilité outils relations client``, ``facturation``, ``politique commerciale``, ``badge``, ``gestion du trafic``, ``signalisation``, ``information trafic``, ``dégâts à véhicule``, ``dépannage``, ``état patrimoine``, ``environnement``, ``sécurité``, ``accès PMR``, ``aires``. 
  
  Le bilan des réclamations est annexé au rapport d'exécution de la concession (Annexe N°20). 

Méthode de calcul::

  Pour chaque ``Niveau``, comptabiliser le nombre d'incident  Utiliser le template Excel disponible ici. 
  
Prendre en compte les règles métier suivantes
- Prendre en compte les réclamations au statut ``Résolu`` e.t ``Actif``.
- Prendre en compte toutes les réclamations dont la date de réception se situe entre le 1 janvier et le 31 décembre inclus de l'année analysée. 
- Prendre en compte uniquement les incidents "parent" et les incidents "enfants" à condiction que l'incident "enfant" est ``Niveau 1 = DEMANDE``. 
- Prendre en compte uniquement les réclamations localisées sur le réseau d'ATMB (cf. liste spécifié dans l'annexe)

- Exclure les réclamations de type ``Avis de paiement``
- Exclure les réclamations de type ``Ticket perdu ou égaré``.
- Exclure les réclamations de type ``CNP``.

Objectif
  NA

Mécanisme de pénalité 
  NA

Propriétaire de donnnées
  Direction Clientèle 
  
Source de données 
  Dynamics. 
  
Rapport BO
  ``Non existant``



Taux de réclamations
----------------------

Enjeux
  Services aux usagers / respect des usagers.

Description
  L'indicateur exprime le niveau de réclamations enregistrées par le service CRC, exprimés en milliard.
  
Méthode de calcul
  Taux de réclamations = (Nombre de réclamations en année / nombre de km parcourus en année) * 1 000 000 000. 
  
  Nombre de réclamations = nombre total de réclamations selon le bilan des réclamations (Xxxx ajouter une ref à l'indicateur).
  Nombre de kilomètre parcourus  = chercher la donnée dans le rapport BO ``aaaa_aaaa -1 KMP ouvert (BOTV) + fermé (BOPR) avec régul``. 
  
Objectif
  NA

Mécathisme de pénalité
  NA

Propriétaire de données
  Direction Clientèle

Source de données
  Dynamics

Rapport BO
  ``Non existant``




Qualité des aires de repos
---------------------------

Enjeux
  Services aux usagers - Confort / agrément.
  
Description
  Qualité des aires de repos sur les paramètres essentiels en vue de la satisfaction des usagers.          

.. note::

   Les évaluations sont réalisées et consolidées sous la responsabilité directe de l’autorité concédante puis envoyées à ATMB.
   
   Premier audit à blanc prévu en 2022, à partir de 2023 l'indicateur sera pénalisable si une aire de repos est notée <=12.

Méthode de calcul
  L’indicateur mesure le niveau de prestations et d' entretien des équipements essentiels des aires de repos (toilettes, parkings, aires de jeu, zones de pique-nique et de détente) en matière de : disponibilité, état, propreté et accessibilité.
  La liste exhaustive des équipements et critères est fournie dans le référentiel joint au contrat d’entreprise: fiche de visite sous forme de grille de notation et notice explicative.   

Périmètre
  Chaque année, au moins une aire de repos est auditée. Les visites ne sont pas effectuées lors des périodes de “jours noirs” du calendrier Bison futé.  
Une aire obtenant une note inférieure ou égale à 12 lors d’une visite fera l’objet d’une seconde visite dans l’année, qui aura lieu au plus tôt un mois après la transmission à ATMB par l’autorité concédante de la grille de notation relative à l’aire de repos concernée. Seule la meilleure des deux notes obtenues sera prise en compte pour la validation de l’objectif.      

Objectif
  A compter de l’année 2022, aucune aire ne doit obtenir une note de <=12. Un audit à blanc est prévu en 2022.
  
Mécathisme de pénalité
  Une pénalité est appliquée annuellement, à compter de l’année 2023, pour chaque aire obtenant une note inférieure à l’objectif.   

Responsable
  Les évaluations sont réalisées et consolidées sous la responsabilité directe de l’autorité concédante.

Source de données
  Non disponible

