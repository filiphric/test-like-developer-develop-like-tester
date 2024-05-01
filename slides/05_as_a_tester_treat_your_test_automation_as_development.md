---
layout: cover
---
# As a tester: treat your test automation as development

<!-- 
- I’ve seen test automation code being treated as second class citizen
- as if test automation code is something less than the application code
- and on one hand we need to be sober to the fact that developers are the ones writing the code which results in the product for our customers
- but that does not make test automation any less important
-->

---
layout: center
---
<img src="/images/linkedin.png" class="h-md" />

<!-- 
- in a recent linkedin post, I asked people - where do you put your test automation code? does it live inside the source code repository? or is it somewhere else completely?
- almost half of responses said that
- this sort of brings me to the point I was making earlier - we’ve split development and testing into different areas, but really - they are part of the same process and should be close to one another
- more importantly, they should be treated as such
- well, because **test automation is development**
-->

---
layout: center
---
# Test automation is development
<!-- 
- you are both developer and tester
- and you should start treating yourself as such
- don’t be ok with your code and you being treated as second class citizen
- and also - don’t be afraid to take your code to that level
- if you don’t want to be treated like second class citizen, than start acting like you are not that
- there are so many good practices we can take from developers
-->

---
layout: default
---
# Taking your code to another level

<v-clicks>

- code formatters
  - eslint, prettier
- reusable libaries, packages, custom commands
- typed languages

</v-clicks>

<!-- 
- it can start by using the same tools as developers
    - use eslint or prettier to create code formatting standards within your test automation team
    - create reusable libraries and packages that can handle common tasks across application, such as custom commands, database seeding script, data factories or configuration helpers
    - you can use typed languages such as TypeScript and annotate your utility functions with JSDoc
-->

---
layout: default
---
# Taking your code to another level
- code formatters
  - eslint, prettier
- reusable libaries, packages, custom commands
- typed languages
- JSDoc annotations
<v-clicks>

- write documentation 
- peer reviews


</v-clicks>

<!-- 

- but it’s not only about tooling, there are things you can implement on process side as well
    - write a good documentation for your test suite - a good test for whether you have written a good Readme doc is to try let someone new into your repo and see if they can set up everything by themselves
    - do peer reviews, and include both developers and testers, to improve quality of your code, but also to make your test automation a whole team effort - this is a great way to dissolve any inequality between developers and testers - once you create that inclusion, your team will work much better
-->
---
layout: default
---

# Taking your code to another level
- code formatters
  - eslint, prettier
- reusable libaries, packages, custom commands
- typed languages
- JSDoc annotations
- write documentation 
- peer reviews
- pair programming sessions

<v-clicks>

- quality checklists
- team triage
- celebrate big wins

</v-clicks>

<!--
- do pair programming sessions, read your colleagues code
    - create quality checklists so that only the highest quality code makes it into production
    - prioritize with your team which tests are the ones that are most critical to write - just as dev teams prioritize which features are most critical to deliver
    - and celebrate big wins - bugs that were found before they went to production, money that was saved thanks to that, problems that were avoided - it is great to remind yourself and the rest of the team of the value that you bring to the company
- turn back to developers
-->
