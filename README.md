# README

heroku link: https://shielded-citadel-55760-b7d857dda73e.herokuapp.com/movies

Note: everything is fine and dandy locally but my heroku doesnt work. I get this error:

2024-02-22T04:11:38.590558+00:00 heroku[router]: at=info method=GET path="/movies" host=shielded-citadel-55760-b7d857dda73e.herokuapp.com request_id=75e8439a-91ca-4e05-bd1b-cc5c5c261678 fwd="50.24.138.116" dyno=web.1 connect=0ms service=108ms status=500 bytes=1891 protocol=https

My understanding is that it is some database issue, but I can not figure it out. 

I think it has to do with a migration not going through>>>

(base) francescoromano@Macbook-Pro-618 rottenpotatoes % heroku run rails db:migrate
Running rails db:migrate on ⬢ shielded-citadel-55760... up, run.2841 (Basic)
W, [2024-02-22T04:10:14.677787 #2]  WARN -- : You are running SQLite in production, this is generally not recommended. You can disable this warning by setting "config.active_record.sqlite3_production_warning=false".
I, [2024-02-22T04:10:14.742138 #2]  INFO -- : Migrating to CreateMovies (20240222021153)
== 20240222021153 CreateMovies: migrating =====================================
-- create_table("movies")
   -> 0.0009s
== 20240222021153 CreateMovies: migrated (0.0010s) ============================

(base) francescoromano@Macbook-Pro-618 rottenpotatoes % heroku run rails db:seed   
Running rails db:seed on ⬢ shielded-citadel-55760... up, run.6984 (Basic)
W, [2024-02-22T04:10:29.774640 #2]  WARN -- : You are running SQLite in production, this is generally not recommended. You can disable this warning by setting "config.active_record.sqlite3_production_warning=false".
You have 1 pending migration:
  20240222021153 CreateMovies
Run `bin/rails db:migrate` to update your database then try again.

and on the server side it shows that the table is being vreated then immediately says its not there:
2024-02-22T04:16:19.630164+00:00 app[api]: Starting process with command `rails db:migrate` by user fwromano@tamu.edu
2024-02-22T04:16:23.012130+00:00 heroku[run.4413]: State changed from starting to up
2024-02-22T04:16:27.922815+00:00 heroku[run.4413]: Process exited with status 0
2024-02-22T04:16:27.949478+00:00 heroku[run.4413]: State changed from up to complete
2024-02-22T04:16:48.442577+00:00 heroku[router]: at=info method=GET path="/movies" host=shielded-citadel-55760-b7d857dda73e.herokuapp.com request_id=b70d6dd9-276c-493a-a423-6b66612e8e93 fwd="50.24.138.116" dyno=web.1 connect=0ms service=28ms status=500 bytes=1891 protocol=https
2024-02-22T04:16:48.419391+00:00 app[web.1]: I, [2024-02-22T04:16:48.419203 #16]  INFO -- : [b70d6dd9-276c-493a-a423-6b66612e8e93] Started GET "/movies" for 50.24.138.116 at 2024-02-22 04:16:48 +0000
2024-02-22T04:16:48.423103+00:00 app[web.1]: I, [2024-02-22T04:16:48.423012 #16]  INFO -- : [b70d6dd9-276c-493a-a423-6b66612e8e93] Processing by MoviesController#index as HTML
2024-02-22T04:16:48.440031+00:00 app[web.1]: I, [2024-02-22T04:16:48.439936 #16]  INFO -- : [b70d6dd9-276c-493a-a423-6b66612e8e93]   Rendered layout layouts/application.html.erb (Duration: 11.3ms | Allocations: 2510)
2024-02-22T04:16:48.440332+00:00 app[web.1]: I, [2024-02-22T04:16:48.440271 #16]  INFO -- : [b70d6dd9-276c-493a-a423-6b66612e8e93] Completed 500 Internal Server Error in 17ms (ActiveRecord: 2.5ms | Allocations: 3996)
2024-02-22T04:16:48.441194+00:00 app[web.1]: E, [2024-02-22T04:16:48.441128 #16] ERROR -- : [b70d6dd9-276c-493a-a423-6b66612e8e93]   
2024-02-22T04:16:48.441195+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93] ActionView::Template::Error (SQLite3::SQLException: no such table: movies):
2024-02-22T04:16:48.441196+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     3: <h1>Movies</h1>
2024-02-22T04:16:48.441200+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     4: 
2024-02-22T04:16:48.441200+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     5: <div id="movies">
2024-02-22T04:16:48.441201+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     6:   <% @movies.each do |movie| %>
2024-02-22T04:16:48.441202+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     7:     <%= render movie %>
2024-02-22T04:16:48.441202+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     8:     <p>
2024-02-22T04:16:48.441202+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]     9:       <%= link_to "Show this movie", movie %>
2024-02-22T04:16:48.441203+00:00 app[web.1]: [b70d6dd9-276c-493a-a423-6b66612e8e93]   
