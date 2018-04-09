This wiki contains code snippets to get more into Jenkins Nodes or Computers 

**get list of Avaiable Nodes in Jenkins**

```groovy
void getNodeList(Jenkins instance) {
    println("--------------------- List of Available Nodes ------------------------------")
    instance.computers.each { comp ->
        println("  " + comp.displayName + "     isOffline -> " + comp.isOffline())
    }
}
```

** Get list of label assigned to Nodes**
```groovy
void getLabelList(Jenkins instance){
    println("--------------------- List of Available Labels ------------------------------")
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
    println("--------------------- Current Node Name ------------------------------")
    println(Computer.currentComputer().getDisplayName())
}
```

** Get Number of Executors in Current Slave **
```groovy
void getNumberOfExecutorInCurrentSlave() {
    println("--------------------- Number of Executer in Current Slave ------------------------------")
    println(Computer.currentComputer().countExecutors())
}
```