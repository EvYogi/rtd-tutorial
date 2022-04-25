Ouvrages d'art
=====

.. _installation:


.. autosummary::
   :toctree: generated

   lumache
   
* This is a bulleted list.
* It has two items, the second
  item uses two lines.
  
* Enjeux

Conservation du patrimoine / sécurité des usagers.

* Description 

Etat de surface des chaussées.

* Méthode de calcul

La méthode prend en compte les mesures marco-texture, de CFT (coefficient de frottement transversal), d’uni longitudinal (ondes courtes) et d’orniérage. Ces deux index unitaires sont croisés deux à deux afin de définir un indicateur adhérence et un indicateur d’uni.
Ces deux indicateurs sont ensuite croisés à l’aide d’un système matriciel pour définir un indicateur global dénommé « indicateur de surface ». 

L’indicateur est calculé annuellement. 

L’indicateur s’applique qu’aux sections courantes d’autoroutes et exclut notamment les bifurcations, les échangeurs, les aires et les plateformes de péage. La méthode ne s’applique pas aux chaussées béton. 

Objectif
----------
L’indicateur est assorti de deux objectifs :
- Objectif 1 : au moins 90% des notes >=3
- Objectif 2 : au moins 95% des notes >=2

Mécanisme de pénalité
----------------------
La pénalité s’applique dès qu’un des deux objectifs n’est pas atteint.

Propriétaire de données
-----------------------
2D2I

Source de données
------------------

Fichiers Excel fournit par le prestataire et stockés sur le réseau. En 2021, le prestataire retenu était NextRoad et en 2021 Ginger.






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
