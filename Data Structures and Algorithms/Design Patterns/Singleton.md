## Singleton Pattern

 - Ensures a class has just a single instance. 
 - Provide a global access point to the instance

```
class Shape{

    private static Shape instance;

    private Shape(){
        
    }
    
    public static synchronized Shape getInstance(){
        if(this.instance == null){
            this.instance = new Shape();
        }
        
        return this.instance;
    }

}

```

Eg : A single database object should be available.
