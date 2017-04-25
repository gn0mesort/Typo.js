This fork of typo.js includes:

- add the option of running suggest asynchronously allowing updating the display with results as they come, and stopping a suggestion     search midway. Also provides much faster performance and smaller memory use on both synchronous and asynchronous suggests.

  The suggest function can now be called in one of three ways:

  suggest(word, limit [=5])
  - runs suggest synchronously
  
  suggest(word, limit [=5], doneFunc, progressFunc) where either doneFunc or progressFunc are defined

  - runs suggest asynchronously
  - returns undefined
  - doneFunc (if given) will be called (with the sorted results array) once the search is done
  - progressFunc (if given) will be called (with the new match) whenever a new match is found in the search
  - if progressFunc returns===false the current search will be aborted
  - will do the equivalent of sleep(0) every 200ms

  suggest()
  - abort a current search if running

- code coverted to ES6 using lebab

- updated english dictionaries (get other dictionaries with git clone https://chromium.googlesource.com/chromium/deps/hunspell_dictionaries)

- added a loadTypo function that returns a promise resolved when the given dictionaries are loaded

- added an ignore(word) 

- improve the ordering of permutations returned from the edits1 function

- closes https://github.com/cfinke/Typo.js/issues/46
- closes https://github.com/cfinke/Typo.js/issues/48
- closes https://github.com/cfinke/Typo.js/issues/49


Original readme:

Typo.js is a JavaScript spellchecker that uses Hunspell-style dictionaries.

Usage
=====

To use Typo, simply load it like so:

```javascript
var Typo = require("typo-js");
var dictionary = new Typo(lang_code);
```

Typo includes by default a dictionary for the `en_US` lang_code.

To check if a word is spelled correctly, do this:

```javascript
var is_spelled_correctly = dictionary.check("mispelled");
```

To get suggested corrections for a misspelled word, do this:
	
```javascript
var array_of_suggestions = dictionary.suggest("mispeling");

// array_of_suggestions == ["misspelling", "dispelling", "misdealing", "misfiling", "misruling"]
```

Typo.js has full support for the following Hunspell affix flags:

* PFX
* SFX
* REP
* FLAG
* COMPOUNDMIN
* COMPOUNDRULE
* ONLYINCOMPOUND
* KEEPCASE
* NOSUGGEST
* NEEDAFFIX

Licensing
=========

Typo.js is free software, licensed under the Modified BSD License.
