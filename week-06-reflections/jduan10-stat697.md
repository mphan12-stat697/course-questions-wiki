
# Questions about Problems and Recipes



[Course Textbook Chapter 5, Problem 1] 
- Question (jduan10-stat697): Can integrity constraints be specified in CREATE TABLE statement?



[Course Textbook Chapter 5, Problem 2] 
- Question (jduan10-stat697): What is the difference between separating by comma and by space?



[Course Textbook Chapter 5, Problem 5] 
- Question (jduan10-stat697): How to save the table created by the CREATE TABLE clause?



[Course Textbook Chapter 5, Problem 6] 
- Question (jduan10-stat697): What will happen if we do not specify a column alias when we’re creating a table?



[Course Textbook Chapter 5, Problem 7] 
- Question (jduan10-stat697): Can we list more than two table names in the FROM clause?



[Course Textbook Chapter 5, Problem 8] 
- Question (jduan10-stat697): Do we need to list column-value pairs in order in the SET clause?



[Course Textbook Chapter 5, Problem 9] 
- Question (jduan10-stat697): Are the new created rows always shown at the bottom of the table?



[Week 6 SAS Recipe: ddl-and-dml-sql-queries] 
- Question (jduan10-stat697): Are the changes in table created by DDL queries automatically be save?



[Week 6 SAS Recipe: obtain-column-information]
- Question (jduan10-stat697): Can we use MACRO in the approach 1&2?



***



# Recipes Exploration Results



```


*Recipe: ddl-and-dml-sql-queries;

* DDL example: define column information;
proc sql;
    create table Work.tmp
    (
         column1 char(42)
        ,column2 num
    );
quit;

* DDL example: obtain column information;
proc sql;
    describe table Work.tmp;
quit;

* DDL example: add column;
proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;

* DDL example: modify column;
proc sql;
    alter table Work.tmp
        modify column1 char(54)
    ;
quit;

* DDL example: delete column;
proc sql;
    alter table Work.tmp
        drop column2
    ;
quit;

* DDL example: delete table;
proc sql;
    drop table Work.tmp;
quit;

* DML example setup: define column information;
proc sql;
    create table Work.iris
        like sashelp.iris
    ;
quit;

* DML example: obtain rows of data;
proc sql;
    select * from Work.iris;
quit;

* DML example: create rows of data from select query;
proc sql;
    insert into Work.iris
        select * from sashelp.iris
    ;
quit;

* DML example: create row of data using values statement for all columns;
proc sql;
    insert into Work.iris
        values('Big Flower',75,80,85,90)
    ;
quit;

* DML example: create row of data using values statement for select columns;
proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower',75)
    ;
quit;

* DML example: update rows of data;
proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

* DML example: delete rows of data;
proc sql;
    delete from Work.iris
        where Species='Big Flower'
    ;
quit;


*Recipe: obtain-column-information;

proc contents order=varnum data=sashelp.iris;
run;

proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;

proc sql;
    select
        name
    from
        dictionary.columns
    where
        lowcase(libname) = 'sashelp'
    and
        lowcase(memname) = 'iris'
    ;
quit;


proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;





```
