# Yarn / NPM #

## Yarn vs. Npm ##

To avoid package version mis-matches, an exact installed version is pinned down in a yarn.lock file. Every time a module is added, Yarn creates (or updates) a yarn.lock file. This way you can guarantee another machine installs the exact same package, while still having a range of allowed versions defined in package.json.

### In conclusion; ###

Npm can have have different versions from the same package.json can be installed which creates inconsistencies.

    yarn global

Unlike npm, where global operations are performed using the -g or --global flag, Yarn commands need to be prefixed with global. Just like npm, project-specific dependencies shouldn’t need to be installed globally.

The global prefix only works for yarn add, yarn bin, yarn ls and yarn remove. With the exception of yarn add, these commands are identical to their npm equivalent.

    yarn install

The npm install command will install dependencies from the package.json file and allows you to add new packages. yarn install only installs the dependencies listed in yarn.lock or package.json, in that order.

    yarn add [–dev]

Similar to npm install <package>, yarn add <package> allows you to add and install a dependency. As the name of the command implies, it adds a dependency, meaning it automatically saves a reference to the package in the package.json file, just as npm’s --save flag does. Yarn’s --dev flag adds the package as a developer dependency, like npm’s --save-dev flag.

    yarn licenses [ls|generate-disclaimer]

At the time of writing, no npm equivalent is available. yarn licenses ls lists the licenses of all installed packages. yarn licenses generate-disclaimer generates a disclaimer containing the contents of all licenses of all packages. Some licenses state that you must include the project’s license in your project, making this a rather useful tool to do that.

    yarn why

This command peeks into the dependency graph and figures out why given package is installed in your project. Perhaps you explicitly added it, perhaps it’s a dependency of a package you installed. yarn why helps you figure that out.

    yarn upgrade [package]

This command upgrades packages to the latest version conforming to the version rules set in package.json and recreates yarn.lock. This is similar to npm update.

Interestingly, when specifying a package, it updates that package to latest release and updates the tag defined in package.json. This means this command might update packages to a new major release.

    yarn generate-lock-entry

The yarn generate-lock-entry command generates a yarn.lock file based on the dependencies set in package.json. This is similar to npm shrinkwrap. This command should be used with caution, as the lock file is generated and updated automatically when adding and upgrading dependencies via yarn add and yarn upgrade.
