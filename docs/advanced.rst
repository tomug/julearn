.. include:: links.inc

Advanced Topics
===============

The following sections are advanced topic which do not need to be read
for a lot of usecases, but still provide some context for those who want it.

Column Type System
******************

Context
^^^^^^^
To be able to discriminate between different types of variables Julearn
uses a Column Type System. This system currently distinguishes between
continuous variables/features, categorical variables/features and confounds.

.. note::
  On most levels of Julearn this Column Type System is only used internally.
  Therefore, users do not have to work with it directly.
  For example, by providing the confounds and categorical variables to the
  :class:`.ExtendedDataFramePipeline` it has all the information needed to
  apply the Column Type System internally without any further input or changes
  to the `pandas.DataFrame`.

How it works
^^^^^^^^^^^^
Every `pandas.DataFrame`_ column has a column name.
Inside of Julearn we add another string containing the type of the column
separated by our delimiter: ``'__:type:__'`` to the original column names.
For example:

  * We have the original columns :

    - ``'Intelligence'``
    - ``'Age'``
    - ``'LikesEvoks'``

  * We know:

    - Intelligence is a **continuous** variable
    - Age is a **confound**
    - LikesEvoks is a **categorical** variable.
      Either someone likes Evoks or not.
  * Inside of Julearn's Column Type System we can provide this information
    by changing the column names to:

      - ``'Intelligence__:type:__continuous'``
      - ``'Age__:type:__confound'``
      - ``'LikesEvoks__:type:__categorical'``

Dynamic Selection (DS)
**********************
Dynamic selection as implmented in julearn is directly taken from the 
developers of DESlib. This class provides techniques for dynamic as well as 
static classifier or ensemble selection. If you want to check out the original 
documentation check `DESlib.doc`_. 

What is Dynamic Classifier Selection (DCS)?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
These implement techniques which only the base classifier with the highest 
competence level for the classification of the query.

What is Dynamic Ensemble Selection (DES)?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
"Dynamic ensemble selection strategies refer to techniques that select an 
ensemble of classifier rather than a single one. All base classifiers that 
attain a minimum competence level are selected to compose the ensemble of 
classifiers." (Directly taken from DESlib Docs)

What are Static ensembles?
^^^^^^^^^^^^^^^^^^^^^^^^^^
These techniques implement a set of static ensemble methods like Single Best, 
Static Selection and Stacked classifier.

Selection Methods
^^^^^^^^^^^^^^^^^

.. list-table::
   :widths: 30 30 70 30 
   :header-rows: 1

   * - Name (str)
     - Description
     - Model type
     - Class
   * - ``OLA``
     - Overall Local Accuracy (OLA) 
     - DCS
     - `OLA`_
   * - ``MCB``
     - Multiple Classifier Behaviour (MCB)  
     - DCS
     - `MCB`_
   * - ``DESP``
     - Dynamic Ensemble Selection performance (DES-P) 
     - DES
     - `DES-P`_ 
   * - ``METADES``
     - Meta learning for dynamic ensemble selection
     - DES
     - `METADES`_
   * - ``KNORAU``
     - k-Nearest Oracle Union (KNORA-U)
     - DES
     - `KNORA-U`_ 
   * - ``KNORAE``
     -  k-Nearest Oracle-Eliminate (KNORA-E) 
     - DES
     - `KNORA-E`_    
   * - ``KNOP``
     - k-Nearest Output Profiles (KNOP)  
     - DES
     - `KNOP`_
   * - ``SingleBest``
     - Selects a single classifier out of the pool with highest score
     - Static
     - `SingleBest`_
   * - ``StaticSelection``
     - Ensemble model that selects N classifiers with the best performance 
     - Static
     - `StaticSelection`_
   * - ``StackedClassifier``
     - Stacked classifier
     - Static
     - `StackedClassifier`_