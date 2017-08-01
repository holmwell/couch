# couch
A small wrapper around nano for getting up and running with CouchDB
and some design docs.

## Usage

```javascript
    var db;
    var designDocs = [{
        url: '_design/members',
        body: 
        {
            version: "1.0.2",
            language: "javascript",
            views: {
                byMemberId: {
                    map: function (doc) {
                        if (doc.type === "member") {
                            emit(doc.memberId, doc);
                        }
                    }
                }
            }
        }
    ];

    var couch = require("@holmwell/couch")('my-local-database', designDocs);
    couch.whenReady(function () {
       db = couch.db; 
    });

    // Assert: db === require('nano')('http://localhost:5984').use('my-local-database')
    // ... and your design docs are in the database.
