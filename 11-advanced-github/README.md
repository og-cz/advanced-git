# Advanced GitHub

## GITHUB API

- Github has an incredibly powerful RESTful API
- currently on Version 3

### optocat comes in many flavors

- api references: developer.github.com/v3/libraries
  ![image.png](attachment:f986cb05-1d2d-4f07-ab9f-3883baca0ca6:image.png)

### making requests

- un-authenticated
  - rate limited. 60 requests per hour
- personal token
  - useful for testing, personal projects
  - requests authenticated as user who owns the token
- OAuth
  - when your application acts on behalf of a user
  - the user will log-in via the OAuth flow in your project

### create and update via API

- github allows you to create via the api as well
- its possible to create and update
  - issues
  - pull reuqest
  - new repository
  - gists
