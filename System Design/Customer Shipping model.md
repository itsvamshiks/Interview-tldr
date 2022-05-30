## Customer Shipping Model design


 - Does each order see multiple items as different entities? Or just one box with all of them packed in it?
    
    Yes, all items packed in a single box


### Involved Entities : 

 - Customer
 - Order
 - Shipping Company

Customers should be able to : 
 - Ship Items/Place Order 
 - Track Order
 - List all Orders

Shipping Company should be able to : 
 - Calculate Shipping Cost
 - Create/Receive an Order
 - 
```

Class Customer{
   private int userID;
   private String firstName;
   private String lastName; 
   private String emailAddress;
   private String phoneNumber;
   private List<Orders> orders;

   public Customer(String firstName,String lastName,String emailAddress,String phoneNumber){
      this.customer_id = random.nextInt(10000);
      this.firstName = firstName;
      this.lastName = lastName;
      this.emailAddress = emailAddress;
      this.phoneNumber = phoneNumber;

      //getters and setters
      
   }
   
   publc void addOrder(Order order){
      this.orders.add(order);
   }
   

}

Class Order{
   private int orderID;
   private String description;
   private String sourceZipCode;
   private String destinationZipCode;
   private String senderInfo;
   private double weight;

   public Order(String description,String sourceZipCode,String destinationZipCode,Customer customer,double weight){
      this.description = description;
      this.sourceZipCode = sourceZipCode;
      this.destinationZipCode = destinationZipCode;
      this.senderInfo = getSenderInfo(customer);
      this.weight = weight;
      
   }


   ///getters and setters

   public String getSenderInfo(Customer customer){
      return customer.getFirstName() + " " + customer.getLastName();
   }

}

public abstract class ShippingCompany{
   private int name;
   private int costPerUnit;
   
   public abstract int calculateShippingCost(int weight,String source,String destination);
   
   public void shipOrder(){
       //Involves other entities like trucks, employees working on shipping it
   }

}

public class Fedex extends ShippingCompany{

   private final String name = "FedeX";
   private final int costPerUnit = 5;
   
   public int calculateShippingCost(int weight,String source,String destination){
      int distance = distanceCalculator.calculateDistance(source,destination);
      return distance * weight * costPerUnit;
   }
   
   public String getName(){
      return this.name;
   }
}

public class ShippingUtility{
   
   public List<Pair<String,Integer>> costCalculator(int weight,String source,String destination){
      ShippingCompany fedex = new Fedex();
      ShippingCompany ups = new UPS();
      
      List<Pair<String,Integer>> costList = new ArrayList<>();
      costList.add(new Pair<>(fedex.getName,fedex.calculateShippingCost(weight,source,destination)));
      costList.add(new Pair<>(ups.getName,ups.calculateShippingCost(weight,source,destination)));
      
   }

}


```
