# mongodbPractise

**Mongo Db 

    - It is NoSql database.
    - Data is stored in the form of database..

MongoDb working 

    - Database ---> contains ---> collections --> contains --> document --> contains --> column_name, values as json object.

Start Mongo 

    - mongo    --> command but it will deprecated in future with mongosh.
	- Install mongosh

** Use of commands in Mongo Db

    1. Show Databases :- 
        - To see all databases.
            - show dbs
        - To see current database.
            - db
        
    2. create & switch to & move in database
        - use db_name :- create and move in db_name database
            - use shooldb
    
    3. Delete a Database :-
        - Move to That Database 
            - use db_name 
        - Drop database
            -db.dropDatabase()
        
    4. clear screen :-
        - cls 

    5. create a collection 
        - for this we write db.collection_name (not displayed until any document is stored.)
            - Move in the database where you want to create a collection
                - use db_name
            - create collection 
                - db.collection_name
        - it will be displayed :- on inserting document
            - db.collection_name.insertOne({"key" : value})
    
    6. show collection
        - show collections
    
    7. create collection with validation rules or defining schema..
        - db.createCollection("collection_name",{validator : {$jsonSchema:{bsonType:"object", required:["name", "age"], properties:{name : {bsonType:"string", description:"most be string and is required"}, age:{bsonType:"int", description:"must required"},}}}})

            - db.createCollection("teacher", {
                validator : {
                    $jsonSchema : {
                        bsonType : "object",
                        required : ["name", "age", "salary"],
                        properties : {
                            name : {
                                bsonType : "string",
                                description : "name is required"
                            },
                            age : {
                                bsonType : "int",
                                description : "age is required"
                            },
                            salary : {
                                bsonType : "double",
                                description : "salary is required"
                            }
                        }
                    }
                }
            })
    
    8. show validation rules.
        - move in to database
            use db_name
        - db.getCollectionInfos({name : "collection_name"})
            db.getCollectionInfos({name : "teacher"})
    
    9. drop or delete collection 
        - db.collection_name.drop()
            - db.teacher.drop()
    
    10. retrive all data from db
        - db.collection_name.find()
            - db.teacher.find()
    
    11. insert single data 
        - db.collection_name.insertOne({key : values, .... })
            - db.teacher.insertOne({"name" : "Rohit Singh", "age" : 23, "salary" : 20000.23})
    
    12. insert multiple data
        - db.collection_name.insertMany([{...}, {...}])
            - db.teacher.insertMany([{"name" : "manik", "age" : 22, "salary":22332.23}, {"name" : "mohit", "age" : 23, "salary": 22344.12}])
    
    13. pretty method
            - for pretty look of the data displayed.
                - db.collection_name.find().pretty()
        
    14. retrive single data.
            - db.collection_name.findOne()
                - db.teacher.findOne()
            
    15. filter data (retrive based on fields)
            - db.collection_name.find(object)
                - db.collection_name.find({"name": "shiva"}) :- all documents with name : shiva

            - only one data to find :- use findOne
                - db.collection_name.findOne({"name": "shiva"})
            
            - find one and delete 
                - db.teacher.findOneAndDelete({"name": "shiva"})
            
            - find one and replace 
                - db.teacher.findOneAndReplace({"age": 22} , {"name" : "shiva", "age":22, "salary": 22222.22})
            
            - find one and update
                - db.teacher.findOneAndUpdate({"name": "ankit"}, {$set : {"name" : "manik"}})
            
    16. update 
            - update one 
                - db.teacher.updateOne({"name": "manik"}, {$set : {name : "ankit"}})
            
            - update many 
                - db.teacher.updateMany({"age": 22} , {$set : {age : 33}})
                
    17. limit 
            - db.collection_name.find().limit(number)
                - show 5 documents.
                    db.teacher.find().limit(5)
    
    18. delete :
            - delete one
                - db.teacher.deleteOne({age : 23})
            
            - delete many
                - db.teacher.deleteMany({age : 33})
    
    19. exit :-
            - ctrl + c
            - ctrl + d
            - .exit
    
    20. Authorization and Role :-

        - create user
            - db.createUser({user : "shiva", pwd : "123456", roles : [{role : "read", db:"schooldb"}]})
        
            - multiple roles : 
                - db.createUser({
                    user : "shiva",
                    pwd : "123456",
                    roles : [
                        {role: "read", db : "schooldb"},
                        {role: "readWrite", db : "schooldb"}
                    ]
                })

                - roles :
                    - read : read data on all non-systems collection
                    - readWrite : both read and write privileges
                    - dbAdmin : provides the ability to perform administrative tasks such as schema-related tasks.
                                It doesnot provide privileges for user and role management.
                    - userAdmin - create and modify roles and user on the current database.
                    - dbOwner : can perform any administrative action on the database. Here privileges are :- readWrite, dbAdmin and userAdmin roles.
                    - readAnyDatabase : can read only any database..
                    - readWriteAnyDatabase : can read and write both on any database.
                    - userAdminAnyDatabase :
                    - dbAdminAnyDatabase : 
                    - root : "provides access to the operation and all the resorces. (a super - user)

        - see users :
            - show users :
                - displays all the users in the current db.

        - enable Authorization
            - open mongo d conf file then uncomment 
            security :
                authorization : enabled
        
        - authenticate user 
            -mongosh --port 27017 --authenticationDatabase "schooldb" -u "shiva" -p "123456"

        - root user
            - db.createUser({
                user : "shivanand",
                pwd : "123456",
                roles : ["root"]
            })
