---
layout: post
title:      "Validation is best that comes from within..."
date:       2019-12-04 22:43:48 -0500
permalink:  validation_is_best_that_comes_from_within
---

**“Belief in yourself is more important than endless worries of what others think of you. Value yourself and others will value you. Validation is best that comes from within.” ― Ngũgĩ wa Thiong’o – Dreams in a Time of War**

Applications need validations to ensure that data that a user inputs is valid before it is saved into the database. ActiveRecords allows us to perform model-level validations. For my Sinatra project, I created an app that will allow music students to log their practice hours each day.  I created a student model and a practice log model.  With the power of ActiveRecord validations, I was able to perform validations of user entered data within the models themselves. These validations are automatically run when the object is created, saved or updated or can be triggered by invoking the *valid?* method before saving.

In my student model, I was able to check that an attribute was not blank, unique (e.g. username, email) and had the correct format for that attribute. In my practice_log model, I checked that practice_minutes was numeric and was within a predetermined range and specified a custom message to be displayed when data entered was not valid. I even created my own custom validation by defining a method (i.e. log_date_in_range) created to make sure that the date the user selected was within the past year. My models are shown below:

```
class PracticeLog < ActiveRecord::Base
  belongs_to :student
  validate :log_date_in_range?
  validates :date, presence: true
  validates :practice_minutes, presence: true
  validates :practice_minutes, numericality: { greater_than_or_equal_to: 10, less_than_or_equal_to: 600,
                                                message: "can be from 10 to 600" }

  def log_date_in_range?
    if !((Date.today - 365)..Date.today).include?(date)
      errors.add(:date, "must be within the past year")
    end
  end
end

class Student < ActiveRecord::Base
  has_secure_password
  validates :password, length: { minimum: 4 }
  validates :fullname, presence: true
  validates :fullname, format: { with: /\A[a-zA-Z][0-9a-zA-Z .,'-]*{1,39}\z/,
                        message: "must be between 2 and 40 characters and only contain alphanumeric or (. , - ') " }
  validates :username, uniqueness: true
  validates :username, presence: true
  validates :username, format: { with: /\A[a-z]+[a-z0-9_]{1,9}\z/,
                        message: "must start with letter and only contain lower case alpha and numeric" }
  validates :email, uniqueness: true
  validates :email, presence: true
  validates :email, format: { with: /\A[^@\s]+@[^@\s]+\z/,
                        message: "invalid email format" }
  
  has_many :practice_logs
end
```
 
 Any errors on validation can be accessed using ActiveRecord’s errors method. I used this feature in conjunction with  the sinatra-flash gem to render error messages.  For example, when creating a new practice_log, I  "build" a new practice log with the data the user input and then validate it .  If it is not valid, I set the flash error message and this is rendered when the user is redirected. 
 ``
@practice_log = current_user.practice_logs.build(params)
            if @practice_log && @practice_log.valid?
                @practice_log.save
                redirect to "/practice_logs"
            else
                flash[:error] = @practice_log.errors.full_messages.to_sentence
                redirect to "/practice_logs/new"
            end
		``
		
		Having the validations in the model using ActiveRecord's built-in features made my code more DRY and robust. In coding, as in life, "Validation is best that comes from within…"



