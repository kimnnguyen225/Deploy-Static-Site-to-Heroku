# How to deploy your static site HTML, CSS, JS to Heroku as a 'fake' PHP app

## What is Heroku? Why do this?
Heroku hosts *apps* on the internet, not *static website*. However, if you want it to run your static porfolio, personal blog, responsive landing page, etc., you can trick [Heroku](https://www.heroku.com/) to think your page is *PHP app*.

## Assumption
- You want to deploy a straight-up HTML, CSS, JavaScript, jQuery, and maybe some images
- You are in the root directory of your site (i.e. the directory that contains all subdirectories and files for the site.
- **Unless you have all of your subdirectories for CSS, JS, etc., and files like HTML in /home or /web as the root directory, then see additional instruction when create Procfile**
- The root directory contains a main HTML page, e.g. index.html
- You have an account with [Heroku](https://www.heroku.com/)
- You have [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) installed on your machine.
- A [Heroku app](https://devcenter.heroku.com/start) and remote are set-up and ready to go.

## Instruction steps
0. Run command, type: **heroku buildpacks:set heroku/php**
1. Add a file called *composer.json* to the root directory **by running cmd or directly from your project folder that you have it opened in IDE** --type: **touch composer.json** or --on command window, type: **type nul > composer.json** (this will create a zero bytes in compoer.json file) or another way, you type: **echo.> composer.json** (**echo.** will create a file with 1 empty line in it)
2. Open *composer.json* and add the following line: `{}`, then save file
3. Add a file called *index.php* to the root directory by running **cmd: touch index.php** or **nul > index.php**
4. Rename/Refactor your project's homepage (e.g. *index.html*) to *home.html*
5. Open *index.php* and add the following line: `<?php include_once("home.html"); ?>`, then save file
6. Add a file called [*Procfile*](https://devcenter.heroku.com/articles/procfile) ***without a file extension*, e.g. *Procfile.text* is not valid** to your app's root directory. It does not function if placed anywhere else.
7. Open *Procfile* and add the following line: `web: vendor/bin/heroku-php-apache2` **Notice:** if your root directory is /web or /home, then add the following line `web: vendor/bin/heroku-php-apache2 /web` or `web: vendor/bin/heroku-php-apache2 /home`
8. Save everything and run `git push heroku master`

## Instruction of how to host your static website *HTML* as *'fake'* PHP app using cmd/heroku CLI git will be under

**https://dashboard.heroku.com/apps/*your-app-name*/deploy/heroku-git**

Once your app is finished deployed to Heroku, you can go back to Heroku and clicks on *Open app* on top right corner (May 2019) or on cmd, type: **start chrome *(or browser of your choice)* https://*yourappname*.herokuapp.com/**

## Dependencies
### For example:
- If your app runs jQuery, then you can go to [CNDJS](https://cdnjs.com/) and search for *jquery*, CND will give you a list of results that it found for the library that your app depends on, hover over the one you want to copy script tag, then place it inside your HTML file. **Benefits?** jQuery library will be pulled from the internet directly versus local file.
