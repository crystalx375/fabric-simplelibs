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
  private bool SOME_BOOL = CONFIG.getOrDefault("example_1", false);
  private int SOME_INTEGER = CONFIG.getOrDefault("example_2", 100);
  private float SOME_FLOAT = (float) CONFIG.getOrDefault("example_3", 0.1);
  private String SOME_STRING = CONFIG.getOrDefault("example_4", "Hello");
  // Or use this:
  private Config() {
    SOME_BOOL = CONFIG.getOrDefault("example_1", false);
    SOME_INTEGER = CONFIG.getOrDefault("example_2", 100);
    SOME_FLOAT = (float) CONFIG.getOrDefault("example_3", 0.1);
    SOME_STRING = CONFIG.getOrDefault("example_4", "Hello");
  }
  // And initialize it
  @Override
	public void onInitialize() {
    Config();
  }
```
The config consists of key-value pairs separated with `=`, if `#` is used as the first char in line, that line will be considered a comment.
If you have any more questions see JavaDoc comments in the source code.
