Backup Windows Data with Robocopy
=================================

.. author:: default
.. categories:: none
.. tags:: windows, sysadmin
.. comments::


Today I looked for a way to create a backup of my girlfriend's Windows XP laptop
home directory (aka ``Eigene Dateien``). I wanted something like `rsync` and
voilá: `robocopy` caught my attention.

I downloaded it with `robocopy GUI`_ but I ended up writing the command into a
``eigenedateien.cmd`` file which directly calls `robocopy` (which is also
available as part of the `Windows Resource Kit Tools`_):

.. code-block:: winbatch

    REM /L         only list examined files
    REM /MIR       mirror - delete target files that are not in the source
    REM /V         verbose
    REM /NP        no progress bar
    REM /FFT       be tolerant on comparing time stamps
    REM /Z         restart if copy failed
    REM /W:5       retry 5 times
    REM /XA:H      exclude hidden files
    REM /LOG:file  log to file
    robocopy ^
        "C:\Dokumente und Einstellungen\Betty\Eigene Dateien" ^
        "\\Nas\home\Eigene Dateien" ^
        /MIR ^
        /V ^
        /NP ^
        /FFT ^
        /Z ^
        /W:5 ^
        /XA:H ^
        /LOG:"C:\robocopy_log.txt"


.. _robocopy GUI: https://technet.microsoft.com/en-us/magazine/2006.11.utilityspotlight.aspx
.. _robocopy examples: http://social.technet.microsoft.com/wiki/contents/articles/1073.robocopy-and-a-few-examples.aspx
.. _Windows Resource Kit Tools: http://www.microsoft.com/en-us/download/details.aspx?id=17657

