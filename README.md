# static-page-object-pattern
Usimg static pages to access any page object from anywhere with state built in at the element level. 

# Introduction 

The static page object pattern is designed around the concept that all page objects are accessible at any time and all browser interaction such as selenium-webdriver is separated out to the underlying architecture. 

# Architecture in brief

Page.Object.Methods

For instance if your page is Student and you were attempting to set the object Name to The value Jane. Your result would be (dependent on Language setters)

Student.Name.value = “Jane”

The methods on the objects are dependent on the DSL of the application and in some cases the language. For instance using Java getters and setters would follow the getName or setName conventions. 

Student.Name.setText(“Jane”)

# Page construction 

The Pages classes should only be made up of static objects. The pattern is designed to only contain the information required to facility the instruction needed at the element level to identify the object. 

In the Student page example Name would be. 

Class Student
 
private static TextInput Name =  new TextInput(“#Name”)

The Student class would only contain these static type objects, which forms the basis of the static-page-object-pattern. 

# Element construction 

The TextInput element described takes a single parameter, in this example this might be a css selector. The construction of an element object must be provided with enough details to  be correctly identified on the page. In the example more information maybe required or further information is required then the Element should be flexible enough to be adaptable. 

For example if the object on occasions required XPath over css then its advised to pass this into the object instead of having multiple objects for various conditions. 

new eTextInput(XPATH, “//Name”)

Elements may also be designed around further details required, such as readonly, protected. The pattern is designed, so that at run time the object contains all the methods appropriate for browser interaction. 

# Advanced Elements

Sometimes elements are more complex than simple get and set types, such as tables or bespoke objects designed for a particular application. The pattern should still be followed that any object which requires interaction should be described in the element form. 

In some of the examples provided in the project code. Tables for instance can designed around Column / Cell or x,y locators. 

Page.Table.ColumnName.methods.cellMethods

If we had a list of students in table then we might have. 

Students.StudentTable.Lastname.findRow(“Smith”).click()

Students.StudentTable.Lastname.findRow(“Smith”).row() this function could return the row Id to be used elsewhere. 

# Element Types

The following list highlights the standard types of elements must frequently found on a page. In the sample docs there are examples of the main types. 

TextField
RadioSelect
OptionSelect
DateField
Button
Link

Occasions where elements such as spans or data inside a p element can be referred to as readonly elements. 

E.g TextElement

The pattern here should be setters are not permitted.

private static TextElement NameField = new TextField(“#name > H1”)

# Element Methods

The methods, which appear on elements should allow simple getter and setter styles actions. 

In the examples given the basic elements described above have the methods defined. Take for example button or link these should have a simple click(). 

# Base Element

Each element should at least inherit a base class, which contains the majority of the underlying code to interact with the browser. 

There are occasions where inheritance makes sense where elements have similarities.

# Browser Interaction & State

I’m calling super from the Element the base class should be aware of the element under action. This also means that interaction or the ready state of the object should take place at this stage. 

Since the pattern is designed around object interaction and not waiting for page ready state then the base class should handle calls such as Ajax. 

# Real time passing data to elements 

Occasions where data is required to be passed into an object such as an iterator should be passed in via a method on the element object. 
