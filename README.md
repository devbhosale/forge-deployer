# Forge Deployer

A simple zero-downtime deployment tool for [Laravel Forge](https://forge.laravel.com/) using [Deployer](https://deployer.org)

## Features

* Configuration options are set via the .env file
* Automatic roll-back if site appears offline after deployment

## Usage

Proceed to create a new site in Forge as you normally would do, but set the web directory to `/current/public`.

After the site has been provisioned head on over the site details and install this Git Repository: `est73/forge-deployer`

Once deployed edit the environment file to make necessary changes. Please make sure to update these variables:

* `APP_URL` *Site url*
* `DEPLOYER_REPOSITORY` *Repository to deploy*
* `DEPLOYER_PHP_VERSION` *PHP version on the Forge server as noted in the Forge Deploy Script*

## Forge Apps setting

* Make sure `Quick Deploy` is **OFF**
* Update the `Deploy Script` to add our Deployer command. *Note the default Forge script has been commented out after the directory change.*
```shell
cd /home/forge/example.com
#git pull origin master
#composer install --no-interaction --prefer-dist --optimize-autoloader
#echo "" | sudo -S service php7.1-fpm reload

#if [ -f artisan ]
#then
#    php artisan migrate --force
#fi

# Initiate Deployer
php vendor/bin/dep forge:deploy
```
* Initiate a deployment by using the `DEPLOY NOW` button in Forge.
* (Optional) Add the `Deployment Trigger URL` to your production repository for automatic deployments.
## Deploy Task

Additional task helpers can be added to the default deploy under these variables:

* `DEPLOYER_BEFORE` *Task to run before the deploy*
* `DEPLOYER_ARTISAN` *Artisan commands during the deploy*
* `DEPLOYER_AFTER` *Task to run after the deploy*

Task can be chained together with the usage of a `|` *example:* `artisan:up|artisan:migrate|artisan:down`

## Available Task Helpers

* `artisan:up` *Disable maintenance mode*
* `artisan:down` *Enable maintenance mode*
* `artisan:migrate` *Execute artisan migrate*
* `artisan:migrate:rollback` *Execute artisan migrate:rollback*
* `artisan:migrate:status` *Execute artisan migrate:status*
* `artisan:db:seed` *Execute artisan db:seed*
* `artisan:cache:clear` *Execute artisan cache:clear*
* `artisan:config:cache` *Execute artisan config:cache*
* `artisan:route:cache` *Execute artisan route:cache*
* `artisan:view:clear` *Execute artisan view:clear*
* `artisan:optimize` *Execute artisan optimize*
* `artisan:queue:restart` *Execute artisan queue:restart*
* `artisan:storage:link` *Execute artisan storage:link*
* `site:status` *Check site status, and rollback deploy if down*



