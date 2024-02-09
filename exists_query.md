# Exists Query 

Exists Query in Elasticsearch is used to find documents where a specified field is present with any non-null value. 

## Documents Are Returned When:

  **Non-Null Values:**  The field has any non-null value, such as 
  * Text   ***`"how are you?`"***
  * Numbers   ***`100, 20.5`***
  * Empty strings   ***`name: ""`***
  * Non Empty Objects   ***`{"age":20,"hair_color":"brown"}`***
  * Non Empty Array   ***`["swimming","driving","skating"]`***
  * Arrays containing  `null`  and another value, such as  ***`[null, "foo"]`***


    
## Documents Are Not Returned When:

 1. **Null Values or Absent Fields:** The field is null or absent from the document, treated as non-existing by Elasticsearch. ***`age: null`***
  2. **Fields with Null Values in Arrays:** Even if the field contains non empty Array and only has null value or null values in the Array are treated as non Existing by Elasticsearch ***`[null] or [null, null, null]`***
 3. **Fields with Empty Array or Object:**  
	 * Empty Array ***`[]`***
	 * Empty Object  ***`{}`**.

**Query To Return Not Null Documents**
     
     GET users/_search
     {"query":{"exists":{"field":"hobbies"}}}

**Query To Return Documents with Null Values**
     
    GET users/_search
    {"query":{"bool":{"must_not":{"exists":{"field":"travelled_countries"}}}}}
