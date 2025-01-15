# Postgres-Lec8-Jan-15-25
PARTITION BY, JSONB, INT[], GENERATED ALWAYS, VIEWS, materialized VIEW
## **Jan-15-25 repeat HW:**
* PARTITION BY - like group by, divide the table to groups by a claus, \
  but unlike group by the actions are on each row and not on the entire group
  * PARTITION BY employee_id **ORDER BY id** = the order by makes to 'do aggregation so far'
  * PARTITION BY employee_id = do the aggregation on all the entire group
* JSON column = can define a column from **JSONB** type, and to access the values in this json:
  * <column name>->><key in the json>
    * example: column name details={'name':'shani',...}, select details->>'name' return 'shani'
  * the B in JSONB= added more functionality on the json values
    * allow the MySQL to be more flexable unlike the limitation of restrictions of the MYSQL like postgres
* INT[]= array type with integer values
  * allow the MySQL to be more flexable unlike the limitation of restrictions of the MYSQL like postgres
* GENERATED ALWAYS: allways generated automatically the value (after any updates on the given other value)
## **Jan-15-25 new subjects:**
  * VIEWS: like a function but only for select Query, and only for read only
    * CREATE view (like a table) from given Query and given the view name like a function:
      * CREATE view get_emp_dept AS
        SELECT....
    * CREATE materialized view mat_get_emp_dept...AS SELECT....= like create view , but unlike the results don't changed 
     like snapshot.
      * if you want to update the materialized: the syntax is:
        * refresh materialized view mat_get_emp_dept
