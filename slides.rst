.. |reg| unicode:: U+00AE .. REGISTERED TRADEMARK
.. |tm| unicode:: U+2122 .. TRADEMARK

Django on Windows
=================

Michael Manfre

----

Michael Manfre
==============

Developer at Semiconductor Research Corporation |reg|

	Pioneers in research collaboration |tm|

Maintainer of django-mssql 

	Django database backend for Microsoft SQL Server

Developer at Brewed By Us, LLC

    `http://brewedbyus.com`_ - Social home brewing web site to create and share recipes, 
    edit and evolve them, and keep a journal so you can keep a record of your brewing journey.

.. _`http://brewedbyus.com`: http://brewedbyus.com

----

Semiconductor Research Corporation |reg|
========================================

    "Semiconductor Research Corporation (SRC) is the world's leading technology research consortium. 
    With member companies and university research programs spanning the globe, SRC plays an 
    indispensable part in the R&D strategies of the industry's most influential entities. 
    SRC-sponsored university research is of the highest caliber and creates knowledge breakthroughs 
    that will invent the industries of tomorrow."
    
    -- `http://www.src.org/about/`_

.. _`http://www.src.org/about/`: http://www.src.org/about/

----

Web site purpose
================

.fx: web-site-purpose

  - Knowledge transfer
  
    - Publications
    - Reporting
    - Track research progress
    - Member feedback
  
  - Meetings & events
  - Student CV and recruitment


----

SRC's current web site
======================

.. figure:: images/homepage-screenshot.png
   :alt: SRC homepage screenshot
   :align: right

Presenter Notes
---------------

Previous distributions: Printed publications, Mailed CDs, Command line database.
  
Generated VB6 files.

----

Powered By
==========

  - Apache
  - CruiseControl.net
  - Django 1.4.1
  - HAProxy (Ubuntu)
  - Memcached
  - Mercurial (Hg)
  - Microsoft SQL Server 2008r2
  - nAnt
  - PowerShell
  - RedGate SQL schema and data compare
  - Windows

----

Why Windows?
============

  - Windows shop

    - IT knowledge

  - Legacy Business Database on MS SQL

    - Triggers, user funcs, stored procs, SSIS, SSRS
    - Replication not an option 
      (tech limitations and historical business reasons)

  - Didn't have a choice

----

Why Django?
===========

  - Previous iteration of site was VB6
  - ASP.NET workflow is a bit slower and heavier
  - Faster prototyping
  - Possibly more reasons, but decision made before I was hired

----

Why SQL Server?
===============

  - Avoid extra database replication services
  
    - SQL Server (master) <--> OpenVMS --> SQL Server (www)
      
      - SSIS jobs pump data from www to OpenVMS and master

  - Secondary factors against Django supported database _____

    - Oracle? Price
    - Postgresql? Not recommended on Windows
    - MySQL? Feature limited
    - Sqlite? Not meant for production

----

SQL Server database backends
============================

django-pyodbc
-------------

  - Cross platform
  - Any ODBC connection
  - Missing datatypes and SQL Server specific features
  - Django 1.4 fork by Alex Vidal - `https://github.com/avidal/django-pyodbc`_ 

django-mssql
------------

  - Windows only
  - SQL server specific
  - Supports more datatypes and server features
  - Supports Django 1.2 - 1.5
  - `http://bitbucket.org/Manfre/django-mssql/`_

.. _`http://bitbucket.org/Manfre/django-mssql/`: http://bitbucket.org/Manfre/django-mssql/
.. _`https://github.com/avidal/django-pyodbc`: https://github.com/avidal/django-pyodbc

----

Future of Django-mssql
======================

  - Support any Django version supported by Django project
  - Support Python 3
  - 100% Pass Django test suite by Django 1.6
  - Improve performance
  - MSSQL sugar. 
  
    - ``raw_callproc``
    
  - More complete documentation

----

HTTP server choices
===================

Three main questions
--------------------

  1. Can it run as a service?
  2. Does it have any known issues that impact the project? (they all have issues)
  3. Is the windows build actively maintained and supported?

On Windows...
-------------

============  ===============  ============  ==================
Server        Runs as Service  Known Issues  Actively Supported
============  ===============  ============  ==================
Apache        Yes              No            Yes
IIS           Yes              No [1]        Yes
nginx         No               No            Yes
Lighttpd      Yes              Yes [2]       No
============  ===============  ============  ==================


.. [1] Difficulty with automated build enviroment caused by changes between the various versions of
       IIS. Each OS and sometimes service pack provides a different IIS version.

.. [2] Several documented issues in release notes at time of evaluation in 2009-2010. Windows
       build no longer actively maintained.

----

Apache on Windows
=================

  - Actively maintained
  - Lots of features
  
    - Can proxy if HAProxy or other option not available
  
  - More resource heavy than other options
  - MPM: mpm_winnt

    - One process, many threads

----

Launch day surprise
===================

- Most pages have lots of IO

  - Network (Request/Response)
  - Cache
  - Database
  - Disk (Templates)

- "Understanding the GIL" - David Beazley `http://www.dabeaz.com/GIL/`_

  - Threads release their lock when blocking for IO

.. _`http://www.dabeaz.com/GIL/`: http://www.dabeaz.com/GIL/


  Dear SRC, 
    Congratulations on launching your new site. Sorry it buckled under non-peak load.
  Sincerely,
    Global Interpreter Lock


----

How We Worked Around It?
========================

- Optimize slow pages
- Web farm on a box
- Load balancer

  - mod_proxy_balancer (on the box)
  - HAProxy


 "I got a fever, and the only cure is more Apaches"

----


It's Not All Bad
================

  "What is life without challenges?" - Richard Castle


- More fault tolerant
- Ready to scale
- Great learning experience

----

Questions And Feedback
======================

.fx: questions

.. figure:: images/manfre-crest.png
   :alt: Manfre's avatar
   :align: right

Michael Manfre

- Twitter: `@manfre`_
- BitBucket: `https://bitbucket.com/Manfre/`_
- Github: `https://github.com/manfre/`_
- Freenode: manfre

- Slides: `http://manfre.github.com/django-on-windows-talk/`_

.. _`@manfre`: http://twitter.com/manfre
.. _`https://bitbucket.com/Manfre/`: https://bitbucket.org/Manfre/
.. _`https://github.com/manfre/`: https://github.com/manfre/
.. _`http://manfre.github.com/django-on-windows-talk/`: http://manfre.github.com/django-on-windows-talk/
