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

* Difference between :append and +=? Not just the whitespace!!!
* Difference between packages and recipes? How many packages can one recipe produce?
* what is the task order in yocto? How do the task depend on one another? How to get a log with the task order of a recipe?

