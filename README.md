# Unit Testing best practices

The following is a collection of conventions and best practices to help achieve effective and maintainable unit tests.

## F.I.R.S.T Properties of Unit Tests

At a high level, aim to achieve the following goals for your unit tests.

**F**ast: the faster your tests run, the more often you’ll run them

**I**solated: each unit test should have a single reason to fail

**R**epeatable: you should obtain the same results every time you run a test

**S**elf-Verifying: a good unit test fails or passes unambiguously

**T**imely: should you write tests before writing the production code or after it’s already built?

> [F.I.R.S.T](http://agileinaflash.blogspot.co.uk/2009/02/first.html)

## Unit Testing Review Guidelines

Use the following checklist as things to consider when writing unit tests.

This is a mirror of:

[The Art of Unit Testing - Unit Testing Review Guidelines](http://artofunittesting.com/unit-testing-review-guidelines/)

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

> The Art of Unit Testing, Appendix A.2: Design goals for testability

Design guideline | Benefit(s)
--- | ---
Use interface-based designs | This allows you to use polymorphism to replace depedencies in the system with your own stubs or mocks
Avoid instantiating concrete classes inside methods with logic. Get instance of clases from helper methods, factories, Inversion of Control containers or other places, but don't directly create them. | This allows you to serve up your own fake instances of classes to methods that require them, instead of being tied down to working with an internal production instance of a class
Avoid direct calls to static methods. Prefer calls to instance methods that later call statics | This allows you to break calls to static methods by overriding instance methods. (You won't be able to override static methods.)
Avoid constructors and static constructors that do logic | Overriding constructors is difficult to implement. Keeping constructors simple will simplyfy the job of inheriting from a class in your tests.
Seperate singleton logic from singleton holder | If you have a singleton, have a way to replace its instance so you can inject a stub singleton or reset it

## Unit Test Naming Conventions

Observe the following conventions when naming your tests.

> The Art of Unit Testing, Table 2.2. Basic rules for placing and naming tests

Object to be tested | Object to create on the testing side
--- | ---
Project | Create a test project named **[ProjectUnderTest]Tests**
Class | For each class, create at least one class with the name **[Class-Name]Tests**
Method | For each method, create at least one test method with the following name: **[Method-Name]_[StateUnderTest]_[ExpectedBehaviour]**

Here are the three parts of the method name:
* **MethodName** - The name of the method you're testing
* **StateUnderTest** - The conditions used to produce the expected behaviour
* **ExpectedTestBehavior** - What you expect the tested method to do under the specified conditions

## Structuring Tests

A unit test usually comprises three main actions:
* Arrange objects, creating and setting them up as necessary
* Act on an object
* Assert that something is as expected

Here's a simple example (XCTest) that demonstrates all three:

```objc
- (void)testActivateOffer_newOffer_ActivatedOffer {
  // arrange
  Offer *offer = [OfferFactory getLatestNewOffer];
  
  // act
  [offer activate]
  
  // assert
  XCTAssert(offer.isActive, @"offer should be activated");
}
```

## Mocks vs Stubs

A mock object is a fake object in the system that decides wheter the unit test has passed or failed. It does so by verifying whether the object under test interacted as expected with the fake object. There's usually no more than one mock per test. Mocks are used for interaction testing. It will save the history of communication, which will be verified later.

A stub is a controllable replacement for an existing dependency (or collaborator) in the system. By using a stub, you can test your code without dealing with the dependency directly.
A stub differs from a mock in that a stub can never fail a test. The asserts the test uses are always against the class under test.

To put it another way, stubs use state verification whereas mocks use behaviour verification.

> [Mocks Aren't Stubs](http://martinfowler.com/articles/mocksArentStubs.html)

> The Art of Unit Testing, 4.1 State-based versus interaction testing


