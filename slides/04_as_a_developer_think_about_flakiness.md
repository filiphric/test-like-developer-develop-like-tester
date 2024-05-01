---
layout: cover
---

# **As a developer think about flakiness**

<!--
- flakiness is something that’s being talked about with testers
- mostly flakiness in test automation
- makes sense, flakiness happens often when we want run an automated check and we get uncertain results
- for this reason, it has somehow happened that the term flakiness, is connected to testing
- but that kind of connection is not really a fair one
-->

---
layout: cover
---

# **As a developer think about flakiness**

<!--
- flakiness can come from many sources
- you can have a flaky test, yes
- but you can also have a flaky server, especially when we are talking about staging or QA areas
- you can also have a flaky app
-->

---
layout: two-cols
---
```js {*|3}
it('adds a product to cart', () => {
  cy.visit('/')
  cy.wait(1000)
  cy.contains('Add to Cart').should('be.visible').click()
  cy.contains('Product added to cart!').should('be.visible')
})
```

::right::
<img src="/images/shoe_failed.png" class="relative top-[10%]" />

<!--
- let’s go back to our example with a sneaker ecommerce site
- we have a Cypress test that attempts to buy a sneaker
- flaky - fails and passes
- when fails - we see we click the button too soon
- fixing on the test - add waiting so the test does not go that fast (`cy.wait(1000)`)
- but this is a slippery slope, because we may be increaing that time, not fixing the real problem
-->

<style>
.two-columns {
  gap: 1rem;
  grid-template-columns: 3fr 5fr !important;
}

.slidev-code-wrapper {
  padding-top: 35%
}
</style>

---
layout: center
disabled: true
---
<span class="text-size-4xl font-bold"><span class="invisible">What happens in</span>CI<span class="invisible">stays in</span>CI</span>

<Arrow x1="545" y1="240" x2="525" y2="290" />
<Arrow x1="720" y1="240" x2="745" y2="290" />
&nbsp;
# What happens in <span v-mark.strike=0>Vegas</span> stays in <span v-mark.strike=0>Vegas</span>

---
layout: two-cols
---
# What do we know
- test opens page and clicks on "Add to cart" button
- test sometimes passes and sometimes fails
- test seems to click the "Add to cart" button too soon
- test runs ok locally but fails on CI
- our app uses REST API to fetch data

::right::
<img src="/images/shoe_failed.png" class="relative top-[20%]" />

<style>
.two-columns {
  gap: 1rem;
  grid-template-columns: 3fr 5fr !important;
}

</style>

<!-- 
- so let’s put our developer hats on for a moment
- we are going to dive into the code and figure out what actually made the test flaky
-->

---
layout: default
---

parent component:
````md magic-move
```tsx
<Counter quantity={quantity} setQuantity={setQuantity} />
<AddToCartButton onClick={addToCart} />
```
```tsx
<Counter quantity={quantity} setQuantity={setQuantity} />
<AddToCartButton onClick={addToCart} isDisabled={quantity === 0} />
```
````

button component:
````md magic-move
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
}

const AddToCartButton = ({ onClick }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick}
    disabled={isDisabled} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4 disabled:opacity-20'
    onClick={onClick}
    disabled={isDisabled} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
````


<!--
- let’s add a new property
- [click] when the number is anything else than 0, isDisabled will be false
- [click] add it to our button as well
- [click] we’ll add an html attribute
- [click] and then add some styling so it’s semi transparent
-->

---
layout: default
---

````md magic-move
```js
it('adds a product to cart', () => {
  cy.visit('/');
  cy.wait(1000);
  cy.contains('Add to Cart').should('be.visible').click();
  cy.contains('Product added to cart!').should('be.visible');
});
```
```js
it('adds a product to cart', () => {
  cy.visit('/');
  cy.contains('Add to Cart').should('be.visible').click();
  cy.contains('Product added to cart!').should('be.visible');
});
```
````

<style>
.slidev-code-wrapper {
  padding-top: 20%
}
</style>

<!--
- as a result, our test code becomes cleaner
- and this is what you should do as a developer who owns test flakines
- it accomplishes two things:
  - fixes hidden issues that customers actually have but never report
  - makes test automation more stable and therefore more reliable
- I am very confident that more than 90% of what we call flaky test is actually a flaky app, it has nothing to do with the test code itself
- this is FINE
-->
