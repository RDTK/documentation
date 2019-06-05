.. _specification-language:

========================
 Language Specification
========================

Concrete Syntax
===============

.. productionlist::
   expression         : `text`
                      : `variable_reference`
   variable_reference : "${" `expression` ("|" `expression`)?"}"
                      : "@{" `expression` ("|" `expression`)?"}"

Abstract Syntax
===============

Values
------

Values that evaluating a "variable expression" can result
in. Basically atomic values of type ``string``, ``real`` or
``boolean`` as well as lists and dictionaries of those:

.. productionlist::
   value        : `atomic_value`
                : `list_value`
                : `dict_value`
   atomic_value : string
                : real
                : boolean
   list_value   : list (`value`)*
   dict_value   : dict (`entry_value`)*
   entry_value  : entry string `value`

Unevaluated Expressions
-----------------------

In addition to atomic values (of type ``string``, ``real`` or
``boolean``) and compound list, dictionaries and concatenation
expressions, these expressions can contain several kinds of variable
references:

.. productionlist::
   expression         : `atomic_value`
                      : `variable_reference`
                      : `concatenation`
                      : `list`
                      : `dict`
   variable_reference : ref      `expression` (default `expression`)?
                      : ref/list `expression` (default `expression`)?
   concatenation      : concat (`expression`)*
   list               : list (`expression`)*
   dict               : dict (`dict_entry`)*
   dict_entry         : entry `expression` `expression`

Semantics
=========

small-step operational semantics https://en.wikipedia.org/wiki/Operational_semantics#Small-step_semantics

In this context, evaluation translates to computing the effective
value of variables which mainly consists of evaluating "variable
expressions" in the context of a set of variable bindings.

The following functions are involved:

value : context, name -> value

  The function `value' performs such an effective value
  computation by coordinating the `lookup' and `expand' function.

lookup : context, name -> variable expression, variable expressions

  `lookup' computes the value of a variable given a set of
  variable bindings.

expand : variable expression, lookup function -> value

  `expand' computes the value of a "variable expression" relying
  on `lookup' to resolve variable references.

TODO which "value" should we use here?

Scalar Variable References
--------------------------

.. parsed-literal::

   :token:`expression` → :token:`expression`'
   ────────────────────────────────                               ScalarRefNoDefaultEvalName
   ref expression → ref expression'

   C ⊢ value ← string
   ──────────────────                                             ScalarRefNoDefaultExpand
   ref string → value

   C ⊢ list expression₁ … ← string
   ───────────────────────────────────────────────────────        ScalarRefNoDefaultTODO
   concat … (ref string) … → list (list … expression₁ …) …

List Variable References
------------------------

.. parsed-literal::

   expression → expression'
   ──────────────────────────────────────────                           ListRefNoDefaultEvalName
   ref/list expression → ref/list expression'

   C ⊢ value ← string TODO still needed?
   ───────────────────────                                              ListRefNoDefaultExpand
   ref/list string → value

   TODO isn't this an error?
   C ⊢ expression₁ ← string, expression₁ → string₂
   ─────────────────────────────────────────────────────────────────    ListRefNoDefaultTODO
   concat string₁ … (ref/list string) … → concat string₁ … string₂ …

   C ⊢ list expression₁ … ← string
   ───────────────────────────────────────────────────────              ListRefNoDefaultTODO
   concat … (ref/list string) … → concat … expression₁ … …

   C ⊢ list expression₁ … ← string
   ───────────────────────────────────────────────────                  ListRefNoDefaultTODO
   list … (ref/list string) … → list … expression₁ … …

Concatenation
-------------

.. parsed-literal::

   expression → expression', …
   ──────────────────────────────────────────────    ConcatEvalParts
   concat … expression … → concat … expression' …

   concat value → value                              ConcatSingleton

   concat string₁ … → "string₁…"                     ConcatExpand

List
----

.. parsed-literal::

   expression → expression', …
   ──────────────────────────────────────────    ListEvalParts
   list … expression … → list … expression' …
