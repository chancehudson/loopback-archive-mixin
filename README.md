Archive
=============

This module is designed for the [Strongloop Loopback](https://github.com/strongloop/loopback) framework. It allows entities of any Model to be archived by adding `deletedAt` and `isDeleted` attributes. Queries following the standard format will not return these entities; they can only be accessed by adding `{ deleted: true }` to the query object (at the same level as `where`, `include` etc).

By default `count` and `update` operations will only apply to models that are not deleted. This is overridden by specifying a defined value for either `deletedAt` or `isDeleted`.

This is heavily based on the [loopback-softdelete-mixin](https://github.com/gausie/loopback-softdelete-mixin) by gausie.

Install
-------

```bash
  npm install --save loopback-archive-mixin
```

Configure
----------

To use with your Models add the `mixins` attribute to the definition object of your model config.

```json
  {
    "name": "Message",
    "properties": {
      "name": {
        "type": "string",
      },
    },
    "mixins": {
      "Archive" : {}
    },
  },
```

This is a minimal mixin, the only customization is the property names assigned for indicating deletion. The default properties are `deletedAt` and `isDeleted`.

```json
  "mixins": {
    "Archive": {
      "deletedAt": "deletedAt",
      "isDeleted": "isDeleted"
    },
  },
```

Retrieving deleted entities
---------------------------

To run queries that include deleted items in the response, add `{ deleted: true }` to the query object (at the same level as `where`, `include` etc).

By default count and update queries will only operate on models that have not been deleted. Specifying either `deletedAt` or `isDeleted` in the matching clause will run the query like normal.
