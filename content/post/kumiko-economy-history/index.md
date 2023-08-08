---
title: Kumiko's Economy System History
description: The history behind Kumiko's complex economy system
slug: kumiko-economy-history
date: 2023-08-07 00:00:00+0000
categories:
    - Kumiko
tags:
    - Development
---

When I first started working on Kumiko, the first thing I wanted to make is an economy system. I wanted to make it where you had to buy items from a marketplace, and then have to buy them. This was the first version of the economy system

## Version 1 - SQLAlchemy and Beanie

SQLAlchemy was used since after watching Fireship, SQLAlchemy was the de-facto ORM of choice for many Python projects. At this time, I was using SQLAlchemy v1.3, where the documentation was really just confusing. I relied on StackOverflow posts in order to figure out the library. This version was written using a query builder version of SQLAlchemy, called SQLAlchemy Core. It was basically the same thing, but you had to write the queries yourself. I also used Beanie, which is a MongoDB ORM. I used it for the marketplace feature, but later on scrapped it. Now you may be wondering why Beanie was used? And why MongoDB? Frankly, the only answer I have is that I wanted to look cool. This was only a couple months after I finished my Python course, and I was in the "looking cool" phase at that time with tech. So I thought with the more servers and tech stacks I used, then more "enterprise" and cooler my project looked like. Anyways, this version actually did make it through development, but I later swapped out the SQLAlchemy Core queries with SQLAlchemy ORM.

## Version 2 - Tortoise ORM

At this time, dissatisfied with what SQLAlchemy had to offer, I stumbled across Tortoise ORM. This ORM looked pleasing to me at this time, and looked relativity easy to swap so that's what I did. I swapped SQLAlchemy for Tortoise ORM. But the orm was lacking in many features, and the way connection pools and connections were handled annoyed me a lot. This was also the time where I was working with Pycord, so.... The bulk of the economy system was written in this version, but I later swapped it out for Prisma.

## Version 3 - Prisma

Looking at Tortoise ORM, I swapped to Prisma. Prisma was the ORM of choice for many JS/TS projects, and went for it. The Prisma python client was ehh and all, but really I was done with searching for ORMs, and decided to make the commitment to use SQL instead.

## Version 4 - asyncpg

To this day, this is the version of the economy system that is used in Kumiko. Asyncpg boasts massive performance gains, such as being 5x faster than psycopg3 (asyncpg can pull in 2.1 million rows per sec, and psycopg3 can pull in 425K rows per sec) 5.89x faster than aiopg, and quite literally, 8.2x faster than node-pg. Ultimately this was what made swap over to asyncpg today, and Kumiko now uses asyncpg at the core. The economy system is now written using asyncpg.