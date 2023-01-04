# MongoDB

## Project 3: The Mongo Mash
You may work on and submit this project with one other person.


### Overview
In this project, you will translate the Project 1 UML solution into MongoDB collections, using JSON schema documents that I will provide. You will write and submit JSON documents to represent several theater, film, and showing documents. You will design a JSON Schema for a collection of actors who are the "stars" of the films in the database, choosing Mongo-appropriate ways to represent the relationship between films and their starring actors. Finally, you will write a few simple MongoDB queries using the MONGOSH shell in Compass.

### Setting up the Collections
Use Compass to create a new database, "project3". Create collections for films, theaters, and showings.

Copy and paste the contents of the schema_films.json file from Canvas (in the Projects module) into the Validation tab of the films collection in Compass. Do the same for schema_theaters.json (theaters collection) and schema_showings.json (showings collection).

You will want to review the schemas for each collection before moving on, and will refer to them when doing the next task.

### Creating validated documents
Begin by creating JSON documents for the following objects. Create them one at a time, stopping to insert them using Compass to make sure you have followed the schema. (Compass will reject the insert if you did not.)  The documents are similar to the data you created at the end of project 2:

A theatre named "Regal Edwards Long Beach", at 7501 E Carson St, Long Beach, CA 90808
Two rooms at this theater
"Screen 1".
This room supports two Formats: "Standard" and "IMAX".
This room has five seats:
Seats 1, 2, 3, and 4 are labeled as "reclining".
Seat 5 has two seat labels: "accessible seating" and "non-reclining".
"Screen 2"
This room supports "IMAX" and "ScreenX" formats.
This room has 1 seat, with no labels.
A film named "No Time to Die", release date October 8 2021, duration 163 minutes, rating PG-13.
Genres: Action, Adventure, and Thriller
A film named "Black Panther: Wakanda Forever", release date November 10 2022, duration 161 minutes, rating PG-13. 
Genres: Action, Adventure, and Superhero
A film named "Akeelah and the Bee", release date March 16 2006, duration 112, rating PG.
Genres: Family, and Drama
Showings for Black Panther: Wakanda Forever
Showing 1: November 10 2022 at 3:45 PM in the Standard format.
Ticket 1 for Seat 1, $18.
Showing 2: November 10 2022 at 7:00 PM in the IMAX format.
Ticket 2 for Seat 1, $22.
Ticket 3 for Seat 5, $15.
Showing 3: November 12 2022 at 1:00 PM in the Standard format.
No tickets sold.
Hint about tickets: tickets require a _id, but because they aren't their own document, Mongo won't provide one automatically. You must add this field by hand, with a special instruction to tell Mongo to make one for you. "_id" : {"$oid" : "<ObjectId()>"} will do the trick.


### A New Collection and Schema
You must now adapt the schema to store the actors who star in each film. An actor has a first name, a last name, a birthday, an IMDB URL (a link to the actor's page on IMDB.com, e.g., https://www.imdb.com/name/nm0000291/ Links to an external site.for Angela Bassett), and an _id that is an objectId. You will design and turn in a JSON schema file to validate actor documents, potentially (but not necessarily required to) changing the schemas for films, theaters, or showings.

Every film has many actors that star in it, and each actor can star in many films. This gives us a many-to-many relationship in UML, without an association class. According to lecture, you must decide whether a film has few, many, or zillions of actors; and whether an actor stars in few, many, or zillions of films. Make these decisions with the broad world of films and actors in mind, not just the films you have been asked to insert into your database. Also consider: in this enterprise -- in which theaters are storing their showings so customers can purchase tickets -- how often is an actor object going to be needed on its own? When loading a film document to display a webpage with that film's details, do you need to know all of the details of every starring actor, or would just a few details for each suffice? Is there an opportunity for denormalization and redundancy to reduce joins between tables for the most-frequent use cases? Should you be able to quickly find all films starring a particular actor? This is all for you to decide and justify (see the Deliverables section).

Implement the design for your actors in the schema accordingly. As noted above, you may need to change other collection schemas, and you must submit those schemas if you change them. When you are done, insert documents in the actors table for these stars of Black Panther: Letitia Wright, Lupita Nyong'o, Danai Gurira, and Angela Bassett. Also insert data for Angela Bassett starring in "Akeelah and the Bee". Again, you might need to modify other documents depending on your schema design.

### Queries
Finally, write mongosh queries to answer the following questions. You will turn in the queries, and not the results of the queries.
Select all films that have "Action" as one of their genres, sorted by film title.
Select the showtime of all Black Panther: Wakanda Forever showings that are on November 11. You don't need to use joins; you can hard-code the filmId of this film. Hint: you can use a filter with both $lt and $gt comparisons. A date is on November 11 2022 if it is greater than midnight of November 11 and less than ____.... To put a date into a query, you must write ISODate("..."), where the parameter is the date in YYYY-MM-DD format.
For each theater, select the name of the theater and also a list of all the film titles and showtimes of all showings scheduled in the theater. This requires a join from theater to showing.

### Deliverables
You must deliver to me, via Dropbox, a single PDF containing the following documents:

Schemas for adding actors to films. Include all schemas that you created or modified to implement this.
A written justification for the decisions you made in implementing the actors (and related) schemas. This 1-2 paragraph response, in full English sentences, should communicate the depth and breadth of decisions you made in designing this part of the schema. You should, at a minimum, answer the questions posed to you in the "A New Collection" section, in the context of your final answer.
JSON documents for the theaters, films, showings, and actors that you were required to create.
mongosh commands that you wrote to solve the 3 queries. I do not need the output of those queries, just the statements themselves.
