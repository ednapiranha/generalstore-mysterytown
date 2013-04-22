# General Store

## What it is

A 2D adventure game maker.

## Setup instructions

Install [node](http://nodejs.org)

Clone the repository

> git clone git://github.com/ednapiranha/generalstore.git

> cd generalstore

> cp local.json-dist local.json

> npm install

## Setting up nunjucks

This will allow you to compile your templates for production

To read more about nunjucks, check out the [documentation](http://nunjucks.jlongster.com)

Download nunjucks and add it to `generalstore/media/js/lib/nunjucks.js`

If you are on development mode, use [nunjucks-dev.js](https://github.com/jlongster/nunjucks/blob/master/browser/nunjucks-dev.js)

If you are on production and have precompiled your templates, use [nunjucks.js](https://github.com/jlongster/nunjucks/blob/master/browser/nunjucks.js)

## Precompiling templates for nunjucks

In development mode, make sure `generalstore/media/js/templates.js` only has the following:

    define(function() {});

In production mode, run the following:

    node_modules/nunjucks/bin/precompile generalstore/templates > generalstore/media/js/templates.js

## Minifying files with Grunt

> node_modules/grunt-cli/bin/grunt

## Configure settings

Create `generalstore/media/js/local_settings.js` and paste the following:

    define([],
      function () {

      'use strict';

      return {
        DEBUG: true
      };
    });

If this is in production mode, change DEBUG to false.

## Run the development site

> node app.js

## Setting up stories

> cd stories

Edit stories in a text editor with the following format:

    level
    1

    location
    A crazy party hut

    background_image
    partyhut.jpg

    description
    This is the party hut!

    character
    name: partybear
    image: partybear.png
    left: 100
    top: 400
    requires: false
    gives: mango
    first_says: Hey there, here is a mango!
    finally_says: I already gave you a mango!

    item
    name: car
    image: car.gif
    left: 500
    top: 400
    requires: mango
    gives: gas
    levels_up_to: 2

All character and item level and name properties are used to generate a unique id. E.g. A level 1 character with the name 'bunny' generates a unique id of 1-bunny.

The story properties represent the following:

* level - The level that this file represents. You can only have one unique level per file.
* location - The location name of the level
* background_image - The image used in the level's main background. If this is a png or gif, replace the extension.
* description - An optional description of the location; write 'false' as the content if you want it to be empty. You can also configure generalstore/config/defaults.json to never show descriptions.
* character - Contains the properties for each character. All properties are mandatory.
* character name - Name of the character.
* character image - Filename of the character image. Save the file in `generalstore/media/images/characters/`.
* character left - Position of the character from the left. Set your game dimensions in generalstore/config/defaults.json
* character top - Position of the character from the top.
* character requires - If an inventory object is needed to be given to the character before an initial interaction is triggered, enter it here. Otherwise, write 'false'.
* character gives - This is what the character gives to the player after initial interaction. If nothing needs to be given, write 'false'.
* character first_says - This is what the character first says to the player on initial interaction.
* character finally_says - This is what the character says on subsequent interactions.
* item - Contains the properties for each item. All properties are mandatory.
* item name - Name of the item. The level and name generate a uniqud id and this will dobule as your item's image filename.
* item image - Filename of the item image. Save the file in `generalstore/media/images/items/`.
* item left - Position of the item from the left.
* item top - Position of the item from the top.
* item requires - If an inventory object is needed to trigger an item's response (especially if there is a `gives` or `levels_up_to` set), enter it here. Otherwise, write 'false'.
* item gives - This is what the item provides the player either on initial interaction or if `requires` is fulfilled.
* item levels_up_to - If `requires` is fulfilled for the item, the scene will change to the level set here.

Once you've completed your txt files, run [http://localhost:3000/generate](http://localhost:3000/generate) in your browser to regenerate the configuration.

## Ready to deploy as a finished standalone package?

You only need the contents within generalstore/generalstore (e.g. config/, media/, templates/, main.html).

After precompiling nunjucks to templates.js and minifying with grunt, main.html should work as is.

Note that you must run this on some kind of webserver and point to main.html as the default landing page.

## Running tests

> make test

and also

Load `generalstore/test/tests.html` in a browser
