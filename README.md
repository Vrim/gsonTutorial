# Intro To GSON in Javafx
###### By Cameron Fairchild

Gson is a library provided by Google for the implementation of JSON in Java.

JSON stands for **J**ava**S**cript **O**bject **N**otation and is essentially just an easy way to represent objects in a text-format. This can be used to store objects of all types in text. Providing the user with easy editing and comprehension of different objects.

### Starting With Dependencies
Open the project that JSON functionality should be added to. Open any file in which you want to add it in and type the following:
`Gson gson;`
NetBeans should prompt you with an error. Click the option that says to `Search Dependency at Maven Repositories`. Click `add` and wait.

Go to your `module-info.java` file and edit it.
Add the following line just above the line with the word `opens`:
```
requires gson;
```
This will download the Gson library and add it to your `POM.xml` file for you.

### Import It
We can either use NetBeans' hints to import it or add the import `import com.google.gson.Gson;` and `import com.google.gson.GsonBuilder;` to the top of our file.


Go back to that `Gson gson;` line and click the error from NetBeans.

Select the option to `Add import for com.google.gson.Gson`

This will add an import line for Gson to your current file.

The line `Gson gson;` can now be safely deleted.

### Using It
Whether you are reading or writing to JSON, you need a `GsonBuilder` class.
Create an instance of this object wherever you intend to use it. 

```
Gson gson = new GsonBuilder().create();
```
This object will convert between JSON and Java Objects

### File Writing
To write, first pick your favourite Writer object. We'll use the FileWriter in this case.
```
// Where object.json is the file name, can also be *.txt
File file = new File("object.json"): 

// Object(s) that you will write
Object object;

// Try with the BufferedWriter
try (Writer writer = new FileWriter(file)) {
    // Make your GsonBuilder
    Gson gson = new GsonBuilder()                   
                    .create();
    // Write to your file
    // This converts it to JSON as a String and writes it to the file
    gson.toJson(object, writer);
}
```

### File Reading
To write, we again need the `GsonBuilder` class.
Taking from the example above, we swap the `Writer` for a `Reader` and instead of `gson.toJson()` we use `gson.fromJson()`
```
try (Reader reader = new FileReader(file)) {
    Gson gson = new GsonBuilder().create();
    
    
    // Gson needs the class of your object to read it
    gson.fromJson(reader, object.class);
}
```
### Setup Of Objects
Gson will only read or wrtie object attributes (variables) that are `private`
This means that any other attributes will not be read to or written from. 
### Annotations

Using the annotation `@Expose` we can control which attributes Gson will see. 
First, we need to import it. This can be done via NetBeans or by adding the import `import com.google.gson.annotations.Expose;`
to the top of the object in question.

Here is an example of an object using the annotation
```
import com.google.gson.annotations.Expose;

public class example {
    // This attribute will not be picked up by Gson
    private int ignoreMe;
    
    // This attribute will be picked up by Gson
    @Expose
    private int lookAtMe;
 }
 ```
 Now that the class is set-up, we need to specify whether to ignore the annotated attributes or only use the ones with annotations.
 ```
 // We just add one extra line
 // This will exclude attributes without the annotation
 Gson gson = new GsonBuilder()
                            .create()
                            .excludeFieldsWithoutExposeAnnotation();
 ```
 To exclude an attribute, we can also use the keyword `transient`
 For instance:
 ```
 private transient int ignoreMe;
 private int lookAtMe;
 ```
 
## Have Fun

Thanks for reading and have fun using JSON!
