# Go Tests

## Getting started

1. Name test files `filename_test.go`
1. Import "testing" package
2. Each test method must:
    - start with "Test". For example, "TestAddition"
    - accept a (t *testing.T) argument
3. 

## Test commands

Run the tests in the current directory: 
```bash
go test -v .
```

## Test methods and usage
```go
t.Errorf('Message to print when the test fails %d', variable)

// %+v prints the structs field names
t.Errorf("Expected %+v Got %+v", expectedMoneyAfterDivision, actualMoneyAfterDivision)
```