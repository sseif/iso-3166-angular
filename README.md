## ISO 3166 for Angular JS

This project is an ISO 3166 (Country codes & US states codes) module for AngularJS. It provides:

* A service (factory) that gives access to all country codes & state codes
* A filter to print country codes as their standard name (FR -> FRANCE)
* A filter to print US states codes as their standard name (AL -> ALABAMA)
* A validation directive to validate country codes and US states codes

## Get it

`npm install https://github.com/sseif/iso-3166-angular.git`

## Use it

Add `iso-3166` to your module dependencies. 

## Features

### Factory

You can have access to country codes information and several utilitary methods.

```javascript
// Declare the factory as dependency
angular.module('myApp', ["iso-3166"])
  .controller('MyCtrl', function (ISO3166) {
    // Country Codes 
    //==============
    // Test if a value is a country code
    console.log(ISO3166.isCountryCode('FR')); // true
    console.log(ISO3166.isCountryCode('FRA')); // false

    // Get country name
    console.log(ISO3166.getCountryName('FR'));
    // FRANCE

    // Get several country names at once (ignores invalid codes)
    console.log(ISO3166.getCountryNames(['DE', 'FR', 'invalid']));
    // {
    //   'DE': 'Germany',
    //   'FR': 'France'
    // }

    // Get country name, manipulated by String methods.
    console.log(ISO3166.getCountryName('FR', 'toLowerCase'));
    // france

    // Get several country names at once (ignores invalid codes)
    console.log(ISO3166.getCountryNames(['DE', 'FR', 'invalid'], 'toLowerCase'));
    // {
    //   'DE': 'germany',
    //   'FR': 'france'
    // }

    // Get country code by country name
    console.log(ISO3166.getCountryCode('France'));
    // FR

    // Get country code by country name, manipulated by String methods.
    console.log(ISO3166.getCountryCode('France'), 'toLowerCase');
    // fr

    // Direct access to the data
    console.log(ISO3166.codeToCountry);
    // {
    //   'FR': 'France',
    //   ...
    // }
    console.log(ISO3166.countryToCode);
    // {
    //   'France': 'FR'
    //  ...
    // }
    console.log(ISO3166.countryCodes);
    // ['AF', 'AX', 'AL', ... ]

    // US States Codes 
    //==============
    // Test if a value is a US state
    console.log(ISO3166.isStateCode('AL')); // true
    console.log(ISO3166.isStateCode('ALA')); // false

    // Get state name
    console.log(ISO3166.getStateName('AL'));
    // Alabama

    // Get several state names at once (ignores invalid codes)
    console.log(ISO3166.getStateNames(['AL', 'AK', 'invalid']));
    // {
    //   'AL': 'Alabama',
    //   'AK': 'Alaska'
    // }

    // Get state name, manipulated by String methods.
    console.log(ISO3166.getStateName('AL', 'toLowerCase'));
    // alabama

    // Get several state names at once (ignores invalid codes)
    console.log(ISO3166.getCountryNames(['AL', 'AK', 'invalid'], 'toLowerCase'));
    // {
    //   'AL': 'alabama',
    //   'AK': 'alaska'
    // }

    // Get state code by state name
    console.log(ISO3166.getStateCode('Alabama'));
    // AL

    // Get state code by state name, manipulated by String methods.
    console.log(ISO3166.getStateCode('Alabama'), 'toLowerCase');
    // al

    // Direct access to the data
    console.log(ISO3166.codeToState);
    // {
    //   'AL': 'Alabama',
    //   ...
    // }
    console.log(ISO3166.stateToCode);
    // {
    //   'Alabama': 'AL'
    //  ...
    // }
    console.log(ISO3166.stateCodes);
    // ['AL', 'AK', 'AS', ... ]
  });
```

### Filter

If you get codes from your REST server, you can print their standard names with the provided filter:

```html
<!-- if countryCode is 'FR', will print 'France' -->
<p>{{countryCode | isoCountry }}</p>
```
```html
<!-- if stateCode is 'AL', will print 'Alabama' -->
<p>{{stateCode | isoState }}</p>
```

On the other hand, if you get names from your REST server, you can print their ISO codes:

```html
<!-- if countryName is 'France', will print 'FR' -->
<p>{{countryName | isoCountryCode }}</p>
```
```html
<!-- if stateName is 'France', will print 'FR' -->
<p>{{stateName | isoStateCode }}</p>
```

### Validation directive

If you want users to enter codes, you can validate it like so (it fits in Angular validation process):

```html
<form name="form" novalidate>
  <input type="text" name="countryField" country-code />
  <span ng-show="form.countryField.$error.countrycode">This must be a country code!</span>
</form>
```

```html
<form name="form" novalidate>
  <input type="text" name="stateField" state-code />
  <span ng-show="form.stateField.$error.statecode">This must be a state code!</span>
</form>
```

## Issues, Feature request

You can use [Github's issues](https://github.com/sseif/iso-3166-angular/issues) to submit feature requests and bug reports.

## Contributions

This project gladly accepts contributions. However, you must agree to give your work explicitely to public domain. To do so, just put this statement in the pull request definition:

```
I dedicate any and all copyright interest in this software to the
public domain. I make this dedication for the benefit of the public at
large and to the detriment of my heirs and successors. I intend this
dedication to be an overt act of relinquishment in perpetuity of all
present and future rights to this software under copyright law.
```

## License

This software is given to the public domain. For more information, see the `UNLICENSE` file.
