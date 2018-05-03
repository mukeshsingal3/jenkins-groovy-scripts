# Overview
Global variables are available in Pipeline directly, not as steps. They expose methods and variables to be accessed within your Pipeline script.

# Global Variable Reference
## pipeline
The pipeline step allows you to define your Pipelines in a more structured way. See the wiki for more information.
## env
Environment variables are accessible from Groovy code as `env.VARNAME` or simply as VARNAME. You can write to such properties as well (only using the env. prefix):

```
env.MYTOOL_VERSION = '1.33'
node {
  sh '/usr/local/mytool-$MYTOOL_VERSION/bin/start'
}
```
These definitions will also be available via the REST API during the build or after its completion, and from upstream Pipeline builds using the build step.

However any variables set this way are global to the Pipeline build. For variables with node-specific content (such as file paths), you should instead use the withEnv step, to bind the variable only within a node block.

A set of environment variables are made available to all Jenkins projects, including Pipelines. The following is a general list of variable names that are available.

**BRANCH_NAME**
For a multibranch project, this will be set to the name of the branch being built, for example in case you wish to deploy to production from master but not from feature branches; if corresponding to some kind of change request, the name is generally arbitrary (refer to CHANGE_ID and CHANGE_TARGET).\

**CHANGE_ID**
For a multibranch project corresponding to some kind of change request, this will be set to the change ID, such as a pull request number, if supported; else unset.

**CHANGE_URL**
For a multibranch project corresponding to some kind of change request, this will be set to the change URL, if supported; else unset.

**CHANGE_TITLE**
For a multibranch project corresponding to some kind of change request, this will be set to the title of the change, if supported; else unset.

**CHANGE_AUTHOR**
For a multibranch project corresponding to some kind of change request, this will be set to the username of the author of the proposed change, if supported; else unset.

**CHANGE_AUTHOR_DISPLAY_NAME**
For a multibranch project corresponding to some kind of change request, this will be set to the human name of the author, if supported; else unset.

**CHANGE_AUTHOR_EMAIL**
For a multibranch project corresponding to some kind of change request, this will be set to the email address of the author, if supported; else unset.

**CHANGE_TARGET**
For a multibranch project corresponding to some kind of change request, this will be set to the target or base branch to which the change could be merged, if supported; else unset.

**BUILD_NUMBER**
The current build number, such as "153"

**BUILD_ID**
The current build ID, identical to BUILD_NUMBER for builds created in 1.597+, but a YYYY-MM-DD_hh-mm-ss timestamp for older builds

**BUILD_DISPLAY_NAME**
The display name of the current build, which is something like "#153" by default.

**JOB_NAME**
Name of the project of this build, such as "foo" or "foo/bar".

**JOB_BASE_NAME**
Short Name of the project of this build stripping off folder paths, such as "foo" for "bar/foo".

**BUILD_TAG**
String of "jenkins-${JOB_NAME}-${BUILD_NUMBER}". All forward slashes ("/") in the JOB_NAME are replaced with dashes ("-"). Convenient to put into a resource file, a jar file, etc for easier identification.

**EXECUTOR_NUMBER**
The unique number that identifies the current executor (among executors of the same machine) that’s carrying out this build. This is the number you see in the "build executor status", except that the number starts from 0, not 1.

**NODE_NAME**
Name of the agent if the build is on an agent, or "master" if run on master

**NODE_LABELS**
Whitespace-separated list of labels that the node is assigned.

**WORKSPACE**
The absolute path of the directory assigned to the build as a workspace.

**JENKINS_HOME**
The absolute path of the directory assigned on the master node for Jenkins to store data.

**JENKINS_URL**
Full URL of Jenkins, like http://server:port/jenkins/ (note: only available if Jenkins URL set in system configuration)

**BUILD_URL**
Full URL of this build, like http://server:port/jenkins/job/foo/15/ (Jenkins URL must be set)

**JOB_URL**
Full URL of this job, like http://server:port/jenkins/job/foo/ (Jenkins URL must be set)
SCM-specific variables such as GIT_COMMIT are not automatically defined as environment variables; rather you can use the return value of the checkout step.