# Relations between Models

By Brennan R.

## Synopses

Models in Django are not always completely distinct, separate units. Often, data from one model is related to another. For example, in a project portfolio app, a portfolio model may be affiliated with a project model. Another example might be a user-account model is is affiliated with blog posts the user makes. In any case, as developers it is important to be able to represent the relations between models so we can easily interact with them in a more fluid manner. 

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

In a One-to-One relationship, a single model stores a foreign key that matches to a singular other model. 
For example, in the portfolio app, each student is associated with a singular portfolio. Since this relation is not bi-directional (student -> portfolio), this is a one-to-one relationship.

![One-to-one relationship between a student and their portfolio](https://kroki.io/dbml/svg/eNqFzkEKwkAMheF9TvEuoAfwFC7cSSmZ6VSjM5OSpsUivbsgKMWNy_8tHt-JQ04YfepSdTwJkA5BLlId58GksC24p6UhoHJJmNnilY2AVFjypgvf1D4NEHBU83bzZ6k_YIdBzXvNonvpGlqJTm_Ed_7DcPG8dUStztHbX4-MLUeXOSGoZgI46OTw9HBa6QVPkFS6)

In Django, a One-to-One relation is made by creating an attribute of a model as an instance of a [`models.OneToOneField`](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.OneToOneField) class. For example, the Student -> Portfolio relation was created using the following code:
```python
class Student(models.Model):
    #Other model member variables/attributes
    
    Port = models.OneToOneField(Portfolio, null = True, on_delete=models.CASCADE)
```

## One-to-Many 

This relation is used when a single object contains a key that many other objects reference as a foreign key. For example, a single teacher who many be the teacher of many students is a One-to-Many relationship. 

![One-to-many relationship between a teacher and their students](https://kroki.io/dbml/svg/eNqFjTEOQEAUBft_incCB1A4hU4Un33YsBv5lkTE3SVClNqZTKbUZiIStR1ohwDewcfEnoZqNh_UdozcawGiBmJTawc1OUXKu13S6hjTT_scPm_schQvz7yr5ZQLuI8wtA==)

In Django, One-to-Many relations are created by adding a [`models.ForeignKey`](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.ForeignKey) attribute to a model. For example, relating many projects to one portfolio can be done using the following code:
```python
class Project(models.Model):
    #Other attributes of the model
    portfolio = models.ForeignKey(Portfolio, on_delete=models.CASCADE)
```

## Many-to-Many

A many-to-many relationship exists when multiple models are related to multiple other models. A great example given on [Andy Marker's article](https://www.smartsheet.com/database-relationships) when giving examples of Many-to-Many relations: "The members of a family can own many pets". This kind of relation can be messy, as requires a separate table be set up to create the association between the two models:

![Many-to-many relationship between family members and their pets](https://kroki.io/dbml/svg/eNqVjzEKwkAURPt_ijmBB7DwBJbpRJYfM4mfZJflswiL5O6SBEFJo90UjzczjbYT0Wu0qYbI2NKfAlgHS4UDHZfsFtUrRtarAEkj8VC_3dUF0IFvVGaRZvVllv8speZfpOFsaQy7tVsKn3XO_ojT97GDdUv14rEOOzazrMQsL83KXtE=)

In Django, Many-to-Many relations are created by adding a [`models.ManyToManyField`](https://docs.djangoproject.com/en/4.2/ref/models/fields/#manytomanyfield) attribute to a model. According to the Django documentation, this will trigger Django to create a separate table to act as the link between the two models. Implementing the family-pet relation can be done using the code below:
```python
class family_member(models.model):
    name = models.CharField(max_length=200)
    age = models.IntegerField

class pet(models.Model):
    name = models.CharField(max_length=200)
    type = models.CharField(max_length=200)
    age = models.IntegerField()

    familyMember = models.ManyToManyField(family_member)

```

## Sources

- [Database Relationship Types & How They Are Established](https://phoenixnap.com/kb/database-relationships)
- [Set Sail on Database Relationships: Understanding One-to-One, One-to-Many, and Many-to-Many](https://www.smartsheet.com/database-relationships)
- [Django 4.2 | Model field reference](https://docs.djangoproject.com/en/4.2/ref/models/fields/)