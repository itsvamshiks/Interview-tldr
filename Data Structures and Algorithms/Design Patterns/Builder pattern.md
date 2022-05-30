## Builder Pattern


If you observe the below example, there is a parent Item interface. There can be different types of items 
Burger and Drink are abstract classes of item. ChickenBurger, Coke etc are the concrete classes of

Here, in the meal class, we can have different types of items, and all have the standard methods like get packing type and price

NOTE : An abstract class doesn't have to override all the methods of the interface it implements


```

1 - Create an interface Item representing food item and packing.

public interface Item{
    public String name();
    public Packing packing();
    public float price();
}

public interface Packing{
    public String pack();
}

2 - Create concrete classes implementing the Packing interface.

public class Wrapper implements Packing{
    @Override
    public String pack(){
        return "Wrapper";
    }
}

public class Bottle implements Packing{
    @Override
    public String pack(){
        return "Bottle";
    }
}

3 - Create abstract classes implementing the item interface providing default functionalities.

public abstract class Burger implements Item{
    @Override
    public Packing packing(){
        return new Wrapper();
    }

    @Override
    public abstract float price();
}

public abstract class Drink implements Item{
     @Override
    public Packing packing(){
        return new Bottle();
    }
    
    @Override
    public abstract float price();
}

4 - Create concrete classes extending Burger and Drink classes


public class ChickenBurger extends Burger {
    @Override
    public float price(){
        return 25.0f;
    }
    
    @Override public String name(){
        return "Chicken Burger";
    }
}

public class FishBurger extends Burger {
    @Override
    public float price(){
        return 30.0f;
    }
    
    @Override public String name(){
        return "Fish Burger";
    }
}

public class Coke extends Drink{
    @Override
    public float price(){
        return 30.0f;
    }
    
    @Override public String name(){
        return "Coke";
    }
}

public class Pepsi extends Drink{
    @Override
    public float price(){
        return 35.0f;
    }
    
    @Override public String name(){
        return "Pepsi";
    }
}

5 - Create a Meal class having Item objects defined above.

public class Meal{
    private List<Item> items = new ArrayList<>();
    
    public void addItem(Item item){
        items.add(item);
    }
    
    public float getCost(){
        float cost = 0.0f;
        
        for(Item item : items){
            cost+= item.price();
        }    
        
        return cost;
    }
    
    public void showItems(){
         System.out.print("Item : " + item.name());
         System.out.print(", Packing : " + item.packing().pack());
         System.out.println(", Price : " + item.price());
    }

}

public class MealBuilder {

   public Meal prepareVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new VegBurger());
      meal.addItem(new Coke());
      return meal;
   }   

   public Meal prepareNonVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new ChickenBurger());
      meal.addItem(new Pepsi());
      return meal;
   }
}





```

