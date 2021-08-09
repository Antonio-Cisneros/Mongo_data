Learn MongoDB in $%#^ minutes

%Asking for help? Use the command
	> help

# Introducing MongoDB

%Create a variable in MongoDB
	You have to write:
##Remember to use the  { to open the statement and } to close it.
##Also use the , to separate the statements of the variable
##Use the "" for strings, instead of write the number's name like "nineteen"
##Write the number 
	> var book_1 = { "book's name": "Siddartha", "Author": "Hermann Hesse"}

%To call the variable and see its contents
	> book_1
%It will display the content of the variable using the braces.

%Create a database 
	> use Silmaril

%Show that we are in the Database
	> db
%The output will be the name of the database that we already create
	> Silmaril

%To change into another DB 

%Visualize the DB that are already created and also display the storage of the database
	> show dbs

# Queries and Data Types

%Insert a collection in a database, it would be state or write in the following way.
## Use the () to start the and ends the insertion of a new collection.
	> db.books.insert({"book's name": "Siddartha",
		"Author": "Hermann Hesse"})


%To display and visualize which are the collection(s) that we created just type
	> db.books.find()
##The contents will be display and their ID

%We can also use the command find to display an specific field of the query
	> db.books.find({"book's name": "Siddartha"})

%Adding integer and float values are available for MongoDB
> db.books.insert({"book's name": "Siddartha", 
	"Author": "Hermann Hesse",
	"price": 200,
	"Publisher": "New directions"})
%The Dates can be added
> db.books.insert({"book's name": "Siddartha", 
	"Author": "Hermann Hesse",
	"price": 200,
	"Publisher": "New Directions",
	"tryDate": new Date(1992, 6, 28)})

% We can store in the collections any type of data using an array
> db.books.insert({"book's name": "Siddartha", 
	"Author": "Hermann Hesse",
	"price": 200,
	"Publisher": "New Directions",
	"tryDate": new Date(1992, 6, 28)
	"Page": ["Parameters"]})

# Removing and Modifying Documents

%You can remove() to delete document that would match or not with the rigth query
	> db.books.remove({"book's name": El Principito})
#The output would show that the remove was did.
#If you a write a certain parameter, it will remove those documents which match with the paramater to remove

