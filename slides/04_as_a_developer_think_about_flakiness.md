---
layout: cover
---

# As a developer:
::span{class="text-4xl line-height-normal block"}
think about flakiness
::

<!--
- let’s turn our attention to developers now, because they have some stuff to learn from testers too. mostly, when it comes to test automation and code stability
- flakiness is something that’s being talked about with testers
- mostly flakiness in test automation
- makes sense, flakiness happens often when we want run an automated check and we get uncertain results
- for this reason, it has somehow happened that the term flakiness, is connected to testing
- but that kind of connection is not really a fair one
-->

---
layout: cover
---

# As a developer:
::span{class="text-4xl line-height-normal block"}
think about flakiness
::

<!--
- flakiness can come from many sources
- you can have a flaky test, yes
- but you can also have a flaky server, especially when we are talking about staging or QA areas
- you can also have a flaky app
-->

---
layout: two-cols
---

# DOM flakiness

```js {*|3-4|*}
it('finds the word "bugs" on a card item', () => {
  cy,visit('/board/1')
  cy.get('[data-cy=card]')
    .eq(0)
    .should('contain.text', 'bugs')
})
```
::right::
<div v-click.hide=2>
  <img src="/images/selecting_elements.png" class="absolute w-160"/>
</div>
<img src="/images/selecting_elements_2.png" class="absolute w-160" v-click.show=2 />

<!-- 
- let’s talk about DOM flakiness first
- consider the following scenario. You want to select a card (the white element on the page) and assert its text
- Notice how both of these elements contain the word "bugs" inside. Can you tell which card are we going to select when using this code?
- You might be guessing the first one, with the text "triage found bugs"
- [click] the reasoning might be, because we select the card element and filter the first one. While that may be a good answer it’s not the most precise one. 
- Correctly it is - whichever card will load first
- [click] consider if at time of the execution of these commands, our app would look like this
- we’d still select card elements, we’d still filter the first one and make our assertion
 -->


---
layout: default
---

# DOM flakiness

<img src="/images/app_tests.png" class="w-140 m-auto" />

<!-- 
- if we ignore what the app is doing, there’s a high chance our test not doing what we expect, and therefore leading to flaky results
- this ties to the graphic I showed before, where these two cog wheels start to grind, or not even move properly
-->

---
layout: two-cols
---

# DOM flakiness

<div class="h-full relative">
  <div class='absolute top-35 w-full'>
````md magic-move
```js
it('finds the word "bugs" on a card item', () => {
  cy,visit('/board/1')
  cy.get('[data-cy=card]')
    .eq(0)
    .should('contain.text', 'bugs')
})
```
```js
it('finds the word "bugs" on a card item', () => {
  cy.visit('/board/1')
  cy.get('[data-cy=card]')
    .should('have.length', 2)
    .eq(0)
    .should('contain.text', 'bugs')
})
```
````
  </div>
</div>

::right::
<img src="/images/selecting_elements.png" class="absolute w-107"/>

<!-- 
- so what is the solution?
- there’s no one size fits all, but my recommendation would be to add a level of determinism to your test
- [click] one solution would be to add assertions to your tests that will serve as checkpoints - places where your app and test are in complete sync
- these will pretty much make sure that the test is not moving faster than the app or vice versa
- the example checks number of elements, but this could be assertion on loaders no longer existing, API request responding, element appearing and so on
-->

---
layout: two-cols
---

# Network flakiness

<div class="h-full relative">
  <div class='absolute top-15 w-full'>

```js {*|3|5-6|8-9|11-12|*|3,8-9}
it('add a todo item', () => {

  cy.visit('/')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 0)

  cy.get('[data-test=new-todo]')
    .type('create code examples{enter}')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 1)
  
});
```

  </div>
</div>

::right::

<img src="/images/todos.png" class="absolute w-110 top-40" v-click.hide=6 />
<img src="/images/api_calls.png" class="absolute w-110 top-65" v-click.show=6 />

<!-- 
- in this example we have a very simple test with a todo app
- we want to test adding a new todo item, so we:
- [click] visit the app
- [click] check whether there are 0 items
- [click] add a new todo item
- [click] check that there is now exactly one
- [click] but as you might have guessed it there’s a hidden problem when it comes to playing nicely with our network
- [click] along the test run, there are two moments when an API call is made
- one is when we open the app under test, the other one is when we create a todo
- GET request fetches all the todo items from the database and happens when we visit the application
- POST request creates a new todo item
- this test is flaky, and it’s because we don’t really take network into account
-->

---
layout: default
---

# Network flakiness

<img src="/images/test_1.png" class="absolute w-210 top-40" v-click="[0, 1]" />
<img src="/images/test_2.png" class="absolute w-210 top-40" v-click="[1, 2]" />
<img src="/images/test_3.png" class="absolute w-210 top-40" v-click="[2, 3]" />
<img src="/images/test_4.png" class="absolute w-210 top-40" v-click="3" />

<!-- 
- let me show you what goes on in the tests, this is the timeline
- [click] we have an assertion that checks that there are no items in our list
- [click] the items in our list get loaded from API. when app opens, it will call the api
- [click] the problem occurs when the response takes a little longer, and our assertion happens way too early
- we obviously cannot have only single item in our list, if the response returns anything else than zero
-->

---
layout: two-cols
---

# Network flakiness

<div class="h-full relative">
  <div class='absolute top-5 w-full'>

````md magic-move
```js {3,4,8}
it('add a todo item', () => {

  cy.intercept('GET', '/api/todos')
    .as('todos')

  cy.visit('/')

  cy.wait('@todos')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 0)

  cy.get('[data-test=new-todo]')
    .type('create code examples{enter}')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 1)
  
});
```
```js {3,4,8}
it('add a todo item', () => {

  cy.intercept('GET', '/api/todos', [])
    .as('todos')

  cy.visit('/')

  cy.wait('@todos')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 0)

  cy.get('[data-test=new-todo]')
    .type('create code examples{enter}')

  cy.get('[data-test="todo-item"]')
    .should('have.length', 1)
  
});
```
````

  </div>
</div>

::right::

<img src="/images/todos.png" class="absolute w-110 top-40" />

<!-- 
- an answer to this type of flakiness is obviously not ignoring the network layer
- one of the solutions as you can see here is intercepting the said API request and waiting for it
- [click] in this case we should probably take it a level further
- since we want to create the very first item, we can mock the empty state, like we do here with an empty array
- this is one way of eliminating network flakiness, there’s obviously more
- the bottom line is that when it comes to network layer, it should not be ignored, especially if we want to avoid test flakiness
-->