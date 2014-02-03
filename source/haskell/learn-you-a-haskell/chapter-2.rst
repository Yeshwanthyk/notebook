==========
Chapter 2
==========

----------------
Lists and Tuples
----------------

* Can't mix various types in lists
* An **If** function should always have an else block
* List can be joined together using **++**; but have to noted that when we do
  that haskell has to traverse the whole list on the left hand side.
* we can use **":"** which is the **cons** operator

.. code-block:: haskell

    5:[1,2,3] -- [5,1,2,3]

* We can use ***"!!"*** to get the index of a list. (Strings are basically lists!!)
* **Lists**
    - **head** takes a list and returns the first element.
    - **tail** takes a list and returns the all the element except the first one.
    - **last** takes a list and returns the last element.
    - **init** takes a list and returns everything except the last element.
    - **reverse** reverses the list
    - **take** takes an number and a list and returns that mn=any elemnts from the list. If index doesn't exist throws an error.
    - **drop** does what take does but gives all elements minus what the index given

.. code-block:: haskell

        drop 3 [1,2,3,4,5,6] -- [4,5,6]

        drop 100 [1,2,3] -- []

* **null** gives wheather is list is null or not
* **minimum**, **maximum**, **product** and **sum** work on lists.

* **Ranges**
    - **cycle** takes a list and cycles it infinitely:
    - **repeat** takes an element and produces it infinitely

.. code-block:: haskell

    [1..10] -- [1,2,3,4,5,6,7,8,9,10]

    [2,4..10] -- [2,4,6,8,10]

    take 5 (cycle[1,2]) -- [1,2,1,2,1]

* **List Comprehension**

    - The last condition is called the predicate. It is also called **filtering**
        .. code-block:: haskell

            [x * 2 | x <- [1..10], x * 12] -- [12,14,16,18,20]

    - We have created a function where we take odd numbers. If they are greater than 10 print "BANG!" else "BOOM!"

        .. code-block:: haskell

            boomBangs xs = [if x <10 then "BOOM!" else "BANG!!" | x <- xs, odd x]

    - We can give two inputs:

        .. code-block:: haskell

            [x*y | x <- [2,5,10], y <- [8,10,11], x*y > 60] -- [55,80,100,110]

    - Strings are lists too:

        .. code-block:: haskell

            removeNonUpperCase st = [c | c <- st, c `elem` [`A`..`Z`]]

    - In GHCI (`Reference`_) :

        .. code-block:: haskell

            let removeNonUpperCase st = [c | c <- st, c `elem` [`A`..`Z`]]


* **Tuples**
    - A tuple can contain different types, unlike a list.
    - But a tuple of fixed size is its own type. Which means, we cannot have:

        .. code-block:: haskell

            [(1,2), (3,4,5), (6,7)] -- Error

    - Like lists **fst** gives first element, **snd** gives second element. Does not works on triples, 4-tuples and soon
    - **zip** is a super cool function:

        .. code-block:: haskell

            zip [1,2,3] [4,5,6,7] -- [(1,4), (2,5), (3,6)]

            zip [1..] ["apples" "bananas" "cherry"] -- [(1,"apple"),(2,"bananas"),(3,"cherry")]

* Prob, which right triangle has integers for all sides to or smaller than 10 and has a perimeter of 24. This problem is solved in steps:

        .. code-block:: haskell

            let triangle = [(a,b,c)| c <- [1..10], b <- [1..10], c <- [1..10]

            let rightTriangle = [(a,b,c) | c<-[1..10], b<-[1..c], a <- [1..b], a^2 + b^2 = c^2, a+b+c == 24]

.. _Reference: http://stackoverflow.com/questions/6184940/hakell-error-parse-error-on-input