﻿.. currentmodule:: Node


addStyleSheet
========================================

.. versionadded:: 1.2

Module
-----------------------------------------------

  :mod:`Node`



Methods
-----------------------------------------------

或许根本不需要此方法，只需

.. code-block:: javascript

    var $=KISSY.all;    
    var styleEl = $("<style>p {color:red}</style>").appendTo("head");