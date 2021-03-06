=======================
Release Notes (pre 1.0)
=======================

.. note::

   These release notes are for versions of ibis **prior to 1.0**. For 1.0 and
   later release notes see :doc:`/release/index`.

v0.14.0 (August 23rd, 2018)
---------------------------

This release brings refactored, more composable core components and rule system
to ibis. We also focused quite heavily on the BigQuery backend this release.

New Features
~~~~~~~~~~~~

* Allow keyword arguments in Node subclasses (:ghissue:`968`)
* Splat args into Node subclasses instead of requiring a list (:ghissue:`969`)
* Add support for ``UNION`` in the BigQuery backend (:ghissue:`1408`,
  :ghissue:`1409`)
* Support for writing UDFs in BigQuery (:ghissue:`1377`). See the BigQuery
  UDF docs for more details.
* Support for cross-project expressions in the BigQuery backend.
  (:ghissue:`1427`, :ghissue:`1428`)
* Add ``strftime`` and ``to_timestamp`` support for BigQuery (:ghissue:`1422`,
  :ghissue:`1410`)
* Require ``google-cloud-bigquery >=1.0`` (:ghissue:`1424`)
* Limited support for interval arithmetic in the pandas backend (:ghissue:`1407`)
* Support for subclassing ``TableExpr`` (:ghissue:`1439`)
* Fill out pandas backend operations (:ghissue:`1423`)
* Add common DDL APIs to the pandas backend (:ghissue:`1464`)
* Implement the ``sql`` method for BigQuery (:ghissue:`1463`)
* Add ``to_timestamp`` for BigQuery (:ghissue:`1455`)
* Add the ``mapd`` backend (:ghissue:`1419`)
* Implement range windows (:ghissue:`1349`)
* Support for map types in the pandas backend (:ghissue:`1498`)
* Add ``mean`` and ``sum`` for ``boolean`` types in BigQuery (:ghissue:`1516`)
* All recent versions of SQLAlchemy are now suppported (:ghissue:`1384`)
* Add support for ``NUMERIC`` types in the BigQuery backend (:ghissue:`1534`)
* Speed up grouped and rolling operations in the pandas backend (:ghissue:`1549`)
* Implement ``TimestampNow`` for BigQuery and pandas (:ghissue:`1575`)

Bug Fixes
~~~~~~~~~

* Nullable property is now propagated through value types (:ghissue:`1289`)
* Implicit casting between signed and unsigned integers checks boundaries
* Fix precedence of case statement (:ghissue:`1412`)
* Fix handling of large timestamps (:ghissue:`1440`)
* Fix ``identical_to`` precedence (:ghissue:`1458`)
* Pandas 0.23 compatibility (:ghissue:`1458`)
* Preserve timezones in timestamp-typed literals (:ghissue:`1459`)
* Fix incorrect topological ordering of ``UNION`` expressions (:ghissue:`1501`)
* Fix projection fusion bug when attempting to fuse columns of the same name
  (:ghissue:`1496`)
* Fix output type for some decimal operations (:ghissue:`1541`)

API Changes
-----------

* The previous, private rules API has been rewritten (:ghissue:`1366`)
* Defining input arguments for operations happens in a more readable fashion
  instead of the previous `input_type` list.
* Removed support for async query execution (only Impala supported)
* Remove support for Python 3.4 (:ghissue:`1326`)
* BigQuery division defaults to using ``IEEE_DIVIDE`` (:ghissue:`1390`)
* Add ``tolerance`` parameter to ``asof_join`` (:ghissue:`1443`)

v0.13.0 (March 30, 2018)
------------------------

This release brings new backends, including support for executing against
files, MySQL, Pandas user defined scalar and aggregations along with a number
of bug fixes and reliability enhancements. We recommend that all users upgrade
from earlier versions of Ibis.

New Backends
~~~~~~~~~~~~

