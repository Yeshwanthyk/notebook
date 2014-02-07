=========
Chapter 6
=========

-----------------
Curried Functions
-----------------

* In haskell, every function officially takes only one parameter. The way we get to give several parametes to function is by having *curried function*

.. code-block:: haskell

    > max 4 5
    > (max 4) 5

    max :: (Ord a) => a-> a -> a
    max :: (Ord a) => a-> (a -> a)

* The space in between is *funciton application*
* You can write *partially applied* functions. By doing so, we are creating functions on the fly.

.. code-block:: haskell

    multiThree :: (Num a) => a-> a-> a
    multiThree x y z = x * y * z

    > let multiTwoWithNine = multiThree 9
    > multiTwoWithNine 2 3
    > 54

