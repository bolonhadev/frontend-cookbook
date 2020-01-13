# Github Pipeline with Travis Set-up

We deploy Github based repositories with [Travis](https://travis-ci.org/) and it needs to be set up properly with commands described below.

## Set-up

1) `Create project on Github` - we use Github for all our opensource projects/libraries
    + Create project as public
    + Project has to be located under [AckeeCZ team](https://github.com/AckeeCZ)
1) `Modify package.json to allow scoped packages`
    + ```js
        "publishConfig": {
          "access": "public"
        }
        ```
    + don’t forget to set the name with scope prefix -> @ackee/jerome

1) `Create Travis account `
    + Sign up - [https://travis-ci.com](https://travis-ci.com) - **.com domain is very IMPORTANT**
    + Join [AckeeCZ team](https://travis-ci.com/organizations/AckeeCZ)
1) `Create Travis CI`
    + Go to your [travis repositories](https://travis-ci.com/organizations/AckeeCZ/repositories)
    + Choose AckeeCZ organization on the left bar
    + Click -> Manage repositories
    + Choose -> Only select repositories **IMPORTANT**
    + Select your github repository
    + Click -> Approve & request for authorization
1) `Create .travis.yml file`
    + Install travis package into your terminal
    + Go to your repository via terminal
    + Log in to Travis with command below
    +     travis login --com
    + Create **.travis.yml** file manually or copy it from [this file](https://github.com/AckeeCZ/petrus/blob/master/.travis.yml)
    + Modify the file
        + Go to [npm](https://www.npmjs.com)
        + Log in with ackee credentials (acc on our ackee password storage)
        + Get access token from the ackee acount (each user MUST create his own token, it CAN NOT be shared)
        + Encrypt the token with travis encryption command
        +     travis encrypt YOUR_AUTH_TOKEN --add deploy.api_key --com
        + Set encrypted api key into you **.travis.yml** file
    + Add/change repository name in the **.travis.yml** file
    + Set *tags: true* (only publish when flag set in commit)
1) `Push .travis.yml file into you repository`
1) `Check results` - [Travis dashboard](https://travis-ci.com/dashboard)
1) `Put building information badge into the README.md file in your repository`
    + Get inspired here - [https://github.com/AckeeCZ/petrus/blob/master/README.md](https://github.com/AckeeCZ/petrus/blob/master/README.md)
1) `If anything went wrong => call your favourite TL :))`
    + :bieb: :heart:
