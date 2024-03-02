# Relations between Models

## Synopses

Models in Django are not always completely distinct, separate units. Often, data from one model is related to another. For example, in a project portfolio app, a portfolio model may be affiliated with a project model. Another example might be a user-account model is is affiliated with blog posts the user makes. In any case, as developers it is important to be able to represent the relations between models so we can more easily interact with them in a more fluid manner. 

## Keys

All of these database relations rely on the use of a key, or a value within the model's database table that helps to identify each entry into the database. The datatype of the key can be anything, but in most cases either a numerical ID or UUID is used to identify each entry. For example, the `id` column of the following table is used as the primary key (shown with a 🔑) of the `project` table

| id 🔑	| title              	| portfolio_id 	| description 	|
|----	|--------------------	|--------------	|-------------	|
| 1  	| Example Project #1 	| 1            	| ...         	|
| 2  	| Example Project #2 	| 2            	| ...         	|
| 3  	| Example Project #3 	| 3            	| ...         	|

Notice how I called the id of the table the *primary* key of the table. A primary key is the value used to identify entries within the table the entry exists in. Conversely, a *foreign* key is the key used to access an entry from a different table. In the project table above, the portfolio_id is referencing the *primary* key in a `portfolio` table. Since this key exists in the `project` table, within this context it is called a *foreign* key.

By using foreign keys, models are able to point to data related to them, and are the tool we use to implement each type of relation.

## One-to-One

## One-to-Many 

## Many-to-Many

## Sources

- [Database Relationship Types & How They Are Established](https://phoenixnap.com/kb/database-relationships)
- [Set Sail on Database Relationships: Understanding One-to-One, One-to-Many, and Many-to-Many](https://www.smartsheet.com/database-relationships)