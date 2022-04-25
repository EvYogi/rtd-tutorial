Chaussées
=====

.. _installation:

Etat de la structure des chaussées
------------

Enjeux
------------

Conservation du patrimoine.

Description 
------------

L’indicateur mesure l’état structurel des chaussées.

Méthode de calcul
-------------------

L’indicateur « ISTRU » calcule la proportion des chaussées en état structurel dégradé, en croisant deux indices intermédiaires résultats de la combinaison d’index unitaires de dégradation de surface et d’uni petites ondes dont les principes sont exposés en annexe à la présente fiche. 
La périodicité d’auscultation est de 3 ans. 
Les voies lentes dans les deux sens de circulation des sections courantes d’autoroutes à l’exclusion notamment des bifurcations, des échangeurs, des aires et des plateformes de péage.  

Objectif
------------
NA

Mécanisme de pénalité 
-----------------------
NA

Propriétaire de donnnées
-------------
2D2I

Source de données 
------------------

Fichiers Excel fournit par le prestataire et stockés sur le réseau. En 2021, le prestataire était NextRoad et en 2021 Ginger. 






To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache



Ouvrages d'art
----------------

Etat des ouvrages d’art (ouvrages d'ouverture >2m)

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

