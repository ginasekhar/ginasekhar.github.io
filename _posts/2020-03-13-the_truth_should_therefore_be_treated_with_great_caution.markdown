---
layout: post
title:      "The Truth... should therefore be treated with great caution."
date:       2020-03-14 03:43:06 +0000
permalink:  the_truth_should_therefore_be_treated_with_great_caution
---


“The truth." Dumbledore sighed. "It is a beautiful and terrible thing, and should therefore be treated with great caution.”
― J.K. Rowling, Harry Potter and the Sorcerer's Stone



Redux  is built on 3 principles :

1.Single source of truth, 2. State is read-only and 3. Changes are made with pure functions


My final project at Flatiron made me appreciate the first principle.

My project was a flash cards application.  My models were subjects, topics and flash_cards.  A subject has_many topics. A topic belongs to a subject and has many flash_cards. A flash_card belongs to a topic.

I used React Router for navigation to the different parts of the application using the <Link> component.

I initially coded my application relying on the route parameters that were being passed in.  
```
<Route exact path=“/topics/:id/flash_cards/new" component={FlashCardInput} />
```

For example when I created a flash card, I needed to know the topic to which that flash card belonged. I initially coded trying to access the information using `props.match.params.id`

While this worked most of the time, there were instances when I switched between topics and added multiple flash cards, that the “params” were “undefined” and the application’s behavior was unpredictable.

As I watched many of the other students in our cohort talk about the issues they were having, many were related to the way the props were passed.  Our cohort lead Nancy reminded us that one of the cornerstones of Redux is “A single source of truth” and that since we had access to the global state we did not have to pass the props around.  She mentioned that several times over multiple study group sessions, but it was only when she told one of the other students, “you know you can store the current user in state and don’t have to pass it around in props”, that it clicked for me.  I could store the current subject and topic in state and not pass it around. I used mapStatetoProps to map those elements from the global state to props.  Once I made the changes, the application behaved predictably.

Dumbledore’s words certainly ring true:

The truth (the data that I was passing) needed to be handled with more care.  Things worked better when I got the data from the global state, the single source of truth.
