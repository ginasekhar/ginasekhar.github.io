---
layout: post
title:      "Do more than belong: participate..."
date:       2020-01-18 04:35:34 +0000
permalink:  do_more_than_belong_participate
---



Do more than belong: participate.  Do more than care:help. Do more than believe:practice. Do more than be fair:be kind. Do more than forgive:forget. Do more than dream:work. - William Arthur Ward

Rails allows us to set up associations between Active Record models.  This association makes it much easier to perform several operations on the records in our application.  The theme of my application was Movies. I created the following models in my application:

1. Movie
2. Showing
3. Ticket
4. User

In my models, I set up the following associations: 

```
class Movie < ApplicationRecord
    ....
    has_many :showings
    has_many :tickets, through: :showings
     ....
end
class Showing < ApplicationRecord

    belongs_to :movie
    has_many :tickets
    has_many :users, through: :tickets
  ...
	end
	
	class Ticket < ApplicationRecord
     belongs_to :user
     belongs_to :showing
	...
	end
	class User < ApplicationRecord
     has_many :tickets
     has_many :showings, through: :tickets
	end

		
		
```

Just establishing the has_many & belongs_to relationships in ActiveRecord gives us access to the following methods:
```
movie.showings – references movie’s showings
movie.showings << showing – establishes a new relation between a movie and a showing
	              showing.movie – references the movie the showing belongs to	
movie.showings.build({ }) –instantiates a new ‘showing’ object and associated it with the movie. It populates                the movie_id attribute on the showing. This is similar to the statement Showing.new({movie_id: movie.id}). It is not saved to the database until you call "save" on the object.
	movie.showings.create({ }) – instantiates a new showing and saves it into the database.
	showing.build_movie – same as above, instantiates a new movie without saving it
	showing.create_movie – same as above, instantiates and saves the movie into the database

```

In my application, I have used these relationships to reference and build objects - for example in my tickets controller, I create a new ticket using the statement`current_user.tickets.build(ticket_params)`.  In my theater owner view of the tickets index page I was able to get information from all 4 models very easily without any hassle using the following code in my view: `<strong>Ticket Type:</strong> <%= ticket.ticket_type %><strong> Number: </strong> <%= ticket.id %> <strong> Customer: </strong><%= ticket.user.name %> <strong> Movie: </strong><%= ticket.showing.movie.title %><strong> Show: </strong> <%= ticket.showing.show_date %> <%= ticket.showing.show_time %> ` .The ActiveRecord associations did all the the database joins for me.  Living up to William Arthur Ward's advice, ActiveRecord models through associations, 'Do more than belong:  they participate'



