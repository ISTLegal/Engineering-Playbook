# Commit Message Convention

This project follows the [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Allowed Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit
- **improvement**: An improvement to a current feature
- **init**: Initial commit

## Rules

- **Type**: Must be lowercase and from the allowed types above
- **Scope**: Optional, must be lowercase
- **Subject**:
  - Cannot be empty
  - Must not end with a period
  - Cannot be sentence-case, start-case, pascal-case, or upper-case
- **Header**: Maximum 100 characters
- **Body**: Each line maximum 100 characters, must have blank line before
- **Footer**: Each line maximum 100 characters, must have blank line before

## ✅ Good Examples

### Simple Commits (Header Only)

```bash
feat: add user authentication endpoints
fix(auth): resolve token validation issue
docs: update API documentation
refactor(database): optimize user queries
test(auth): add unit tests for login service
```

### Complete Commits (Header + Body + Footer)

```bash
feat(auth): implement OAuth2 social login integration

Add support for Google, Facebook, and GitHub OAuth2 providers.
This enables users to register and login using their existing
social media accounts, improving user experience and reducing
registration friction.

- Add OAuth2 service providers
- Implement social login controllers
- Add user profile sync from social accounts
- Update authentication middleware

Closes #123
BREAKING CHANGE: Login API now requires provider parameter
```

## ❌ Bad Examples

```bash
Fix bug                          # No type
feat: Add new feature.           # Ends with period
FEAT: new feature               # Uppercase type
feat(Auth): new feature         # Uppercase scope
feat:new feature                # Missing space after colon
Added some stuff                # Vague description
WIP: working on feature         # Temporary commit message
```

## Message Structure

### Header

The message header is a single line that contains a succinct description of the change containing a **type**, an optional **scope**, and a **subject**.

#### Type

This describes the kind of change that this commit is providing. Must be one of the allowed types listed above.

#### Scope

Scope can be anything specifying the place of the commit change. For example **events**, **kafka**, **userModel**, **authorization**, **authentication**, **loginPage**, etc...

#### Subject

This is a very short description of the change.

- Use imperative, present tense: "change" not "changed" nor "changes"
- Don't capitalize first letter
- No dot (.) at the end
- Maximum 100 characters

### Body

- Just as in `subject` use imperative, present tense: "change" not "changed" nor "changes"
- Includes motivation for the change and contrasts with previous behavior
- Each line maximum 100 characters
- Must have blank line before body

### Footer

Finished, fixed or delivered stories should be listed on a separate line in the footer prefixed with "Finishes", "Fixes", or "Delivers" keywords like this:

```
[(Finishes|Fixes|Delivers) #STORY_ID]
```

Other footer information can include:

- Breaking changes
- Issue references (Closes #123)
- Co-authored-by information

## Complete Example

```
feat(kafka): implement exactly once delivery

- ensure every event published to Kafka is delivered precisely once
- implement error handling for failed delivery
- add monitoring for delivery failures

[Delivers #130635935]
```

## Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [AngularJS commit convention](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/)
- [Writing Git Commit Messages](http://365git.tumblr.com/post/3308646748/writing-git-commit-messages)
- [A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
