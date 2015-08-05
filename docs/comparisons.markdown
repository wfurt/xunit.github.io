---
layout: default
title: Comparing xUnit.net to other frameworks
breadcrumb: Documentation
---

# Comparing xUnit.net to other frameworks

## Table of Contents
* [Attributes](#attributes)
* [Assertions](#assertions)

## Attributes

*Note: This table was written back when xUnit.net 1.0 has shipped, and needs to be updated with information regarding the latest versions of the unit testing frameworks.*

{: .table .smaller }
| NUnit 2.2               | MSTest 2005           | xUnit.net 2.x                         | Comments |
| :---------------------- | :-------------------- | :------------------------------------ | :------- |
| `[Test]`                | `[TestMethod]`        | `[Fact]`                              | Marks a test method. |
| `[TestFixture]`         | `[TestClass]`         | *n/a*                                 | xUnit.net does not require an attribute for a test class; it looks for all test methods in all public (exported) classes in the assembly.
| `[ExpectedException]`   | `[ExpectedException]` | `Assert.Throws`<br>`Record.Exception` | xUnit.net has done away with the ExpectedException attribute in favor of `Assert.Throws`. See [Note 1](#note1) |
| `[SetUp]`               | `[TestInitialize]`    | Constructor                           | We believe that use of `[SetUp]` is generally bad. However, you can implement a parameterless constructor as a direct replacement. See [Note 2](#note2) |
| `[TearDown]`            | `[TestCleanup]`       | `IDisposable.Dispose`                 | We believe that use of `[TearDown]` is generally bad. However, you can implement `IDisposable.Dispose` as a direct replacement. See [Note 2](#note2) |
| `[TestFixtureSetUp]`    | `[ClassInitialize]`   | `IClassFixture<T>`                    | To get per-class fixture setup, implement `IClassFixture<T>` on your test class. See [Note 3](#note3) |
| `[TestFixtureTearDown]` | `[ClassCleanup]`      | `IClassFixture<T>`                    | To get per-class fixture teardown, implement `IClassFixture<T>` on your test class. See [Note 3](#note3) |
| *n/a*                   | *n/a*                 | `ICollectionFixture<T>`               | To get per-collection fixture setup and teardown, implement `ICollectionFixture<T>` on your test collection. See [Note 3](#note3) |
| `[Ignore]`              | `[Ignore]`            | `[Fact(Skip="reason")]`               | Set the Skip parameter on the `[Fact]` attribute to temporarily skip a test. |
| `[Property]`            | `[TestProperty]`      | `[Trait]`                             | Set arbitrary metadata on a test |
| *n/a*                   | `[DataSource]`        | `[Theory]`<br>`[XxxData]`             | Theory (data-driven test). See [Note 4](#note4) |

## Attribute Notes

<a name="note1">**Note 1:**</a> Long-term use of `[ExpectedException]` has uncovered various problems with it. First, it doesn't specifically say which line of code should throw the exception, which allows subtle and difficult-to-track failures that show up as passing tests. Second, it doesn't offer the opportunity to fully inspect details of the exception itself, since the handling is outside the normal code flow of the test. `Assert.Throws` allows you to test a specific set of code for throwing an exception, and returns the exception during success so you can write further asserts against the exception instance itself.

<a name="note2">**Note 2:**</a> The xUnit.net team feels that per-test setup and teardown creates difficult-to-follow and debug testing code, often causing unnecessary code to run before every single test is run. For more information, see <http://jamesnewkirk.typepad.com/posts/2007/09/why-you-should-.html>.

<a name="note3">**Note 3:**</a> xUnit.net provides a new way to think about per-fixture data with the use of the `IClassFixture<T>` and `ICollectionFixture<T>` interfaces. The runner will create a single instance of the fixture data and pass it through to your constructor before running each test. All the tests share the same instance of fixture data. After all the tests have run, the runner will dispose of the fixture data, if it implements `IDisposable`. For more information, see [Shared Context](shared-context.html).

<a name="note4">**Note 4:**</a> xUnit.net ships with support for data-driven tests call Theories. Mark your test with the `[Theory]` attribute (instead of `[Fact]`), then decorate it with one or more `[XxxData]` attributes, including `[InlineData]` and `[MemberData]`. For more information, see [Getting Started](getting-started.html).

## Assertions

*Note: this table was written back when xUnit.net 1.0 has shipped, and needs to be updated with information regarding the latest versions of the unit testing frameworks.*

{: .table .smaller }
| NUnit 2.2             | MSTest 2005           | xUnit.net 1.x      | Comments |
| :-------------------- | :-------------------- | :----------------- | :------- |
| `AreEqual`            | `AreEqual`            | `Equal`            | MSTest and xUnit.net support generic versions of this method |
| `AreNotEqual`         | `AreNotEqual`         | `NotEqual`         | MSTest and xUnit.net support generic versions of this method |
| `AreNotSame`          | `AreNotSame`          | `NotSame`          | |
| `AreSame`             | `AreSame`             | `Same`             | |
| `Contains`            | `Contains`            | `Contains`         | |
| `DoAssert`            | *n/a*                 | *n/a*              | |
| *n/a*                 | `DoesNotContain`      | `DoesNotContain`   | |
| *n/a*                 | *n/a*                 | `DoesNotThrow`     | Ensures that the code does not throw any exceptions |
| `Fail`                | `Fail`                | *n/a*              | xUnit.net alternative: `Assert.True(false, "message")` |
| `Greater`             | *n/a*                 | *n/a*              | xUnit.net alternative: `Assert.True(x > y)` |
| `Ignore`              | `Inconclusive`        | *n/a*              | |
| *n/a*                 | *n/a*                 | `InRange`          | Ensures that a value is in a given inclusive range (note: NUnit and MSTest have limited support for `InRange` on their `AreEqual` methods) |
| `IsAssignableFrom`    | *n/a*                 | `IsAssignableFrom` | |
| `IsEmpty`             | *n/a*                 | `Empty`            | |
| `IsFalse`             | `IsFalse`             | `False`            | |
| `IsInstanceOfType`    | `IsInstanceOfType`    | `IsType`           | |
| `IsNaN`               | *n/a*                 | *n/a*              | xUnit.net alternative: `Assert.True(double.IsNaN(x))` |
| `IsNotAssignableFrom` | *n/a*                 | *n/a*              | xUnit.net alternative: `Assert.False(obj is Type)` |
| `IsNotEmpty`          | *n/a*                 | `NotEmpty`         | |
| `IsNotInstanceOfType` | `IsNotInstanceOfType` | `IsNotType`        | |
| `IsNotNull`           | `IsNotNull`           | `NotNull`          | |
| `IsNull`              | `IsNull`              | `Null`             | |
| `IsTrue`              | `IsTrue`              | `True`             | |
| `Less`                | *n/a*                 | *n/a*              | xUnit.net alternative: `Assert.True(x < y)` |
| *n/a*                 | *n/a*                 | `NotInRange`       | Ensures that a value is not in a given inclusive range |
| *n/a*                 | *n/a*                 | `Throws`           | Ensures that the code throws an exact exception |
