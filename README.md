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
      * the results are been generated when you create the view and on refresh and save and not changed. 
    *  stored procedure (functions/procedure)- chapter 46:  like views but can be any one of the CRUD options
      * works with SQL syntax
      * create or replace function <function name usally starts with sp_...> returns <return type>
        language plpgsql as
        $$ - to put special characters
        BEGIN
            return 'hello world';
        END;
        $$
        * to call the function:
          * select * from <function name>()
      * concat strings: CONCAT(str1,str2) 
      * create procedure <name>- create function that doesn't return value
        * to call procedure:
          * call <name<();
      * to send parameters in a function: foo (parameter <parameter type>)
        * foo(m double precision,r double precision) return **double precision** 
        * double precision= float(8) =because there is not double type so need the precision
      * since the function return table with the return, you can use it in the from:
        * select * from sp_sum(3.5,4)
            where sp_sum>7
      * to return more than 1 value:
        * create function sp_prod_div(x double precision,y double precision, **out** "prod res" double precision, **out** "div res" double precision)
          * in the begin-end section, assign the results to the out parameters
          * out replace the return
          * no need to send the out parameters when you call the function:
            * select * from sp_prod_div(3,4.9)
      * if the function signature changes need to add the drop function and the change the function signature