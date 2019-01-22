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
Next, you need to decide whether you are writing or reading from/to a file.

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
    // This converts it to a Json string and writes it to the file
    gson.toJson(object, writer);
}
```
