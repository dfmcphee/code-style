Code Review
===========

This is forked/stolen from ^W^W inspired by
[Thoughtbot's code review guide](https://raw.githubusercontent.com/thoughtbot/guides/master/code-review/README.md)

A guide for reviewing code and having your code reviewed.

Why code reviews?
-----------------
Code is reviewed before being merged into `master`. The goal of review is to ensure that changes are delivering business value to our customers - not to perfect our code.

When reviewing, consider whether a change:

* Delivers business value. Understand why it is being made and why it is required.
* Does what it says it does. Try to break it.
* Can be maintained by the most junior member of our team.
* Meets our standards and is well written.

Don't let minor technical issues block shipping.

A reviewer may give +1 on a review. Small fixes need +1, complex fixes and large features +2. A branch should have at least +1 before you hit the green button.

It's important to separate our self-worth from the code we write so that we are always open to feedback that will help us improve.

When reviewing code that changes user facing components it is important that reviews play the role of a User Advocate and consider how the change will impact our users.

Is the copy written in such a way that it would be understand by someone who has learned English as their second language?

Is the change consistent with the user's mental model of our system?

Everyone
--------

* Accept that many programming decisions are opinions. Discuss tradeoffs, which
  you prefer, and reach a resolution quickly.
* Ask questions; don't make demands. ("What do you think about naming this
  `:user_id`?")
* Ask for clarification. ("I didn't understand. Can you clarify?")
* Avoid selective ownership of code. ("mine", "not mine", "yours")
* Avoid using terms that could be seen as referring to personal traits. ("dumb",
  "stupid"). Assume everyone is attractive, intelligent, and well-meaning.
* Be explicit. Remember people don't always understand your intentions online.
* Be humble. ("I'm not sure - let's look it up.")
* Don't use hyperbole. ("always", "never", "endlessly", "nothing")
* Don't use sarcasm.
* Keep it real. If emoji, animated gifs, or humor aren't you, don't force them.
  If they are, use them with aplomb.
* Talk in person if there are too many "I didn't understand" or "Alternative
  solution:" comments. Post a follow-up comment summarizing offline discussion.

Having Your Code Reviewed
-------------------------

* Be grateful for the reviewer's suggestions. ("Good call. I'll make that
  change.")
* Don't take it personally. The review is of the code, not you.
* Explain why the code exists. ("It's like that because of these reasons. Would
  it be more clear if I rename this class/file/method/variable?")
* Extract some changes and refactorings into future tickets/stories.
* Link to the code review from the ticket/story. ("Ready for review:
  https://github.com/organization/project/pull/1")
* Push commits based on earlier rounds of feedback as isolated commits to the
  branch. Do not squash until the branch is ready to merge. Reviewers should be
  able to read individual updates based on their earlier feedback.
* Seek to understand the reviewer's perspective.
* Try to respond to every comment.
* Wait to merge the branch until Continuous Integration (TDDium, TravisCI, etc.)
  tells you the test suite is green in the branch.
* Merge once you feel confident in the code and its impact on the project.

Reviewing Code
--------------

Understand why the code is necessary (bug, user experience, refactoring). Then:

* Communicate which ideas you feel strongly about and those you don't.
* Identify ways to simplify the code while still solving the problem.
* If discussions threaten progress on the PR then move it offline. Usually
  disagreement can be resolved quickly if the involved parties discuss things in
  front of a whiteboard.
* Offer alternative implementations, but assume the author already considered
  them. ("What do you think about using a custom validator here?")
* Seek to understand the author's perspective.
* Sign off on the pull request with a :thumbsup: or "Ready to merge" comment.

Style Comments
--------------

Reviewers should comment on missed style guidelines. Ideally you should add
a link to the relevant section in the style guide. That way you don't have to
repeat the reasoning of a particular guideline in your comment.

Example comment (markdown):

    [Return early when possible](https://github.com/mobify/mobify-code-style/tree/master/javascript#return-early-when-possible)
    
Which renders as:

> [Return early when possible](https://github.com/mobify/mobify-code-style/tree/master/javascript#return-early-when-possible)

An example response to style comments:

    Whoops. Good catch, thanks. Fixed in a4994ec.

If you disagree with a guideline, open an issue on the guides repo rather than
debating it within the code review. In the meantime, apply the guideline.

Reading material
----------------
* http://blogs.atlassian.com/2009/11/code_review_in_agile_teams_part_i/
* https://blogs.atlassian.com/2010/03/code_review_in_agile_teams_part_ii/