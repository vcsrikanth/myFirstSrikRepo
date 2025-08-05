# Function Documentation Template

This template provides a standardized format for documenting functions across different programming languages. Use this template to ensure consistent and comprehensive function documentation.

## Template Structure

```markdown
# FunctionName

Brief description of what the function does and its purpose.

## Syntax

```language
functionName(parameter1, parameter2, ...parameterN)
```

## Parameters

- `parameter1` (type) - Description of the first parameter
- `parameter2` (type, optional) - Description of optional parameter with default value
- `...parameterN` (type) - Description of additional parameters

## Return Value

- **Type**: Description of return type
- **Description**: What the function returns and under what conditions

## Exceptions/Errors

- `ErrorType1`: When this error occurs and why
- `ErrorType2`: Another possible error condition

## Examples

### Basic Usage
```language
// Example code here
```

### Advanced Usage
```language
// More complex example
```

## Notes

- Additional information about the function
- Performance considerations
- Browser/environment compatibility
- Related functions or alternatives

## See Also

- [RelatedFunction1](#) - Brief description
- [RelatedFunction2](#) - Brief description
```

## Language-Specific Examples

### JavaScript/TypeScript Functions

```markdown
# debounce

Creates a debounced function that delays invoking the provided function until after `wait` milliseconds have elapsed since the last time the debounced function was invoked.

## Syntax

```typescript
debounce<T extends (...args: any[]) => any>(
  func: T,
  wait: number,
  immediate?: boolean
): (...args: Parameters<T>) => void
```

## Parameters

- `func` (Function) - The function to debounce
- `wait` (number) - The number of milliseconds to delay
- `immediate` (boolean, optional) - If true, trigger the function on the leading edge instead of trailing

## Return Value

- **Type**: Function
- **Description**: Returns the new debounced function

## Examples

### Basic Usage
```javascript
const debouncedSave = debounce(saveData, 300);
debouncedSave(); // Will only execute after 300ms of no calls
```

### With Immediate Execution
```javascript
const debouncedSubmit = debounce(submitForm, 1000, true);
debouncedSubmit(); // Executes immediately, then waits 1000ms
```

### In React Component
```jsx
const SearchComponent = () => {
  const [query, setQuery] = useState('');
  
  const debouncedSearch = useMemo(
    () => debounce((searchTerm) => {
      // Perform search
      console.log('Searching for:', searchTerm);
    }, 500),
    []
  );
  
  useEffect(() => {
    if (query) {
      debouncedSearch(query);
    }
  }, [query, debouncedSearch]);
  
  return (
    <input
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search..."
    />
  );
};
```

## Notes

- Useful for limiting the rate of function execution
- Commonly used for search inputs, resize handlers, and API calls
- The debounced function can be cancelled using the `cancel` method if implemented

## See Also

- [throttle](#throttle) - Limits function execution to once per specified interval
- [useDebouncedValue](#useDebouncedValue) - React hook for debounced values
```

### Python Functions

```markdown
# calculate_fibonacci

Calculates the nth Fibonacci number using dynamic programming for optimal performance.

## Syntax

```python
def calculate_fibonacci(n: int, memo: Dict[int, int] = None) -> int
```

## Parameters

- `n` (int) - The position in the Fibonacci sequence (must be >= 0)
- `memo` (Dict[int, int], optional) - Memoization dictionary for caching results

## Return Value

- **Type**: int
- **Description**: The nth Fibonacci number

## Exceptions

- `ValueError`: Raised when n is negative
- `TypeError`: Raised when n is not an integer

## Examples

### Basic Usage
```python
result = calculate_fibonacci(10)
print(result)  # Output: 55
```

### With Custom Memoization
```python
memo_cache = {}
result1 = calculate_fibonacci(50, memo_cache)
result2 = calculate_fibonacci(51, memo_cache)  # Uses cached values
```

### Error Handling
```python
try:
    result = calculate_fibonacci(-1)
except ValueError as e:
    print(f"Error: {e}")  # Error: n must be non-negative
```

## Performance

- **Time Complexity**: O(n) with memoization, O(2^n) without
- **Space Complexity**: O(n) for the memoization dictionary

## Notes

- Uses memoization to avoid redundant calculations
- For very large values of n, consider using iterative approach
- Returns 0 for n=0 and 1 for n=1 by definition

## See Also

- [calculate_factorial](#calculate_factorial) - Calculate factorial of a number
- [is_prime](#is_prime) - Check if a number is prime
```

### Java Methods

```markdown
# validateEmail

Validates an email address using regex pattern matching and additional business rules.

## Syntax

```java
public static ValidationResult validateEmail(String email, boolean strictMode)
```

## Parameters

- `email` (String) - The email address to validate (cannot be null)
- `strictMode` (boolean) - If true, applies stricter validation rules

## Return Value

- **Type**: ValidationResult
- **Description**: Object containing validation status and error messages

```java
public class ValidationResult {
    private boolean isValid;
    private List<String> errors;
    
    // getters and setters
}
```

## Exceptions

- `IllegalArgumentException`: Thrown when email parameter is null
- `PatternSyntaxException`: Thrown if regex pattern is malformed (rare)

## Examples

### Basic Usage
```java
ValidationResult result = validateEmail("user@example.com", false);
if (result.isValid()) {
    System.out.println("Email is valid");
} else {
    System.out.println("Errors: " + result.getErrors());
}
```

### Strict Mode Validation
```java
ValidationResult result = validateEmail("user+tag@example.co.uk", true);
// Strict mode may reject certain valid but uncommon email formats
```

### Batch Validation
```java
List<String> emails = Arrays.asList(
    "valid@example.com",
    "invalid-email",
    "another@test.org"
);

