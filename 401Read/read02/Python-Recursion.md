# Unit tests and TDD

### Unit tests are some pieces of code to exercise the input, the output and the behaviour of your code. You can write them anytime you want.

### The first one is the test name. The tests can be considered as your alive documentation. We need to be descriptive about it and to say what is expected and what we are testing.

### The test file name should follow the same name of module name. For instance, if our module is gender.py, our test name should be test_gender.py. It’s ideal to separate the tests folder from production code (the implementation)

## Other thing to care about is the structure. A convention widely used is the AAA: Arrange, Act and Assert.

- **Arrange**: you need to organize the data needed to execute that piece of code (input);

- **Act**: here you will execute the code being tested (exercise the behaviour);

- **Assert**: after executing the code, you will check if the result (output) is the same as you were expecting.

## The Cycle
### The cycle is made by three steps:
🆘 Write a unit test and make it fail (it needs to fail because the feature isn’t there, right? If this test passes, call the Ghostbusters, really).

✅ Write the feature and make the test pass! (you can dance after that).

🔵 Refactor the code — the first version doesn’t need to be the beautiful one (don’t be shy)