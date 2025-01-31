# Information on how Github is administered and managed within CDL

## What GitHub Account Should I use for my work at CDL?

GitHub accounts are stongly tied to individual emails.  

The use of shared/administrative accounts in actively discouraged by GitHub through multi-factor authentication policies.

GitHub organization policies should be created with an assumption that multiple individual users will adminster policies.  These users should be removed from the GitHub organization when the users separate from CDL.

### Options
- Re-use a pre-existing GitHub account
  - Many CDL developers have chosen this option in order to showcase a portfolio of work before and after joining CDL. 
- Create a new GitHub account dedicated for my work at CDL
  - Many CDL staff have chosen this option as well. 
- Create a separate GitHub account in order to administer a GitHub organization
  - Our CDL Systems Adminstrators have chosen this option for administering GitHub.
  - This requires the use of a secondary email or an email alias.
 
### Server-based deployments 
- Create a [machine user](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#machine-users)

## What email(s) should I associate with my GitHub account

A GitHub account can be configured with multiple email addresses.  

We recommend that you associate your CDL email address with the GitHub account that you use for your work at CDL.

## Performing Git operations using my GitHub account

Many Git/GitHub operations can be performed within the GitHub web interface.
- Create issues
- Comment on issues
- Create pull requests
- Merge pull requests
- View Code
- Edit Code - this option is ok for simple edits to a single file

For work that you perform on your desktop or on a CDL server, you will likely need to authorize a **git client** to use your GitHub credentials.
- pull code from a public repo - no authorization is needed
- pull code from a private repo - authorization is needed
- push code to a repo (public or private) - authorization is needed

### Examples of a Git Client
- GitHub desktop
- VSCode
- [`git`](https://cli.github.com) command line tool

### Authorizing a Git Client
> [!NOTE]
> GitHub no longer allows you to use your GitHub password to authorize a git client.

Authorization Options
- #### GitHub Desktop
  - in this instance, the url to your repo will look like `https://github.com...` 
  - when you attempt to clone a private repository, GitHub desktop will prompt you for authentication on GitHub.com
  - GitHub desktop relies on an active web connection to GitHub.com
- #### `git` command line client
  - in this instance, the url to your repo will look like `https://github.com...` 
  - when you attempt to clone a private repository, the git tool will prompt you for a username/password
    - the username does not matter
    - for the password, provide a GitHub personal access token
      - GitHub fine-grained personal access tokens have an expiration date and will require periodic regeneration
- #### Configure an ssh key
  - in this instance, the url to your repo will look like `git@github.com...`
  - from **your desktop**, you must create an ssh key using a command line tool such as `ssh-keygen` and name it something like `~/.ssh/github_rsa`
  - you must load your PUBLIC ssh key to your GitHub account
    - Settings / SSH and GPG Keys
    - Note that SSH keys have no expiration on GitHub
  - you must add the following to your `~/.ssh/config`
  - when connecting to a CDL server, it is recommended that you forward your ssh credentials to the server rather than duplicating your ssh key on the server.
    - `ssh -A` 
```
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/github_rsa
```

### GitHub Access Tokens vs SSH Keys

- GitHub Access Tokens
  - Access rights can be revoked at any time 
  - Can be configured with an expiration
  - Access rights can be scoped to particular behaviors
  - Can perform git operations (clone/push/pull)
  - Can perform GitHub API operations
- SSH Keys
  - Access rights can be revoked at any time
  - Cannot be configured with an expiration
  - Can be "forwarded" to a server
  - Can perform git operations (clone/push/pull)
  - Cannot perform GitHub API operations

## What Type of Billing Plan should my GitHub account have?

GitHub offers 3 types of plans
- Personal
- Pro
- Enterprise

Due to cost, CDL does not have an enterprise plan.

Most CDL users have been able to qualify for a free pro account using [GitHub for Education](https://github.com/education) benefits.

- [ ] Create a confluence page describing how to apply for these benefits

## What is a GitHub Organization?  How does CDL utilize GitHub Organizations?

## I need to create a new repo, which organization should I use?

## I need to create a new repo, should it be public or private?

## What content should *never* be stored it git (even in a private repo?)

## What collaboration settings are recommended for my new GitHub repo?

## What CI/CD tools should I utilize with my repository?

Options
- GitHub actions
- AWS CodePipeline
- Jenkins

## When should I authorize an application to access my GitHub repo?

## When should I create an Access Token?

- Access tokens can be created to authorize a github client (as a login credential)
- Access tokens can be used to authorize a script to perform git operations
- Access tokens can be used to authorize a program to make GitHub api calls

## What type of access token should I use?

Access token creation is configured under **Settings/Developer Settings/Personal Access Tokens**.

If the creator of an access token is not a GitHub Organization owner, the token must be approved by a GitHub Organization Owner before it can be used.

An organization owner can revoke fine-graned tokens that have been granted organization access rights.

### Options
- Classic token (`ghp...`)
  - can be configured with/without an expiration
  - permission scopes are too broad and generally grant more rights than is desireable.
- Fine-grained Access Token (`github_pat_...`)
  - users are discourged from creating one without an expiration
  - access rights can be scoped
    - to particular github apis
    - to particular repositories
    - to a particular organization

> [!NOTE]
> At this time, CDL recommends the use of fine-grained access tokens

### Access Token Alternatives
- SSH keys
- GitHub Apps

## GitHub Apps

We should be very selecitve about the apps that are approved at an Org level.

This is the primary mechanism that we use to enable AWS Code Build/Pipeline tools to access GitHub events.

<img width="1096" alt="image" src="https://github.com/user-attachments/assets/b3c46347-d978-4cdc-99d1-cbf949f0798d" />


## How can I access the GitHub api?

## Which GitHub api should I use?

Options
- GraphQL
- API

## Can we use GitHub Codespaces?

## Best Practices

### Developer Best Practices

#### SSH Keys for GitHub

#### Access Tokens

#### Forking CDL repositories

#### Signed Commits

### Organization Admin Best Practices

### Product/Project Management Best Practices
