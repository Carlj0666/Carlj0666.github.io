---
layout: post
title:      "Has_many & belongs_to have many methods!"
date:       2021-03-04 20:55:22 -0500
permalink:  has_many_and_belongs_to_have_many_methods
---

Macros in Rails come loaded with a bunch of useful methods, it's why we use them. For my Rails project I used a Synth model, as well as a Tech model to mention just two. Through has_many and belongs_to (both Active Record Associations), we establish relationships between our models.
### In this example the Synth model belongs_to a Tech:
```
class Synth < ApplicationRecord
  belongs_to :tech
```
##### Here's a rundown of the methods you'll have access to with this simple line of code `belongs_to` quoted from:  [API Dock](https://apidock.com/rails/ActiveRecord/Associations/ClassMethods/belongs_to)<br>

Methods will be added for retrieval and query for a single associated object, for which this object holds an id:

association is a placeholder for the symbol passed as the name argument, so belongs_to ***:tech*** would add among others ***tech***.nil?.

* association
Returns the associated object. nil is returned if none is found.

* association=(associate)
Assigns the associate object, extracts the primary key, and sets it as the foreign key. No modification or deletion of existing records takes place.

* build_association(attributes = {})
Returns a new object of the associated type that has been instantiated with attributes and linked to this object through a foreign key, but has not yet been saved.

* create_association(attributes = {})
Returns a new object of the associated type that has been instantiated with attributes, linked to this object through a foreign key, and that has already been saved (if it passed the validation).

* create_association!(attributes = {})
Does the same as create_association, but raises ActiveRecord::RecordInvalid if the record is invalid.
 
* reload_association
Returns the associated object, forcing a database read.

### Continuing with the example the Tech model has_many Synths:<br>
```
class Tech < ApplicationRecord
  has_many :synths
```

##### Here's a rundown of the methods you'll have access to with this simple line of code `has_many` quoted from:   [API Dock](https://apidock.com/rails/ActiveRecord/Associations/ClassMethods/has_many)<br>

Specifies a one-to-many association. The following methods for retrieval and query of collections of associated objects will be added:

collection is a placeholder for the symbol passed as the name argument, so has_many ***:synths*** would add among others ***synths***.empty?.

* collection<br>
Returns a Relation of all the associated objects. An empty Relation is returned if none are found.

* collection<<(object, …)<br>
Adds one or more objects to the collection by setting their foreign keys to the collection’s primary key. Note that this operation instantly fires update SQL without waiting for the save or update call on the parent object, unless the parent object is a new record. This will also run validations and callbacks of associated object(s).

* collection.delete(object, …)<br>
Removes one or more objects from the collection by setting their foreign keys to NULL. Objects will be in addition destroyed if they’re associated with dependent: :destroy, and deleted if they’re associated with dependent: :delete_all.

***If the :through option is used, then the join records are deleted (rather than nullified) by default, but you can specify dependent: :destroy or dependent: :nullify to override this.***

* collection.destroy(object, …)<br>
Removes one or more objects from the collection by running destroy on each record, regardless of any dependent option, ensuring callbacks are run.

* If the :through option is used, then the join records are destroyed instead, not the objects themselves.

* collection=objects<br>
Replaces the collections content by deleting and adding objects as appropriate. If the :through option is true callbacks in the join models are triggered except destroy callbacks, since deletion is direct by default. You can specify dependent: :destroy or dependent: :nullify to override this.

* collection_singular_ids<br>
Returns an array of the associated objects’ ids

* collection_singular_ids=ids<br>
Replace the collection with the objects identified by the primary keys in ids. This method loads the models and calls collection=. See above.

* collection.clear<br>
Removes every object from the collection. This destroys the associated objects if they are associated with dependent: :destroy, deletes them directly from the database if dependent: :delete_all, otherwise sets their foreign keys to NULL. If the :through option is true no destroy callbacks are invoked on the join models. Join models are directly deleted.

* collection.empty?<br>
Returns true if there are no associated objects.

* collection.size<br>
Returns the number of associated objects.

* collection.find(…)<br>
Finds an associated object according to the same rules as ActiveRecord::FinderMethods#find.

* collection.exists?(…)<br>
Checks whether an associated object with the given conditions exists. Uses the same rules as ActiveRecord::FinderMethods#exists?.

* collection.build(attributes = {}, …)<br>
Returns one or more new objects of the collection type that have been instantiated with attributes and linked to this object through a foreign key, but have not yet been saved.

* collection.create(attributes = {})<br>
Returns a new object of the collection type that has been instantiated with attributes, linked to this object through a foreign key, and that has already been saved (if it passed the validation). Note: This only works if the base model already exists in the DB, not if it is a new (unsaved) record!

* collection.create!(attributes = {})<br>
Does the same as collection.create, but raises ActiveRecord::RecordInvalid if the record is invalid.

* collection.reload<br>
Returns a Relation of all of the associated objects, forcing a database read. An empty Relation is returned if none are found.

### Lot's to do
Here's an example of how I used one of the above methods in my recent project. I broke down the steps in a pry:

I placed the pry before the (collection.build) method (@tech.synths.build). This time there's no data:
```
[3] pry(#<TechesController>)> @tech.synths.build
=> #<Synth:0x00007f9f92c38640
 id: nil,
 name: nil,
 brand: nil,
 hybrid: nil,
 price: nil,
 description: nil,
 user_id: nil,
 tech_id: nil,
 created_at: nil,
 updated_at: nil>
```
Here I saved the instance in the varibale new_synth, then use build, and add in the attributes that would usually come from the form being submitted:

```pry(#<TechesController>)> new_synth = @tech.synths.build(name: "name for build", brand: "builders brand", hybrid: true, price: 199.00, description: "This is how we build it")
```
=> #<Synth:0x00007f9fb2efe260
 id: nil,
 name: "name for build",
 brand: "builders brand",
 hybrid: true,
 price: 199.0,
 description: "This is how we build it",
 user_id: nil,
 tech_id: nil,
 created_at: nil,
 updated_at: nil>
 ```
 And here you see the new synth!
 
 ```
 [10] pry(#<TechesController>)> new_synth
=> #<Synth:0x00007f9fb2efe260
 id: nil,
 name: "name for build",
 brand: "builders brand",
 hybrid: true,
 price: 199.0,
 description: "This is how we build it",
 user_id: nil,
 tech_id: nil,
 created_at: nil,
 updated_at: nil>
```