* File Support for CSV & HDF5 (:ghissue:`1165`, :ghissue:`1194`)
* File Support for Parquet Format (:ghissue:`1175`, :ghissue:`1194`)
* Experimental support for ``MySQL`` thanks to @kszucs (:ghissue:`1224`)

New Features
~~~~~~~~~~~~

* Support for Unsigned Integer Types (:ghissue:`1194`)
* Support for Interval types and expressions with support for execution on the
  Impala and Clickhouse backends (:ghissue:`1243`)
* Isnan, isinf operations for float and double values (:ghissue:`1261`)
* Support for an interval with a quarter period (:ghissue:`1259`)
* ``ibis.pandas.from_dataframe`` convenience function (:ghissue:`1155`)
* Remove the restriction on ``ROW_NUMBER()`` requiring it to have an
  ``ORDER BY`` clause (:ghissue:`1371`)
* Add ``.get()`` operation on a Map type (:ghissue:`1376`)
* Allow visualization of custom defined expressions
* Add experimental support for pandas UDFs/UDAFs (:ghissue:`1277`)
* Functions can be used as groupby keys (:ghissue:`1214`, :ghissue:`1215`)
* Generalize the use of the ``where`` parameter to reduction operations
  (:ghissue:`1220`)
* Support for interval operations thanks to @kszucs (:ghissue:`1243`,
  :ghissue:`1260`, :ghissue:`1249`)
* Support for the ``PARTITIONTIME`` column in the BigQuery backend
  (:ghissue:`1322`)
* Add ``arbitrary()`` method for selecting the first non null value in a column
  (:ghissue:`1230`, :ghissue:`1309`)
* Windowed ``MultiQuantile`` operation in the pandas backend thanks to
  @DiegoAlbertoTorres (:ghissue:`1343`)
* Rules for validating table expressions thanks to @DiegoAlbertoTorres
  (:ghissue:`1298`)
* Complete end-to-end testing framework for all supported backends
  (:ghissue:`1256`)
* ``contains``/``not contains`` now supported in the pandas backend
  (:ghissue:`1210`, :ghissue:`1211`)
* CI builds are now reproducible *locally* thanks to @kszucs (:ghissue:`1121`,
  :ghissue:`1237`, :ghissue:`1255`, :ghissue:`1311`)
* ``isnan``/``isinf`` operations thanks to @kszucs (:ghissue:`1261`)
* Framework for generalized dtype and schema inference, and implicit casting
  thanks to @kszucs (:ghissue:`1221`, :ghissue:`1269`)
* Generic utilities for expression traversal thanks to @kszucs (:ghissue:`1336`)
* ``day_of_week`` API (:ghissue:`306`, :ghissue:`1047`)
* Design documentation for ibis (:ghissue:`1351`)

Bug Fixes
~~~~~~~~~

* Unbound parameters were failing in the simple case of a
  :meth:`~ibis.expr.types.TableExpr.mutate` call with no operation
  (:ghissue:`1378`)
* Fix parameterized subqueries (:ghissue:`1300`, :ghissue:`1331`, :ghissue:`1303`,
  :ghissue:`1378`)
* Fix subquery extraction, which wasn't happening in topological order
  (:ghissue:`1342`)
* Fix parenthesization if ``isnull`` (:ghissue:`1307`)
* Calling drop after mutate did not work (:ghissue:`1296`, :ghissue:`1299`)
* SQLAlchemy backends were missing an implementation of
  :class:`~ibis.expr.operations.NotContains`.
* Support ``REGEX_EXTRACT`` in PostgreSQL 10 (:ghissue:`1276`, :ghissue:`1278`)

API Changes
-----------

* Fixing :ghissue:`1378` required the removal of the ``name`` parameter to the
  :func:`~ibis.param` function. Use the :meth:`~ibis.expr.types.Expr.name`
  method instead.

v0.12.0 (October 28, 2017)
--------------------------

This release brings Clickhouse and BigQuery SQL support along with a number of
bug fixes and reliability enhancements. We recommend that all users upgrade
from earlier versions of Ibis.

