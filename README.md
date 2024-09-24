# swift-testing-cheat-sheet

The description and example code snippet is taken from Apple document.  
For more information, see the [Migrating a test from XCTest](https://developer.apple.com/documentation/testing/migratingfromxctest#Convert-setup-and-teardown-functions) article.

## What is Swift Testing?

- Define test functions almost anywhere with a single attribute.
- Group related tests into hierarchies using Swift’s type system.
- Integrate seamlessly with Swift concurrency.
- Parameterize test functions across wide ranges of inputs.
- Enable tests dynamically depending on runtime conditions.
- Parallelize tests in-process.
- Categorize tests using tags.
- Associate bugs directly with the tests that verify their fixes or reproduce their problems.

## XCTest vs Swift Testing

|Type|XCTest|Swift Testing||
|:-|:----|:----------|:---------:|
|Import|`import XCTest`| `import Testing`|[Example](#import)|
|Test suite|`class ExampleTests: XCTestCase`|`struct ExampleTests`|[Example](#test-suite)|
|Setup and teardown|`class ExampleTests: XCTestCase`|`struct ExampleTests`|[Example](#setup-and-teardown)|
|Test method|`@Test func example()`|`func testExample()` |[Example](#test-method)|

## [Import](https://developer.apple.com/documentation/testing/migratingfromxctest#Import-the-testing-library)

### XCTest

```swift
import XCTest
@testable import Example
```

### Swift Testing

```swift
import Testing
@testable import Example
```

## [Test suite](https://developer.apple.com/documentation/testing/migratingfromxctest#Convert-test-classes)

### XCTest

```swift
class ExampleTests: XCTestCase { ... }
```

### Swift Testing

```swift
struct ExampleTests { ... }
// or
final class ExampleTests { ... }
```

## [Setup and teardown](https://developer.apple.com/documentation/testing/migratingfromxctest#Convert-setup-and-teardown-functions)

### XCTest

```swift
class ExampleTests: XCTestCase {
  var foo: NSNumber!

  override func setUp() async throws {
    foo = 100
  }

  override func tearDown() {
    foo = 0 
  }
}
```

### Swift Testing

```swift
struct ExampleTests {
  var foo: NSNumber

  // setUp()
  init() async throws {
    foo = 100
  }

  // tearDown()
  deinit {
    foo = 0
  }
}

// class test suite
final class ExampleTests {
  var foo: NSNumber

  // setUp()
  init() async throws {
    foo = 100
  }

  // tearDown()
  deinit {
    foo = 0
  }
}
```

## [Test method](https://developer.apple.com/documentation/testing/migratingfromxctest#Convert-test-methods)

### XCTest

```swift
class ExampleTests: XCTestCase {
  func testExample1() { ... }
  func testExample2() async { ... }
  func testExample3() throws { ... }
  func testExample4() async throws { ... }
}
```

### Swift Testing

```swift
struct ExampleTests {
  @Test func example1() { ... }
  @Test func example2() async { ... }
  @Test func example3() throws { ... }
  @Test func example4() async throws { ... }
}
```
