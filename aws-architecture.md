# AWS Architecture

Our project uses AWS to deploy applications through Elastic Beanstalk, S3, and RDS.

### Elastic Beanstalk

The teacher platform and backend are both deployed through Elastic Beanstalk. There are variables within the Elastic Beanstalk environment for both the backend and teacher platform that connect it to the correct components.

#### Backend

The variables include:

* `DATABASE_HOST` - the URL to the database server
* `DATABASE_NAME` - the name of the database used
* `DATABASE_USER` - the username to log in with on the database server
* `DATABASE_PASSWORD` - the password for the database server
* `DEBUG` - whether to put the server in debug mode or not
* `SECRET_KEY` - a Django secret key which must be set \(should probably be random\)

#### Teacher platform

The variables include:

* `BACKEND_API_URL` - the url to the backend you would like to use
* `GAME_LINK` - the link to the Parlay Island game

### S3

The game is deployed using Amazon S3 statically serving up the contents of the WebGL package.

### RDS

The database for the stage and prod backend is stored in RDS in a single PostgreSQL database server. They use two different database names to separate out the data without requiring another instance.

