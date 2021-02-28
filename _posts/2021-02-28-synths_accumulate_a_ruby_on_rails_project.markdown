---
layout: post
title:      "Synths Accumulate, A Ruby on Rails Project"
date:       2021-02-28 17:40:11 -0500
permalink:  synths_accumulate_a_ruby_on_rails_project
---


Based on this title I'm imagining a ruby colored train traveling at high velocity, grabbing up pallets of knobby, buttony awesome looking synthesizers, which is kind of what the idea of this app represents! As my third project during my time here at Flatiron, the complexity has jumped, but echos of Sinatra can still be heard in the distance. So let's go, this train travels fast.

We had the fortune of drilling MVC and naming conventions that translate well from Sinatra to Rails on the way to this stop off so we were prepared to recognize some important connections there. 

## Requirements
* Use the Ruby on Rails framework
* Include at least one has_many, at least one belongs_to, and at least two has_many :through relationships
* Include a many-to-many relationship implemented with has_many :through associations. The join table must include a user-submittable attribute — that is to say, some attribute other than its foreign keys that can be submitted by the app's user
* Models must include reasonable validations
* Include at least one class level ActiveRecord scope method
* The application must provide standard user authentication, including signup, login, logout, and passwords
* The authentication system must also allow login from some other service
* Include a nested new route with form that relates to the parent resource
* Include a nested index or show route
* Display validation errors
* Application must be, within reason, a DRY
* No scaffolding!

## Active Record you old dog!
Active record plays a big roll in this project and it's so important to have a good grasp on your model associations but don't over think it! You are using an idea, a metaphor for a thing, and making a model out of it with it's parts all labeled and nicely setup. Think about how those things relate, does it make sense? It really needs to or come time to code those relationships and deciding how things work become way more difficult! The actual associations are not as hard as the time we put into thinking about th way they will interact and be functional together, think, but don't over think it. You can tell I've thought about this.

## Validations are valid
Yep, security for your apps is way cool! If it can be stickered, chipped at, wheat pasted, broken into, toilet papered or otherwise, someone will do it. Validates and using scope within validations is really interesting. You can do a lot in just lines of code to protect your database from strange data so your prices aren blank, or $qwerty.95, or so you don't have 100 "unique" items in your list! You can check for: Presence, Uniqueness and Numericality to name a few!

## How not to get lost on Rails
My best advice, ASK QUESTIONS! This project and some of the concepts that we cover are pretty complex and combined into assemblies they can be positively labyrinthine! Even though we are on Rails, it's easy to miss a stop or take the wrong fork so ask directions from your instructor if you are feeling lost. Stop and meet with your fellow students to compare your ideas. It takes time but the concepts will come together like the previous ones did : )

## Projects show us the whole picture
I love project time! Bringing it all together really serves to paint the bigger picture of how all these fantastic tools are related, and how much we can build do with them! The train stops here...


