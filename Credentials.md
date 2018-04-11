**Get access to currently defined credentials **

```groovy
def credentials_store = jenkins.model.Jenkins.instance.getExtensionList(
        'com.cloudbees.plugins.credentials.SystemCredentialsProvider'
        )
credentials_store.each {  println "credentials_store.each: ${it}" }

credentials_store[0].credentials.each { it ->
    if (it instanceof com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl) {
      println "username: ${it.username}"
      println "password: ${it.password}"
      println "description = ${it.description}"
      println("= = = = = = =")
    }
}
```