List<ValidationResult> results = emails.stream()
    .map(email -> validateEmail(email, false))
    .collect(Collectors.toList());
```

## Validation Rules

### Standard Mode
- Basic regex pattern matching
- Checks for @ symbol and domain
- Allows common email formats

### Strict Mode
- RFC 5322 compliant validation
- Rejects unusual but technically valid formats
- Additional length and character restrictions

## Notes

- Uses compiled regex patterns for better performance
- Supports internationalized domain names (IDN)
- Thread-safe implementation

## See Also

- [validatePhoneNumber](#validatePhoneNumber) - Phone number validation
- [sanitizeInput](#sanitizeInput) - Input sanitization utilities
```

### C# Methods

```markdown
# ProcessDataAsync

Asynchronously processes a collection of data items with configurable parallelism and error handling.

## Syntax

```csharp
public static async Task<ProcessingResult<T>> ProcessDataAsync<T>(
    IEnumerable<T> data,
    Func<T, CancellationToken, Task<T>> processor,
    ProcessingOptions options = null,
    CancellationToken cancellationToken = default
)
```

## Parameters

- `data` (IEnumerable<T>) - The collection of items to process
- `processor` (Func<T, CancellationToken, Task<T>>) - Async function to process each item
- `options` (ProcessingOptions, optional) - Configuration options for processing
- `cancellationToken` (CancellationToken, optional) - Token for cancellation support

## Return Value

- **Type**: Task<ProcessingResult<T>>
- **Description**: Async task returning processing results and statistics

```csharp
public class ProcessingResult<T>
{
    public IReadOnlyList<T> SuccessfulItems { get; }
    public IReadOnlyList<ProcessingError> Errors { get; }
    public TimeSpan ProcessingTime { get; }
    public int TotalProcessed { get; }
}
```

## Exceptions

- `ArgumentNullException`: Thrown when data or processor is null
- `OperationCanceledException`: Thrown when operation is cancelled
- `AggregateException`: Contains multiple exceptions from parallel processing

## Examples

### Basic Usage
```csharp
var numbers = Enumerable.Range(1, 100);
var result = await ProcessDataAsync(
    numbers,
    async (num, ct) => {
        await Task.Delay(10, ct); // Simulate processing
        return num * 2;
    }
);

Console.WriteLine($"Processed {result.TotalProcessed} items");
```

### With Custom Options
```csharp
var options = new ProcessingOptions
{
    MaxDegreeOfParallelism = 4,
    ContinueOnError = true,
    BatchSize = 50
};

var result = await ProcessDataAsync(
    largeDataSet,
    ProcessItemAsync,
    options,
    cancellationToken
);
```

### Error Handling
```csharp
try
{
    var result = await ProcessDataAsync(data, processor);
    
    if (result.Errors.Any())
    {
        foreach (var error in result.Errors)
        {
            _logger.LogError(error.Exception, 
                "Failed to process item: {Item}", error.Item);
        }
    }
}
catch (OperationCanceledException)
{
    _logger.LogInformation("Processing was cancelled");
}
```

## Configuration Options

```csharp
public class ProcessingOptions
{
    public int MaxDegreeOfParallelism { get; set; } = Environment.ProcessorCount;
    public bool ContinueOnError { get; set; } = false;
    public int BatchSize { get; set; } = 1000;
    public TimeSpan Timeout { get; set; } = TimeSpan.FromMinutes(30);
}
```

## Performance Considerations

- Uses `Parallel.ForEach` for CPU-bound operations
- Implements semaphore for controlling concurrency
- Batching reduces memory pressure for large datasets

## Notes

- Supports cancellation through CancellationToken
- Thread-safe implementation
- Provides detailed error reporting
- Optimized for both CPU and I/O bound operations

## See Also

- [ProcessDataInBatches](#ProcessDataInBatches) - Batch processing variant
- [ParallelProcessor](#ParallelProcessor) - Lower-level parallel processing utilities
```

## Documentation Checklist

When documenting a function, ensure you include:

- [ ] Clear, descriptive function name
- [ ] Brief purpose description
- [ ] Complete syntax with type information
- [ ] All parameters with types and descriptions
- [ ] Return value type and description
- [ ] Possible exceptions/errors
- [ ] At least 2-3 practical examples
- [ ] Performance considerations (if relevant)
- [ ] Browser/environment compatibility (if relevant)
- [ ] Related functions or alternatives

## Best Practices

### Writing Descriptions

- **Be Concise**: Start with a one-line summary
- **Be Specific**: Explain exactly what the function does
- **Use Active Voice**: "Calculates" not "is used to calculate"
- **Include Context**: When and why to use this function

### Parameter Documentation

- **Include Types**: Always specify parameter types
- **Mark Optional**: Clearly indicate optional parameters
- **Explain Constraints**: Mention valid ranges, formats, etc.
- **Default Values**: Document default values for optional parameters

### Example Guidelines

- **Start Simple**: Begin with basic usage examples
- **Show Variety**: Include different use cases
- **Handle Errors**: Show proper error handling
- **Real-World Context**: Use realistic scenarios

### Cross-References

- Link to related functions
- Reference relevant documentation sections
- Include external resources when helpful
- Maintain consistent linking format

## Template Customization

Adapt this template based on your project's needs:

- **Add Sections**: Include project-specific sections
- **Remove Sections**: Skip irrelevant sections
- **Modify Format**: Adjust to match your documentation style
- **Language Features**: Include language-specific features

This template ensures comprehensive, consistent function documentation that helps developers understand and use your code effectively.