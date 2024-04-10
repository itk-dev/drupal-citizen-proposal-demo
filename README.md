# Drupal citizen proposal

Demo site for <https://github.com/itk-dev/drupal-citizen-proposal>.

## Development

Start the show:

```shell name=install
docker compose pull
docker compose up --detach
docker compose exec phpfpm composer install
```

Install and open site:

``` shell name=install-site
docker compose exec phpfpm vendor/bin/drush --yes site:install minimal --site-name='Citizen proposal'

# Add a little niceness
docker compose exec phpfpm vendor/bin/drush --yes theme:install claro olivero
docker compose exec phpfpm vendor/bin/drush --yes config:set system.theme admin claro
docker compose exec phpfpm vendor/bin/drush --yes config:set system.theme default olivero
docker compose exec phpfpm vendor/bin/drush --yes pm:enable toolbar

# install citizen proposal module
docker compose exec phpfpm vendor/bin/drush pm:enable citizen_proposal --yes
docker compose exec phpfpm vendor/bin/drush pm:enable citizen_proposal_openid_connect --yes
# Set the frontpage
docker compose exec phpfpm vendor/bin/drush --yes config:set system.site page.front '/citizen-proposal'

open "$(docker compose exec phpfpm vendor/bin/drush --uri=$(docker compose port nginx 8080) user:login /)"
```
