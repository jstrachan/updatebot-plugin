Updatebot Plugin
-------------------

[UpdateBot](https://github.com/fabric8-updatebot/updatebot) is a bot which updates dependencies in source code via Pull Requests.

The Updatebot Jenkins Plugin provides an easy way to use [UpdateBot](https://github.com/fabric8-updatebot/updatebot) inside your[Jenkins Pipeline](https://github.com/jenkinsci/pipeline-plugin)

### Example  

Here's an example of using the `updateBotPush` command inside your pipeline:

```groovy
node {

    stage('Release') { 
        git 'https://github.com/jstrachan-testing/updatebot-npm-sample.git'

        // TODO do the actual release first...
        
        // TODO wait for the release to be in maven central...
    }

    stage('UpdateBot') {
        // now lets update any dependent projects with this new release
        // using the local file system as the tagged source code with versions
        updateBotPush
    }
}

```

The `updateBotPush` command then uses the [UpdateBot Configuration mechanism](https://github.com/fabric8-updatebot/updatebot#configuration) to find which git repositories to perform pull requests on. 

Typically this configured via a local `.updatebot.yml` file or if there is no `.updatebot.yml` file then [UpdateBot](https://github.com/fabric8-updatebot/updatebot) will look for a github repository at https://github.com/organisation/organisation-updatebot/ where `organisation` is your actual github organisation name.