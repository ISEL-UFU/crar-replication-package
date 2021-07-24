Improved Retrieval of Programming Solutions with Code Examples Using a Multi-featured Score
=========================================================================================

```
Improved Retrieval of Programming Solutions with Code Examples Using a Multi-featured Score
Rodrigo F. Silva; Mohammad Masudur Rahman; Carlos Eduardo C. Dantas; Chanchal Roy; Foutse Khomh; Marcelo A. Maia
```

[![DOI](https://zenodo.org/badge/138428994.svg)](https://zenodo.org/record/5115300#.YPxYDTrQ9H6)

Prerequisites
-----------------------------------------------------------

Note: all the experiments were conducted over a server equipped with 86 GB RAM, 3.1 GHz on 12 cores and 64-bit Linux Mint Cinnamon operating system. We strongly recommend a similar or better hardware environment. The operating system however could be changed.

Softwares:
    1. Java 1.8
    2. Postgres 12.7 - Configure your DB to accept local connections. An example of pg_hba.conf configuration:

..
\# TYPE  DATABASE        USER            ADDRESS                 METHOD
\# "local" is for Unix domain socket connections only
local   all             all                                     md5
\# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
..

3. PgAdmin (we used PgAdmin 4) but feel free to use any DB tool for PostgreSQL.


Configuring the dataset
-----------------------------------------------------------

    1. Download the SO Dump of March 2019 (backup2019crar-min.backup). This is a preprocessed dump, downloaded from the official web site containing the main tables we use. We only consider Java posts. Postsmin table (representing posts table) has extra columns with the preprocessed data used by Crar.

    2. On your DB tool, create a new database named stackoverflow2019journaldycrokage. This is a query example:

CREATE DATABASE stackoverflow2019journaldycrokage
  WITH OWNER = postgres
       ENCODING = 'UTF8'
       TABLESPACE = pg_default
       LC_COLLATE = 'en_US.UTF-8'
       LC_CTYPE = 'en_US.UTF-8'
       CONNECTION LIMIT = -1;

    3. Restore the downloaded dump to the created database.
    
Obs: restoring this dump would require at least 30 Gb of free space. If your operating system runs in a partition with insufficient free space, create a tablespace pointing to a larger partition and associate the database to it by replacing the "TABLESPACE" value to the new tablespace name: TABLESPACE = tablespacename.

    4. Assert the database is sound. Execute the following SQL command: “select id, title,sentencevectors from postsmin po limit 100”.


Running CRAR
-----------------------------------------------------------


Download the artifacts
-----------------------------------------------------------

Download the project folder. Place it preferably in your home folder, ex /home/user/crar. Check your installation. Make sure your crar folder (/home/user/crar) contains this structure:

..
./data 
crar.jar
replication-package-application.properties
...

Note: for now we only provide the replication package. The complete source code will be released soon.

Setting Parameters
-----------------------------------------------------------

Edit replication-package-application.properties and set the ######### Must be set following parameters:

CRAR_HOME = the root folder of the project (ex /home/user/crar) where you must place the project artifacts (crar.jar, data folder, replication-package-application.properties).

spring.datasource.username = your db user

spring.datasource.password= = your db password

spring.datasource.url= your database URL, as for example: jdbc:postgresql://localhost:5432/stackoverflow2019journaldycrokage.

Running the jar
-----------------------------------------------------------

Open a terminal, go to the project folder and run the following command: java -Xms1024M -Xmx50g -jar crar.jar --spring.config.location=./replication-package-application.properties . This command uses the file replication-package-application.properties to overwrite the default parameters which must be set as described above. The results will be displayed in the terminal. The total duration of the experiment is around 2 hours. 
