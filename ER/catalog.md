## Catalog

```plantuml

@startuml Catalog
 
'New Functionality
'Let User to Mark Reactions on Moment in Movies and Show Such Friends Reactions when Movie is Played.
 
entity Movies {
    * movie_id : uuid
    --
    * name : varchar
    * image : string
    * description : varchar
    * duration : smallint
    * cast_id : uuid
    * year : year
    * gross_worldwide : integer
    * rating_id : smallint
}
 
entity Ratings {
    * rating_id : uuid
    --
    * name : varchar
}
 
entity Genres {
    * genre_id : uuid
    --
    * name : varchar
}
 
entity MovieGenres {
    * movie_id : uuid
    * genre_id : uuid
}
 
entity Persons {
    * person_id : uuid
    --
    * full_name : varchar
    * birthday : date
}
 
entity Roles {
    * role_id : uuid
    --
    * name : varchar
}
 
entity MoviePersonages {
    * movie_id : uuid
    * person_id : uuid
    * personage_name : varchar
}
 
entity Casts {
    * cast_id : uuid
    --
    * person_id : uuid
    * role_id : smallint
}
 
entity Countries {
    * country_id : uuid
    --
    * name : varchar
    * flag : string
}
 
entity MovieCountries {
    * movie_id : : uuid
    * country_id : uuid
}
 
entity Awards {
    * award_id : uuid
    --
    * name : varchar
    * prize_image: string
}
 
entity Nominations {
    * nomination_id : uuid
    --
    * name : varchar
    * description: varchar
}
 
entity AwardsMovies {
    * award_id : uuid
    * nomination_id : uuid
    * movie_id : integer
    * person_id : integer
}
 
entity Reactions #0E0 {
    * movie_id : uuid
    * user_id : uuid
    * duration : smallint
    * reaction_type_id : smallint
}
 
entity ReactionTypes #0E0 {
    * reaction_type_id : smallint
    --
    * name : string
    * image : string
}
 
Ratings ||..|| Movies
 
Movies }|.. MovieGenres
Genres }|.. MovieGenres
 
Movies }|.. MoviePersonages
Persons }|.. MoviePersonages
 
Casts  ||..|| Movies
 
Persons }|.. Casts
Roles }|.. Casts
 
Movies }|.. MovieCountries
Countries }|.. MovieCountries
 
Awards }|.. AwardsMovies
Nominations }|.. AwardsMovies
Movies }|.. AwardsMovies
Persons }|.. AwardsMovies
 
Persons }|.. Lists
 
Movies }|.. Reactions
ReactionTypes }|.. Reactions
 
@enduml
```