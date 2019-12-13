# Automated testing

We want working apps. But how can we be sure the old features still work properly when we've just refactored its code because of a new feature? We need to test the old feature, but how?

Sure we can manually click on all buttons, fill out fields, open modals and visually check it works. But it's slow and imagine you should do it for every important part 
of the app every week.   

Here come automated tests to save our mental health 😜

Writing tests is easy, there is no advanced logic, no complex code structures or expressions (at least they shouldn't be 😅). **Writing tests that truly make your app reliable**
and don't require to be modified every time you change piece of code change, that's a real challenge! 

In our recipes we will focus on how to accomplish those tests, trying to give
more examples and practical hints than theoretical advices.

You can go through all the "chapters" or pick the one you just need.

## Chapters

* 🐶 [Testing Essentials](testing/Essentials.md) - about [Matchers](testing/Essentials.md#matchers) and [Mocking](testing/Essentials.md#mocking)
* 📦 Testing Components, Containers & Hooks
* 🏗 Testing Selectors & Utils
* 🕰 Sagas
* 🌅 E2E testing
* 🤙 Manual testing