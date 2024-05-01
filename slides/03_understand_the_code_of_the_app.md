---
layout: cover
---

# **As a tester: Learn to understand the code of the application you are testing**

<!--
- it’s pretty obvious, that developers understand the code they are writing
- the big question is - should testers understand it as well?
- my answer is yes
- obviously, there’s no need for testers to get to the level of your senior CTO
- my hot take: black box testing is no longer efficient for a tester
- there’s no need for you to be able to spot an error in code - that would make you a better developer, not better tester
- the technical knowledge that has the potential to make you a better tester is more about knowing what are the building blocks of your app
-->

---
layout: center
---

<img src="/images/signup_failed.png" class="h-xs" />
<!--
- let’s say you have found an error on a login screen
- is this an error on the frontend? is it a backend error? once the developer fixes it, what are you going to focus on?
- with black box approach, you can run your 53 test cases after developer deploys a fix and spend couple of hours re-testing the whole login flow - even then you might find out, that the deploy was unsuccessful and you have been testing wrong version of the app
- once you get a better understanding of what’s going on in your app - you may find out that there was an error on the frontend and you had a typo in your API url - testing this can get much simpler
-->

---
layout: center
---

<img src="/images/shoe_failed.png" class="h-lg" />

<!--
- another example
    - take a look at this application - it throws an error - could not buy sneakers - this is an error a user sees and it is good enough for a customer report, but I believe as testers we should be able to go further
-->

---
layout: center
---

<img src="/images/shoe_devtools.png" class="h-lg" />

<!--
- a great place to start are browser devtools
    - replicating an error and noticing an error code from API will give you a better understanding on what caused this error
    - as a result - it makes you a better teammate to your developer colleague - you can now provide much better context, or you can now understand, that this is something you need to go to your backend developer and not a colleague from frontend

couple of examples:
-->

---
layout: center
---

<img src="/images/formula_1.png" class="h-lg" />

<!-- 
I am a big fan of Formula 1 - it’s a competition with fast cars and a world-class engineering. 
- it is no longer a sport for the best drivers in the world, but a sport for best engineering teams in the world. 
- these teams also have test engineers 
- they need to understand materials, manufacturing process, aerodynamics
- able to analyze data and performance
- the level of technical knowledge these engineers need to posses is astounding
-->

---
layout: center
---

<img src="/images/boeing.jpg" class="h-lg" />

<!--
- another example is aviation 
- A flight test engineers ensures that an airplane functions properly, before they are flown. 
- They are the ones that confirm that an aircraft is in working condition. 
- They check all the components and make sure they meet the performance standards
- as a side note - I’m sure you heard about troubles with Boeing company
- you might be interested that back in 2019, Boeing introduced a plan to elimintate 900 quality engineering positions in favor of automation
-->
---
layout: center
---

<img src="/images/boeing.jpg" class="h-lg" />

<!--
- and I’m pretty sure we’re going to be teaching our kids about how prioritizing production over quality is bad path to make
- but the point I’m trying to make here is that we should hold software testers to a same standard of technical knowledge
- and I’m aware that testers deal with business requirements and need to make sure that whatever we ship serves our customers. the analytical work still needs to be done - but it needs to be complemented with technical knowledge
- so between business and engineering - choose both
-->

---
layout: center
---

# Rise of AI

<!--
- and there’s one final reason why we should get more technical as testers. the rise of AI has put a lot of question marks into our future and people keep asking - will AI replace testers? will it replace developers?
    - in my opinion, it may happen to a certain extent - but there’s a catch - most of AI that’s being used is generative - based on code that’s already on the internet, based on good code and bad code, uncomplete documentations, hacky implementations
    - most of what AI can generate is a patchwork - and there’s a lot of space for humans to assess whether the generated code is good or bad - in other words, it meets quality criteria or not
    - this is the reason why I think testing as a practice isn’t going anywhere, but also that there’s a greater pressure than ever for testers to get a good technical understanding

- let’s turn our attention to developers now, because they have some stuff to learn from testers too. mostly, when it comes to test automation and code stability
-->