New Backends
~~~~~~~~~~~~

* BigQuery backend (:ghissue:`1170`), thanks to @tsdlovell.
* Clickhouse backend (:ghissue:`1127`), thanks to @kszucs.


New Features
~~~~~~~~~~~~

* Add support for ``Binary`` data type (:ghissue:`1183`)
* Allow users of the BigQuery client to define their own API proxy classes
  (:ghissue:`1188`)
* Add support for HAVING in the pandas backend (:ghissue:`1182`)
* Add struct field tab completion (:ghissue:`1178`)
* Add expressions for Map/Struct types and columns (:ghissue:`1166`)
* Support Table.asof_join (:ghissue:`1162`)
* Allow right side of arithmetic operations to take over (:ghissue:`1150`)
* Add a data_preload step in pandas backend (:ghissue:`1142`)
* expressions in join predicates in the pandas backend (:ghissue:`1138`)
* Scalar parameters (:ghissue:`1075`)
* Limited window function support for pandas (:ghissue:`1083`)
* Implement Time datatype (:ghissue:`1105`)
* Implement array ops for pandas (:ghissue:`1100`)
* support for passing multiple quantiles in ``.quantile()`` (:ghissue:`1094`)
* support for clip and quantile ops on DoubleColumns (:ghissue:`1090`)
* Enable unary math operations for pandas, sqlite (:ghissue:`1071`)
* Enable casting from strings to temporal types (:ghissue:`1076`)
* Allow selection of whole tables in pandas joins (:ghissue:`1072`)
* Implement comparison for string vs date and timestamp types (:ghissue:`1065`)
* Implement isnull and notnull for pandas (:ghissue:`1066`)
* Allow like operation to accept a list of conditions to match (:ghissue:`1061`)
* Add a pre_execute step in pandas backend (:ghissue:`1189`)

Bug Fixes
~~~~~~~~~

* Remove global expression caching to ensure repeatable code generation
  (:ghissue:`1179`, :ghissue:`1181`)
* Fix ``ORDER BY`` generation without a ``GROUP BY`` (:ghissue:`1180`,
  :ghissue:`1181`)
* Ensure that :class:`~ibis.expr.datatypes.DataType` and subclasses hash
  properly (:ghissue:`1172`)
* Ensure that the pandas backend can deal with unary operations in groupby
* (:ghissue:`1182`)
* Incorrect impala code generated for NOT with complex argument (:ghissue:`1176`)
* BUG/CLN: Fix predicates on Selections on Joins (:ghissue:`1149`)
* Don't use SET LOCAL to allow redshift to work (:ghissue:`1163`)
* Allow empty arrays as arguments (:ghissue:`1154`)
* Fix column renaming in groupby keys (:ghissue:`1151`)
* Ensure that we only cast if timezone is not None (:ghissue:`1147`)
* Fix location of conftest.py (:ghissue:`1107`)
* TST/Make sure we drop tables during postgres testing (:ghissue:`1101`)
* Fix misleading join error message (:ghissue:`1086`)
* BUG/TST: Make hdfs an optional dependency (:ghissue:`1082`)
* Memoization should include expression name where available (:ghissue:`1080`)

Performance Enhancements
~~~~~~~~~~~~~~~~~~~~~~~~

* Speed up imports (:ghissue:`1074`)
* Fix execution perf of groupby and selection (:ghissue:`1073`)
* Use normalize for casting to dates in pandas (:ghissue:`1070`)
* Speed up pandas groupby (:ghissue:`1067`)

Contributors
~~~~~~~~~~~~

The following people contributed to the 0.12.0 release ::

    $ git shortlog -sn --no-merges v0.11.2..v0.12.0
    63	Phillip Cloud
     8	Jeff Reback
     2	Kriszti??n Sz??cs
     2	Tory Haavik
     1	Anirudh
     1	Szucs Krisztian
     1	dlovell
     1	kwangin


0.11.0 (June 28, 2017)
----------------------

