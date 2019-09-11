Elm
****

.. code-block:: Elm

    isNegative n = n < 0

    isNegative 4 -- true

    -- Anon fns
    \n -> n < 0

    over9000 powerLevel = if powerLevel > 9000 then "It's over 9000!!!" else "meh"

------
Lists
------

.. code-block:: Elm

   names = [ "Alice", "Bob", "Chuck" ]

   List.isEmpty names

   List.length names

   List.reverse names

   double n = n * 2

   nums = [2, 3, 5]

   List.map double nums 

------
Tuples
------