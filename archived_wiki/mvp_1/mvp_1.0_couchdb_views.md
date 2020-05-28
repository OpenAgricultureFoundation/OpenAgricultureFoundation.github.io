---
layout: wiki_archive
---

### CouchDB Views

As always, refer to the
[manuals](http://guide.couchdb.org/draft/views.html) for the best
documentation. The easiest way to create views is within CouchDB Futon
(the web interface). Click on the mvp\_sensor\_data database to navigate
down into it, then under the menu "View" go to the "temporary view" and
create a new one (or edit an existing one). Click on the "View Code"
window arrow to drop down the code editing window. The view I created
has the following code:

``` 
 function(doc) {
      if(doc.value && doc.attribute && doc.status == 'Success')
      {
          emit([doc.attribute, doc.name, doc.timestamp], doc);
      }
 } 
```

The bottom window shows the query results. Click on "Save As" and save
it in the \_design/doc file as "attribute\_value"

This view returns more data than you want, you will use query parameters
within the curl http to select subsets of these records.
