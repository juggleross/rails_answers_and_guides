`# articles`

      https://coursehunters.net/course/egghead-get-started-with-postgresql
      http://sqlfiddle.com #postgresql fiddle

1. How you can install gem pg?
      
            sudo apt-get install libpq-dev
            gem install
2. How you can install pg?
            
            sudo apt-get update
            sudo apt-get install postgresql postgresql-contrib
3. How you can begin work with pg?
      
            sudo -i -u postgres
            psql
4. How you can add new pg user?
            
            # as postgres user:
            # createuser --interactive
            
            Output
                  Enter name of role to add: sammy
                  Shall the new role be a superuser? (y/n) y
5. How you can select user?
      
            sudo adduser sammy
            sudo -i -u sammy
            psql
6. How you can create db for user?
            
            createdb sammy
7. How you can select db?
            
            psql -d postgres
10. How you can setup all pg database for rails app?  
            
            tp> sudo -u postgres createuser rubyuser -s
            tp> sudo -u postgres psql
            
            postgres=# CREATE DATABASE library_development OWNER rubyuser; 
            
            # Configuring database.yml
            
            default: &default
               adapter: postgresql
               encoding: unicode

            development:
               adapter: postgresql
               encoding: unicode
               database: library_development
               username: rubyuser
               password: <Password for rubyuser>

            test:
               -\\-

            production:
               -\\-
 2. How you can change user pg password?
      
            # run psql and write:
            postgres=# alter role pushkin password '1'
            # or 
            postgres=# \password pushkin
            
# ------------------------------------PostgreSQL - Syntax----------------------------------------------------

8. How you can watch curent db?
      
            \conninfo
9. How you can watch list of all existing database?
            
            \list or \l
10. How youc can connected to database?
            
            \c database_name
2. How you can create or destroy database?
            
            CREATE DATABASE name;
            DROP DATABASE name;
            
3. How you can create/drop table?
            
            CREATE TABLE COMPANY(
               ID INT PRIMARY KEY     NOT NULL,
               NAME           TEXT    NOT NULL,
               AGE            INT     NOT NULL,
               ADDRESS        CHAR(50),
               SALARY         REAL
            );
            
            # drop 
            DROP TABLE COMPANY
            
4. How you can watch list of all table?
            
            \d 
            # and with with describe table 
            \d table_name
5. How you can insert value into table?         
             
             INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS) VALUES (1, 'Paul', 32, 'California');
6. How you can select value from table?
            
            SELECT ID, NAME, SALARY FROM COMPANY ;
            or 
            select * from company;
7. How you can update value?        
            
            UPDATE table_name
            SET column1 = value1, column2 = value2...., columnN = valueN
            WHERE [condition];
8. How you can delete the existing records from a table?
            
            DELETE FROM angels WHERE surname='BY';
9. How you can sort records by name?
            
            SELECT * FROM COMPANY ORDER BY NAME DESC;
            
# ------------------------------------PostgreSQL - PROBLEMS----------------------------------------------------

3. How you can fix problem: psql: FATAL: Peer authentication failed for user “rubyuser”?
            
            1. Open /etc/postgresql/9.5/main/pg_hba.conf with root access
              sudo nano /etc/postgresql/9.5/main/pg_hba.conf
            2. Change peer to md5 in these lines.

            Before changing
                  # "local" is for Unix domain socket connections only
                  local   all             all                                     peer
                  # IPv4 local connections:
                  host    all             all             127.0.0.1/32            peer
                  # IPv6 local connections:
                  host    all             all             ::1/128                 peer
            After your change
                  # "local" is for Unix domain socket connections only
                  local   all             all                                     md5
                  # IPv4 local connections:
                  host    all             all             127.0.0.1/32            md5
                  # IPv6 local connections:
                  host    all             all             ::1/128                 md5
           3. Save the file with pressing Ctrl-O. Exit nano with Ctrl-X
           4. Restart postgresql using
                  sudo service postgresql restart
            
5. How to install pg to macOSX?     
            
            https://gist.github.com/lxneng/741932
6. Unistal postgres?

             https://gist.github.com/mrcasals/2788529
7. Working database for pg?
            
       default: &default
         adapter: postgresql
         encoding: unicode
         username: postgres
         host: localhost
         # For details on connection pooling, see rails configuration guide
         # http://guides.rubyonrails.org/configuring.html#database-pooling
         pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

       development:
         <<: *default
         database: sakurami_development

       test:
         <<: *default
         database: sakurami_test

       production:
         <<: *default
         database: sakurami_production
8. How to install pg gem for mac? 

            # you need to install PG first https://postgresapp.com/downloads.html
            
            gem install pg -- --with-pg-config=/Applications/Postgres.app/Contents/Versions/latest/bin/pg_config
            
9. How to add command line commands for Postgresql APP on mac?
            
            sudo mkdir -p /etc/paths.d &&
            echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp

10. How to download pg_dump from a remote server?

            pg_dump your_project_production -U your_project_production --password --host 10.6.240.111 > prod.sql
            psql your_project_development < prod.sql
