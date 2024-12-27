---
title: Entity Component Systems
author: Link459
layout: post
date: 2024-12-27
permalink: /ecs/
---

# The World
Everything needs to happen somewhere, our lives do in the universe. 
The live of a game happens in what I'll from now on call the **World**, the world contains all the information required to run a game,
you'll have things like your characters position in it,the enemy health, the number 42. It can be anything you want.
But what lives in a world besides all the previously mentioned information?

# The Entity
Conceptually an entity is basically nothing, it exists but it doesn't do anything, kinda like a discord moderator. Only when you add something to it (components) will it do something.
In reality an entity is a unique identifier so you can associate what components relate to each other.
You would usually create them like this `Entity entity = world.spawn();`

# Components
What are components anyway? They are just data, plain old data. Nothing more than a struct in c/c++/rust/zig/any other language.
A component gets associated with an entity, so you can retrieve it's data when you need it.
Here `world.add(entity,Id{.name = "John Doe",.age = 27});` the component Id with the data inside will get associoated with our previously created entity.
Well you might be thinking it's great that we have data (components) and ways to group them together (entities) but where is the functionality?

# Systems
Systems are the most important things when it comes to an ecs, they go over each entity with a certain set of components. 
Then once they get the data they can interact with it, like updating enemy positions, or even things like spawning more entities and components.
A system is nothing more than the retrival and updating of components.
How they look like can greatly differ between the implementation of the ecs paradigm.
Some might do thinks like having functions which can query the world through their parameters, others might just provide one way to retrieve 
components from the world and you have to deal with how to iterate them. 

# The Good
Arrays, Vectors or whatever else you wan't to call them are great,providing fast data access and iterations.
An ecs greatly benefits from this, instead of having hundreds of pointers to heap allocated abstract classes, you just have arrays with data, the seperation between data and functionality allows this.
It's hard to fit your mind around what systems do and how they interact with eachother. Writing them can be daunting at first. 
Having to migrate from data and functionality being coupled to them being seperated, is no easy task.
But once you understand why having them seperate is great, you don't wan't to go back. You just have linear execution so debugging gets easier.
The data can be whatever you don't need to write a wrapper around it integrating it into your tree-like game world.
Just write a system querying for it and it just works. No dealing with copy/move constructors/assignment operators anymore
just put them in the ecs world and be done.
You can also disable a system without having to worry that everything will break.

# The Bad
Code duplication is a major issue that i've encountered over my time writing a game engine with an ecs at it's core. 
For every system or engine component that interacts with multiple components or resources you first need to query them from the world. It's not a major issue but over time it can get quite annoying.


# The Truth

The truth is, that it doesn't matter. Whether you use an object oriented design or a fancy data oriented one.
In the end it's about what you create with it.
If you create the 'perfect' architecture but never end up using it, it wasn't that great to begin with.
Not once did I stop to think how it was like to use my entity component system. Only once I started to actually use it myself did I realise how bad it was to interact with.
Only after multiple revisions on how it works am I truly content with how it works.
