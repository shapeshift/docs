# Testing

Bug fixes and features should always come with tests. A guide for writing tests has been provided in each repository to make the process easier. Looking at other tests to see how they should be structured can also help.

The test files should live next to the code that it is testing.

Before submitting your changes in a pull request, always run the full test suite.

### Testing Tools

- Unit - test both front and back end code in isolation

  - backend - [jest](https://jestjs.io/docs/getting-started)
  - frontend - [jest](https://jestjs.io/docs/getting-started), [react testing library](https://testing-library.com/docs/react-testing-library/intro/), [react testing library hooks](https://github.com/testing-library/react-hooks-testing-library#example)

- Integration - test our APIs
  - [cypress](https://docs.cypress.io/guides/core-concepts/writing-and-organizing-tests)
- E2E - to test the full stack completely on critical flows
  - [cypress](https://docs.cypress.io/guides/core-concepts/writing-and-organizing-tests)
    - When selecting dom elements use `data-test-*` instead of using a class or id.

### Testing UI Business Logic

Separate the business logic from the view as much as possible. Create hooks, helpers & reducers to utilize this logic from the UI and test that code in isolation from its UI.
