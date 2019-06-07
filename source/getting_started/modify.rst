Modify Distribution
===================

Distribution Variables?
-----------------------

Explain the head - create a new example dist


Adding a Project
----------------

To add a specific project version you can use the shorthand::

    - name@version


Setting Parameters
..................

Example, setting a jenkins build timeout:

.. code-block:: YAML

    - name: pcl
      version: pcl-1.8.0
      parameters:
        timeout/minutes: 600


