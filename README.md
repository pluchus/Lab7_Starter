# Lab 7 - Unit and E2E Testing
Kyle Kim
https://github.com/pluchus/Lab7_Starter

## Check Your Understanding

**1)** Where would you fit your automated tests in your Recipe project development pipeline?

I would put them inside a Github action that runs whenever code is pushed, since that way the tests are guaranteed to run before code makes it into main and we don't have to rely on individual people remembering to run them locally. Running them only after all development is done feels too late, because by then any regressions are already buried under newer commits and harder to track back to the change that broke them.

**2)** Would you use an end to end test to check if a function is returning the correct output? (yes/no)

No, since end-to-end tests are designed to simulate a real user going through the website front to back, and checking the output of a single function is much more of a unit test responsibility. Trying to use E2E for that would be slow and brittle, when a unit test would catch the same bug in a fraction of the time.

**3)** What is the difference between navigation and snapshot mode?

Navigation mode runs Lighthouse on the page right after it loads, which means it gives you actual performance metrics like load time, but it cannot see anything that happens after the initial load, so user interactions and dynamic content changes aren't covered. Snapshot mode analyzes the page in whatever state it is currently in, which is mostly useful for accessibility checks since those don't depend on timing, but you lose the performance data and any insight into JS-driven changes to the DOM.

**4)** Name three things we could do to improve the CSE 110 shop site based on the Lighthouse results.

1) The site's `<html>` tag is missing a `lang` attribute, which is a real accessibility issue since screen readers rely on that to pick the right pronunciation for the content, so adding `lang="en"` to index.html is an easy fix.
2) There is no meta description on the page, which Lighthouse flags under SEO, and adding a short description tag inside the `<head>` would help search engines actually surface the site.
3) Lighthouse also flagged render-blocking resources, so deferring the non-critical CSS or JS using `defer`/`async` attributes on the script tags, or splitting the stylesheet into critical and non-critical chunks, would let the page render its initial content faster.
