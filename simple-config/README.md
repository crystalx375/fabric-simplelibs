Simple to use, single file, gloabal configuration lib for Fabric mods.

```Java
  // Load config 'config.properties', if it isn't present create one 
  // using the lambda specified as the provider.

  // Or use SimpleConfig CONFIG = SimpleConfig.of("folder_name", "config_name")
  SimpleConfig CONFIG = SimpleConfig.of("config_name")
          .provider(this::defaultConfig)
          .version(1) // version (int) if outdated (>), config will be updated
          .request();

  // Custom config provider, returnes the default config content
  // if the custom provider is not specified SimpleConfig will create an empty file instead
  private String defaultConfig(String filename) {
    return """
            # Comment
            example_1 = false
            example_2 = 100
            example_3 = 0.1
            example_4 = Hello
            """;
  }

  // And that's it! Now you can request values from the config:
  private String SOME_BOOL = CONFIG.getOrDefault("example_1", false);
  private int SOME_INTEGER = CONFIG.getOrDefault("example_2", 100);
  private bool SOME_FLOAT = CONFIG.getOrDefault("example_3", 0.1);
  private bool SOME_STRING = CONFIG.getOrDefault("example_4", "Hello");
```
The config consists of key-value pairs separated with `=`, if `#` is used as the first char in line, that line will be considered a comment.
If you have any more questions see JavaDoc comments in the source code.
