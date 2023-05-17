# Files Sharing

>  
> FILES SHARING VERSION 2 JUST RELEASED
>  


## Description

This PHP application based on Laravel 10.9 allows to share files like Wetransfer. You may install it **on your own server**. It **does not require** any database system, it works with JSON files into the storage folder. It is **multilingual** and comes with english and french translations for now. You're welcome to help translating the app.

This application provides two links per bundle :
- a bundle preview link : you can send this link to your recipients who will see the bundle content. For example: http://yourdomain/bundle/dda2d646b6746b96ea9b?auth=965242. The recipient can see all the files of the bundle and download the bundle as a ZIP archive.
- a bundle download link : you can send this link yo your recipients who will download all the files of the bundle at once (without any preview). For example: http://yourdomain/bundle/dda2d646b6746b96ea9b/download?auth=965242.

Each of these links comes with an authorization code. This code is the same for the preview and the download links.

The application also comes with a Laravel Artisan command as a background task who will physically remove expired bundle files of the storage disk. This command is configured to run every five minutes among the Laravel scheduled commands.

## Features

- uploader access permission: IP based or login/password
- creation of a new bundle
- define settings : title, description, expiration date, number max of downloads, password...
- upload one or more files via drag and drop or via browsing your filesystem
- ability to keep adding files to the bundle days later
- sharing link with bundle content preview
- ability to download the entire bundle as ZIP archive (password protected when applicable)
- direct download link (doesn't preview the bundle content)
- garbage collector which removes the expired bundles as a background task
- multilingual (EN and FR)
- easy installation, **no database required**
- secured by tokens, authentication codes and non-publicly-accessible files

## Demo

A video demo is available [on Youtube](https://youtu.be/hO4tRaZa4N4)

![demo image](https://github.com/axeloz/filesharing/blob/main/public/images/capture.png "Demo Image")

## Requirements

Basically, nothing more than Laravel itself:
- PHP >= 8.1
- Ctype PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

Plus:
- JSON PHP Extension (included after PHP 5.2+)
- ZipArchive PHP Extension (included after PHP 5.3+)

The application also uses:
- http://www.dropzonejs.com/
- https://alpinejs.dev/
- https://tailwindcss.com/
- https://momentjs.com/
- https://axios-http.com/
- https://lodash.com/

## Installation

- configure your domain name. For example: files.yourdomain.com
- clone the repo or download the sources into the webroot folder
- configure your webserver to point your domain name to the `./public` folder
- run `composer install`
- run `yarn --production` (or `npm install --production`)
- run `yarn build` (or `npm run build`)
- make sure that the PHP process has write permission on the `./storage` folder
- generate the Laravel KEY: `php artisan key:generate`
- run `cp .env.example .env` and edit `.env` to fit your needs
- (optional) you may create your first user `php artisan fs:create-user`
- start the Laravel scheduler (it will delete expired bundles of the storage). For example `* * * * * /usr/bin/php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1`
- (optional) to purge bundles manually, run `php artisan fs:purge-expired`


Use your browser to navigate to your domain name (example: files.yourdomain.com) and **that's it**.

## Configuration

In order to configure your application, copy the .env.example file into .env. Then edit the .env file.

| Configuration | Description |
| ------------- | ----------- |
| `APP_NAME`    | the title of the application |
| `APP_ENV`     | change this to `production` when in production (`local` otherwise) |
| `APP_DEBUG` | change this to `false` when in production (`true` otherwise) |
| `APP_TIMEZONE` | change this to your current timezone |
| `APP_LOCALE` | change this to "fr" or "en" |
| `UPLOAD_PREVENT_DUPLICATES` | Should the app block duplicate files (true / false) |
| `HASH_MAX_FILESIZE`| max size for hashing file to check for duplicate files. If files are bigger than limit, they will not be hashed. Find the best value for better cpu / memory consumption |
| `UPLOAD_MAX_FILES` | (*optional*) maximal number of files per bundle |
| `UPLOAD_MAX_FILESIZE` | (*optional*) change this to the value you want (K, M, G, T, ...). Attention : you must configure your PHP settings too (`post_max_size`, `upload_max_filesize` and `memory_limit`). When missing, using PHP lowest configuration |
| `UPLOAD_LIMIT_IPS` | (*optional*) a comma separated list of IPs from which you may upload files. Different formats are supported : Full IP address (192.168.10.2), Wildcard format (192.168.10.*), CIDR Format (192.168.10/24 or 1.2.3.4/255.255.255.0) or Start-end IP (192.168.10.0-192.168.10.10). When missing, filtering is disabled. |


## Authentication

You may provide a list of IPs to limit access to the upload feature.  
Or you can create users with login/password credentials.   
You can also **mix the two methods**.

>  
> Warning: if your leave the `UPLOAD_LIMIT_IPS` empty and you don't create users, the upload will be publicly accessible
>  

## Known issues

If you are using Nginx, you might be required to do additional setup in order to increase the upload max size. Check the Nginx's documentation for `client_max_body_size`.

## Development

If your want to modify the sources, you can use the Laravel Mix features:
- configure your domain name. For example: files.yourdomain.com
- clone the repo or download the sources into the webroot folder
- configure your webserver to point your domain name to the public/ folder
- run a `composer install`
- run a `yarn install`
- run a `yarn dev` in order to recompile the assets when changed

## Roadmap / Ideas / Improvements

There are many ideas to come. You are welcome to **participate**.
- add PHP unit testing
- more testing on heavy files
- customizable / white labeling (logo, name, terms of service, footer ...)

## Licence

GPLv3

| Permissions     | Conditions                    | Limitations |
| --------------- | ----------------------------- | ----------- |
| Commercial use  | Disclose source               | Liability   |
| Distribution    | License and copyright notice  | Warranty    |
| Modification    | Same license                  |             |
| Patent use      |  State changes                |             |
| Private use     |                               |             |

https://choosealicense.com/licenses/gpl-3.0/

## Welcome on board

If you are willing to **participate** or if you just want to talk with me : axel@mabox.eu


Powered by
<p><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>
