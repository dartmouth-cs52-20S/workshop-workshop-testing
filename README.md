# CS52 Workshops:  Testing

![](https://media.giphy.com/media/6NlmBQLhWy2QM/giphy.gif)

A testing framework acts as a dev tool for both front-end and back-end programming. For front-end testing, these frameworks can be used to simulate UI/UX before completion (button clicks, dragging, etc), while snapshot testing can be used to compare states over time.
These frameworks provide vital tools for making effective and efficient code!


## Overview

In this workshop, you're going to learn how to implement some basic unit testing using Mocha/Chai. In Part 1, we will work through a simple implementation of an isolated unit test. This well help us to build up some of the basic skills for testing that we'll need later. In Part 2, we will extend some of these skills from Part 1 to see how unit testing can be applied to our React environment. Hopefully, by the end of this workshop, you'll feel comfortable implementing your own unit tests.

## Setup

Really really easy! Just some yarn add stuff.

1. Make a new directory

```
mkdir workshop-testing
```

2. Inside the directory, setup yarn

``` 
yarn init
```
and answer the questions like your name, etc, otherwise just press enter.

Now you should have a ```package.json```. Great.


3. Time to add mocha and chai! :gift_heart:
```javascript
yarn add mocha chai --dev 
```
That's it! :crocodile:

![](https://media.giphy.com/media/3o6Zt11R527fgtrIJO/giphy.gif)

^^Literally a picture of you right now

<br/>
<br/>

# Part 1: Now let's get coding!:zap::zap:


1. First, create a new index file for your project - we won't need this per se, but it's good form! Treat this as though we're building up a more fleshed out app that you'd like to apply a test to.

```javascript
touch index.html && code index.html
```
<br/>

2. Construct your HTML file. Let's title this document "Testing!". Include `main.js` and `main-test.js` as source files in your body.

<details>
 <summary>HTML code provided here, in case you got stuck</summary>
 
 ```htmlembedded
<!DOCTYPE html>
<html>
    <head>
        <title> Testing! </title>
    </head>
    <body>
        <script src="./main.js"></script>
        <script src="./main-test.js"></script>  
    </body>
</html>
```

</details>

<br />

<br />

3. Now, what we're going to do is start making a simple calculator app. We're going to factor our code here so we keep our tests and our functions seperate. First, let's make our main file, we'll call it `main.js`.

```javascript
touch main.js && code main.js
```

<br/>

4. Then let's create a simple function that requires two parameters, and returns the sum of them both. Remember, we made our own directory here so we might not want to use ES6 syntax.

    Done? Great! :hatching_chick:

    Here's what it should look like:

```javascript
const add = function(a, b) {
     return a + b;
     }
```

<br/>

**5. Now code more functions! (yes write something by yourself**) we #apologize :sweat:

Write some basic functions that perform each of the four fundamental mathematic operations - `add` (already done!!), `subtract`, `multiply`, and `divide`. Here let's just make them as simple as possible, returning the result of the given mathematical operation applied to your two parameters (as we did with `add` above). 

For example, `divide` should `return a / b`. 

<br/>

6. Let's create the file where we're going to run our tests. 

```javascript
touch main-test.js && code main-test.js
```

This file is where we'll call the functions we just made and apply Mocha and Chai to see some unit tests in action. Let's add the necessary imports to the top of the file.

```javascript
const chai = require('chai')
const expect = chai.expect
const main = require('./main');
```

Here, we're importing Chai (the assertion library we're using here), which is what will actually run through the code and check if the values our functions are outputting are the values that we'd like to see. We'll be using `expect` statements in this test, as you will see in a second. `expect` is one of Chai's assertion styles, we could also use `should` statements or `assert` statements. We're also going to need to import our functions from our main file. 

But wait, hold up, we never exported those functions! You're right, as we learned before, you're the genius. Let's go back and do that now.

<br/>

7. Add the following to the bottom of your `main.js` file. This will allow us to export the functions we've made, enabling us to call them in our `main-test.js` file.

```javascript
module.exports = {
    add,
    subtract,
    multiply,
    divide,
}
```

<details>
<summary>IN CASE OF EMERGENCY - what your main.js should look like now </summary>

```javascript
const add = function(a, b) {
    return a + b;
    }
const subtract = function(a, b) {
    return a - b;
    }
const multiply = function(a,b) {
    return a * b;
}
const divide = function(a,b) {
    return a / b;
}
module.exports = {
    add,
    subtract,
    multiply,
    divide,
}
```

</details>

<br />
<br/>

8. Finally, we're ready to get to work writing some tests. First, let's run one for our add function. Put this block of code into our `main-test.js` file.

``` javascript
    describe('Addition', () => {
    it('1+2 should equal 3', () => {
        expect(main.add(1, 2)).to.equal(3)
    })
})
```
Here is where you begin to see Mocha and Chai at work. 
The `describe` function provides a way to group tests within Mocha; they allow us to better organize our tests and nest them into different groups. We pass `describe` the name of our testing group and a callback function (`it` here). 
The `it` function is used for individual test cases. It takes two parameters, a string explaining what our test should do, and a callback function that contains our actual test. 
The `expect` function is where we perform our actual tests. We call our function `main.add` with the proper input parameters (`1` and `2` above), then enter the expected output within the `to.equal()`, here that is `3`.

<br/>

9. Let's add our other functions now. We've provided the code below, but be sure to put your own test cases for subtraction and multiplication in the `expect` statements (replace X, Y, and Z) and describe them in your `it` statements.

```javascript
describe('Subtraction', () => {
    it('WHAT YOU EXPECT', () => {
        expect(main.subtract(X,Y)).to.equal(Z)
    })
})

describe('Multiplication', () => {
    it('WHAT YOU EXPECT', () => {
        expect(main.multiply(X,Y)).to.equal(Z)
    })
})

describe('Division', () => {
    it('2/0 should equal 0', () => {
        expect(main.divide(2,0)).to.equal(0)
    })
})
```

<br/>

10. Now let's factor it out a little. All these functions are mathematical, so why not group them together using `describe`? Let's wrap everything in a `describe` function with the group name "Math". 

```javascript
describe('Math', () => {
// the rest of your code in main-test.js
})
```

<br/>

11. We're good to go, right? Time to run some tests. This is another area where we use Mocha. Mocha is the test runner, so it's what we use to actually run the tests when the time comes. Enter the following into your command line:

```javascript
yarn mocha main-test.js
```

<br/>

![](https://i.imgur.com/o7SbJqk.png)

12. Whoopsy daisy! :open_mouth: We got an error in our `divide` function, because we forgot to account for an edge case. Let's fix that up, go to `main.js` and add an error check within the function.

```javascript
const divide = function(a,b) {
    if (b == 0) {
        return "ERROR";
    } else {
    return a / b;
    }
}
```

<br/>

13. Let's go back to our `main-test.js`, and change the output we expect in our `expect` statement. We don't want to be able to divide by 0, so if a user passes in 0 as the second parameter we should return an error. Here, for simplicity's sake, we're just returning a string `"ERROR"`. We've provided your new division test:

```javascript
describe('Division', () => {
    it('2/0 should equal "ERROR"', () => {
        expect(main.divide(2,0)).to.equal("ERROR")
    })
})
```

14. Run the tests again, using the same command `yarn mocha main-test.js`. Everything should pass! Here's a sample of what the terminal output should look like:

![](https://i.imgur.com/pOiuNip.png)


<br/>

Starting to get the hang of it?? Let's try another one!
Now we're going to do some simple string comparison, to give another example.

<br/>

15. So now go back to the `main.js` file and add our new function below `divide`. **Make sure to add "length_check" to the module.exports!**

```javascript
const length_check = function(a,b) {
    return a.length == b.length;
}
```

<br/>

16. Now we will add the tests to our `main-test.js` file. We'll test both cases (when the strings are equal, and when they're not). Notice how these are wrapped in a `describe` tag called "Strings", as this is a different category of tests. You should put these tests at the bottom of the file so that it is not part of our "Math" group of tests!


``` javascript
describe('Strings', () => {
    describe('String Length', () => {
    it('The lengths should match', () => {
        expect(main.length_check("The dog ran in the park", "The dog ran in the park")).to.equal(true)
    }
    )
})

describe('String Length', () => {
    it('The lengths should not match', () => {
        expect(main.length_check("The dog ran in the park", "The dog ran in the large park")).to.equal(false)
    }
    )
})
})
```
<br/>

17. If you haven't already guessed, now let's test it! (In case you forgot...)

```javascript
yarn mocha main-test.js
```

![](https://i.imgur.com/ZkiKVQL.png)


If all your tests passed then...

![reference link](https://media.giphy.com/media/10h3idv6iEAzyo/giphy.gif)

Voila! You're done with part 1!

<br/>
<br/>
<br/>
<br/>


# Part 2
Now we're going to extend our testing knowledge to our starterpack with Mocha, Chai and... Enzyme (helps us test react stuff)!

![](https://www.mrdubuque.com/uploads/2/4/5/0/24509062/enzyme-gif-orig_orig.gif)


### To begin,
Open and git clone your starter pack, then enter your new directory. 

```
git clone LINKTOYOURSTARTERPACK workshop-testing-pt2
```


```javascript
cd workshop-testing-pt2
```

<br/>
<br/>

In your starterpack folder, just in case, we are going to pull up the v2 of your starterpack that has the Counter! You guessed it, we are testing that feature!





```javascript
git checkout tags/v2
```

Now create a new "testing" branch! (Remember how to do that?? No? Me netiher tbh :fish:) Here is how!

```javascript
git checkout -b testing
```

So this created a new branch LOCALLY.

Once you've created your new branch, you're going to need to install some Enzyme capabilities.

<br/>
<br/>

### Installing Enzyme

Install Mocha, Chai, and Enzyme (and some other fun cool stuff that is necessary to make it all work together)

```javascript
yarn add mocha chai jsdom enzyme enzyme-adapter-react-16 @babel/register ignore-styles --dev
```

Wooohoo, great job! :) :alien: :dancer: :alien: 

Next, let's set up some boilerplate files that we'll need... I know, boringgggg


```javascript
mkdir test
cd test
code helpers.js dom.js
```
In your `helpers.js` file, add the following:
```javascript
import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

configure({ adapter: new Adapter() });

```

And in your `dom.js` file, add this:
```javascript
import { JSDOM } from 'jsdom';

const { window } = new JSDOM('<!doctype html><html><body></body></html>');

function copyProps(src, target) {
  const props = Object.getOwnPropertyNames(src)
    .filter((prop) => typeof target[prop] === 'undefined')
    .reduce((result, prop) => ({
      ...result,
      [prop]: Object.getOwnPropertyDescriptor(src, prop),
    }), {});
  Object.defineProperties(target, props);
}

global.window = window;
global.document = window.document;
global.navigator = {
  userAgent: 'node.js',
};

copyProps(window, global);
```

Dom will mount the program in a ~fake browser~ for React  
*Don't worry if this is confusing... it's just some FUN boilerplate*

<br/>
<br/>

Ok **awesome!!** :smiley::smile:, so now let's actually make our testing files. This is meant to help you build some intuition on testing with Mocha and Chai (and Enzyme) in a more complex scenario (our very own React app!)

<br/>
<br/>

### In your src folder...

Let's make the basic structure of our app, similar to what we did in our starterpack and short assignments. We're going to make an `app.js` file and an `index.js` file.
```javascript
code App.js
```
``` javascript
import React, { Component } from 'react';

class App extends Component {
  constructor() {
    super();

    this.state = {
      counter: 0,
    };

  }

  render() {
    const { counter } = this.state;

    return (
      <div>
        <h1>My Counter</h1>
        <Counter counter={counter} />

        <button
          type="button"
          id="add-button"
          onClick={this.onIncrement}
        >
          Increment
        </button>

        <button
          type="button"
          id="dec-button"
          onClick={this.onDecrement}
        >
          Decrement
        </button>
      </div>
    );
  }
}

export const Counter = ({ counter }) => <p>{counter}</p>;

export default App;

```

OK! So we have the basic constructor and render, but let's add in some functions!:skull:

#### Underneath the constructor and above render, add
```javascript
onIncrement = () => {
  this.setState(doIncrement);
}

onDecrement = () => {
  this.setState(doDecrement);
}
```


#### Underneath the import statement and above the class definition, add
``` javascript
export const doIncrement = (prevState) => ({
  counter: prevState.counter + 1,
});

export const doDecrement = (prevState) => ({
  counter: prevState.counter - 1,
});
```

<br/>
<br/>

## Now.. 

These files will wrap up building the app!


```javascript
code index.js
```

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

import App from './App';

ReactDOM.render(
  <App />,
  document.getElementById('main'),
);
```

<br/>


### Great job! You built an App!!!
![](https://media.giphy.com/media/dkGhBWE3SyzXW/giphy.gif)

<br/>
<br/>
<br/>


### TESTING, FINALLY.


To be able to run the test we need to add the following into our  ```package.json``` under *scripts* to be able to run the mocha test since it is mocha that deals with the structure of the tests, remember:question: 

``` json
"test:mocha": "mocha --require @babel/register --require ./test/helpers.js --require ./test/dom.js --require ignore-styles 'src/**/*.spec.js'",
```


<br/>

Finally the testing file!!

```javascript
code App.spec.js
```


Now let's add our imports to the top of the `App.spec.js` file. We'll need `mocha`, `chai,`, `react`, `enzyme`, and `app`.

``` javascript
import {
  describe, it, beforeEach, before,
} from 'mocha';
import { expect } from 'chai';
import React from 'react';
import {
  shallow,
} from 'enzyme';
import App from './App';
```

Once we have this... we can start building up our testing file :0 


Remember, we organize tests in our mocha file using the `describe` function, think of it as a title to a series of tests.

- `it` describes the test themselves, it will take two arguments, (1) the test description and (2) the test itself 
- `before` runs a set of commands *once* before all tests  
- `beforeEach` will run the given commands before *every* test

Ok, we know, we know... you just wanna see this stuff WORK

![](https://media.giphy.com/media/V3Efs7rlD9i8/giphy.gif)

<br/>
<br/>

#### Well here you go...


``` javascript
describe('App Component Functionality Testing', () => {
  let wrapper;

  before(() => {
    wrapper = shallow(<App />);
  });

  beforeEach(() => {
  wrapper.setState({ counter: 0 });
  });

  it('increments the counter through button till 42 (the zoom password)', () => {
    for (let i = 0; i < 42; i += 1) {
      wrapper.find('#add-button').simulate('click');
    }
    expect(wrapper.state().counter).to.equal(42);
  });

  it('decrements the counter to -1 (the quality of my lab) using decrement button', () => {
    for (let i = 0; i < 43; i += 1) {
      wrapper.find('#dec-button').simulate('click');
    }
    const myLabQuality = -1;
    expect(wrapper.state().counter).to.equal(myLabQuality);
  });
});
```
To run this, we just need to run `yarn test:mocha` to run the script we added in the `package.json` before that will just tell mocha to run the tests.

Just some notes on what we did here...(1) When we called shallow(<App />) we created a shallow clone of our App which we could run our testing on (2) We found the increment button using `.find` and then simulated clicking it 42 times (3) In our second test, we found the decrement button and simulated clicking it 43 times


WHAT THE HECK IT DIDN'T WORK! See if you can catch the bug with everything you know! :)

(if you couldn't get it here's the answer)

<details>
 <summary>Fix the bug please</summary>
 <br/>

You gotta move the `wrapper.setState({counter:0})` into the `before()` section because if you run it before each test... the counter value will get reset and our test wouldn't work! Yes, `beforeEach()` is going to be empty. That's okay.


</details>

<br/>
<br/>
<br/>

![](https://media.giphy.com/media/l522kgooW2Qo9xtK5Z/giphy.gif)

<br/>
<br/>
<br/>

## Summary / What you Learned

* [x] How to do a simple implementation of Mocha and Chai together
* [x] Transferring that implementation to a React app (+ learning how to use Enzyme!)
* [x] That testing your code really CAN be fun! :D $$$

<br/>

## Reflection


1. What might be some other uses for Mocha, Chai, and Enzyme in projects that we've done so far?
2. Could you describe the different purposes between Mocha, Chai and Enzyme?


<br/>

## Resources

* https://www.youtube.com/watch?v=n0mB-RZhFa4
* https://itnext.io/how-to-make-tests-using-chai-and-mocha-e9db7d8d48bc
* https://codeburst.io/how-to-test-javascript-with-mocha-the-basics-80132324752e
* https://www.robinwieruch.de/react-testing-mocha-chai-enzyme-sinon
