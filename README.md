# propel-assessment-environment
Environment for pipeline

# Getting started
The env values for the application are in fact powered by the .env file in this repo. For that reason, the local .env inside the Symfony app _should_ be comitted to VCS, but the .env file in this environment should _not_.

To build/run, choose a profile from below and run ```docker compose --profile PROFILENAME up```

## The Profiles
This docker compose uses profiles. The active profiles at the moment are:
* app
* full
* preflight
* 
### API profile
This profile, as the name suggests, only builds/boots the API and the services required to run it.

### Full profile
This profile boots the entire stack, including api and frontend. It does _not_ boot the preflight services.

### Preflight
Services in this profile are not designed to be run constantly. They include such things as PHPStan, which should be run pre-commit, hence the name.

# Services
## propel-assessment-app
A basic Laravel App, powered by PHP8.3
[api, full]

## propel-assessment-app-nginx
The nginx server for the pipeline app.
[api, full]

### propel-assessment-frontend-nginx
The nginx server for the pipeline frontend.
[frontend, full]

### propel-assessment-node
The build for the propel-assessment frontend. node 20, typescript
[frontend, full]

### propel-assessment-db
MariaDB server for app
[api, full]

### propel-assessment-composer
Composer container, responsible for regularising requirements. Runs once, then exiss.
[api, full]

### propel-assessment-phpstan
PHPStan checker. Does not run by default. Defaults to level 6, uses phpstan.neon inside the app repo.