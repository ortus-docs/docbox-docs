---
description: Learn how to annotate your BoxLang or CFML code for DocBox documentation generation
icon: pencil
---

# Annotating Your Code

📝 DocBox reads your classes and creates documentation according to your objects, inheritance, implementations, functions, arguments, comments and metadata.  We try to follow the [JavaDoc](https://www.oracle.com/java/technologies/javase/javadoc-tool.html) style of annotations even though it is not 100% compatible yet.

## 💬 DocBox Comments

DocBox comments may be placed above any class declaration, property, function, or argument which we want to document.

```java
/**
 * This is a Javadoc compliant comment for DocBox
 */
```

These comments are commonly made up of two sections:

* The description of what we're commenting on
* The standalone block tags \(marked with the `@` symbol\) which describe specific meta-data
* Also all core engine attributes to components, properties, functions and arguments will be documented automatically for you.

For the full JavaDoc spec click here: [https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)

## 📚 Class Annotating

{% tabs %}

{% tab title="BoxLang" %}

Please note that BoxLang allows you to use both documentation annotation and code annotation styles.

```js
/**
* Hero is the main entity we'll be using to create awesome stuff
*
* @author Captain America
*/
@name( "SuperHero" )
@transient
class {
    // properties and functions
}
```

{% endtab %}

{% tab title="CFML" %}

```java
/**
* Hero is the main entity we'll be using to create awesome stuff
*
* @author Captain America
*
*/
component name="SuperHero" accessors="true" transient{
    // properties and functions
}
```

{% endtab %}

{% endtabs %}

This is a simple component declaration where we define the hint for the component and add block tags like `@author` .  All attributes to the component will be documented for you as name-value pairs on the final output.

## 🎯 Property Annotating

{% tabs %}

{% tab title="BoxLang" %}

```js
/**
* Hero is the main entity we'll be using to create awesome stuff
*
* @author Captain America
*
*/
@name( "SuperHero" )
@transient
class{

    /**
     * A collection of aliases this superhero is known as
     */
    property name="alias" type="array";

    /**
     * Internal alias name
     *
     * @deprecated true
     */
    @propertyCodeAnnotation
    @serialize( false )
    property name="_alias" type="array";
}
```

{% endtab %}

{% tab title="CFML" %}

```java
/**
* Hero is the main entity we'll be using to create awesome stuff
*
* @author Captain America
*
*/
component name="SuperHero" accessors="true" transient{

    /**
     * A collection of aliases this superhero is known as
     */
    property name="alias" type="array";

    /**
     * Internal alias name
     * @deprecated true
     */
    property name="_alias" type="array";
}
```

{% endtab %}

{% endtabs %}

Properties also have comments and you can add `@` blocks as well.

## Function Annotations

```java
/**
 * get Java FileInputStream for resource bundle
 *
 * @rbFilePath path + filename for resource, including locale + .properties
 *
 * @return java.io.FileInputStream
 *
 * @throws ResourceBundle.InvalidBundlePath
 */
public function getResourceFileInputStream( required string rbFilePath ){
}
```

Functions can have a variety of block tags alongside the main description of the function.  Also notice that each argument can also be documented via the `@argName` block tag.

### Argument Annotations

Arguments can also have multiple annotations for documentation or semantic usage purposes.

```text
/**
 * get Java FileInputStream for resource bundle
 *
 * @rbFilePath path + filename for resource, including locale + .properties
 * @rbFilePath.deprecated true
 *
 * @return java.io.FileInputStream
 * @throws ResourceBundle.InvalidBundlePath
 */
public function getResourceFileInputStream( required string rbFilePath ){
}
```

This is done by using a `.` period delimiter and then adding another block name or semantic name to use.

## Core Blocks

Here are some of the core blocks that can be used in DocBox:

| Tag | Explanation |
| :--- | :--- |
| `@author` | Provides information about the author, typically the  author’s name, e-mail address, website information, and so  on. |
| `@version` | Indicates the version number. |
| `@since` | Used to indicate the version with which this class, field, or  method was added. |
| `@return` | Provides a description of a method’s return value. |
| `@throws` | Indicates exceptions that are thrown by a method or  constructor. You can add multiple `@throws` in a function declaration. |
| `@deprecated` | Indicates that the class, field, or method is deprecated and  shouldn’t be used. |
| `@{anything}` | Anything you like. That's right, DocBox will document any block pairs for you in a simple output manner. |
| `@see` | _Not implemented yet_ |

### Custom DocBox Blocks

Here are some blocks that ONLY DocBox can read:

| Tag | Explanation |
| :--- | :--- |
| `@doc.type` | This is an annotation that can be placed on either a function or argument declaration. This annotation is used to specify what generic type is being used, which is particularly useful when a return or argument type is an `array` or a `struct` or `any`.  The value can be a single type or a list. |

```java
/**
 * Get foo array
 *
 * @doc.type com.Foo
 */
private array function getFooArray(){
  return variables.foo;
}

// Inline
private array function getFooArray() doc.type="com.Foo"{
  return variables.foo;
}

/**
 * Set my struct
 *
 * @myStruct.doc.type uuid,string
 */
private void function setMyStruct( required struct myStruct ){
  instance.myStruct = arguments.myStruct;
}

// Inline
private void function setMyStruct(
  required struct myStruct doc.type="uuid,string"
){
  instance.myStruct = arguments.myStruct;
}
```

## 🏷️ Custom Annotations

DocBox supports standard JavaDoc tags and recognizes custom annotations for enhanced documentation.

### @doc.type

The `@doc.type` annotation allows you to specify generic types for complex return types and arguments. This is especially useful for documenting collections and typed data structures.

**Syntax:**
```
@doc.type TypeName
@doc.type KeyType,ValueType
```

**Examples:**

#### Return Type Generics

Document arrays with specific element types:

```java
/**
 * Gets all active users from the database
 *
 * @return Array of User objects
 * @doc.type Array<User>
 */
public array function getActiveUsers() {
    return queryExecute( "SELECT * FROM users WHERE active = 1" )
        .map( function( row ) {
            return new User( row );
        } );
}
```

Document structs with key/value types:

```java
/**
 * Gets user preferences as a configuration map
 *
 * @return Struct mapping setting names to values
 * @doc.type Struct<String,Any>
 */
public struct function getUserPreferences() {
    return {
        "theme": "dark",
        "fontSize": 14,
        "autoSave": true
    };
}
```

#### Parameter Type Generics

Document typed parameters:

```java
/**
 * Processes a batch of user records
 *
 * @users Array of User objects to process
 * @users.doc.type Array<User>
 */
public void function processBatch( required array users ) {
    for ( var user in arguments.users ) {
        user.process();
    }
}
```

Document complex struct parameters:

```java
/**
 * Updates user settings with validation
 *
 * @settings Map of setting names to their values
 * @settings.doc.type Struct<String,Any>
 */
public void function updateSettings( required struct settings ) {
    validateSettings( arguments.settings );
    saveSettings( arguments.settings );
}
```

#### Inline Generic Annotations

BoxLang also supports inline `doc.type` attributes:

```java
// Return type with inline generic
public array function getUsers() doc.type="Array<User>" {
    return entityLoad( "User" );
}

// Parameter with inline generic
public void function setCache(
    required struct cache doc.type="String,Any"
) {
    variables.cache = arguments.cache;
}
```

#### Complex Generic Types

For nested or complex types:

```java
/**
 * Gets a map of user IDs to their roles
 *
 * @return Map of numeric user IDs to arrays of role names
 * @doc.type Struct<Numeric,Array<String>>
 */
public struct function getUserRoles() {
    return {
        1: [ "admin", "editor" ],
        2: [ "viewer" ],
        3: [ "editor", "contributor" ]
    };
}
```

### Best Practices for @doc.type

1. **Be Specific**: Use concrete types instead of generic "Any" when possible
2. **Consistency**: Use the same naming convention throughout your codebase
3. **Documentation**: Combine with `@return` or parameter hints for full context
4. **Complex Types**: Break down complex nested types into multiple lines for clarity

```java
/**
 * Gets a complex data structure for reporting
 *
 * @return Nested structure containing report data
 * - Outer struct: Department name -> Department data
 * - Department data: Struct with "users" (Array<User>) and "metrics" (Struct<String,Numeric>)
 * @doc.type Struct<String,Struct>
 */
```
