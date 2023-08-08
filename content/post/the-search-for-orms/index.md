---
title: The search for the perfect ORM
description: The search for the perfect ORM framework for Kumiko
slug: the-search-for-orms
date: 2023-07-22 00:00:00+0000
categories:
    - Kumiko
tags:
    - Development
---

Throughout the development process, Kumiko has changed a lot. One of the major frameworks that changed a ton were the ORM frameworks used. 

## SQLAlchemy and Beanie

Kumiko started development in Nov 2021. At this time, I had spent a couple of months learning how to write Discord bots, and developing Rin. Kumiko was supposed to be the "mutlipurpose fork of Rin", meaning that it was just an extension of Rin. The first major feature to tackle was the economy system. Originally I used SQLAlchemy Core and Beanie (SQLAlchemy Core is a query builder version of their ORM). Now you may be asking, what's up with Beanie? Well at that time, I had seperated the marketplace feature to use MongoDB instead. And found Beanie to work perfectly well for that. Later on I scrapped it. The first version of the economy system basically didn't even make it through. Now for my opinions about the ORMs.

Pros:
- SQLAlchemy is the de-facto ORM used in Python. It's very well documented, and has a lot of support.
- Uses asyncpg as it's driver (which later on and to this day is what Kumiko internally uses)

Cons:
- It's very complex. It's not something that you can just pick up and use. It takes a lot of time to learn how to use it.
- The documentation is just way too complex
- Trying to make joins is way too complex, and there are no good examples on how to do it.

Overall, if you are using SQLAlchemy for Discord bots, look somewhere else instead

## Tortoise ORM

As I searched for another ORM, one popped in my radar - Tortoise ORM. Tortoise ORM is now what we call a query builder. It was the first "native" async ORM for Python that was decent at that time (SQLAlchemy had an async mode, but it was just a port and not natively implemented). You would create your tables in models, and then write some code that would take the models and create the tables. Joins were ehh to make, and it was just a pain to use. 

Pros:
- Django-like API (well even piccolo takes the cake for that)

Cons:
- Basically a dead project right now
- Very little good examples, and documentation
- The migrations tool never worked for me for some odd reason

Overall, if you are using Tortoise ORM for Discord bots, look somewhere else instead. It's literally a nightmare to use

## Prisma

Prisma is famously known to the ORM of choice for JavaScript/TypeScript developers. It just made things a lot more easier to use, by abstracting all of the models into one `schema.prisma` file, and made it quite frankly really easy to use. There is a Python version of the client, but it's still in development. But it is pretty stable. The Prisma Python client works by providing an ORM like API to the end user, and then all of the queries are formed and ran in the Prisma Engine. The Python client does bundle the engine with it, so folks don't have to worry about it. But I never made a full rewrite when I switched to the last driver.

Pros:
- Migrations are very very easy to use
- The `schema.prisma` file works for all databases, including MongoDB and others
- Stable Python client
- Very easy to use

Cons:
- Takes wayyyy too much ram. It takes around 150MB of RAM to run
- The API basically makes it like Motor instead. Just way too complex.

## asyncpg

Now asyncpg is not a ORM, but a PostgreSQL driver for Python. It's quite literally the fastest Python driver (and PostgreSQL driver) out there. asyncpg has the record for being able to fetch millions of rows per second. The rationale for switching was this: after switching all of these ORMs, I wanted something simple. It's like learning only using Python and Java to avoid the deep end of C/C++ and Rust. asyncpg quite literally beats out every single ORM out there when it comes to performance, so it was like getting C native performance. To this day, it's what Kumiko uses, and the economy system is built entirely on asyncpg now.

Pros:
- Very fast. 5x faster than psycopg3-async, 5.89x faster than aiopg, and 8.2x faster compared to node-pg
- Very simple to use. Literally you just need to know how to write SQL, and you are good to go
- Connection pools are thing

Cons:
- None

And yea, that's the whole entire history of searching for one, but at the end, not evening using one.