This release brings initial Pandas backend support along with a number of
bug fixes and reliability enhancements. We recommend that all users upgrade
from earlier versions of Ibis.

New Features
~~~~~~~~~~~~
* Experimental pandas backend to allow execution of ibis expression against
  pandas DataFrames
* Graphviz visualization of ibis expressions. Implements ``_repr_png_`` for
  Jupyter Notebook functionality
* Ability to create a partitioned table from an ibis expression
* Support for missing operations in the SQLite backend: sqrt, power, variance,
  and standard deviation, regular expression functions, and missing power
  support for PostgreSQL
* Support for schemas inside databases with the PostgreSQL backend
* Appveyor testing on core ibis across all supported Python versions
* Add ``year``/``month``/``day`` methods to ``date`` types
* Ability to sort, group by and project columns according to positional index
  rather than only by name
* Added a ``type`` parameter to ``ibis.literal`` to allow user specification of
  literal types

Bug Fixes
~~~~~~~~~
* Fix broken conda recipe
* Fix incorrectly typed fillna operation
* Fix postgres boolean summary operations
* Fix kudu support to reflect client API Changes
* Fix equality of nested types and construction of nested types when the value
  type is specified as a string

API Changes
~~~~~~~~~~~
* Deprecate passing integer values to the ``ibis.timestamp`` literal
  constructor, this will be removed in 0.12.0
* Added the ``admin_timeout`` parameter to the kudu client ``connect`` function

Contributors
~~~~~~~~~~~~

::

    $ git shortlog --summary --numbered v0.10.0..v0.11.0

      58 Phillip Cloud
       1 Greg Rahn
       1 Marius van Niekerk
       1 Tarun Gogineni
       1 Wes McKinney

0.8 (May 19, 2016)
------------------

This release brings initial PostgreSQL backend support along with a number of
critical bug fixes and usability improvements. As several correctness bugs with
the SQL compiler were fixed, we recommend that all users upgrade from earlier
versions of Ibis.

New Features
~~~~~~~~~~~~
* Initial PostgreSQL backend contributed by Phillip Cloud.
* Add ``groupby`` as an alias for ``group_by`` to table expressions

Bug Fixes
~~~~~~~~~
* Fix an expression error when filtering based on a new field
* Fix Impala's SQL compilation of using ``OR`` with compound filters
* Various fixes with the ``having(...)`` function in grouped table expressions
* Fix CTE (``WITH``) extraction inside ``UNION ALL`` expressions.
* Fix ``ImportError`` on Python 2 when ``mock`` library not installed

API Changes
~~~~~~~~~~~
* The deprecated ``ibis.impala_connect`` and ``ibis.make_client`` APIs have
  been removed

0.7 (March 16, 2016)
--------------------

This release brings initial Kudu-Impala integration and improved Impala and
SQLite support, along with several critical bug fixes.

New Features
~~~~~~~~~~~~
* Apache Kudu (incubating) integration for Impala users. See the `blog post <http://blog.ibis-project.org/kudu-impala-ibis>`_ for now. Will add some documentation here when possible.
* Add ``use_https`` option to ``ibis.hdfs_connect`` for WebHDFS connections in
  secure (Kerberized) clusters without SSL enabled.
* Correctly compile aggregate expressions involving multiple subqueries.

To explain this last point in more detail, suppose you had:

.. code-block:: python

   table = ibis.table([('flag', 'string'),
                       ('value', 'double')],
                      'tbl')

   flagged = table[table.flag == '1']
   unflagged = table[table.flag == '0']

   fv = flagged.value
   uv = unflagged.value

   expr = (fv.mean() / fv.sum()) - (uv.mean() / uv.sum())

The last expression now generates the correct Impala or SQLite SQL:

.. code-block:: sql

   SELECT t0.`tmp` - t1.`tmp` AS `tmp`
   FROM (
     SELECT avg(`value`) / sum(`value`) AS `tmp`
     FROM tbl
     WHERE `flag` = '1'
   ) t0
     CROSS JOIN (
       SELECT avg(`value`) / sum(`value`) AS `tmp`
       FROM tbl
       WHERE `flag` = '0'
     ) t1

