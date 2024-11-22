---
layout: cover
---
# As a tester:

::span{class="text-4xl line-height-normal block"}
DRY (don't repeat yourself)
::

<!-- 
- you are probably well familiar with this principle
- dry - don’t repeat yourself
- it is a good principle to start with, but of course as everything, it can be overdone
- senior developers know how to make design decisions that make the code maintainable and easy to read
- as testers we are also responsible for our test code
- and we should think like those senior developers as well
- we need to make design decisions that make the code maintainable and easy to read
-->

---
layout: cover
---
# As a tester:

::span{class="text-4xl line-height-normal block"}
DRY (don't repeat yourself)
::

<!-- 
- DRY principle sometimes serves this goal well, but there’s actually more to it than not writing the same function twice
- test automation code has its specifics
- instead of being used by the users, it’s being used as part of our development process
- it can be a part of a pipeline or a nigthly build
- this means that we may need to implement DRY principle not only to the code creation, but code execution as well
-->

---
layout: two-cols
---
# Applying DRY principle to execution

- test tagging

::right::
<img src="/images/tags.png" class="w-sm pt-[35%] pl-[20%]" />


<!-- 
- make smart decisions on which tests to execute
    - you can tag your tests and only run those that need to be ran at the current stage of your development
-->

---
layout: two-cols
---
# Applying DRY principle to execution

- test tagging
- test measurements

::right::
<img src="/images/dashboard.png" class="w-4xl pt-[45%]" />

<!-- 
- you can create reports and metrics that matter
    - for example, you can measure test execution time
    - flakines, flaky rate, failure rate
    - things that help you focus on the right thing, reduce execution time
-->

---
layout: two-cols
---
# Applying DRY principle to execution

- test tagging
- test measurements
- code coverage

```js
it('opens the page', () => {
  cy.visit('/')
})
```

::right::

<img src="/images/code_coverage.png" class="h-md pt-[20%] pl-[20%]" />


<!-- 
- another killer feature - code coverage
    - you might have heard about this one
    - code coverage gets a bad rep, because the metric many look at is the percentage of how much code is covered
    - but this is not what code coverage is for and definitely not something that it is useful for
    - code coverage can show you what parts of your code are being overtested and which part of your code have not been tested at all - you can treat it as a map
    - this can be a huge help for writing your tests in more optimal way - not repeating yourself in test execution
    - example - 24%
-->

---
layout: two-cols
---
# Applying DRY principle to execution

- test tagging
- test measurements
- code coverage
- login strategies

::right::

<img src="/images/cy_session.png" class="w-md pl-10% pt-10%" />
<img src="/images/pw_session.png" class="w-md pl-10%" />


<!-- 
- also - you can be really smart with test execution
    - if you are testing an app that needs a login, instead of using UI you can use API, or even better, use UI but only use it once
    - I’ve mentioned cypress - therejs this really cool cy.session() command that will make a snapshot of your browser state after a login
    - you can then use this snapshot in all your test
    - just login once and you are done, it’s amazing
-->