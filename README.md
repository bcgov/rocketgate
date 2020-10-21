## Rocketgate
A GraphQL-based gateway to interact with Rocket.Chat.  Initally providing search functionality.


## To Run Locally:

1. copy and fill in env vars `cp .env.example .env`
2. install packages `npm install`
3. run `npm start`


## Run in Openshift

Ideally you want this to be managed by a pipeline :) 

### Pre Reqs:

1. Install the secret: `oc process -f openshift/secret.yaml -p TOKEN=<rocketchat auth token> -p USER_ID=<rocketchat user id> | oc apply -f -`

## Run via Pipeline CLI
2. This requires an open PR in your github repo! 
  - `cd .pipeline`
  - to build `npm run build -- --pr=<pr num>`
  - to deploy `npm run deploy -- --pr=<pr num> --env=<dev|test|prod>`

## Run via Manifests

- you can trigger a build and deploy by running the `bc.yaml` and `dc.yaml` templates

