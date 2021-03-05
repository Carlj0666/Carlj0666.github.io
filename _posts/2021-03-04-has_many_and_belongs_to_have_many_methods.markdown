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
##### Here's a rundown of the methods you'll have access to with this simple line of code `belongs_to` from:  [Rails Guides](https://guides.rubyonrails.org/association_basics.html)<br>

Each instance of our Tech model will have access to the following methods:

##### tech - 
* This returns the associated object, or nil.<br>
@tech = @synth.tech

##### tech= - 
* This method assigns the associated object to this object.<br>
@synth.tech = @tech

##### build_tech - 
* This returns a new object of the associated type, and is instantiated from the attributes that are passed in.<br>
@tech = @synth.build_tech(tech_number: 123, tech_name: "BUILD TECH")

##### create_tech - 
* This does that same as above but with the foreign key set. After this passes validation, it also gets saved!
@tech = @synth.create_tech(tech_number: 123, tech_name: "BUILD TECH")

##### create_tech! - 
* Just like above but this one raises ActiveRecord::RecordInvalid, if invalid.
* @tech = @synth.create_tech!(tech_number: 123, tech_name: "BUILD TECH")

##### reload_tech - 
* This returns all the associated objects and forces a database read.


### Continuing with the example the Tech model has_many Synths:<br>
```
class Tech < ApplicationRecord
  has_many :synths
```

##### Here's a rundown of the methods you'll have access to with this simple line of code `has_many` quoted from:   [Rails Guides](https://guides.rubyonrails.org/association_basics.html)<br>

### In this example the Tech has_many Synths:
```
class Tech < ApplicationRecord
 has_many :synths
```
There's ***17*** methods tht come with has_many!<br>
* collection<br>
* collection<<(object, ...)<br>
* collection.delete(object, ...)<br>
* collection.destroy(object, ...)<br>
* collection=(objects)<br>
* collection_singular_ids<br>
* collection_singular_ids=(ids)<br>
* collection.clear<br>
* collection.empty?<br>
* collection.size<br>
* collection.find(...)<br>
* collection.where(...)<br>
* collection.exists?(...)<br>
* collection.build(attributes = {})<br>
* collection.create(attributes = {})<br>
* collection.create!(attributes = {})<br>
* collection.reload<br>
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
Here I saved the instance in the variable new_synth so we can check it later, then I used .build, and added in the attributes:

```pry(#<TechesController>)> new_synth = @tech.synths.build(name: "name for build", brand: "builders brand", hybrid: true, price: 199.00, description: "This is how we build it")
```
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
Here's several BUILT at the same time:
```pry(#<TechesController>)> @tech.synths.build([{name: 'Gimme a B'}, {name: 'U'}, {name: 'I'}, {name: 'L'}, {name: 'D'}])=> [#<Synth:0x00007ffe2f3650f8
  id: nil,
  name: "Gimme a B",
  brand: nil,
  hybrid: nil,
  price: nil,
  description: nil,
  user_id: nil,
  tech_id: nil,
  created_at: nil,
  updated_at: nil>,
 #<Synth:0x00007ffe2f36fe18
  id: nil,
  name: "U",
  brand: nil,
  hybrid: nil,
  price: nil,
  description: nil,
  user_id: nil,
  tech_id: nil,
  created_at: nil,
  updated_at: nil>,
 #<Synth:0x00007ffe2f36ebd0
  id: nil,
  name: "I",
  brand: nil,
  hybrid: nil,
  price: nil,
  description: nil,
  user_id: nil,
  tech_id: nil,
  created_at: nil,
  updated_at: nil>,
 #<Synth:0x00007ffe2f36d988
  id: nil,
  name: "L",
  brand: nil,
  hybrid: nil,
  price: nil,
  description: nil,
  user_id: nil,
  tech_id: nil,
  created_at: nil,
  updated_at: nil>,
 #<Synth:0x00007ffe2f36c740
  id: nil,
  name: "D",
  brand: nil,
  hybrid: nil,
  price: nil,
  description: nil,
  user_id: nil,
  tech_id: nil,
  created_at: nil,
  updated_at: nil>]
	```
	
	#### So there's all kinds of awesome and powerful methods that come with those "little" macros has_many and belongs_to! That's all for now!
	
