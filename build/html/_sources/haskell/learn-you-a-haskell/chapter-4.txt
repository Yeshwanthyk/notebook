=========
Chapter 4
=========

* Pattern matching is shown with the example in **factorial.hs**
* We should always try to have a catch-all pattern in order to avoid errors.
* Catch-all examples

.. code-block:: haskell

        first :: (a,b,c) -> a
        first(x,_,_)    = x

        second :: (a,b,c) -> b
        first(_,y,_)    = y

* We can pattern match in list comprehensions. If a match fails, it ignores and moves to the next one:

.. code-block:: haskell

        let xs = [(1,3), (4,5), (7,8)]
        [a+b | (a,b) <- xs]

* You can write patterns for breaking up something into names whilst still keeping a reference to the whole thing:

.. code-block:: haskell

        capital :: String -> String
        capital "" = "Empty string"
        capital all@(x:xs) = "The first letter of" ++ all ++ "is" ++ x

* Pipes **|** in functions which are akin to if statements:

.. code-block:: haskell

        bmiTell :: (RealFloat a) => a -> String
        bmiTell weight height
            | weight / height ^ 2<= 18.5 = "You're underweight"
            | weight / height ^ 2<= 28 = "Normal"
            | otherwie = "You're are a whale."

* There is no **=** after the function name and its parameters before the first guard.
* Instead of repeating across the code base we can use **where**:

.. code-block:: haskell

        bmiTell :: (RealFloat a) => a -> String
        bmiTell bmi
            | bmi <= skinny = "You're underweight"
            | bmi <= normal = "Normal"
            | otherwie = "You're are a whale."
            where bmi = weight / height ^ 2
                  skinny = 18.5
                  normal = 25.0

* The **where** does not pollute other namespaces. And pattern matching can be used in **where**
* **let <bindings> in <expression>** are similar to **where** except
    - they are expressions themselves.
    - they can be used by functions in local scope:

    .. code-block:: haskell

            (let (a,b,c) = (1,2,3) in a+b+c) * 100 -- 600

            [let square x = x * x in (square 5, square 3, square 2)] -- [(25,9,4)]

    - You can put **let** in list comprehensions:

    .. code-block:: haskell

            calcBmis :: (RealFLoat a) => [(a,a)] -> [a]
            calcBmis xs = [bmi | (w,h) <- xs, let bmi = w/h ^ 2, bmi > 25.0]

* We can do pattern matching for **case expressions**:

.. code-block:: haskell

        describeList :: [a] -> String
        describeList xs = "The list is" ++ case xs of [] -> "empty"
                                                      [x] -> "singleton list"
                                                      [xs] -> lomger list
