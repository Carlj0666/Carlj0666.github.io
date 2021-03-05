---
layout: post
title:      "Params, not just a clever name."
date:       2021-03-04 22:07:08 -0500
permalink:  params_not_just_a_clever_name
---

*A question: What determines the keys in a params hash?*

The Answer: It's magical. Rails magic can be mystifying, in other words, what's going on behind the brim of that top hat is not always obvious. 

The Details in the magic (hint, there's 2 answers): 
The :name in our form_for example provide the key:
```
<%= form_for(@synth) do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %><br>
```
It's the name of the attribute from the field in the above HTML form that provides the key. So they key could be whatever you name it!

* In a POST request, params will get passed to the controller usually from a form.


* In a GET request, params get passed to the controller from the URL in the user’s browser.<br>

(EXAMPLE: `get '/synths/:id', to: 'synths#show'` <br>
*So entering '/synths/1' passes in the 1 to the params. We can see in the pry the params shows as follows:*
```
"id"=>"12"
```
"key"=>"value"
```
def show
    @synth = Synth.find(params[:id])
  end
```

In this show action we can see that the dynamic segment :id will get passed the :id from the URL. In keeping with the above example, we would get a Synth with an ID of 1.



### What about Strong Params?

Strong params protects your database by only allowing certain "whitelisted" attributes to be saved to the database.

```
def synth_params
    params.require(:synth).permit(:name, :brand, :hybrid, :price, :description)
  end
```

***Require*** looks for params[:synth] in the above example, and will throw an error if it's not there, it also prevents bad actors from using dev tools to tamper with things. ***Permit*** is followed by the list of permitted attributes. Once everything passes the save occurs! In short, we use Strong Params to protect the Database from bad data. 

You can see it in use here passed in to a new Synth that we'll make and save with ***Create***:
```
def create
    @synth = Synth.new(synth_params)
```

Just for fun, You can see heere how strong params protects your site!
Using the inspector we can see the price field:
![](https://i.imgur.com/wJMpA8c.png)
Here I've changed price to balance:
![](https://i.imgur.com/9uY7fPj.png)
Now I enter in the desired balance:
![](https://i.imgur.com/6O34k7s.png)
Here you can see the errors but you'll notice that the balance has changed back to price.
![](https://i.imgur.com/W0lRMF1.png)

```
[4] pry(#<SynthsController>)> @synth.errors
=> #<ActiveModel::Errors:0x00007f8f17f93190
 @base=
  #<Synth:0x00007f8ee6884628
   id: nil,
   name: "New balance synth",
   brand: "Super Expensive!",
   hybrid: false,
   price: nil,
   description: "Check my new balance!",
   user_id: 1,
   tech_id: 12,
   created_at: nil,
   updated_at: nil>,
 @errors=
  [#<ActiveModel::Error attribute=price, type=blank, options={}>,
   #<ActiveModel::Error attribute=price, type=not_a_number, options={:value=>nil}>]>
```
You can see the errors generated above shows that the price type is blank. Since we changed it to balance, in the form, the price is nil. Cool!