Bug Fixes
~~~~~~~~~
* ``CHAR(n)`` and ``VARCHAR(n)`` Impala types now correctly map to Ibis string
  expressions
* Fix inappropriate projection-join-filter expression rewrites resulting in
  incorrect generated SQL.
* ``ImpalaClient.create_table`` correctly passes ``STORED AS PARQUET`` for
  ``format='parquet'``.
* Fixed several issues with Ibis dependencies (impyla, thriftpy, sasl,
  thrift_sasl), especially for secure clusters. Upgrading will pull in these
  new dependencies.
* Do not fail in ``ibis.impala.connect`` when trying to create the temporary
  Ibis database if no HDFS connection passed.
* Fix join predicate evaluation bug when column names overlap with table
  attributes.
* Fix handling of fully-materialized joins (aka ``select *`` joins) in
  SQLAlchemy / SQLite.

Contributors
~~~~~~~~~~~~
Thank you to all who contributed patches to this release.

::

  $ git log v0.6.0..v0.7.0 --pretty=format:%aN | sort | uniq -c | sort -rn
      21 Wes McKinney
       1 Uri Laserson
       1 Kristopher Overholt

0.6 (December 1, 2015)
----------------------

This release brings expanded pandas and Impala integration, including support
for managing partitioned tables in Impala. See the new :ref:`Ibis for Impala
Users <backends.impala>` guide for more on using Ibis with Impala.

The :ref:`Ibis for SQL Programmers <sql>` guide also was written since the 0.5
release.

This release also includes bug fixes affecting generated SQL correctness. All
users should upgrade as soon as possible.

New Features
~~~~~~~~~~~~

* New integrated Impala functionality. See :ref:`Ibis for Impala Users
  <backends.impala>` for more details on these things.

  * Improved Impala-pandas integration. Create tables or insert into existing
    tables from pandas ``DataFrame`` objects.
  * Partitioned table metadata management API. Add, drop, alter, and
    insert into table partitions.
  * Add ``is_partitioned`` property to ``ImpalaTable``.
  * Added support for ``LOAD DATA`` DDL using the ``load_data`` function, also
    supporting partitioned tables.
  * Modify table metadata (location, format, SerDe properties etc.)  using
    ``ImpalaTable.alter``
  * Interrupting Impala expression execution with Control-C will attempt to
    cancel the running query with the server.
  * Set the compression codec (e.g. snappy) used with
    ``ImpalaClient.set_compression_codec``.
  * Get and set query options for a client session with
    ``ImpalaClient.get_options`` and ``ImpalaClient.set_options``.
  * Add ``ImpalaTable.metadata`` method that parses the output of the
    ``DESCRIBE FORMATTED`` DDL to simplify table metadata inspection.
  * Add ``ImpalaTable.stats`` and ``ImpalaTable.column_stats`` to see computed
    table and partition statistics.
  * Add ``CHAR`` and ``VARCHAR`` handling
  * Add ``refresh``, ``invalidate_metadata`` DDL options and add
    ``incremental`` option to ``compute_stats`` for ``COMPUTE INCREMENTAL
    STATS``.

* Add ``substitute`` method for performing multiple value substitutions in an
  array or scalar expression.
* Division is by default *true division* like Python 3 for all numeric
  data. This means for SQL systems that use C-style division semantics, the
  appropriate ``CAST`` will be automatically inserted in the generated SQL.
* Easier joins on tables with overlapping column names. See :ref:`Ibis for SQL Programmers <sql>`.
* Expressions like ``string_expr[:3]`` now work as expected.
* Add ``coalesce`` instance method to all value expressions.
* Passing ``limit=None`` to the ``execute`` method on expressions disables any
  default row limits.

API Changes
~~~~~~~~~~~

* ``ImpalaTable.rename`` no longer mutates the calling table expression.

