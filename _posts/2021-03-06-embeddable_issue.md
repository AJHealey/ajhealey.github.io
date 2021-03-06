---
layout: post
title:  "Dude, where is my value object?!"
date:   2021-03-06
image:  embeddable.jpg
tags:   JPA hibernate java
---

### What is an Embeddable?
Embeddables are a feature of JPA that allows us to include a value object inside an entity. Without this, we should create "id" for each instance and thus ... make them entities.
My first encounter of this kind of mapping was a project where people were trying to enforce Domain Driven Design.

### How to use them ?
I won't write a new tutorial on the matter but, to keep it simple, we 
1. define a class representing the value object
2. add the right annotations
3. use the object in the entities
... and VOILA!

### Hibernate management
My issue was that during a process, some data of my value object were null. Nothing exceptional, I was instantiating the objects, persisting them and tried to get them back...
But nothing came back from the database. Nevertheless, the data were there, I could see them. So, what was happening?
In fact, it took me some time to find out that Hibernate considers embeddable without values as null and thus make the field in the entity as it.
But my objects were holding data in one of their fields. So why the NPE?

### Edge case: Used as a Map
Oh, I forget to precise that I was trying to achieve a fancy mapping with my embeddables: putting them in a Map.

### Resources
* https://www.baeldung.com/jpa-embedded-embeddable
* https://www.baeldung.com/spring-persisting-ddd-aggregates
* https://www.logicbig.com/tutorials/java-ee-tutorial/jpa/map-with-embeddable-values.html
