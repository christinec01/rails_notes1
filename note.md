
rails new 
-d postgresql 
-B skips bundle 

gems to add:
awesome_print
better_errors
faker

Schema

Schema for Parkr-Anon

Premises (for fleshing out necessary routes/actions)

User should be able to see all cities

Indicates necessity of paths:
GET /cities
User should be able to see all parks listings within a city

Indicates necessity of paths:
GET /cities/:city_id/parks
User should be able to create a park listing within a city

Indicates necessity of paths:
GET /cities/:city_id/parks/new
POST /cities/:city_id/parks
User should be able to view a park listing and all its corresponding reviews

Indicate necessity of paths:
GET /cities/:city_id/parks/:id
User should be able to edit (but not delete) a park listing

Indicate necessity of paths:
GET /cities/:city_id/parks/:id/edit
PUT /cities/:city_id/parks/:id/
User should be able to write, edit, and delete a review for a park listing

Indicate necessity of paths:
GET /cities/:city_id/parks/:park_id/reviews/new
POST /cities/:city_id/parks/:park_id/reviews
PUT /cities/:city_id/parks/:park_id/reviews/:id
DELETE /cities/:city_id/parks/:park_id/reviews/:id


Client Requests (for custom routes)

"I want to be redirected to the page with all of the cities when I visit /."

"I want an alternate URL in addition to /cities to see all cities. It should be /cities/all".

SETTING UP ROUTES
routes.rb
```
Rails.application.routes.draw do
root 'cities#index' <======= root 'controller#action'
resources :cities, only :index do
resources :parks, only [:index, :new] do<========= every time you do resources :thing do, everything inside of that becomes a nested
                                                   resource of the resource above it
resources :reviews

end
end
```
cities_controller
```

def index
@cities = City.all
end
```
in the list of cities(cities/index.html.erb), you can do a link_to method in the erb using <%=city.name
so <%= link_to city.name, city_parks_path(city) %> the city_parks_path is a helper(its the prefix in rails routes), then you look at the uri that this route needs and 
notice it needs the id of the city, thats why (city) is there in parenthises 


to link to edit:
link_to 'edit part information', edit_city_park_path...etc


for custom routes, in the controller, do get 'your path here' to: "controller#action"
