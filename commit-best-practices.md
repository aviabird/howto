## Commit Best Practices

### Important points

#### Group Related Functionality

A commit should be like a bundle of related changes.
For example, fixing two
different bugs should produce two separate commits. Also, if a feature is very
large then it should be broken down into small logical chunks and commits should
be for small chunks. If by mistake you modify some other file then do not stage
it. Git infact has support to stage [parts of one file](https://stackoverflow.com/questions/1085162/commit-only-part-of-a-file-in-git).


#### Commit Often

Consider committing often, since tasks are usually broken down into small chunks it's better to commit as soon as a component is completed. Committing often also allows people to integrate changes quickly and have less number of merge conflicts if they come. Rolling back small commits and reimplementing them is easier, if you commit too many changes rolling back brings bigger headaches.


#### Test your code before you commit

Please make sure the component you have added is tested properly. It will also help people reviewing the code by letting them have better insight into what edge cases have been covered and, they can have better suggestions for you.

#### Writing better commit messages

Good commit messages are love letters you write to your future yourself. It helps a lot in understanding the kind of assumptions that were made while writing the code. Add the pivotal link where a detailed description would be present.

#### Keeping a constant format.

- Capitalized, short (50 chars or less) summary

- More detailed explanatory text, if necessary. Wrap it to about 72 characters. In some contexts, the first line is treated as the subject of an email and the rest of the text as the body. The blank line separating the summary from the body is critical (unless you omit the body entirely); tools like rebase can get confused if you run the two together.

- Always leave the second line blank.

- Write your commit message in the imperative: "Fix bug" and not "Fixed bug" or "Fixes bug." This convention matches up with commit messages generated by commands like git merge and git revert.

- Further paragraphs come after blank lines.

  - Bullet points are okay, too
  - Typically a hyphen or asterisk is used for the bullet, preceded by a single space, with blank lines in between, but conventions vary here
  - Use a hanging indent

- Add a `#Comment` to add some special note about the commit.


#### One liner commits
One liner commits should be usually avoided but, they can be used if fixes are too small.