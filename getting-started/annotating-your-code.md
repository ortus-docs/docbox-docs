# Annotating Your Code

DocBox reads your CFCs and creates documentation according to your objects, inheritance, implementations, functions, arguments, comments and metadata.  We try to follow the [JavaDoc](https://www.oracle.com/java/technologies/javase/javadoc-tool.html) style of annotations even though it is not 100% compatible yet.

## DocBox Comments

DocBox comments may be placed above any CFC, property, function, or argument which we want to document.

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

## DocBox at the CFC Level

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

This is a simple component declaration where we define the hint for the component and add block tags like `@author` .  All attributes to the component will be documented for you as name-value pairs on the final output.

## DocBox at the Property Level

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

Properties also have comments and you can add `@` blocks as well. 

## DocBox at the Function Level

```java
/**
 * get Java FileInputStream for resource bundle
 *
 * @rbFilePath path + filename for resource, including locale + .properties
 *
 * @return java.io.FileInputStream
 * @throws ResourceBundle.InvalidBundlePath
 */
public function getResourceFileInputStream( required string rbFilePath ){
}
```

Functions can have a variety of block tags alongside the main description of the function.  Also notice that each argument can also be documented via the `@argName` block tag.

### Argument Annotations

Arguments can also have multiple annotations for documentation or semantic usage purposes.

```text
cBox at the Function Level
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
| `@doc_abstract` | Used on components to demarcate them as abstract components. Please note that you can also use the `abstract` attribute that ColdFusion 2016+ introduced.  |
| `@doc_generic` | This is an annotation that can be placed on either a function or argument declaration. This annotation is used to specify what generic type is being used, which is particularly useful when a return or argument type is an `array` or a `struct` or `any`.  The value can be a single type or a list. |

```java
/**
 * @doc_abstract true
 */
component doc_abstract="true" { ... }
component doc_abstract { ... }


/**
 * Get foo array
 * 
 * @doc_generic com.Foo
 */
private array function getFooArray(){
  return variables.foo;
}

// Inline
private array function getFooArray() doc_generic="com.Foo"{
  return variables.foo;
}

/**
 * Set my struct
 *
 * @myStruct.doc_generic uuid,string
 */
private void function setMyStruct( required struct myStruct ){
  instance.myStruct = arguments.myStruct;
}

// Inline
private void function setMyStruct( 
  required struct myStruct doc_generic="uuid,string" 
){
  instance.myStruct = arguments.myStruct;
}
```

## Examples

All of the ortus repos have all their CFC documented.  Please check out some of them here:

* [https://github.com/Ortus-Solutions/DocBox](https://github.com/Ortus-Solutions/DocBox)
* [https://github.com/coldbox/coldbox-platform](https://github.com/coldbox/coldbox-platform)
* [https://github.com/Ortus-Solutions/commandbox](https://github.com/Ortus-Solutions/commandbox)
* [https://github.com/Ortus-Solutions/ContentBox](https://github.com/Ortus-Solutions/ContentBox)



