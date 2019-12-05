---
layout: post
title:      "Validation is best that comes from within..."
date:       2019-12-04 22:43:48 -0500
permalink:  validation_is_best_that_comes_from_within
---

**“Belief in yourself is more important than endless worries of what others think of you. Value yourself and others will value you. Validation is best that comes from within.” ― Ngũgĩ wa Thiong’o – Dreams in a Time of War**

Applications need validations to ensure that data that a user inputs is valid before it is saved into the database. ActiveRecords allows us to perform model-level validations. For my Sinatra project, I created an app that will allow music students to log their practice hours each day.  I created a student model and a practice log model.  With the power of ActiveRecord validations, I was able to perform validations of user entered data within the models themselves. These validations are automatically run when the object is created, saved or updated or can be triggered by invoking the *valid?* method before saving.

In my student model, I was able to check that an attribute was not blank, unique (e.g. username, email) and had the correct format for that attribute. In my practice_log model, I checked that practice_minutes was numeric and was within a predetermined range and specified a custom message to be displayed when data entered was not valid. I even created my own custom validation by defining a method (i.e. log_date_in_range) created to make sure that the date the user selected was within the past year.