%Updating an existing document you have to use the update() option
#You must use the "$set" if you only write "set" that will be your new parameter
	> db.books.update({"book's name": "El principito"},
		{"$set": {"Author": Antoine de Saint-Exupéry})

%If you want to update no just one document, update all the documents that match with the new parameter of the query
#Use "multi":true for that.
	> db.books.update({"book's name": "El principito"},
		{"$set": {"Author": Antoine de Saint-Exupéry},
		{"multi": true})

#It will match with the other documents which have the same parameter.

%If you want, you can create a counter and you wanted to increase it in a log document.
%Use the $inc operator.
	> db.logs.update({"Weapon": Iron Greatsword},
		{"$inc": {"count": 1}})
#If you do that but the document doesn't exist, it won't do anything.
#Apply the option "upsert" for that.
	> db.logs.update({"Weapon": Iron Greatsword},
		{"$inc": {"count": 1}},
		{"upsert": true})
#If you repeat the same command the counter will change or increase according to the "upsert" option.

##Let's add 3 documents.
	> db.potions.insert({"name": "Fus Rho Da", "Color": "Blue"})
	> db.potions.insert({"name": "Storm", "Color": "Purple"})
	> db.potions.insert({"name": "Slay Dragon", "Color": Red"})
	
%Removing the fields from a collection that you never use is possible.
##Use the $unset operation for that.
##The brackets {} means that you are selecting all the potions collections.
##Also use the multi = true option you verify the match between documents and parameters.
	> db.potions.update({},{"$unset": {"color": ""}},{"multi": true})

# Advanced Modification

%Insert a new potion with a secret ingredient
	> db.potions.insert(
	{"name": "Cure disease",
	"Vendor": "Arcadia",
	"price": 164,
	"score": 67,
	"tryDate": new Date(2011, 4,23),
	"ingredients": ["Blisterwert", "secret", "Mudcrab chitin"],
	"ratings": {"strength": 8, "flavor": 5}
	}
)
	
##If you want to change field names, use the $rename operator for that.
	> db.potions.update({},
	{"$rename": {"score": "grade"}},
	{"multi": true}
	)
## use the find() and observe what happen with the field.
##The field that you changed, it will be moving at the end of the potions.

%Knowing a "secret" ingredient in a document you must require the update() options
##As the parameter is an array you have to write all the elements
##Another option is using the position of the value which will be change.
	> db.potions.update(
	{"name": "Cure disease"},
	{"$set": {"ingredientes.1": "Sugar"}}
	)
##Use the find() option to verify if the update was did.
##Insert more potions and use the ingredients.$ for all the arrays.

%Doing the same statement if you want to update a field that was wrote in {}
	> db.potions.update(
	{"name": "Cure disease"},
	{"$set": {"ratings.strength": 10}}
	)
	
MongoDB provides a diversification of methods to modify values or fields.
	$max --> Update the greater value or it's created 
	$min --> Update the lower value or it's created
$mul --> Multiplies the current field by specifing the value, if it's empty gives you 0

##Let's insert another document
	> db.potions.insert({"name": "Shrinking", "vendor": "Faradas",
	"categories": ["tasty", "effective"]})

%Using the $pop operator will remove the value depending either the first or last value
	> db.potions.update({"name": "Shrinking"}, {"$pop": {"categories": 1}})

##The output will show only first element
## 1 for the first value
## -1 for the last value

##Using $push operator will do the opposite it will add another value and it will be at the end
	> db.potions.update({"name": "Shrinking"},{"$push": {"categories": "budget"}})

##Additionally, $addToSet operator will add a value to the end, if the value exist it doesn't change and if not it will be added.
	> db.potions.update({"name": "Shrinking"},{"$addToSet": {"categories": "budget"}})

##A relative of $pop operator is $pull operator that will remove using the name of the value.
	> db.potions.update({"name": "Shrinking"},{"$pull": {"categories": "tasty"}})

# Query Operators

%You can find multiple parameters using the find() option
	> db.potions.find(
	{
	"vendor": "Kettlecooked",
	"rating.flavor": 5})
#It will display the name of the documents.

# Comparison operators

$gt	Greater than
$gte	Greater than or equal to
$ne	Not equal to
$lt	Less than
$lts	Less than or equal to

%You can use the find() options by applying a comparsion between prices, inequality, range
	> db.potions.find({"price": {"$gt": 10, "$lt": 20}})
	> db.potions.find({"vendor": {"$ne": "Kettlecooked"}})
	> db.potions.find({"sizes": {"$elemMatch": {"$gt": 8, "$lt": 16}}})
	> db.potions.find({"sizes": {"$gt": 8, "$lt": 16}})

##Careful with the last two find() options, recognize the match for each number

# Customizing Queries

%Developing list to visualize the documents that you created

##Know you can code a projection using the find() option in ordered to specify the labels or fields of a collection.
	> db.potions.find({"grade": {"$gte": 30}},
	{"vendor": true, "name": true})

##The output shows the fields that you selected like "vendor" and "name"
##The true it the condition to choose the field.
## The opposite to visualize the other fields or exclude the fields.
	> db.potions.find({"grade": {"$gte": 30}},
	{"vendor": false, "price": false})

%You can use an optimal find() option or an exclusive fields by using the "_id"
	>db.potions.find({"grade": {"$gte": 30}},
	{"vendor": true, "price": true, "_id": false}) 

##The inclusion or exclusion of the fields depend on the statement true or false but depend on the context.
	> db.potions.find({"grade": {"$gte": 30}},
	{"name": true, "vendor": false})

##Using a find() function gives the option to visualize all the documents.

%Knowing the characteristics of the find() option give you the "cursos object"
	> db.potions.find({"vendor": "Kettlecooked"})
#It will visualize at least the first 20 documents.
##If you have more than 20 documents.
	> db.potions.find()

#Also visualize the first 20 documents.
##And the option of type "it" is for showing the rest.

%Counting the number of documents that you have the count() option is preference.
	> db.potions.find().count()

%You can sort the documents on ascending or descending order
##Use 1 (Ascending) or -1 (Descending)
	> db.potions.find().sort({"price": 1})
	> db.potions.find().sort({"price": -1})

%The limit() and skip() options is a basic method to page your documents.
	> db.potions.find().limit(3)
	> db.potions.find().skip(3).limit(3)

##Using big numbers are not useful if you are using the skip() option when you are working with large collections.

#Data Modeling

When you make a survey for a user registration and on the User Profile surveys, the fields can be related to the users. MongoDB allows on embedded documents specifying or adding certain missing data if the are hole on the query.
If there are a duplication on the data, you can make a reference on a new collection it could be added to the potion's collection. You must use the id of the each document to develop a better query and reference a the collection that you just did.
Features on embedded documents provides (not a the best NoSQL format) the available options to grap the exact parameters of a document to be collected. There are atomic operations that guarantee if the are an update on the parameters and there is a mistake on the syntax, the none of the update will occur.
Once you made the reference on a document, the collection will have that part of the information that was referenced. Multi-document syntax for implement a reference is not supported. You can't write new parameters in atomic level if the syntax doesn't is from the same collection.
MongoDB doesn't allow transactions for the relationship between queries and collection.

# Data Modeling Decisions

The difference between embedding and referencing a document would be not hard decision.

Embedding:
	~ Single query
	~ Documents accsed through parent
	~ Atomic writes

Referencing:
	~ Requires 2 queries
	~ Documents exist independently
	~ Doesn't support multi-document writes

Comments are allowed on both but using embebbing is easier because for the query on the user registration, embedding will work most of the time and referencing only can comment using multiple queries.

According to size of data, reference allows more for the use of multiple queries that callow the indepently documents to be processed. Embedding and referencing should be decided for the size limit on the 50 comments.

Summarize those features:

Embedding is better for the collection to a comment (less than 100 comments per document, rarely are less than 50 comments).
Referencig is better for the commets to user fields.

The guidelines stages that is better to make a embedded document according to the conditions on the data modeling.

# Common Aggregations

#Using the collections on MongoDB provide us the opportunity to find the exact of documents that we have using the $group operator for that.

##Insert 6 extra potions with the parameters "name", "vendor" and "grade".
##After you insert the potions, use the following command.
	> db.potions.aggregate([{"$group": {"_id": "$vendor"}}])

#The output must in this case the names of the vendors.
#If you have a null is for the potions that don't have a vendor

#Another method is using the accumulator of the each field on the document
	> db.potions.aggreagate([{"group": {"_id": "vendor", "total": {"$sum": 1}}}])

%it should display the vendor and how many potions have the name of that vendor
%Using "$" means that a field perform a task

% More Operator options are...
	> db.potions.aggregate([{"group": {"_id": "vendor", "total": {"$sum": 1},
	"grade_total": {"$sum": "$grade"}}}])

	> db.potions.aggregate([{"group": {"_id": "vendor",
	"avg_grade": {"$avg": "$grade"}}}])
	
	> db.potions.aggregate([{"group": {"_id": "vendor",
	"max_grade": {"$max": "$grade"}}}])

	db.potions.aggreagate([{"group": {"_id": "vendor",
	"min_grade": {"$min": "$grade"}}}])


# The Aggregation Pipeline

Do not have unicorns on the your collections, the solution for that is query potions, group by vendor and sum the number of potions per vendor.
##You must use the aggregate method as a pipeline for the parameters and fields, where the collection would be filtered as document and the grouped.
##Emmploy the $match operator for a better performance and $group for a better filter for the data.

On the previous sections, it was used the $sort operator, it'is also useful for the stage of the documents. Limit operator provide the grouped number of documents for the stage, and the $project operator is a optimal find and more fast to avoid the errors and help us to make a better pipeline

	>db.potions.aggregate([
	{"$match": {"price": {"$lt": 15}}},
	{"$project": {"_id": false, "vendor_id": true, "grade": true}},
	{"$group": {"_id": "$vendor", "avg_grade": {"$avg": "$grade"}}},
	{"$sort": {"avg_grade": -1}},
	{"$limit": 3}
	])


--------------------------------------------------------------------
# Question section

1. Why not MongoDb?
It's not weull suited for applications that need: multi-object transactions, 
SQL (For the implementations on specific queries), Strong ACID guarantees and 
traditional BI (The run of different number of applications).

2. Is the are difference between using SQL?
A user has many questions; a question has many answer.

MongonDB can have document relationship, it's far easier to query relations in SQL.

3. Does MongoDb require a lot of RAM?
MondoDB uses the free memory that is on the computer as its cache.

4. When should we use MongoDB?
If you can represent your data in a form of a bunch of documents, MongoBD is the option.


5. When should not we use Mongo DB?
If you would rather imagine your data as a bunch of interconnected tables, MongoDB would not be the right option.

6. When MongoDB is friend for our data?
MongoDB is very fast and reliable, but never forget you don't have relational information in your Db.

Which means if you change something in the structure of your document, it could be possible you don't have the data to fill the holes in your stored parameters.

7. MongoDB produce a lot of computer work?
In general, creates more for the client server, join the data one has to issue multiple queries and do the join in the client.


8. MongoDB or MySQL?
MongoDB's databases are great when you usually know where your data is. With Mongo, the related data is either nested in the parent data or it has primary/foreign keys. In the other hand, if you are need to use aggregate functions and feel the need to query data in complex ways that using Mongo can't achieved through simple relations, use MySQL.

9. When to use a single collection on MongoDB?
Almost never, applications have structure, and deal with data containing structure even if that structure is some form of meta-structure.

Otherwise every piece of code would be one-off never to be used again.

10. Working as an analytic tool?
MongoDB provides a custom map/reduce implementation for those simple relationships on documents or parameters.

11. Collection per day or Database per day?
The better to fit is a collection per day for the map/reduce work to summarize the data.

12. Advantages using MongoDB?
	1. Document can have any structure within one collection.
	2. Good speed
	3. Good means for replication

13. What the limit size for a document on MongoDB?
MongoDB allows only 16 MB for each document 

14. How is the performance on MongoDB?
MongoDB is able to check your queries' filtering condition instead of going through each document in the collection.
With the time, queries would be getting slower and with the amount oof documents in a collection the reason is how you stored the index of the collection.

15. MongoDB has Keys?
MongoDB doesn't support server side foreign key relationships, normalization is also discouraged if your structure is more complex then probably you should choose a SQL and no a NOSQL.

# Topics to approach on MongoDB if your a new learner on MongoDB
	
	~ How to create a collection
	> db.createCollection("Collectionname")

	~ Indexes
%An extra topic to board is the use of index on MongoDB, because without an index the collection and its fields are only for consulting.
	> db.collection.createIndex([Key and index type])
You cand add options to the command if you to develop an optimal or exclusive index for the collection.
	> db.collection.createIndex([Key and index type], [options])
	> db.collection.createIndex ({name: -1})
##It will create a single key descending index on the name field.

	~ Using database commands to take advantage of advance features
%To run a command against the current databases.
	> db.runCommand({command})
%To run an administrative command against the admin database.
	> db.adminCommand({command})
 

///////////////////////////////////////////////////////////////////////////
References
https://stackoverflow.com/questions/4288615/why-not-mongodb
https://softwareengineering.stackexchange.com/questions/54373/when-would-someone-use-mongodb-or-similar-over-a-relational-dbms
https://stackoverflow.com/questions/26423721/what-situations-is-mongodb-perfect-for
/////////////////////////////////////////////////////////////////////////////

Author: Antonio Cisneros
