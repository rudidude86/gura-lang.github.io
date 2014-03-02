---
layout: page
lang: en
title: Database Access
---

Database Access
---------------

### SQLite3 Database Operation

The following code careates SQLite3 database and registers contents in a CSV file.

    import(csv)
    import(sqlite3)
    
    Person = struct(name:string, email:string,
                    gender:string, age:number, birthday:string, mobile:string)
    
    sqlite3.open('50records-en.sqlite3') {|db|
        db.exec(R'''
        create table people (
            name     text,
            email    text,
            gender   text,
            age      integer,
            birthday text,
            mobile   text
        )
        ''')
        people = Person * csv.readlines(open('50records-en.csv'))
        db.transaction {
            for (person in people) {
                db.exec("insert into people values ('%s', '%s', '%s', %d, '%s', '%s')" % \
                        person.tolist())
            }
        }
    }

The code below extracts and prints information from a database that has been
created by the program above.

    import(sqlite3)
    
    Person = struct(name:string, email:string,
                    gender:string, age:number, birthday:string, mobile:string)
    sqlite3.open('50records-en.sqlite3') {|db|
        people = Person * db.query('select * from people')
        println(people)
    }
