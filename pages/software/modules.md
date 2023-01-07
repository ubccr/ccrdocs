# Useful Module Commands

The `module` command has a variety of subcommands, outlined in the table below.
You may shorten the command to `ml`, but the shortened command may require
specialized syntax.

| Command                 | Description                         |
| ----------------------- | ----------------------------------- |
| `module avail`          | List available software.            |
| `module spider <module>`| Searches for a particular software. |
| `module load <module>`  | Load a module to use the software.  |
| `module unload <module>`| Remove or unload a module           |
| `module purge`          | Remove all modules.                 |
| `module save <name>`    | Save the state of all loaded module |
| `module restore <name>` | Restore a state of saved modules.   |
| `module help`           | Find information about additional   |

For more information, refer to the [Lmod user guide](https://lmod.readthedocs.io/en/latest/010_user.html#user-s-tour-of-the-module-command)

## Loading modules automatically

!!! Danger "Do not load modules automatically"
    We advise against loading modules automatically in your `.bashrc`

Instead we recommend that you load modules only when required, for example in
your job scripts. To facilitate the repeated loading of a large number of
modules we recommend you use a [module collection](#module-collections).

## Module collections

Lmod allows you to create a collection of modules. To do so, first load the
desired modules. For example:

```
$ module load gcc openmpi
```

Then use the save sub-command to save this collection:

```
$ module save my_modules
```

The my_modules argument is a name you give the collection. Then in a later
session or in a job you can restore the collection with the command:

```
$ module restore my_modules
```

To list out all your module collections you can run:

```
$ module savelist
```

## Sticky modules

Several modules are loaded by default for you when you login. These are also
known as "sticky" modules and are maintained by CCR. You should not unload
these modules as they provide a standard set of configurations for CCR's
software environment. 

For reference these include:

| Module         | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| CCRconfig      | environment variables for global scratch, local scratch and util |
| gentoo         | Sets up environment variables for CCR's compatability layer      |
| StdEnv         | CCR Standard Environment                                         |
