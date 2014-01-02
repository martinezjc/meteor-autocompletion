meteor-autocompletion
=====================

`meteor-autocompletion` provides autocompletion to `<input>` fields in [MeteorJS](https://meteor.com). The package will search for the inputed text in a MeteorJS collection and return similar results. Results can be choosed using the arrow keys and enter or by clicking with the mouse.

![Autocompleting a name](https://raw.github.com/sebdah/meteor-autocompletion/master/docs/example.png)

Installation
------------

Install `meteor-autocompletion` using [Meteorite](http://oortcloud.github.io/meteorite/):

    mrt add meteor-autocomplete

Configuration
-------------

We will use a collection called `Friends` in the example below to search for friends names when typing in the `<input>` field.

Check out the MeteorJS example app in the `example` directory for a full example.

### Example client HTML

Add an `<input>` field to your template with an `id` attribute:

    <head>
      <title>meteor-autocompletion test app</title>
    </head>

    <body>
      <h1>meteor-autocomplete test app</h1>
      {{>search}}
    </body>

    <template name="search">
      <h3>Search</h3>
      <input type="text" id="searchBox">
    </template>

### Example client JavaScript

Then add JavaScript code similar to the below.

    /**
    * Template - search
    */
    Template.search.rendered = function () {
      AutoCompletion.init("input#searchBox");
    }

    Template.search.events = {
      'keyup input#searchBox': function () {
        AutoCompletion.autocomplete({
          element: 'input#searchBox',       // DOM identifier for the element
          collection: Friends,              // MeteorJS collection object
          field: 'name',                    // Document field name to search for
          limit: 0,                         // Max number of elements to show
          sort: { name: 1 }});              // Sort object to filter results with
          //filter: { 'gender': 'female' }}); // Additional filtering
      }
    }

Take extra care looking at the parameters to `AutoCompletion.autocomplete`. We are in this example fetching data from the element with identifyer `input#searchBox`. We will then match the text with the `name` field in the `Friends` collection. You can limit the number of returned rows using `limit` and send any sorting directions using `sort`. In this case, we're sorting the names from A to Z.

### Configuration options

The following configuration options can be sent to `AutoCompletion.autocomplete`:

`element` - DOM identifier for the element

`collection` - MeteorJS collection object

`field` - Field name in the collection to search

`limit` - Limit the number of results. `0` will return all results.

`sort` - Pass a MongoDB sorting object to the query

`filter` - Pass additional filtering rules to the query
