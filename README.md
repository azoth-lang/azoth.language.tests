# Azoth Language Tests

These tests verify a compiler/implementation of the Azoth language. They are written so they do not
rely on the Azoth standard library or any other Azoth packages. They are truly a test of the
language only and not of any of the standard library or package ecosystem. However, the tests do
require a special test package to be provided by the test harness/platform. This is a minimal
package that must be implemented. It is intentionally kept small to make implementing a test harness
easy.

## Test Package

The test package consists of two type declarations in the global namespace, extensions to the simple
types for conversion to string, and any necessary implementation. The two types are a simplified
`string` struct and a `Test_Output` trait to in lieu of console output.

### Strings

The `string` struct provided by the test harness should be equivalent to the implementation below.
More methods will likely be necessary internally to support other functionality in the test package.

```azoth
published copy struct string
{
    public let bytes: const Raw_Array[byte];

    public new(.bytes) { }

    published implicit operator "_"(value: const Raw_Array[byte]) -> string
    {
        return new string(value);
    }
}
```

### Test Output

The `Test_Output` trait provided by the test package must match the declaration below. This is a
capability accepted by the main function.

```azoth
published trait Test_Output
{
    published fn write(mut self, value: string);

    published fn write_line(mut self, line: string);

    published fn write_line(mut self);
}
```

### Convert to String

The boolean, integer, and floating point types should all be extended with a `to_invariant_string()`
method converting them to a string in the invariant local.
