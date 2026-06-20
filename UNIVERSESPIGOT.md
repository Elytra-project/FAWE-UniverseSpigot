# UniverseSpigot build notes

This fork can compile the Bukkit plugin against a private UniverseSpigot API or
kernel jar without committing that jar or its local path.

Configure one of the following outside Git:

- `UNIVERSESPIGOT_API_JAR`
- `UNIVERSESPIGOT_KERNEL_JAR`
- `universeSpigotApiJar` in `local.properties` or a Gradle property

`local.properties` and `local-libs/` are ignored. Keep private jars there or in
another local-only location. Do not commit server jars, decompiled server code,
or machine-specific absolute paths.

Example:

```properties
universeSpigotApiJar=<path-to-private-universespigot-api-or-kernel-jar>
```

Build the Bukkit plugin with:

```powershell
.\gradlew.bat --no-daemon :worldedit-bukkit:shadowJar
```

The shutdown failure seen in runtime logs through `CraftScheduler.cancelTasks`
and anonymous `CraftScheduler` classes is a kernel scheduler compatibility
issue. This fork should not depend on CraftBukkit anonymous implementation
classes to work around it.
