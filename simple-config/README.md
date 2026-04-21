Simple to use, single file, global configuration lib for Fabric mods.

```Java
public class NAME {
    private static NAME instance;

    public final boolean example_1;
    public final int example_2;
    public final float example_3;
    public final double example_4;
    public final String example_5;
    
    private NAME() {
        // Or use SimpleConfig CONFIG = SimpleConfig.of("folder_name", "config_name")
        // Load config 'config_name.properties', if it isn't present create one 
        // using the lambda specified as the provider.
        SimpleConfig config = SimpleConfig.of("config_name")
                .provider(this::NAME)
                .version(1) // version (int) if outdated (<), config will be updated
                .request();
        example_1 = config.getOrDefault("example_1", false);
        example_2 = config.getOrDefault("example_2", 100);
        example_3 = config.getOrDefault("example_3", 0.1);
        example_4 = config.getOrDefault("example_4", 0.001);
        example_5 = config.getOrDefault("example_5", "Hello");
    }

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

    public static NAME get() {
        if (instance == null) {
            instance = new NAME();
        }
        return instance;
    }

    // You can also use this for reload
    public static void reload() {
        instance = new NAME();
    }

    // And this for dynamic config save (Mod Menu + Cloth Config)
    public static void save(Map<String, Object> changes) {
        Path path = FabricLoader.getInstance().getConfigDir()
                .resolve("Folder_Path").resolve("file_name.properties");
        SimpleConfig.writer(path, changes);
    }
}
```
The config consists of key-value pairs separated with `=`, if `#` is used as the first char in line, that line will be considered a comment.
If you have any more questions see JavaDoc comments in the source code.
