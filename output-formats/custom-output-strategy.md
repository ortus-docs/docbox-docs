# Custom Output

🛠️ In addition to the mainstream output formats, you can extend DocBox's `AbstractTemplateStrategy` component to generate your own custom-formatted documentation:

```javascript
component extends="docbox.strategy.AbstractTemplateStrategy" accessors="true"{
   /**
    * Generate JSON documentation
    *
    * @metadata All component metadata, sourced from DocBox.
    */
   component function run( required query metadata ){
      // generate custom documentation format from arguments.metadata
   }
}
```
