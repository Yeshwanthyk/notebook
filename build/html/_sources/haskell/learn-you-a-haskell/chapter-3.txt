=========
Chapter 3
=========

-----
Types
-----

* Haskell has ***type inference***. This just means that haskell can infer on its own without us explicitly telling it what the type of a function or a expression is.
* It is good practice to define the type of a function. Except for small fucntions.
* We can use **:t** in GHCI to find out the type:

.. code-block:: haskell

    > :t "Hello!" -- "Hello!" :: [Char]

* A string is a **[Char]** type because it is a list of characters:

.. code-block:: haskell

        > : "a" -- "a" :: Char

* Taking the removeNonUpperCase fn from Chapter 2:

.. code-block:: haskell

        removeNonUpperCase st = [c | c <- st, c `elem` [`A`..`Z`]]

Its type would be:

.. code-block:: haskell

        removeNonUpperCase :: [Char] -> [Char]

It means that it maps from a string to a string.
* What happens when we have multiple parameters?:

    .. code-block:: haskell

            addThree :: x y z = x + y + z

    Type:

    .. code-block:: haskell

        addThree :: Int -> Int -> Int -> Int

* Common types are:
    - **Int** used for whole numbers. It is bounded, which means it has a min and max.
    - **Integer** unbounded. **Int** is more efficient
    - **Float** and **Double**
    - **Bool**
    - **Char**

-------------------
Generics in haskell
-------------------

    - :t head

    .. code-block:: haskell

            head :: [a] -> a

    which means that given any "a" it would output a single "a"

    - ^^^ "a" is a ***type variable***

-----------
Typeclasses
-----------

  - :t (==)

  .. code-block:: haskell

        (==) :: (Eq a) => a -> a -> Bool

  - Everything before => is called ***class constant***
  - Complex topic. `Extra Reading`_

.. _Extra Reading: http://book.realworldhaskell.org/read/using-typeclasses.html
