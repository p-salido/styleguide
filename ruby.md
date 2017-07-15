## General Considerations

Every line of code is read much more than it is written.
Strive to write code which is easy to read.

Readability of code is a balance between complexity and size.
It is possible to go too far in either direction (Perl, Java).

This guide does not attempt to define idiomatic ruby; there are other
resources that do so. Try to match the style of surrounding code
and follow accepted Ruby community practices.

Mind how your code appears on Github, in terminals and in editors of
people who have more than one editor window on their screen.
Avoid starting important parts of the code beyond the 79th column.
Post-expression conditionals are a very common example of this.

Most of the guidelines in this document are not absolute requirements. If there
is a good reason to do something differently, go for it. Context matters.

## Architecture

The flow of control should be: controllers -> services -> models.
A controller may invoke a service or a model method, but a model method
should not instantiate or invoke a service. The same principle
applies to name references - a model should not reference constants
on a service.

Bridge code can call out to platform code, platform code should not call
out to bridge code or use symbols defined in the bridge code.

Related to flow of logic is flow of data, which should be: user input ->
data model -> presentation. Operations should generally be
performed on data model objects rather than raw user input or presentation
output.

Services should be created for operations that involve multiple model
classes. Methods in a model class should operate on that class alone.
It is often convenient to operate on embeded or dependent models; smaller
methods doing so are generally OK to place in the parent/owning model,
larger methods may be better off in service objects.

Service objects are encouraged, and can contain and cache state.
[This](https://blog.engineyard.com/2014/keeping-your-rails-controllers-dry-with-services)
is a brief introduction and [this](https://www.netguru.co/blog/service-objects-in-rails-will-help)
is a more extensive one.

Avoid duplicating code. Consider extracting helper methods and service
objects to reduce code duplication.

There should be a single source of truth for each piece of data.
It is OK to have derived fields for efficiency or convenience reasons,
but the values in the derived fields should have a defined means of computation
from the source of truth. Values in the "source of truth" fields should not
be overwritten from derived data.

Prefer named constants over magic literals.

## Data Interchange

Dates exposed through API endpoints should be formatted according to ISO 8601.

TBD: money formatting.

## Tests

New features should have tests written for them, at least for the
success path. This can be a controller test, a request test or an
integration test depending on the feature.

Each user-visible page should have at least one integration
test covering its basic success path.

Bugs reported by product or outside users should have regression
tests written in conjunction with the fixes.

Engineer writing a test is responsible for making the test robust
in the face of unrelated changes in the codebase. This includes factories,
test setup and the test code itself.

## Refactoring

The person refactoring a piece of code is responsible for ensuring the new
code works correctly. This requires, at a minimum, either manually testing
the new code or ensuring there is appropriate test coverage for all changes.

Refactoring should be done in separate commits from behavior changes.

When creating a new way of doing something, adjust existing code to use
the new way rather than leaving both ways in the codebase. If old code
cannot be migrated to the new way for some reason, mark the code that needs
to be updated with comments and indicate when the update can happen or what
is preventing it from happening.

## Formatting

If in doubt, match the style of surrounding code.

Explicit parentheses are encouraged in method definitions and method calls.

Trailing commas are encouraged in multi-line expressions.

## Commits

Try to make one commit per logical change. It's fine to make several commits
as part of a larger change. Take advantage of Git's index/staging area
and interactive rebase - [this](https://tomayko.com/blog/2008/the-thing-about-git)
is an excellent introduction to the concept and
[here](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History) is
some documentation that can be helpful.

Favor putting documentation into the code itself as comments
over putting it into commit messages.