Contributors
~~~~~~~~~~~~

::

    $ git log v0.5.0..v0.6.0 --pretty=format:%aN | sort | uniq -c | sort -rn
    46 Wes McKinney
     3 Uri Laserson
     1 Phillip Cloud
     1 mariusvniekerk
     1 Kristopher Overholt


0.5 (September 10, 2015)
------------------------

Highlights in this release are the SQLite, Python 3, Impala UDA support, and an
asynchronous execution API. There are also many usability improvements, bug
fixes, and other new features.

New Features
~~~~~~~~~~~~
* SQLite client and built-in function support
* Ibis now supports Python 3.4 as well as 2.6 and 2.7
* Ibis can utilize Impala user-defined aggregate (UDA) functions
* SQLAlchemy-based translation toolchain to enable more SQL engines having
  SQLAlchemy dialects to be supported
* Many window function usability improvements (nested analytic functions and
  deferred binding conveniences)
* More convenient aggregation with keyword arguments in ``aggregate`` functions
* Built preliminary wrapper API for MADLib-on-Impala
* Add ``var`` and ``std`` aggregation methods and support in Impala
* Add ``nullifzero`` numeric method for all SQL engines
* Add ``rename`` method to Impala tables (for renaming tables in the Hive
  metastore)
* Add ``close`` method to ``ImpalaClient`` for session cleanup (#533)
* Add ``relabel`` method to table expressions
* Add ``insert`` method to Impala tables
* Add ``compile`` and ``verify`` methods to all expressions to test compilation
  and ability to compile (since many operations are unavailable in SQLite, for
  example)

API Changes
~~~~~~~~~~~
* Impala Ibis client creation now uses only ``ibis.impala.connect``, and
  ``ibis.make_client`` has been deprecated

Contributors
~~~~~~~~~~~~
::

    $ git log v0.4.0..v0.5.0 --pretty=format:%aN | sort | uniq -c | sort -rn
          55 Wes McKinney
          9 Uri Laserson
          1 Kristopher Overholt

0.4 (August 14, 2015)
---------------------

New Features
~~~~~~~~~~~~
* Add tooling to use Impala C++ scalar UDFs within Ibis (#262, #195)
* Support and testing for Kerberos-enabled secure HDFS clusters
* Many table functions can now accept functions as parameters (invoked on the
  calling table) to enhance composability and emulate late-binding semantics of
  languages (like R) that have non-standard evaluation (#460)
* Add ``any``, ``all``, ``notany``, and ``notall`` reductions on boolean
  arrays, as well as ``cumany`` and ``cumall``
* Using ``topk`` now produces an analytic expression that is executable (as an
  aggregation) but can also be used as a filter as before (#392, #91)
* Added experimental database object "usability layer", see
  ``ImpalaClient.database``.
* Add ``TableExpr.info``
* Add ``compute_stats`` API to table expressions referencing physical Impala
  tables
* Add ``explain`` method to ``ImpalaClient`` to show query plan for an
  expression
* Add ``chmod`` and ``chown`` APIs to ``HDFS`` interface for superusers
* Add ``convert_base`` method to strings and integer types
* Add option to ``ImpalaClient.create_table`` to create empty partitioned
  tables
* ``ibis.cross_join`` can now join more than 2 tables at once
* Add ``ImpalaClient.raw_sql`` method for running naked SQL queries
* ``ImpalaClient.insert`` now validates schemas locally prior to sending query
  to cluster, for better usability.
* Add conda installation recipes

Contributors
~~~~~~~~~~~~
::

    $ git log v0.3.0..v0.4.0 --pretty=format:%aN | sort | uniq -c | sort -rn
         38 Wes McKinney
          9 Uri Laserson
          2 Meghana Vuyyuru
          2 Kristopher Overholt
          1 Marius van Niekerk

0.3 (July 20, 2015)
-------------------

First public release. See http://ibis-project.org for more.

New Features
~~~~~~~~~~~~
* Implement window / analytic function support
* Enable non-equijoins (join clauses with operations other than ``==``).
* Add remaining :ref:`string functions <api.string>` supported by Impala.
* Add ``pipe`` method to tables (hat-tip to the pandas dev team).
* Add ``mutate`` convenience method to tables.
* Fleshed out ``WebHDFS`` implementations: get/put directories, move files,
  etc. See the :ref:`full HDFS API <api.hdfs>`.
* Add ``truncate`` method for timestamp values
* ``ImpalaClient`` can execute scalar expressions not involving any table.
* Can also create internal Impala tables with a specific HDFS path.
* Make Ibis's temporary Impala database and HDFS paths configurable (see
  ``ibis.options``).
* Add ``truncate_table`` function to client (if the user's Impala cluster
  supports it).
* Python 2.6 compatibility
* Enable Ibis to execute concurrent queries in multithreaded applications
  (earlier versions were not thread-safe).
* Test data load script in ``scripts/load_test_data.py``
* Add an internal operation type signature API to enhance developer
  productivity.

Contributors
~~~~~~~~~~~~
::

    $ git log v0.2.0..v0.3.0 --pretty=format:%aN | sort | uniq -c | sort -rn
         59 Wes McKinney
         29 Uri Laserson
          4 Isaac Hodes
          2 Meghana Vuyyuru

0.2 (June 16, 2015)
-------------------

New Features
~~~~~~~~~~~~
* ``insert`` method on Ibis client for inserting data into existing tables.
* ``parquet_file``, ``delimited_file``, and ``avro_file`` client methods for
  querying datasets not yet available in Impala
* New ``ibis.hdfs_connect`` method and ``HDFS`` client API for WebHDFS for
  writing files and directories to HDFS
* New timedelta API and improved timestamp data support
* New ``bucket`` and ``histogram`` methods on numeric expressions
* New ``category`` logical datatype for handling bucketed data, among other
  things
* Add ``summary`` API to numeric expressions
* Add ``value_counts`` convenience API to array expressions
* New string methods ``like``, ``rlike``, and ``contains`` for fuzzy and regex
  searching
* Add ``options.verbose`` option and configurable ``options.verbose_log``
  callback function for improved query logging and visibility
* Support for new SQL built-in functions

  * ``ibis.coalesce``
  * ``ibis.greatest`` and ``ibis.least``
  * ``ibis.where`` for conditional logic (see also ``ibis.case`` and
    ``ibis.cases``)
  * ``nullif`` method on value expressions
  * ``ibis.now``

* New aggregate functions: ``approx_median``, ``approx_nunique``, and
  ``group_concat``
* ``where`` argument in aggregate functions
* Add ``having`` method to ``group_by`` intermediate object
* Added group-by convenience
  ``table.group_by(exprs).COLUMN_NAME.agg_function()``
* Add default expression names to most aggregate functions
* New Impala database client helper methods

  * ``create_database``
  * ``drop_database``
  * ``exists_database``
  * ``list_databases``
  * ``set_database``

* Client ``list_tables`` searching / listing method
* Add ``add``, ``sub``, and other explicit arithmetic methods to value
  expressions

API Changes
~~~~~~~~~~~
* New Ibis client and Impala connection workflow. Client now combined from an
  Impala connection and an optional HDFS connection

Bug Fixes
~~~~~~~~~
* Numerous expression API bug fixes and rough edges fixed

Contributors
~~~~~~~~~~~~
::

    $ git log v0.1.0..v0.2.0 --pretty=format:%aN | sort | uniq -c | sort -rn
         71 Wes McKinney
          1 Juliet Hougland
          1 Isaac Hodes

0.1 (March 26, 2015)
--------------------

First Ibis release.

* Expression DSL design and type system
* Expression to ImpalaSQL compiler toolchain
* Impala built-in function wrappers

::

    $ git log 84d0435..v0.1.0 --pretty=format:%aN | sort | uniq -c | sort -rn
        78 Wes McKinney
         1 srus
         1 Henry Robinson
