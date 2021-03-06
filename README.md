<img src="https://travis-ci.org/RiffynInc/querybuilder-rules.svg?branch=master">

#querybuilder-rules

A subset of the [jQuery QueryBuilder library](http://querybuilder.js.org/index.html), modified to work in a node.js environment. This module allows you to convert the **rules** object that's generated by the jQuery QueryBuilder UI into the native query language for various database engines.

##Supported Databases

* SQL
* MongoDB

##Example

```javascript
//an example of a rules object that's generated by the jQuery QueryBuilder UI.
var rules = {
  "condition": "AND",
  "rules": [
    {
      "id": "name",
      "field": "name",
      "type": "string",
      "input": "text",
      "operator": "equal",
      "value": "Sh"
    }
  ]
}

//load this module
var QueryBuilder = require('querybuilder-rules');

//create a new instance variable
var qb = new QueryBuilder();

//generate a SQL Where statement
console.log(qb.getSQL(false, false, rules).sql);

//generate mongoDB find parameter
console.log(db.getMongo(rules));
```

###Methods

#####.getSQL(*mode*, *linebreaks*, *rules*)

| parameter | description  |
|:---|:---|
| **mode** | <ul><li>`false` to output plain SQL</li><li>`'question_mark'` to output prepared statement with `?` placeholders</li><li>`'numbered'` to output prepared statement with numbered (`$1`, `$2`, ...) placeholders</li><li>`'named'` to output prepared statement with named (`:id`, `:category`, ...) placeholders</li></ul> |
| **linebreaks** | Set to true to enable new lines in output. |
| **rules** | The rules object that's generated by the jQuery QueryBuilder library. |

Returns an object with two keys:

| key | description  |
|:---|:---|
| **sql** | SQL WHERE statement for a given set of rules. |
| **params**  | If *mode* is not set to `false`, this value will contain an array of parameters that belong to the corresponding placeholders that exist in the SQL statement. |

#####.getMongo(*rules*)

Returns an object representing the MongoDB `find` parameter for a given set of rules.

###Tests
Enter the following command at the CLI to run the full set of Mocha tests:

```cli
make test
```

###Contributions
Your contributions are appreciated! If you'd like to add support for a additional database engines, please include a full set of tests. 

###License
Covered under the [MIT Licesnse](./LICENSE), Copyright (c) 2016 [Riffyn, Inc](http://riffyn.com).
