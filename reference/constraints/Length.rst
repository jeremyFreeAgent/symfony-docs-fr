Length
======

Valide que la longueur d'une chaîne de caractères donnée se situe *entre* une
valeur minimum et une valeur maximum.

.. versionadded:: 2.1
    La contrainte Length a été ajoutée dans Symfony 2.1.

+----------------+----------------------------------------------------------------------+
| S'applique à   | :ref:`propriété ou méthode<validation-property-target>`              |
+----------------+----------------------------------------------------------------------+
| Options        | - `min`_                                                             |
|                | - `max`_                                                             |
|                | - `charset`_                                                         |
|                | - `minMessage`_                                                      |
|                | - `maxMessage`_                                                      |
|                | - `exactMessage`_                                                    |
+----------------+----------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Length`          |
+----------------+----------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\LengthValidator` |
+----------------+----------------------------------------------------------------------+

Utilisation de base
-------------------

Pour vérifier que la longueur du champ ``firstName`` d'une classe se situe entre
« 2 » et « 50 », vous pouvez procéder comme suit :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/EventBundle/Resources/config/validation.yml
        Acme\EventBundle\Entity\Participant:
            properties:
                firstName:
                    - Length:
                        min: 2
                        max: 50
                        minMessage: Votre nom doit faire au moins 2 caractères
                        maxMessage: Votre nom ne peut pas être plus long que 50 caractères

    .. code-block:: php-annotations

        // src/Acme/EventBundle/Entity/Participant.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Participant
        {
            /**
             * @Assert\Length(
             *      min = "2",
             *      max = "50",
             *      minMessage = "Votre nom doit faire au moins 2 caractères",
             *      maxMessage = "Votre nom ne peut pas être plus long que 50 caractères"
             * )
             */
             protected $firstName;
        }

Options
-------

min
~~~

**type**: ``integer`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est la valeur de la longueur « minimale ». La validation échouera
si la longueur de la donnée saisie est **plus petite** que cette valeur minimale.

max
~~~

**type**: ``integer`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est la valeur de la longueur « maximale ». La validation échouera
si la longueur de la donnée saisie est **plus grande** que cette valeur maximale.

charset
~~~~~~~

**type**: ``string``  **default**: ``UTF-8``

Le charset qui sera utilisé pour calculer la longueur de la valeur. La fonction PHP
:phpfunction:`grapheme_strlen` est utilisée si elle est disponible. Sinon, la fonction PHP
:phpfunction:`mb_strlen` est utilisée si elle est disponible. Si aucune de ces deux fonctions
n'est disponible, la fonction :phpfunction:`strlen` sera utilisée.

minMessage
~~~~~~~~~~

**type**: ``string`` **default**: ``This value is too short. It should have {{ limit }} characters or more.``.

Le message qui sera affiché si la longueur de la valeur saisie est inférieur à l'option `min`_.

maxMessage
~~~~~~~~~~

**type**: ``string`` **default**: ``This value is too long. It should have {{ limit }} characters or less.``.

Le message qui sera affiché si la longueur de la valeur saisie est supérieur à l'option `max`_.

exactMessage
~~~~~~~~~~~~

**type**: ``string`` **default**: ``This value should have exactly {{ limit }} characters.``.

Le message qui sera affiché si les valeurs min et max sont égales, et que la longueur
de la valeur soumise n'est pas exactement cette valeur.
