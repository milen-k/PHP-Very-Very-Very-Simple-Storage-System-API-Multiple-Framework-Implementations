# v3s3-laravel5
A Very Very Very Simple Storage System (V3s3) RESTful API written in Laravel 5<br />
<br />
This is part of a collection of repositories which provides an implementation of a simple storage system RESTful API using different PHP Frameworks. The project aims to directly compare the differences in setup and syntax between each of the represented frameworks.<br />
<br />
See the Wiki page for a hyperlinked list of all the repositories in the collection.
<hr />
# THE DEVELOPMENT PROCESS
**1. INSTALLING LARAVEL**
```
cd /path/to/htdocs
composer create-project --prefer-dist laravel/laravel v3s3-laravel5
```
<br />
**2. CONFIGURING APACHE**
The project's document root should be `/path/to/htdocs/v3s3-laravel5/public`.<br />
If you want to avoid the overhead caused by Apache when parsing `.htaccess` files you can disable config overriding by setting `AllowOverride None` on the project root directory and use your global Apache configuration _(ex. httpd.conf)_. Check the `/path/to/htdocs/v3s3-laravel5/example_apache_virtualhost.conf` file for reference.<br />
<br />
**3. CODE GENERATOR**
Laravel 5 comes with a command line interface (CLI) located at `/path/to/htdocs/v3s3-laravel5/artisan`. It can be used to create a basic (skeleton) version of some of the project-specific components.
```
cd /path/to/htdocs/v3s3-laravel5
php artisan make:model --controller -- V3s3
```
This creates 2 files:<br />
**/path/to/htdocs/v3s3-laravel5/app/V3s3.php** (the model)<br />
**/path/to/htdocs/v3s3-laravel5/app/Http/Controllers/V3s3Controller.php** (the controller)<br />
The classes have neither methods nor properties.<br />
A "CRUD" version of the controller could be created by passing an extra parameter like so: `php artisan make:model --controller --resource -- V3s3`. This will add `index`, `create`, `store`, `show`, `edit`, `update`, `destroy` methods to the `V3s3Controller` class along with some dependencies injected in some of the methods as parameters. The **V3s3 API** is non-standard and has only 4 methods.<br />
<br />
**4. FRAMEWORK CONFIG AND EXCLUSION OF LOCAL PARAMETERS**
Laravel has a local parameters file which is excluded using `.gitignore`:<br />
**/path/to/htdocs/v3s3-laravel5/.env** (database connection credentials are be specified here; the project uses `mysql-v3s3` as connection name (`DB_CONNECTION` value); the `.env.example` file contains an example template)<br />
The default database connection name must be specified and configured with the `.env` parameters in the framework database config file `/path/to/htdocs/v3s3-laravel5/config/database.php`.<br />
<br />
There are 2 files where routes can be specified each one having its trade-offs:<br />
**/path/to/htdocs/v3s3-laravel5/routes/api.php**<br />
and<br />
**/path/to/htdocs/v3s3-laravel5/routes/web.php**<br />
The routes are organized in so-called "route groups" with the `api.php` routes falling under the **"api"** group and the `web.php` routes under the **"web"** one.<br />
The **"api"** routes are prefixed with an `/api` segment so if we want to use the `api.php` file all URL paths will need to start with `/api`. This behavior can be altered by removing the `prefix('api')` on lines 68 and the `->` on line 69 in `/path/to/htdocs/v3s3-laravel5/app/Providers/RouteServiceProvider.php`.<br />
This project uses the `web.php` file for specifying the API routes. By default Laravel 5 loads several "middleware" for the **"web"** group with some of them completely irrelevant for a RESTful API (like session and cookie services) and a CSRF token verify service which causes a `TokenMismatchException` on data submission requests (like PUT and POST) if no token has been provided. Thus these services should be commented out in `/path/to/htdocs/v3s3-laravel5/app/Http/Kernel.php` which will also save some of the overhead caused by loading them.<br />
<br />
**5. ROUTING**
Other than the above routing is pretty straightforward and specified in the `/path/to/htdocs/v3s3-laravel5/routes/web.php` file.<br />
<br />
**6. THE MODEL**
The database table which the model is associated with is specified in the model class `protected $table` property.<br />
<br />
**7. I18N**
Laravel 5 supports PHP array file translation resources and the files are stored in the `/path/to/htdocs/v3s3-laravel5/resources/lang/<language id>` directory. 
# NOTABLE NEW/MODIFIED PROJECT-SPECIFIC FILES
**/path/to/htdocs/v3s3-laravel5/LV5-readme.md** (renamed from `readme.md`)<br />
**/path/to/htdocs/v3s3-laravel5/README.md** (new)<br />
**/path/to/htdocs/v3s3-laravel5/example_apache_virtualhost.conf** (new)<br />
**/path/to/htdocs/v3s3-laravel5/public/.env.example** (modify lines 9-13)<br />
<br />
**/path/to/htdocs/v3s3-laravel5/public/.env** (modify lines 9-13) (excluded using `.gitignore`)<br />
**/path/to/htdocs/v3s3-laravel5/config/database.php** (modify line 16 and add lines 57-72)<br />
<br />
**/path/to/htdocs/v3s3-laravel5/app/Providers/RouteServiceProvider.php** (comment out lines 30, 31, 32, 34, 35)<br />
<br />
**/path/to/htdocs/v3s3-laravel5/routes/web.php** (add lines 17-23)<br />
<br />
**/path/to/htdocs/v3s3-laravel5/resources/lang/en/V3s3Translation.php** (new)<br />
**/path/to/htdocs/v3s3-laravel5/app/Modules/V3s3/Controllers/V3s3Controller.php** (new)<br />
**/path/to/htdocs/v3s3-laravel5/app/Modules/V3s3/Exception/V3s3InputValidationException.php** (new)<br />
**/path/to/htdocs/v3s3-laravel5/app/Modules/V3s3/Helpers/V3s3Html.php** (new)<br />
**/path/to/htdocs/v3s3-laravel5/app/Modules/V3s3/Helpers/V3s3Xml.php** (new)<br />
**/path/to/htdocs/v3s3-laravel5/app/Modules/V3s3/Models/V3s3.php** (new)<br />

