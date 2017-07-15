## General Considerations

Every line of code is read much more than it is written.
Strive to write code which is easy to read.

Readability of code is a balance between complexity and size.
This guide does not attempt to define idiomatic ruby; there are other
resources that do so. Try to match the style of surrounding code
and follow accepted Ruby community practices.

Mind how your code appears on Github, in terminals and in editors of
people who have more than one editor window on their screen.
Avoid starting important parts of the code beyond the 79th column.
Post-expression conditionals are a very common example of this.

## Architecture

The flow of logic should be: controllers -> services -> models.
A controller may invoke a service or a model method, but a model method
should not instantiate or invoke a service. The same principle
applies to name references - a model should not reference constants
on a service.

Related to flow of logic is flow of data, which should be: user input ->
data model -> presentation. As much as possible operations should be
performed on data model objects rather than raw user input or presentation
output.

Services should be created for operations that involve multiple model
classes. Methods in a model class should, as much as possible, deal with
that class alone.

Service objects are encouraged, and can contain and cache state.
[This](https://blog.engineyard.com/2014/keeping-your-rails-controllers-dry-with-services)
is a brief introduction and [this](https://www.netguru.co/blog/service-objects-in-rails-will-help)
is a more extensive one.

## Tests

New features should have tests written for them, at least for the
success path. This can be a controller test, a request test or an
integration test depending on the feature.

Each user-visible page should have at least one integration
test covering its basic success path.

Bugs reported by product or outside users should have regression
tests written in conjunction with the fixes.

Engineer writing a test is responsible for making the test robust
in the face of unrelated changes in the codebase.

## Formatting

If in doubt, match the style of surrounding code.

Explicit parentheses are good, specifically in method definitions
and method calls.

Use trailing commas in multi-line expressions.

## Commits

Try to make one commit per logical change. It's fine to make several commits
as part of a larger change. Take advantage of Git's index/staging area
and interactive rebase - [this](https://tomayko.com/blog/2008/the-thing-about-git)
is an excellent introduction to the concept and
[this](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History) is
some documentation you may find helpful.

Favor putting documentation into the code itself over putting it into
commit messages.
