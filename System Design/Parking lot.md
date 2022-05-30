# Parking Lot Design

### Requirements
 - Parking Lot has multiple floors with multiple parking slots each
 - Multiple entry and exit spots
 - Show how many parking lots available
 - Customers can collect parking ticket from entry points and pay at exit points
 - System should not allow cars if the lot is full
 - Parking slots are various types : Compact,Large,Handicapped,MotorCycle
 - System should support parking vehicles of different types like car, truck, motorcycle
 - Each parking slot has a sign which shows if it's available
 - Each floor should show how many slots available in it
 - System should support per-hour parking fee model

### Entities Involved 
 - Parking Lot
 - Vehicle
 - Parking Spot
 - Ticket

```
public enum VehicleType{
    MOTORCYCLE,
    CAR,
    VAN,
    TRUCK
}

public abstract class Vehicle{
    private String licenseTag;
    private VehicleType type;
    private ParkingTicket ticket;
    
    public Vehicle(VehicleType type, String licenseTag){
        this.type = type;
        this.licenseTag = licenseTag;
    }
    
    public void assignTicket(ParkingTicket ticket){
        this.ticket = ticket;
    }
}

public class Car extends Vehicle{
    public Car(String licenseTag){
        super(VehicleType.CAR,licenseTag);
    }
}

public class Van extends Vehicle{
    public Van(String licenseTag){
        super(VehicleType.VAN,licenseTag);
    }
}

public class Truck extends Vehicle{
    public Truck(String licenseTag){
        super(VehicleType.TRUCK,licenseTag);
    }
}

public class Motorcycle extends Vehicle{
    public Motorcycle(String licenseTag){
        super(VehicleType.MOTORCYCLE,licenseTag);
    }
}


public enum ParkingSpotType{
    COMPACT,LARGE,MOTORCYCLE;
}

public abstract class ParkingSpot{
    private String number;
    private boolean available;
    private Vehicle vehicle;
    private final ParkingSpotType type;
    
    public ParkingSpot(ParkingSpotType type){
        this.type = type;
    }
    
    public boolean isAvailable(){
        return this.available;
    }
    
    public void assignVehicle(Vehicle vehicle){
        this.vehicle = vehicle;
        this.available = false;
    }
    
    public void removeVehicle(){
        this.vehicle = null;
        this.available = true;
    }

}

public class CompactSpot extends ParkingSpot{
    public CompactSpot(){
        super(ParkingSpotType.COMPACT);
    }
}

public class LargeSpot extends ParkingSpot{
    public LargeSpot(){
        super(ParkingSpotType.LARGE);
    }
}

public class MotorCycleSpot extends ParkingSpot{
    public MotorCycleSpot(){
        super(ParkingSpotType.MOTORCYCLE);
    }
}


Pakring Floor - Each floor has set number of parking spots

public class ParkingFloor{
    private String name;
    private Map<String,CompactSpot> compactSpots;
    private Map<String,LargeSpot> largeSpots;
    private Map<String,MotorCycleSpot> motorcycleSpots;
    
    public ParkingFloor(String name){
        this.name  = name;
    }
    
    public void addParkingSpot(ParkingSpot spot){
        switch(spot.getType()){
            case ParkingSpotType.COMPACT:
                compactSpots.put(spot.getNumber(),spot);
                break;
            case ParkingSpotType.LARGE:
                largeSpots.put(spot.getNumber(),spot);
                break;
            case ParkingSpotType.MOTORCYCLE:
                motorcycleSpots.put(spot.getNumber(),spot);
                break;
            default:
                System.out.println("Invalid Parking Spot type"); 
        }
    }
    
    public void assignVehicleToSpot(Vehicle vehicle,ParkingSpot spot){
        spot.assignVehicle(vehicle);
    }
    
   
    public void freeSpot(ParkingSpot spot){
        spot.removeVehicle();
    }
}

class ParkingLot{
    private String name;
    private Location address;
    private ParkingRate parkingRate;
    
    private int compactSpotCount;
    private int largeSpotCount;
    private int motorcycleSpotCount;
    
    private final int maxCompactSpotCount;
    private final int maxLargeSpotCount;
    private final int maxMotorcycleSpotCount;
    
    private Map<String,ParkingFloor> parkingFloors;
    
    private Map<String,ParkingTicket> activeTickets;
    
    private static ParkingLot parkingLot = null;
    
    private ParkingLot(){
        //initialize all variables;
    } 
    
    public ParkingLot getParkingLotInstance(){
        if(this.parkingLot == null)
            this.parkingLot = new ParkingLot();
            
        return this.parkingLot;    
    }
    
    public isFull(VehicleType type){
        if(type == VehicleType.TRUCK){
            return this.largeSpotCount >= this.maxLargeSpotCount;
        }else if(type == VehicleType.VAN || type == VehicleType.CAR){
            return this.compactSpotCount >= this.maxCompactSpotCount;
        }else if(type == VehicleType.MOTORCYCLE){
            return this.motorcycleSpotCount >= this.maxMotorcycleSpotCount;
        }else{
            return (this.largeSpotCount + this.compactSpotCount + this.motorcycleSpotCount) >= 
                   (this.maxLargeSpotCount + this.maxCompactSpotCount + this.maxMotorcycleSpotCount)
        }
    }
    
    public synchronized ParkingTicket getNewParkingTicket(Vehicle vehicle) throws ParkingFullException {
        if(this.isFull(vehicle.getType()))
            throw new ParkingFullException();
            
        ParkingTicket ticket = new ParkingTicket();
        vehicle.assignTicket(ticket);
        incrementSpotCount(vehicle.getType());
        ticket.saveInDB(); // Will save the ticket with start time stamp
        return ticket;
    }
    
    private boolean incrementSpotCount(VehicleType type) {
        if (type == VehicleType.TRUCK) {
          largeSpotCount++;
        } else if (type == VehicleType.CAR || type == VehicleType.VAN) {
          compactSpotCount++;
        } else if (type == VehicleType.MOTORCYCLE) {
          motorcycleSpotCount++;
        } 
   }
   
   private 


}

class ParkingTicket{
    Vehicle vehicle;
    ParkingSpot parkingSpot;
    Date entryTime;
    Date exitTime;
    
    public ParkingTicket(Vehicle vehicle,Parkingspot)

}

```


