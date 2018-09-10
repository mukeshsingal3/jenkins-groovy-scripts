**Get all the folders with Owners**
```java
import com.cloudbees.hudson.plugins.folder.Folder

Jenkins.instance.getAllItems(Folder).each { Folder item -> 
  if(!item.getFullDisplayName().contains('Visualizer') && !item.getFullDisplayName().contains('Fabric')){
    item.getProperties().each{ prop ->
      if(prop instanceof org.jenkinsci.plugins.ownership.model.folders.FolderOwnershipProperty){
        println item.getName() + " "+ prop.getOwnership()
      }
    }
  }
}


/* Get All jobs and Build Numbers */
void getAllJobs(Jenkins instance){
    println("------------------------ Get All Jobs ---------------------------")
    instance.getAllItems().each{ item->
        Job job = item instanceof com.cloudbees.hudson.plugins.folder.Folder? null : item

        if(job && !job.getBuilds().isEmpty()){
            println("Job Name :                 "+job?.displayName)
            println("Job type :                 "+job.toString())
            println("Last Build Number :        "+job?.lastBuild?.displayName)
            println("Last Build Status          " + job?.lastBuild?.result)
            println("Build Status Summary :     "+job?.lastBuild?.buildStatusSummary?.message)
            println("Last Build Stated on       "+job?.lastBuild?.time?.dateString)
            println("Last Build Duration :      "+job?.lastBuild?.durationString)
            println("Last Build Dir             "+job?.lastBuild?.rootDir)
            println("Last Build cause :         ")
            job?.lastBuild?.getCauses().each { cause ->
                println("                           "+cause.getShortDescription())
            }
            println("Characterstic Information ")
            job?.lastBuild?.characteristicEnvVars.each{
                println("                           "+it.key + "   ->    "+it.value)
            }
            println("--------------------------------")
        }
    }
}

/**  Get Job last Build logs
 *   @Params Job object
 *   @instance Jenkins Instance
 */

void getLastBuildogs(String jobName, Jenkins instance){
    instance.getAllItems().each{ item->
        Job job = item instanceof com.cloudbees.hudson.plugins.folder.Folder? null : item
        if(job){
            if (job.displayName == jobName){
                Run lastBuild = job.getLastBuild()
                if(lastBuild){
                    file = lastBuild.getLogFile()
                    println(file.getText())
                }
            }
        }
    }
}



/*  Get all job names */
void getAllJobsNames(Jenkins instance) {
    println("--------------------- All Job Names ------------------------------")
    x = instance.getAllItems()
    instance.getJobNames().each { job ->
        println("  * " + job)
    }
}

/*  Get all Folder names */
void getAllFolderNames(Jenkins instance) {
    println("--------------------- All Folder Names ------------------------------")
    
    instance.getAllItems().each { item ->
        if (item instanceof com.cloudbees.hudson.plugins.folder.Folder) {
            println(item.getFullDisplayName())
        }
    }
}


/* Get current build paramters */
void getCurrentBuildParamters() {
    println("--------------------- Current Build Parameter ------------------------------")

    Build build = Executor.currentExecutor().currentExecutable
    ParametersAction parametersAction = build.getAction(ParametersAction)
    parametersAction?.parameters.each { ParameterValue value ->
        println value
    }
}

```