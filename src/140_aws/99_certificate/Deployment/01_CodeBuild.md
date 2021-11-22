### Q1
A developer working on an AWS CodeBuild project wants to overrride a build command as part of a build run to test a change. The developer has access to run the builds but does not have access to the code and to edit the CodeBuild project.  
What process should the developer use to override the build command?
https://docs.aws.amazon.com/codebuild/latest/userguide/run-build.html#run-build-cli
* Update the buildspec.yml configuration file that is part of the source code and ren a new build
* Update the command in the Build Commands section during the build run in the AWS console. 
* **Run the start build AWS CLI command with buildspecOverride property set to the new buildspec.yml file**
    * use the AWS CLI command to specify different parameters that need to be run for the build. Since the developer has access to run the build, he can run the build changing the parameters from the command line
    * *buildspecOverride* optional string. A build spec declaration that overrides for this build one defined in the build projec. If this value is set, it can be either an inline build spec definition, or the path to an alternate build spec file relative to the value of the build-in CODEBUILD_SRC_DIR enviroment variable.
* Update the buildspec property in the StartBuild API to override the build command during build run

