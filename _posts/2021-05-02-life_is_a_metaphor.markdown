---
layout: post
title:      "Life is a metaphor? "
date:       2021-05-02 22:45:37 +0000
permalink:  life_is_a_metaphor
---

# ...and it can all be "codified"

Having completed several projects, and with the tendency no for me to view EVERYTHING through the lens of software development, I'm surprised to find that not only am I learning several coding languages, frameworks and other related technologies, but there are many links to other fields of study.  As we develop applications with the intent of modeling real life things, places, ideas, problems and more, we attempt to create connections and interactions that will result in meaningful output. The possibilities are endless and that is an inspiring prospect as I move forward on this journey. 

## Code what you like

![](https://pbs.twimg.com/media/ETLN-SYU4AEyjhv.jpg)
>Epic pedal collection

When I'm not coding, I make music. I not only play instruments, but with a background in audio engineering I of course have attempted to incorporate my interests into my learning here. For my Javascript project, I chose to make an application that allows a user to add to an ever growing list of effects pedals. 

#### What is an effects pedal? Think of it like an object

![](https://circuitscheme.com/wp-content/uploads/2011/04/Jimi-Hendrix-Fuzz-Face.jpg)
>Fuzz effect circuit diagram

One can think of an effects pedal as an object in OO programming. Each pedal has it's own methods and capabilities, outputs and place in the scheme of your signal chain. In terms of audio, we pass sound (data,) from one pedal (object), through the various methods which take in user input in the form of knob turns, button pushes etc (params) and we effect the final output of the sound. 

## Frontend / Backend === AD/DA conversion?!
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Conversion_AD_DA.png/300px-Conversion_AD_DA.png)
# ===
```
  fetch("http://127.0.0.1:3000/pedals", config)
  .then(response => response.json())
  .then(pedal => {
    const newPedal = new Pedal({id: pedal.data.id, ...pedal.data.attributes})
    newPedal.render()
    newPedalsForm.reset()
  })
```

In this project we utilize frontend and  backend concepts. We provide data from our backend database, our own API, to a frontend web application that renders all the data we get from the API and renders it to the DOM. We learned about and implemented Fetch requests, which is an interesting process of converting data back and forth between the front and backend into data types that are readable by each. There is a concept in audio engineering called AD/DA conversion in which analog audio signals are converted into digital representations of voltage values, which can then be read and used by digital systems. It's the process of taking sound, and converting it into numbers! Or in programming it's not unlike taking ideas, and turning it into data, or turning strings, into objects, into html!

## Simple, yet capable and full of potential
![](https://fastly.4sqi.net/img/general/width960/-YX7agDWbNCd0jc3BNYQ9CMIg5VZWa7mpzs6Cq6Nh4w.jpg)
>The former Systems 2 in Brooklyn, NY

In terms of moving parts, the Javascript project is not super complicated, the interactions can get complex, but it's also pretty concise. The best part of all this is that during development on can start to see all the possibility to extend the functionality of a given application. Javascript can provide a simple list, on up to complex games and tools. As before, the lights start to turn on during the project build, because all these seemingly abstract ideas start to really work together for me. I'm excited to see where we go next, and how I might take my love of music and related technologies to the next level through development. My end goal is to simulate hardware devices like effects pedals and synthesizers, and put them into software modeled versions that can be improved and changed as the need arises and I can see that it's all possible from here. 

