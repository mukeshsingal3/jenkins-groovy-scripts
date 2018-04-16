```groovy
void getObjectInfo(obj){
    println("----------------------------------------------------")
    if(obj == null){
        println("Object is null")
    }
    println("Class Name :"+ obj.class.name)
    println("\nProperties")
    obj.metaClass.properties.each{ p->
        if(p.getter){
            def out = new StringBuffer()
            out << 'Name : ' + p.name.toString().padRight(30)
            out << 'Property : ' + p.getProperty(obj).toString().padRight(30)
            out << 'Type : ' + p.type.toString()

            println(out.toString())
        }
    }
    println("\nMethods")
    obj.class.getDeclaredMethods().each{ m->
        println("    ->   ${m.toString()}")
    }
}
```