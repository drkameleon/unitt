<h1 align="center">
    Unitt
</h1>

<p align="center">
    <i>Unitt</i> is a basic unit-test tool for the 
    <a href="https://github.com/arturo-lang/arturo/">
        Arturo Programming language
    </a>
    <br><br>
    <img 
        alt="Arturo logo" 
        width="20" 
        src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo.png#gh-light-mode-only"
    />
    <img 
        alt="Arturo logo" 
        width="20" 
        src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo-lightgray.png#gh-dark-mode-only" 
    />
</p>

## At a Glance

<p align="center">
<img 
    alt="Running Unitt from terminal"
    width="720"
    src="./docs/running unitt screenshot.png"
/>
</p>

## Trying Unitt

*Unitt* may be splited into two sections: *the tester* and *the tests*.

*The tester* is the section responsible to find, run and return error codes to the final user.
While *the tests* are responsible to group the rules and logic of the tests.

### Initial setup

It's recomended that your *runner* be at the root of your directory, right before your *tests* folder.

All of your *tests* must begin with the `test` prefix and end with the `.art` extension to be found,
since you may want to mix them with some other files.

Being that said, that is the right way of setting up your *tester*:

Let's consider that you have the following directory:

```
src/
    ...
tests/
    ...
main.art
tester.art
```

Into your `tester.art`, you must:

```art
import {unitt}

do ::
    runTests "tests"
```

To run it, call:

```
arturo tester.art
```

> [!TIP] 
> You may want to use a hashbang to don't need to call arturo for every run.

### The *tests* itself

A real example of tests:

```art
test "appending binaries with integer is working" [
    b: to :binary 0
    assert -> as.binary 2 = append b 1
    assert -> as.binary 1 = b ++ 1
]

test.prop "appending binaries with integer returns a binary" [
    b: to :binary 0
    assert -> binary? append b 1
    assert -> binary? b ++ 1
]
```

This will show you:

```
❌ - assert that appending binaries with integer is working
     assertion : [as binary 1 = append b 1]

✅ - assert that appending binaries with integer is working
     assertion : [as binary 1 = b ++ 1]

✅ ~ assert that appending binaries with integer returns a binary
     assertion : [binary? append b 1]

✅ - assert that appending binaries with integer returns a binary
     assertion : [binary? b ++ 1]
```

> [!NOTE]
> Property-based tests have `~` as separator. 


## Documentation

### *Runner*
- `runTests: $[folder :string]`:
    The *runner function*, this function will look for *tests* inside the relative `folder`.
    Remember that all *tests* must begin with the `test` prefix, and be an `.art` extension. 

### *Tests*
- `test: $[description :string, testCase :block]`:
    The test case itself, you need to pass a clear description to it,
    And the logic that you're trying to assert.
    - `.prop`:
        Indicates that a test is property-based.
- `assert: $[condition :block]`:
    A function that is only available inside the `test` case,
    makes an assertion given the `condition`.

---

> Background photo on ["At a Glance"](#at-a-glance) 
  by [Jack Anstey](https://unsplash.com/@jack_anstey?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [Unsplash](https://unsplash.com/photos/aerial-photography-of-road-zS4lUqLEiNA?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)