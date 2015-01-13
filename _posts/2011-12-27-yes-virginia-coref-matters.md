---
published: true
title: "Coreference for Learning to Extract Relations: Yes, Virginia, Coreference Matters, by Ryan Gabbard, Marjorie Freedman, and Ralph Weischedel (some folks at Raytheon), ACL 2011 short paper."
layout: post
author: Matt
tags:
- Relation Extraction
- Coreference Resolution
---

This is a simple short paper with one main point. When you build an information extraction system
(theirs in semi-supervised), including the output of a coreference resolution system should
increase your recall, at the cost of precision. That's pretty much what you would expect; the
result is intuitive.

What was surprising was that the boost in recall was huge, with the system including coreference
information having two or three times (or more) the recall of the system without it. Also
surprising was that precision didn't take much of a hit and even improved in some instances. The
authors suggest that, while coreference is noisy, using it led to more local patterns because the
two entities in the relation were generally closer together in the sentence than in the system
without coreference information. Thus the local patterns balanced out the noise of the automatic
coreference, and they did a little noise control in their learning algorithm, too.

I actually just did this same experiment for a class project, though our experiment was mostly an
afterthought and it was pretty rushed. We saw the opposite result, with an increase in precision
and a decrease in recall.

I think the difference is from a few things. First, we were using a weakly-supervised approach with
known entities from Freebase that we found in news articles. They used an iterative semi-supervised
approach, which in the end is very similar to weak supervision, but presumably it starts with
better seed examples. I think the result was that our initial data that we learned the classifier
from was more noisy than their data. That is, the automatic processing of news articles to find
entity pairs by string matching is a noisy process, and so there were a lot of bad sentences that
we assumed encoded relation instances. They were able to start with some very high precision
examples and slowly expand their set.

The reason this has to do with coreference resolution is that our processing of the coreference
results was pretty bad, and we ended up throwing away two thirds of our data due to faulty
processing (among other things). I have a strong suspicion that among the sentences we threw away
were many sentences that were bad examples to begin with, and that is why our precision went up
when we threw them away. The take away from this experiment, then, is that if you are trying to
automatically build training data, the more independent ways you have of producing examples (i.e.,
string matching and coreference resolution), the more clean your data will be.

Also, another reason for the difference in our outcomes is that they were using Wikipedia as a
large chunk of their dataset. Entities are easy to find in Wikipedia, and pronouns are really
common in articles describing those entities. Of course you're going to get a huge boost if you use
coreference information there. I don't have any data to back this up, but I suspect the potential
for improvement from coreference resolution is a lot smaller in news articles than in wikipedia,
because sentences are a lot less declarative and don't have as many pronouns. Instead they express
the relations in the words themselves, using every mention as a way to add more information about
the entities (e.g., Steve Jobs, founder of Apple, Inc., was in Detroit today for a convocation. The
computer company executive spoke about... The mention in the second sentence, the computer company
executive, would probably be an entire sentence with a pronoun in Wikipedia, but the mention itself
encodes the information in the news article).

I guess that was long. If any of you are still reading, you must really be interested =). I do this
mostly for myself, to organize my thoughts after reading a paper and to have them in a place I can
find them again. If you do actually read these and find them interesting, I would be interested in
knowing that.
