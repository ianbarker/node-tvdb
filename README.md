# node-tvdb

[![wercker status](https://app.wercker.com/status/19dcad373ede868e37754a0367d68382/s/master "wercker status")](https://app.wercker.com/project/bykey/19dcad373ede868e37754a0367d68382)

Node.js library for accessing [TheTVDB API](https://api.thetvdb.com/swagger#/). Refactored from [joaocampinhos/thetvdb-api](https://github.com/joaocampinhos/thetvdb-api) to give nicer output and lots of additional features.

Pull requests are always very welcome.

## Features

- Handle errors from API as JavaScript errors
- Only returns relevant data (no need to call response.Data.Series etc.)
- Set language at initialisation or on each function call
- Return values through promises (dropped callback support)
- Use new JSON API from TheTVDB
- [Tests with Mocha and Wercker CI](https://app.wercker.com/#applications/53f155d02094f9781d058f98)

## Installation

Install with [npm](http://npmjs.org/):

``` shell
npm install --save node-tvdb
```

And run tests with [Mocha](http://mochajs.org):

``` shell
TVDB_KEY=[YOUR API KEY HERE] npm test
```

> _Mocha is installed as a development dependency; you do not need to install it globally to run the tests._

## Example Usage

To start using this library you first need an API key. You can request one [here](http://thetvdb.com/?tab=apiregister). Then just follow this simple example that fetches all the shows containing "The Simpsons" in the name.

``` javascript
let TVDB = require("node-tvdb");
let tvdb = new TVDB("ABC123");

tvdb.getSeriesByName("The Simpsons")
  .then(response => { /* process data */})
  .catch(error   => { /* handle error */});
```

## API

See [tests](test) and [theTvDb api documentation](https://api.thetvdb.com/swagger#/) for details about response data format.

### let client = new Client(API_KEY, [language])

Set up tvdb client with API key and optional language (defaults to "en")

``` javascript
let Client = require("node-tvdb");

let tvdb           = new Client("ABC123"); // lang defaults to "en"
let tvdbPortuguese = new Client("ABC123", "pt");
```

### getLanguages

Get available languages useable by TheTVDB API  
([thetvdb API](https://api.thetvdb.com/swagger#!/Languages/get_languages))

``` javascript
tvdb.getLanguages()
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesByName

Get basic series information by name  
([thetvdb API](https://api.thetvdb.com/swagger#!/Search/get_search_series))

``` javascript
tvdb.getSeriesByName("Breaking Bad")
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesById

Get basic series information by id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id))

``` javascript
tvdb.getSeriesById(73255)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesByImdbId

Get basic series information by imdb id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Search/get_search_series))

``` javascript
tvdb.getSeriesByImdbId("tt0903747")
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesByZap2ItId

Get basic series information by zap2it id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Search/get_search_series))

``` javascript
tvdb.getSeriesByZap2ItId("EP00018693")
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesAllById

Get series and episode information by series id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id) / [thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id_episodes))

``` javascript
tvdb.getSeriesAllById(73255)
    .then(response {
      /* handle response */
      console.log(response.seriesName); // response contains series data
      console.log(response.Episodes.length); // response contains an array of episodes
    })
    .catch(error { /* handle error */ });
```

### getEpisodesBySeriesId (alias: getEpisodesById)

Get all episodes by series id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id_episodes))

``` javascript
tvdb.getEpisodesBySeriesId(153021)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getEpisodeById

Get episode by episode id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Episodes/get_episodes_id))

``` javascript
tvdb.getEpisodeById(4768125)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getEpisodeByAirDate

Get series episode by air date  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id_episodes_query))

``` javascript
tvdb.getEpisodeByAirDate(153021, "2011-10-03")
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getActors

Get series actors by series id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id_actors))

``` javascript
tvdb.getActors(73255)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getSeriesBanner

Get series banner by series id  
([thetvdb API](https://api.thetvdb.com/swagger#!/Series/get_series_id_filter))

``` javascript
tvdb.getSeriesBanner(73255)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

### getUpdates

Get a list of series updated since one or between two given unix timestamps  
([thetvdb API](https://api.thetvdb.com/swagger#!/Updates/get_updated_query))

``` javascript
tvdb.getUpdates(1400611370, 1400621370)
    .then (response => { /* handle response */ })
    .catch(error    => { /* handle error */    });
```

## License

The MIT License (MIT)
