# Configuring DocBox

1. Create a `generateDocs.cfm` CFML script file which will contain the docbox configuration
2. Edit `generateDocs.cfm` and add CFML which will:
   1. Create a new instance of `docbox.DocBox`
   2. Choose an output format - `.addStrategy( "HTML" )`
   3. Pass strategy parameters - `addStrategy( "HTML", { outputDir : 'tmp/docs' } )`
   4. Run Docbox: `.generate()`

```js
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "CommandBox",
        outputDir : "#expandPath( './docs' )#
    } )
    .generate(
       source = expandPath( "/app" ),
       mapping = "app",
       excludes="(coldbox)"
    );
```

You can generate multiple formats simultaneously with the `.addStrategy()` method:

```js
new docbox.DocBox()
   .addStrategy( "HTML", {
      projectTitle="My Docs",
      outputDir="#expandPath( '/docs/html' )#"
   } )
   .addStrategy( "JSON", {
      projectTitle="My Docs",
      outputDir="#expandPath( '/docs/json' )#"
   } )
   .generate(
      source = expandPath( "/app" ),
      mapping = "app",
      excludes="(coldbox)"
   );
```