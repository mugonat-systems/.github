# .github

# Deploying Laraval Apps

## Checklist
- [] Package [`spatie/laravel-backup`](https://spatie.be/docs/laravel-backup/v5/installation-and-setup) for automated backups
- [] Package [`sentry/sentry-laravel`](https://docs.sentry.io/platforms/php/guides/laravel/) for application error monitoring
- [] Package [`laravel/pulse`](https://laravel.com/docs/12.x/pulse#installation) for realtime performance monitoring 

## Initial Deployement
- On your local machine run `npm run build` which will create a folder `public/build`, with the optimized assets for your app
- Upload all files except `vendor`, `node_modules`, `storage` folders
- On the server in the application root directory run:
- `mkdir storage storage/framework storage/app storage/app/private storage/app/public storage/framework/cache storage/framework/cache/data storage/framework/sessions storage/framework/views`
- `composer install --no-dev --optimize-autoloader`
- Check your `.env` file for correct config such as database connection, environment, app url, debug etc
- If using laravel-auto/migrations run `php artisan migrate:auto`, otherwise run `php artisan migrate`
- Run `php artisan db:seed` if you have default seeders that need to be run
- `php artisan optimize` to cache everything

## Running an update deployment
- `php artisan backup:run` to safekeep your existing instance
- Upload changed files making sure not to replace or delete anything inside `storage/*` folder
- `composer install --no-dev --optimize-autoloader` to update any changes to your depnedencies
- If using laravel-auto/migrations run `php artisan migrate:auto`, otherwise run `php artisan migrate`
- `php artisan optimize` to cache everything
