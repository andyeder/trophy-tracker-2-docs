# Testing conventions 

Every Unit should have a Unit test providing a minimum of 80% test coverage. The coverage figures should not be a target but a guide to those areas of the unit requiring additional test cases.  

When preparing test data be aware that the JavaScript engine processes JSON faster than the equivalent JavaScript Array/Object.  

## [FIRST](https://www.appsdeveloperblog.com/the-first-principle-in-unit-testing/) testing principles 

* **Fast**: Each test case should as compact as possible with as few dependencies as possible to ensure is runs quickly.  

* **Isolated/Independent**: Each test case should be independent of the other test cases. It should not matter what order the tests are run it or if the test is run on its own.  

* **Repeatable**: Tests should be repeatable and deterministic; their values shouldn’t change based on being run on different environments. Each test should set up its own data and should not depend on any external factors to run its test  

* **Self-validating**: Test cases should provide an unambiguous outcome consistent with the name of the test case.  

* **Thorough**: There should be tests for all happy paths and all known unhappy paths, especially the edge cases. The latter will increase over time. Exercise exception cases and consider both paths and routes through the code.  

For example, two sequential if/else statements require just two tests to exercise all the paths through the code (True/True plus False/False) but four test cases to exercise all the routes through the code (True/True, True/False, False/True, False/False.)  

## [AAA(A)](https://www.thephilocoder.com/unit-testing-aaa-pattern/) test case structure 

* **Arrange** the test environment including preparing the Unit subject to test (UST).  

* **Act**: perform the action that effects the test and changes the environment. 

* **Assert**: Apply assert statements to confirm the impact on the test environment (and the Unit) as expected. 

The fourth A: Consider adding **Affirm/Assure** steps immediately after the Arrange steps to check the test environment is as expected. This offers some protection from false positives resulting from invalid assumptions about the test environment. 

## General guidance 

1. Wrap related test cases in at least one 'describe' block, using `beforeEach/beforeAll/afterEach/afterAll` blocks to maintain a common environment.  

1. Only use assertions (expect statements in Jest) inside test cases. 

1. Branches and loops should not be used within test cases but can be used in functions called by the test case. However, as per point 2, assertions should NOT be used inside functions. 

1. Functions can be used/called from within a test case to help prepare the environment or create a component but there should be not assertions inside the function, instead return the result and evaluate it inside the test case. 

1. Test cases should avoid including branching or looping logic, even when this means creating considerably more, almost identical test cases. 

1. When using multiple expect statements in an async test case, use the expect.assertions to provide Jest with an indication of how many expect statement are required to confirm the test case. This avoids some false positives. 

1. Where the number of 'expect' statements that will be executed in a test case cannot be determined (see point 15) a comment should be added to the test case stating the fact. 

1. Nesting of describe blocks is encouraged especially where these aids testing and simplifies environment preparation. 

1. Pragmas used to instruct the test/coverage tools should be used only as a last resort and justified at review time. 

1. Use of the node test environment for non-GUI component unit tests by adding `* @jest-environment node` in the header comment. 

1. Do not use snapshots in unit tests as they provide insufficient benefit. They are fragile and the process of comparison is time consulting.

1. Use a behavioural testing style when proving GUI components. 

1. Extract business logic from GUI components into a view-model module for unit testing in a more conventional way. 

1. Consider replacing and existing RTL snapshots with alternative assertions where possible. 

1. For new components try to avoid using snapshots in favour of more programmatic assertion methods. 

1. Avoid calling 'expect' statements inside a 'waitfor' block as this makes it impossible to calculate reliably the number of expects will be executed in async test cases. 

## Jest/RTL testing 

| Type of Query | 0 Matches | 1 Match | >1 Matches | Retry (Async/Await) |
| :-----------: | :-------: | :-----: | :--------: | :-----------------: |
| **Single Element** |||||
| `getBy...` |	Throw error	| Return element	| Throw error	| No |
| `findBy...` | 	Throw error	| Return element	| Throw error	| Yes |
| `queryBy...` |	Return `null`	| Return element	| Throw error	| No |
| **Multiple Elements** |||||			
| `getAllBy...` |	Throw error	| Return array	| Return array	| No |
| `findAllBy...` |	Throw error	| Return array	| Return array	| Yes |
| `queryAllBy...`|	Return `[]`	| Return array	| Return array	| No |

The table above illustrates which functions to use in which circumstances, such as async or not expected. 