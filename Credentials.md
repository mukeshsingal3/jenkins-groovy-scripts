**Get access to currently defined credentials**

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

**Method 2**
```groovy
import com.cloudbees.plugins.credentials.Credentials

Set<Credentials> allCredentials = new HashSet<Credentials>();

def creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
      com.cloudbees.plugins.credentials.Credentials.class
);

allCredentials.addAll(creds)

Jenkins.instance.getAllItems(com.cloudbees.hudson.plugins.folder.Folder.class).each{ f ->
 creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
      com.cloudbees.plugins.credentials.Credentials.class, f)
  allCredentials.addAll(creds)
  
}
```