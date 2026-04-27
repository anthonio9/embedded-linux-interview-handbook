## Yocto

* What is an override? How does it propagate, where can it be used?
  
  Good explanation of the **override** mechanism is available [here at stackoverflow](https://stackoverflow.com/q/50225540/11287083)
  
  BitBake provides a very easy-to-use way to write conditional metadata. It is done by a mechanism called overrides.

  The OVERRIDES variable contains values separated by colons (:), and each value is an item we want to satisfy conditions. So, if we have a variable that is conditional on arm, and arm is in OVERRIDES, then the version of the variable that is specific to arm is used rather than the non-conditional version, as shown:

  ```sh
  OVERRIDES = "architecture:os:machine"
  TEST = "defaultvalue"
  TEST:os = "osspecificvalue"
  TEST:other = "othercondvalue"
  ```
  In this example, TEST will be osspecificvalue due to the condition of os being in OVERRIDES.
  More about OVERRIDES can be found in the bitbake documentation [3.3 Conditional Syntax (Overrides)](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#conditional-syntax-overrides)

  But that is not all of it, let's dig deeper!

  `OVERRIDES`, as previously mentioned is a colon `:` separated list of strings. It's build with [the instruction](https://git.yoctoproject.org/poky/plain/meta/conf/bitbake.conf) below:

  ```sh
  OVERRIDES = "${TARGET_OS}:${TRANSLATED_TARGET_ARCH}:pn-${PN}:layer-${FILE_LAYERNAME}:${MACHINEOVERRIDES}:${DISTROOVERRIDES}:${CLASSOVERRIDE}${LIBCOVERRIDE}:forcevariable"
  ```

  Each of the string (or list of strings) variables is filled in a different _*.conf_ / _*.bbclass_ file, however the most important for now are `MACHINEOVERRIDES` and `DISTROOVERRIDES`. Those are set in custom machine and distro _*.conf_ files, respectively. The _*.conf_ files are processed first, the variables defined in them are available to all the recipes in a manner similar to the _glboal_ variables, known from languages like C++.

  There is no `IMAGEOVERRIDES` and it is not possible to adjust the `OVERRIDES` list from a recipe in way that would make the changes visible to the other recipes. Each recipe has its own local environment copy, not accessible from outside. However, if really needed `OVERRIDES` list can be altered manually from a recipe, only for its own needs.

* Difference between :append and +=? Not just the whitespace!!!
* Difference between packages and recipes? How many packages can one recipe produce?
* what is the task order in yocto? How do the task depend on one another? How to get a log with the task order of a recipe?

  The task order usually follows the standard pipeline, which consists of tasks as below:
  
  do_fetch → do_unpack → do_patch → do_prepare_recipe_sysroot → do_configure → do_compile → do_install → do_package → do_package_write_* → do_rootfs
  
  + do_fetch — downloads source (tarballs, git repos, etc.)
  + do_unpack — extracts sources into the working directory
  + do_patch — applies patches listed in SRC_URI
  + do_prepare_recipe_sysroot — populates the sysroot with dependencies so configure/compile can find them
  + do_configure — runs configuration (autoconf, cmake, meson, etc.)
  + do_compile — builds the software
  + do_install — installs files into ${D} (a staging area)
  + do_package — splits installed files into packages (${PN}, ${PN}-dev, ${PN}-dbg, etc.)
  + do_package_write_rpm/deb/ipk — writes the actual package files
  + do_rootfs — assembles packages into a root filesystem (only in image recipes)

  To list the task order use `listtasks` command:
  ```bitbake -c listtasks <recipe>``` - prints all tasks for a recipe along with their descriptions. It doesn't show the dependency graph directly, but lists everything available.

