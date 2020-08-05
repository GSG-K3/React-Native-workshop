# Testing:

As your codebase expands, small errors and edge cases you don’t expect can cascade into larger failures. Bugs lead to bad user experience and ultimately, business losses. One way to prevent fragile programming is to test your code before releasing it into the wild.

![React Test](https://reactnative.dev/docs/assets/diagram_testing.svg)

# React Native Testing Library

The React Native Testing Library (RNTL) is a lightweight solution for testing React Native components. It provides light utility functions on top of react-test-renderer, in a way that encourages better testing practices. Its primary guiding principle is:

```
The more your tests resemble the way your software is used, the more confidence they can give you.
```

# Installation

Open a Terminal in your project's folder and run:

```js
npm install --save-dev @testing-library/react-native
```

This library has a peerDependencies listing for react-test-renderer and, of course, react. Make sure to install them too!

```js
npm install --save-dev @testing-library/jest-native
```

Then automatically add it to your jest tests by using setupFilesAfterEnv option in your Jest configuration (it's usually located either in package.json under "jest" key or in a jest.config.js file):

```js
{
  "preset": "react-native",
  "setupFilesAfterEnv": ["@testing-library/jest-native/extend-expect"]
}
```

# Example:

```js
import { render, fireEvent } from '@testing-library/react-native';
import { QuestionsBoard } from '../QuestionsBoard';

test('form submits two answers', () => {
  const allQuestions = ['q1', 'q2'];
  const mockFn = jest.fn();

  const { getAllByA11yLabel, getByText } = render(
    <QuestionsBoard questions={allQuestions} onSubmit={mockFn} />
  );

  const answerInputs = getAllByA11yLabel('answer input');

  fireEvent.changeText(answerInputs[0], 'a1');
  fireEvent.changeText(answerInputs[1], 'a2');
  fireEvent.press(getByText('Submit'));

  expect(mockFn).toBeCalledWith({
    '1': { q: 'q1', a: 'a1' },
    '2': { q: 'q2', a: 'a2' },
  });
});
```

You can find the source of QuestionsBoard component and this example [here.](https://github.com/callstack/react-native-testing-library/blob/master/src/__tests__/questionsBoard.test.js)

# Resources:

- [React Testing Overview](https://reactnative.dev/docs/testing-overview)

- [React Native Testing Library](https://callstack.github.io/react-native-testing-library/)
