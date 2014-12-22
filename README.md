# unit-testing-guidelines

Unit testing best practices

## Unit Testing Review Guidelines

Use the following checklist as things to consider when writing unit tests.

This is a mirror of:
The Art of Unit Testing - Unit Testing Review Guidelines (http://artofunittesting.com/unit-testing-review-guidelines/)

#### Readability

* Make sure setup and teardown methods are not abused. **It’s better to use factory methods** for readability.
* Make sure the test **tests one thing only**.
* Check for good and consistent **naming conventions**.
* Make sure that only **meaningful assert messages** are used, or none at all (meaningful test names are better).
* Make sure **asserts are separated from actions** (different lines).
* Make sure tests don’t use **magic strings and values as inputs**. use the simplest inputs possible to prove your point.
* Make sure there is consistency in location of tests. make it **easy to find related tests** for a method, or a class, or a project.

#### Maintainability

* Make sure tests are **isolated from each other and repeatable**.
* Make sure that testing private or protected methods is not the norm (**public is always better**).
* Make sure tests are not **over-specified**.
* Make sure that **state-based testing is preferred** over using interaction testing.
* Make sure **strict mocks are used as little as possible** (leads to over specification and fragile tests).
* Make sure there is no more than **one mock per test**.
* Make sure tests do not **mix mocks and regular asserts** in the same test (testing multiple things).
* Make sure that tests **'verify' mock calls only on the single mock** object in the test, and not on all the fake objects in the tests (the rest are stubs, this leads to over specification and fragile tests).
* Make sure the test verifies only on a **single call to a mock object**. Verifying multiple calls on a mock object is either over specification or testing multiple things.
* Make sure that only in very rare cases **a mock is also used as a stub** to return a value in the same test.

#### Trust

* Make sure the test does not contain **logic or dynamic values**.
* **Check coverage** by playing with values (booleans or consts).
* Make sure unit tests are **separated from integration tests**.
* Make sure tests don’t use things that keep changing in a unit test (like DateTime.Now ). **Use fixed values**.


