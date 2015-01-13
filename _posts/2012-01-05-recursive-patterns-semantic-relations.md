---
published: true
title: "Learning Arguments and Supertypes of Semantic Relations using Recursive Patterns, by Zornitsa Kozareva and Eduard Hovy, ACL 2010."
layout: post
author: Matt
tags:
- Relation Extraction
---

This is essentially a follow on to the last paper I posted. Last time they used the phrase "such
as" to build a kind of ontology of things starting with a single seed (like "animals such as lions
and _ "). This time they expand the work to 14 other phrases, aiming to show that you can learn
arbitrary semantic relations using the same basic methodology. For instance, they use " _ and _ fly
to _ ", to learn selectional preferences for what things tend to fly and where they fly to, and " _
and nice dress" to learn adjectives that describe dresses. It's an interesting approach, and they
have pretty good success for getting a general idea of what arguments tend to go with what words. I
wonder about its scalability, though, as there are thousands of verbs in English, not counting all
of the particles and prepositions they can take, and their methodology seemed pretty intensive for
each phrase they test. But it does give some credence to some things we've been thinking recently,
that you can use simple verbs to approximate many or most relations that people are interested
in.
