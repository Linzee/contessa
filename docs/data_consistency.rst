Data consistency
==============================

Basic consistency-checks are a way to proof that data is consistent after a transfer/transform operation.
Typical check can be a comparison of the number of rows between source and destination after a synchronisation.


Basic info
------------------------------

For this purpose, Contessa has *ConsistencyChecker* (alternative object to ContessaRunner).
It takes 2 tables (possibly from 2 different source DBs) and compares the results of the same query (typically `count(*)`)
Output of this check is simply a boolean value, denoting whether the results are the same.
Result is then in form of **ConsistencyCheck** instance saved to the given result table, together with the table names
and name of the check.


Basic usage
------------------------------

.. code-block:: python
    consistency_checker = ConsistencyChecker(DB_URI)

    consistency_checker.run(
        consistency_checker.COUNT,
        left_check_table={"schema_name": "tmp", "table_name": "user"},
        right_check_table={"schema_name": "public", "table_name": "user"},
        result_table={"schema_name": "data_quality"},
        context={"task_ts": datetime.now()},
    )