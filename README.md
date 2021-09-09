# Mongodb Tutorial


## aggregation
Mongodb aggregation are doing most same job as mongoose-quary-builder

Aggregation Pipelining can execute an operation on some input and use
this output as the input for the next command and so on.

There have some keywords same as mongoose-quary-builder too.

#### Keywords

<mark>$project</mark> - Show some specific fields (same .select("id user")).

<mark>$match</mark> - Match fields with some conditions.

<mark>$group</mark> - Grouping the fields to perform aggregation.
         This can make new fields like mongodb fields with
         fields-value-group and return to next operation.

<mark>$sort</mark> - Performing the sorting(same as .sort({'id'})).   

<mark>$limit</mark> - Limit the documents to display( same as .limit(10)).

#### syntax

db.employee.aggregation([{},{} ....]);

you can add your aggregation in the array.

#### example

db.employee.find()   
{"_id":1, "name":"Joy", "city": "London", "age":20, "salary":23000}
{"_id":2, "name":"Jhon", "city": "Delhi", "age":22, "salary":25000}
{"_id":3, "name":"Anupam", "city": "Delhi", "age":12, "salary":32000}
{"_id":4, "name":"Gaurav", "city": "Mumbai", "age":20, "salary":25000}
{"_id":5, "name":"Barun", "city": "Kolkata", "age":23, "salary":16000}
{"_id":6, "name":"Vivek", "city": "Mumbai", "age":20, "salary":27000}
{"_id":7, "name":"Shubhan", "city": "Kolkata", "age":22, "salary":18000}


example 001
```javascript
db.employee.aggregation([
                          {$group:{_id:"$city"}},
                          {$sort:{_id:-1}}
                        ]);
```

result  
{"_id":"Mumbai"}   
{"_id":"Landon"}   
{"_id":"Kolkata"}   
{"_id":"Delhi"}   


example 002
```javascript
db.employee.aggregation([
                          {$match:{salary:{$gt:25000}}},
                          {$project:{_id:0, name:1, city:1}}
                        ]);
```

result   
{ name":"Anupam", "city": "Delhi"  }   
{ name":"Vivek",  "city": "Mumbai" }


example 002
```javascript
db.employee.aggregation([
                          {$sort:{salary:1}},
                          {$project:{_id:0, name:1, city:1}}
                        ]);
```

result
{"name":"Barun", "salary":16000}
{"name":"Shubhan", "salary":18000}
{"name":"Joy", "salary":23000}
{"name":"Jhon", "salary":25000}
{"name":"Gaurav", "salary":25000}
{"name":"Vivek", "salary":27000}
{"name":"Anupam", "salary":32000}
