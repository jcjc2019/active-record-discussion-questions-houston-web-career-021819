# ActiveRecord Discussion Questions

## Part One - Reading the Documentation

Looking at Documentation is an important part of programming. You don't have to memorize anything, but you should get familiar with the types of information you can find in different docs. For this exercise, go through the ActiveRecord documentation [here](http://guides.rubyonrails.org/active_record_querying.html#retrieving-objects-from-the-database) with your table mates and answer the following questions about each method.

1. What argument or arguments does the method take?
2. What type of object does the method return?
3. What happens if none of the parameters match? (i.e. what if `Tweet.find(5)` can't find that tweet? How about `Tweet.find_by(id: 6)`? 

Methods:

1. `find`

    1. What argument or arguments does the method take?
    - `find(id_number)`

    2. What type of object does the method return?
    - an array of class instances

    3. What happens if none of the parameters match? (i.e. what if `Tweet.find(5)` can't find that tweet? How about `Tweet.find_by(id: 6)`? 
    - The find method will raise an `ActiveRecord::RecordNotFound` exception unless a matching record is found for all of the supplied primary keys.


2. `.find_by`
    1. What argument or arguments does the method take?
    - first column name and corresponding entry in the column

    2. What type of object does the method return?
    - a class instances

    3. What happens if none of the parameters match? (i.e. what if `Tweet.find(5)` can't find that tweet? How about `Tweet.find_by(id: 6)`? 
    - return nil
    - The `find_by!` method behaves exactly like `find_by`, except that it will raise ActiveRecord::RecordNotFound if no matching record is found. For example: `find_by!(id: 6)` will return `ActiveRecord::RecordNotFound` if `tweets.id = 6` does not exist.


3. `.where`

    1. What argument or arguments does the method take?
    - follow SQL query syntax
    - Client.where("orders_count = ?", params[:orders])

    2. What type of object does the method return?
    - class instances

    3. What happens if none of the parameters match? (i.e. what if `Tweet.find(5)` can't find that tweet? How about `Tweet.find_by(id: 6)`? 
    - return nil

4. `.all`
    1. What argument or arguments does the method take?
    - no argument

    2. What type of object does the method return?
    - an array of all class instances

5. `.first`
    1. What argument or arguments does the method take?
    - The first method finds the first record ordered by primary key (default).
    - no argument, or an integer[key id 3]

    2. What type of object does the method return?
    - first instance, if no argument
    - array of first integer[3] class instances

    3. What happens if none of the parameters match? 
    - The `first` method returns nil if no matching record is found and no exception will be raised.
    - The `first!` method behaves exactly like first, except that it will raise ActiveRecord::RecordNotFound if no matching record is found.

6. `.destroy`
    1. What argument or arguments does the method take?
    - integer(s) that equals an id or several ids in the table

    2. What type of object does the method return?
    - nil

    3. What happens if none of the parameters match? 
    -  probably return nil. 


## Part Two - Name that SQL! 

Pretend that you have a `tweets` table with two columns - `message` and `user_id`. Given the code below, write in a notebook or on a whiteboard what SQL statements will fire when the following methods are called? 

```ruby
class Tweet < ActiveRecord::Base

end
``` 

1. `Tweet.all` 
```sql
SELECT * FROM tweets
```

2. `Tweet.find(5)`
```sql
SELECT * FROM tweets WHERE tweets.id = 5 LIMIT 1
```

3. `Tweet.find_by(user_id: 7)`
```sql
SELECT * FROM clients WHERE (tweets.user_id = 7) LIMIT 1
```

4. `Tweet.where(user_id: 7)` 
```sql
SELECT * FROM clients WHERE (tweets.user_id = 7) LIMIT 1
```

5. `Tweet.create(user_id: 5, message: 'making some coffee')`
```sql
INSERT INTO tweets (user_id, message) VALUES (5, 'making some coffee')
```

6. `Tweet.destroy(7)` 
```sql
DELETE FROM tweets WHERE tweets.id = 7 
```