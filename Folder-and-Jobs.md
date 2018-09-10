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
```