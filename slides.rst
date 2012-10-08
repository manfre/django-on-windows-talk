.. |reg| unicode:: U+00AE .. REGISTERED TRADEMARK
.. |tm| unicode:: U+2122 .. TRADEMARK

Django on Windows with Apache
=============================

Michael Manfre

Semiconductor Research Corporation |reg|

	Pioneers in research collaboration |tm|

django-mssql 

	Django database backend for Microsoft SQL Server

----

Semiconductor Research Corporation |reg|
========================================

    "Semiconductor Research Corporation (SRC) is the world's leading technology research consortium. 
    With member companies and university research programs spanning the globe, SRC plays an 
    indispensable part in the R&D strategies of the industry's most influential entities. 
    SRC-sponsored university research is of the highest caliber and creates knowledge breakthroughs 
    that will invent the industries of tomorrow."
    
    -- `http://www.src.org/about/`_

----

Web site purpose
================

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
  - Django
  - HAProxy (Ubuntu)
  - Memcached
  - Microsoft SQL Server
  - nAnt
  - PowerShell
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

Why Not IIS, ASP.NET, PHP, etc?
-------------------------------

- Contact me after the talk

----

Windows MPM Options
-------------------

- mpm_winnt
  
  - One process, many threads

----

What's Wrong With Threads?
--------------------------

- Uses more resources
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
------------------------

- Optimize slow pages
- Web farm on a box
- Load balancer

  - mod_proxy_balancer (on the box)
  - HAProxy


 "I got a fever, and the only cure is more Apaches"

----

It's Not All Bad
----------------

  "What is life without challenges?" - Richard Castle


- More fault tolerant
- Ready to scale
- Great learning experience

----

Is There A Better Way?
----------------------

If you have ideas, questions, or comments, please contact me.

Michael Manfre

manfre on `Twitter`_ | `Bitbucket`_ | `Github`_ | Freenode

Slides: `http://bit.ly/dj12manfretalk`_

.. _`Twitter`: http://twitter.com/manfre
.. _`Bitbucket`: https://bitbucket.org/Manfre
.. _`Github`: https://github.com/manfre 
.. _`http://bit.ly/dj12manfretalk`: http://bit.ly/dj12manfretalk

.. _`http://www.src.org/about/`: http://www.src.org/about/
