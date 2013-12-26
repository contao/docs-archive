class Config
------------

Provide methods to manage configuration files.

### Description ###

**Definition:** `class Config`

**Located in:** *system/libraries/Config.php*

**Class hierarchy:** *Config*



### Methods ###

- *public* [`getInstance`](Config/getInstance.md) – Return the current object instance (Singleton)
- *public* [`save`](Config/save.md) – Save the local configuration file
- *public* [`isComplete`](Config/isComplete.md) – Return true if the installation is completed
- *public* [`getActiveModules`](Config/getActiveModules.md) – Return all active modules (starting with "backend" and "frontend") as array
- *public* [`add`](Config/add.md) – Add a configuration variable to the local configuration file
- *public* [`update`](Config/update.md) – Alias for Config::add()
- *public* [`delete`](Config/delete.md) – Delete a configuration variable from the local configuration file
