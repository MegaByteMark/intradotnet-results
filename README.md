# IntraDotNet.Results

A standalone library for simple Result pattern implementation.

## Overview

The `Result` and `ValueResult` classes provide a functional approach to error handling, eliminating the need for exceptions in many scenarios. They represent operations that can either succeed with a value or fail with an error.

## `Result` Class

### Basic Usage

```csharp
// Success case
var successResult = Result.Success();

// Failure case
var failureResult = Result.Failure("Something went wrong");

// Check if operation succeeded
if (result.IsSuccess)
{
    Console.WriteLine(result.Value);
}
else
{
    Console.WriteLine(result.AggregateErrors);
}
```

### Properties

- `IsSuccess`: Boolean indicating if the operation succeeded
- `IsFailure`: Boolean indicating if the operation failed
- `AggregateErrors`: A line new delimited string of error messages (only populated when IsFailure is `true`)
- `Errors`: A collection of error messages (only populated when IsFailure is `true`)

## ValueResult<T> Class

### Basic Usage

```csharp
// Success case
var successResult = ValueResult<int>.Success(42);

// Failure case
var failureResult = ValueResult<int>.Failure("Invalid input");

// Implicit conversion from value
ValueResult<string> result = "Hello"; // Implicit failure
```

### Key Differences from `Result`

`Results` is intended to be used for results returned from functions that would otherwise be `void`. 
`ValueResult` is intended to be used where a return value is expected.

### Try-Parse Pattern

```csharp
public ValueResult<int> TryParseInt(string input)
{
    if (int.TryParse(input, out int result))
        return ValueResult<int>.Success(result);
    
    return ValueResult<int>.Failure($"'{input}' is not a valid integer");
}
```
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Guidelines

- Ensure any install or build dependencies are removed before the end of the layer when doing a build
- Update the README.md with details of changes to the interface
- Increase the version numbers and the README.md to the new version that this Pull Request would represent
- You may merge the Pull Request in once you have the sign-off of an other developer, or if you do not have permission to do that, you may request the reviewer to merge it for you