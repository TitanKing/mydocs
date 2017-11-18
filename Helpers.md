# Other development helper libraries #

Here is a list of libraries that I found to be useful and almost essential.

## [Expect](https://github.com/mjackson/expect) ##

When you use expect, you write assertions similarly to how you would say them, e.g. "I expect this value to be equal to 3" or "I expect this array to contain 3". When you write assertions in this way, you don't need to remember the order of actual and expected arguments to functions like assert.equal, which helps you write better tests.

    npm install --save expect

## [deepFreeze](https://github.com/substack/deep-freeze) ##

Prevents mutations in pure function testing used in unit tests.

    npm install --save deep-freeze