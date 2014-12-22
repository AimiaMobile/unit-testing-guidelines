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

## Test Design Guidelines and Benefits

The following guidelines will help you to design more testable code.

Ref: The Art of Unit Testing, Appendix A.2: Design goals for testability

Design guideline | Benefit(s)
--- | ---
Use interface-based designs | This allows you to use polymorphism to replace depedencies in the system with your own stubs or mocks
Avoid instantiating concrete classes inside methods with logic. Get instance of clases from helper methods, factories, Inversion of Control containers or other places, but don't directly create them. | This allows you to serve up your own fake instances of classes to methods that require them, instead of being tied down to working with an internal production instance of a class
Avoid direct calls to static methods. Prefer calls to instance methods that later call statics | This allows you to break calls to static methods by overriding instance methods. (You won't be able to override static methods.)
Avoid constructors and static constructors that do logic | Overriding constructors is difficult to implement. Keeping constructors simple will simplyfy the job of inheriting from a class in your tests.
Seperate singleton logic from singleton holder | If you have a singleton, have a way to replace its instance so you can inject a stub singleton or reset it



