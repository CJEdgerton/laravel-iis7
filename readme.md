# Steps to get Laravel site working on IIS7

## Server Setup: 
- Install PHP
- Install Composer
- Install Git ( include the installation of git command line tools )
- Check php.ini settings ( reference included file )
- Ensure that you have enabled the necessary "extensions"
  - Click root of server in Server Manager
  - PHP manager
  - Enable or disable plugins
  - Make sure that you have the correct extensions enabled based on PHP versions used etc
  - Extensions are stored in ProgramFiles\PHP\version\ext\, download them there if needed.
    >The extensions that you enable are global despite the menu appearing on the root of the server, AND within each created site. Enable all extensions that are used for any application, even if applications are using different PHP versions and different extensions.


## Application Setup:

1. Download the application / setup Laravel parts
   - `cd` into whatever directory you serve applications from 
   - `git clone` application
   - `cd` into application
   - run `composer install`
   - run `composer update`
   - configure your .env file
   - set application key: `php artisan key:generate`
      >Never lose the key!!! You will not be able to decrypt any encrypted data if you change the key!!!
   - run `composer dump-autoload`
   - run migrations: `php artisan migrate` | `php artisan db:seed` ( varies by case )

2. Copy the web.config that is in this directory to the public dir of your application
   - example: wwwroot\apps\test_app\public

3. Create a new site in Server Manager
   - Go to Server Manager
   - Right click Sites
   - Add Web Site
   - Set name
   - Set physical path to public directory of application
      - This can also be editted if needed at: Actions > Basic Settings > Physical Path > E:\wwwroot\apps_dir\test_app\public
   - Set http binding to IP and host.
      - This can also be editted if needed at: Edit Bindings on right menu  

4. Change permissions of app's storage folder
   - In File Explorer go to your application's storage folder. example: wwwroot\apps_dir\test_app\public\storage
   - Set IUSR permissions to "Full Control" 
      - Right click -> Properties
      - Security Tab
      - Select IUSR
      - Edit
      - Check Full Control

## *** Important Notes ***

- If using Datatables
   - Go to site
   - Choose Request Filtering
   - Click the URL tab in middle of screen
   - Choose Edit Feature Setting 
   - Change the value of the "Max Query String" field
      - Default limit is sometimes to low and causes datatable's request to throw a 404 or other error

- Application Key
   - Once application key is set and any encryted data has been stored, DO NOT change it.
   - The key is used to decrypt any hashed passwords or data encrypted with Laravel encryption helpers.

- PHP Extensions
   - The extensions that you enable are global despite the menu appearing on the root of server, and within each application's (site's) main menu.
   - Enable all extensions that are used for any application, even if applications are using different PHP versions and different extensions. 



