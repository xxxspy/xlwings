.. _migrate_to_0.9:

Migrate to v0.9
===============

The purpose of this document is to enable you a smooth experience when upgrading to xlwings v0.9.0 and above by laying out
the concept and syntax changes in detail. If you want to get an overview of the new features and bug fixes, have a look at the
:ref:`release notes <v0.9_release_notes>`. Note that the syntax for User Defined Functions (UDFs) didn't change.

Full qualification: Using collections
-------------------------------------

The new object model allows to specify the Excel application instance if needed:

* **old**: ``xw.Range('Sheet1', 'A1', wkb=xw.Workbook('Book1'))``

* **new**: ``xw.apps[0].books['Book1'].sheets['Sheet1'].range('A1')``

See :ref:`syntax_overview` for the details of the new object model.

Connecting to Books
-------------------

* **old**: ``xw.Workbook()``
* **new**: ``xw.Book()`` or via ``xw.books`` if you need to control the app instance.

See :ref:`connect_to_workbook` for the details.

Active Objects
--------------

::

    # Active app (i.e. Excel instance)
    >>> app = xw.apps.active

    # Active book
    >>> wb = xw.books.active  # in active app
    >>> wb = app.books.active  # in specific app

    # Active sheet
    >>> sht = xw.sheets.active  # in active book
    >>> sht = wb.sheets.active  # in specific book

    # Range on active sheet
    >>> xw.Range('A1')  # on active sheet of active book of active app

Round vs. Square Brackets
-------------------------

Round brackets follow Excel's behavior (i.e. 1-based indexing), while square brackets use Python's 0-based indexing/slicing.

As an example, the following all reference the same range::

    xw.apps[0].books[0].sheets[0].range('A1')
    xw.apps(1).books(1).sheets(1).range('A1')
    xw.apps[0].books['Book1'].sheets['Sheet1'].range('A1')
    xw.apps(1).books('Book1').sheets('Sheet1').range('A1')

Access the underlying Library/Engine
------------------------------------

* **old**: ``xw.Range('A1').xl_range`` and ``xl_sheet`` etc.

* **new**: ``xw.Range('A1').api``, same for all other objects

This returns a ``pywin32`` COM object on Windows and an ``appscript`` object on Mac.


Cheat sheet
-----------

Note that ``sht`` stands for a sheet object, like e.g. (in 0.9.0 syntax): ``sht = xw.books['Book1'].sheets[0]``

+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            | v0.9.0                                           | v0.7.2                                                             |
+============================+==================================================+====================================================================+
| Active Excel instance      | ``xw.apps.active``                               | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| New Excel instance         | ``app = xw.App()``                               | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Get app from book          | ``app = wb.app``                                 | ``app = xw.Application(wb)``                                       |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Target installation (Mac)  | ``app = xw.App(spec=...)``                       | ``wb = xw.Workbook(app_target=...)``                               |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Hide Excel Instance        | ``app = xw.App(visible=False)``                  | ``wb = xw.Workbook(app_visible=False)``                            |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Selected Range             | ``app.selection``                                | ``wb.get_selection()``                                             |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Calculation mode           | ``app.calculation = 'manual'``                   | ``app.calculation = xw.constants.Calculation.xlCalculationManual`` |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| All books in app           | ``app.books``                                    | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Fully qualified book       | ``app.books['Book1']``                           | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Active book in active app  | ``xw.books.active``                              | ``xw.Workbook.active()``                                           |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| New book in active app     | ``wb = xw.Book()``                               | ``wb = xw.Workbook()``                                             |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| New book in specific app   | ``wb = app.books.add()``                         | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| All sheets in book         | ``wb.sheets``                                    | ``xw.Sheet.all(wb)``                                               |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Call a macro in an addin   | ``app.macro('MacroName')``                       | unsupported                                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| First sheet of book wb     | ``wb.sheets[0]``                                 | ``xw.Sheet(1, wkb=wb)``                                            |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Active sheet               | ``wb.sheets.active``                             | ``xw.Sheet.active(wkb=wb)`` or ``wb.active_sheet``                 |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Add sheet                  | ``wb.sheets.add()``                              | ``xw.Sheet.add(wkb=wb)``                                           |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Sheet count                | ``wb.sheets.count`` or ``len(wb.sheets)``        | ``xw.Sheet.count(wb)``                                             |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Add chart to sheet         | ``chart = wb.sheets[0].charts.add()``            | ``chart = xw.Chart.add(sheet=1, wkb=wb)``                          |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Existing chart             | ``wb.sheets['Sheet1'].charts[0]``                | ``xw.Chart('Sheet1', 1)``                                          |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Chart Type                 | ``chart.chart_type = '3d_area'``                 | ``chart.chart_type = xw.constants.ChartType.xl3DArea``             |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Add picture to sheet       | ``wb.sheets[0].pictures.add('path/to/pic')``     | ``xw.Picture.add('path/to/pic', sheet=1, wkb=wb)``                 |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Existing picture           | ``wb.sheets['Sheet1'].pictures[0]``              | ``xw.Picture('Sheet1', 1)``                                        |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Matplotlib                 | ``sht.pictures.add(fig, name='x', update=True)`` | ``xw.Plot(fig).show('MyPlot', sheet=sht, wkb=wb)``                 |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Table expansion            | ``sht.range('A1').expand('table')``              | ``xw.Range(sht, 'A1', wkb=wb).table``                              |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Vertical expansion         | ``sht.range('A1').expand('down')``               | ``xw.Range(sht, 'A1', wkb=wb).vertical``                           |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Horizontal expansion       | ``sht.range('A1').expand('right')``              | ``xw.Range(sht, 'A1', wkb=wb).horizontal``                         |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
|                            |                                                  |                                                                    |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Set name of range          | ``sht.range('A1').name = 'name'``                | ``xw.Range(sht, 'A1', wkb=wb).name = 'name'``                      |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+
| Get name of range          | ``sht.range('A1').name.name``                    | ``xw.Range(sht, 'A1', wkb=wb).name``                               |
+----------------------------+--------------------------------------------------+--------------------------------------------------------------------+