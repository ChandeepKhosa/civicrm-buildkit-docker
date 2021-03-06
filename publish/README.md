# Publishing Dockerfiles

The following script creates various CiviCRM Dockerfiles and associated assets.

At the moment, it creates Dockerfiles for `civicrm:php5.6` and `civicrm:php7.0`, both based on the appropriate `php:*.*-apache-jessie` base image. It could be extended to generate other versions of CiviCRM as well (e.g. `php7.0-fpm`)

It does not currently build images for the Dockerfiles or publish these images to Dockerhub (though it could be extended to do so).

## Usage

Until the above images are automatically published, you can use these files as follows:

1. Reference a different Dockerfile in the `docker-compose.yml` distributed with this repository:

```yml
civicrm:
  build: publish/civicrm/php5.6
```

2. Build and tag an image `docker build publish/civicrm/php5.6 -t civicrm:5.6`

## Updating Dockerfiles

1. From the `publish` directory, run `composer install`
2. Make any necessary changes to the `templates` and `publish.php` script.
3. Run `php publish.php`
4. Check the generated directories in `publish/civicrm`
5. Optionally, copy the contents of `publish/civicrm/php7.0` to `civicrm` with `cp -r publish/civicrm/php7.0/* civicrm`

## Publishing updates to https://hub.docker.com

Lets say you wanted publish the image for the civicrm container you are currently using. `docker ps` will show the list of containers in use. `docker inspect --format='{{.Image}}' $CONTAINER_ID` will give you the appropriate the Image ID.

You can then tag the image id with michaelmcandrew/civicrm like this `docker tag $IMAGE_ID michaelmcandrew/civicrm` and publish it with `docker push michaelmcandrew/civicrm`.
