Readme
=

The script ImportCSV.sql can be used to copy data from an H2 db into a CSV file , there is no specific order to run the queries to import the data from H2 to the CSV files.  The CSV files generated would be later be used by ImportCSV.sql to rebuild the data into the MariaDB or MySQL database.

In case that a modification in the ImportCSV.sql, keep in mind that the correct order of queries should be followed. This because the dependencies on the existing database would affect the success of the import.

Instructions
--
## Step 1:  Install MariaDB or MySQL 
Install and configure MariaDB or MySQL as per [Database Configuration](https://docs.opencast.org/r/8.x/admin/#configuration/database/) document instructions.

## Step 2:  Dump H2 data into CSV's
To dump H2 data into CSV files use(under your own risk) the script CreateCSV.sql found in the [H2-Migration](https://github.com/opencast/helper-scripts/H2-Migration/) folder. Run the script directly from the console by using:

```sh
% java -cp h2*.jar org.h2.tools.RunScript -url "jdbc:h2:.../build/opencast-dist-develop-8.5/data/opencast/db;MODE=MySQL;DATABASE_TO_LOWER=TRUE" -user "sa" -pass "sa" -script ".../CreateCSV.sql"
```
Alternatively it is possible to Download and install the [H2 console installer](http://www.h2database.com/html/download.html) and run the script from the H2 console. When connecting the H2 database use  `jdbc:h2:.../build/opencast-dist-develop-8.5/data/opencast/db;MODE=MySQL;DATABASE_TO_LOWER=TRUE`. Notice the `MODE=MySQL;DATABASE_TO_LOWER=TRUE` used to maximaze the compatibility between H2 and MySQL or MariaDB. (Default username and password to connect to H2 is `sa`)

## Step 3:  Import data from CSV to MariaDB or MySQL

Connect to the MariaDB or MySQL. 
```sh
% mysql -u root -p opencast
```

Use the script [ImportCSV.SQL](https://github.com/opencast/helper-scripts/H2-Migration/) to import all data from the CSV files to the MariaDB or MySQL: 
```
mysql> source ImportCSV.sql;
```




