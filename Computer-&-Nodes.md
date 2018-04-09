This wiki contains code snippets to get more into Jenkins Nodes or Computers 

**Get list of Avaiable Nodes in Jenkins**

```groovy
void getNodeList(Jenkins instance) {
    instance.computers.each { comp ->
        println("  " + comp.displayName + "     isOffline -> " + comp.isOffline())
    }
}
```

**Get the list of label assigned to Nodes**
```groovy
void getLabelList(Jenkins instance){
    instance.getC
    instance.getLabels().each {
        println(it.getName() )
        getObjectInfo(it)
        it.getNodes().each{ node->
            println("   ->    "+    node.getNodeName())
        }
    }
}
```

**Get Current build Node name**
```groovy
void getCurrentBuildNodeName() {
    println(Computer.currentComputer().getDisplayName())
}
```

**Get Number of Executors in Current Slave**
```groovy
void getNumberOfExecutorInCurrentSlave() {
    println(Computer.currentComputer().countExecutors())
}
```