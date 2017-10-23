Case Management System Training Prototype
-----------------------------------

### To run on your machine:
1). git clone https://github.com/nyimbi/cms_train.git
cd cms_train

Create a database on your system called cms
2). createdb cms

3). Change th config.py file to reflect your username and password
SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost/cms’

4). fabmanager create-db
5). fabmanager create-admin
6). fabamanager run


### How we built this ####
https://editor.ponyorm.com/user/nyimbi/cmgmt_ke1/designer

Thats the link to the data model design.


Any statement that starts with a $ indicates things we types at the command prompt. Do not type the "$" :-)


1). First we created a new application using
$ fabmanager create-app

2). We initiated a git repository by
-  creating a repository on github called cms_train
- then initialized the local git repository

$ git init
- Associated the repository with a remote

$ git remote add origin https://github.com/nyimbi/cms_train.git

- Added the initial files to the local repository
$ git add .

- Not necessary by nice to do just to understand where we are
$ git status

- Made the first commit
$ git commit -m "Initial commit of CMS, nothing done yet"

- Pushed our local changes upstream
$  git push -u origin master

- Now we have our local and remote synchronized
# https://github.com/nyimbi/cms_train


3). Create a temp database for the schema
-  since we did not create a database for the user "shared" nor give them access to PostgreSQL, we need to do so. This is only done once in the lifetime of a machine or server

-  Change role to superuser
$ sudo -s

- login as the postgres user (masquerading)
$ su  - postgres
# note the space after the -

$ createuser shared
$ createdb shared
-  so that the user has their own database, should they need it ever

$psql 
- login to the PostgreSQL server as user postgres (who has super powers)
$$ alter user shared with password '....' createdb;

- $$ means to type in psql
- Look at https://www.postgresql.org/docs/9.4/static/sql-alteruser.html for the syntax of the ALTER USER command
-  I put ... for the password because this will eventually be on github and publicly available. NEVER WRITE PASSWORDS, KEYS in to a file that you manage with git

# Where we should be now
- we have created a temporary database called ctmp
- We exported the database schema from pony orm
- We have imported the schema into our ctmp database
- we have run gen_script.sh against our imported schema to generate models.py and views.py in the apps directory
- You might notice that every time you run gen_script it backsup your last version of models and views

# Now for the next and final steps
* We add the mixins.py to the apps folder
-  we will review mixins.py to see what it has to offer. If you have repeated database structures that you use, put those structures in mixins. Thus a Plaintiff, A Complainant, A Judge, A Prisoner are  all people who have names, DoB, Place of Birth etc - we create those fields in a mixin and any entity can inherit from them.

- We create the app database, not ctmp another one cms
$ createdb cms

- edit config.py so that it reflects this database 
- We now generate the actual database for the application using fabmanager create-db
- Then we edit the view to suit our tastes
- DONE 
 
Base Skeleton to start your application using Flask-AppBuilder
--------------------------------------------------------------

- Install it::

	pip install flask-appbuilder
	git clone https://github.com/dpgaspar/Flask-AppBuilder-Skeleton.git

- Run it::

	fabmanager run


That's it!!

