# Python Tests

## Getting started

1. Name test files `test_filename.py`
2. Import unittest package
3. Each test class must:
    - start with "Test". For example, "TestAddition"
    - subclass the (unittest.TestCase)
4. Each test method must:
    - start with "test'. For example, 'testMethodName'
    - accept (self) argument
4. Add the following to the bottom to ensure this class can be run as a script:
```python
if __name__ == '__main__':
    unittest.main()
```

## Test commands

Run the tests in `test_filename.py`: 
```bash
$ python3 test_filename.py -v
```

## Test methods and usage
```python
self.assertEquals(correct, test_value)
```