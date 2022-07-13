## Data Classification App (DCA)

The Data Classification App is a project that belongs to the Alan Turing Institute and the code base is not available within the NewcastleRSE project listing.

The Docker image used `python3.8-nodejs16` contains both Python and Node as we use npm commands in the Dockerfile to install Gulp. Gulp is used within the Django app to compile and minify CSS and JS files.

### Development

The DCA is a Django application that utilises a Postgres database. In a local development environment only 2 containers are set up in the docker-compose.yml file: the Postgres db and the Django app. Python's own webserver is used to run the application locally on port 8000. 


### Production

In the production environment, the set-up is more complex. There are multiple containers created: Postgres db, the Django app, Nginx, Certbot, Authelia and Redis.

Authelia is multi-factor authentication (MFA) gateway application. Its has Redis as dependency. Certbot is used with a letsEncrypt generation file (not included here) to provide SSL certification.

Nginx is used as a router to map domain requests to Authelia first, then if Authentication is successful, the user is logged directly into the DCA. Gunicorn is a Python based webserver that handles running the application. 

Authlelia integration with Nginx required that a main hosting domain was created with sub-domains, and these were used as part of the Nginx routing strategy.
