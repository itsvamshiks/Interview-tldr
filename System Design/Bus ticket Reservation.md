## Bus Ticket reservation System

Design a Bus ticket reservation system where user can book a ticket from any bus, and the tickets with the least id is returned. Lets say 3,6,7,8 are the available seat numbers, return 3 first. Consider cancellations too. Each bus has a fixed number of tickets. The

###Functional Requirements

- Platform should be able to list all the buses available from that city to destination city.
- Buses belong to different travel companies
- Travel companies should operate between certain routes
- Users should be able to search based on the timings, travel company besides just the source and destination
- User should be able to reserve one or more tickets in a specific bus
- The bus should have different categories of tickets (for now, just 1)
- The user should be able to retrieve their reservations, and cancel them too, based on a cancellation period
- Currently searching for buses from stop A to B directly


```

class TransportOperator{
    String id;
    String name;
    List<Route> routeList;
    List<Bus> buses;
    
    public TransportOperator(String id, String name, ArrayList<Route> routeList,ArrayList<Bus> buses){
        this.id = id;
        this.name = name;
        this.routeList = routeList;
        this.buses = buses;
    }
    
}

class Route{
    String sourceCity;
    String destinationCity;
    int distance;
}

class BusItenerary {
    String id;
    Bus bus;
    Route route;
    PriorityQueue<Seat> availableSeats;
    Map<String, Seat> reservedSeats;
    String startTime;
    String endTime;
    
    public BusItenerary(String id, Bus bus,Route route){
        this.bus = bus;
        List<Seat> busSeats = bus.getSeats();
        for(Seat seat : busSeats){
            availableSeats.add(seat);
        }
    }
    
    public List<String> assignSeats(int count){
        
        List<String> seatIds = new ArrayList<>();
        for(int i = 0;i < count;i++){
            Seat seat = availableSeats.poll();
            seat.reserve();
            seatIds.add(seat.getId());
            reservedSeats.put(seat.getId(),seat);
        }
    }

    public void cancelSeatAssignment(List<String> seatIds){
        for(String id: seatIds){
            Seat reservedSeat = reservedSeats.remove(id);
            reservedSeat.free();
            availableSeats.add(reservedSeat);
        }
    }

}

public abstract class Bus{
    String id;
 
}

public GeneralBus extends Bus{
    List<Seat> generalSeats;

}

public LuxuryCoach extends Bus{
    List<Seat> generalSeats;
    List<Seat> luxurySeats;
    
}

public enum SeatStatus{
    RESERVED,
    AVAILABLE
}

public enum SeatType{
    REGULAR,
    PREMIUM,
    ACCESSIBLE
}

class Seat{
    SeatStatus status;
    String ID;
    SeatType type;
}


class User{
    String id;
    String name;
    String address;
    String email;
    String contact;
    
    
    void makeBooking(int seats,BusItenerary busItenerary){}
    
    List<Booking> getBookings(){}
    
}


class Booking{
    String id;
    int numberofSeats;
    List<Seat> reservedSeats;
    BusItenerary busItenerary;
    String userId; 

}

class Admin{
    addTravelAgent(){
    
    }
    
    addBus(){
    
    }
    
    addRoute(){
    }
    
    addItenerary(){
    
    }
}

class Platform{

    registerAccount(){
    
    }
    
    createBooking(details){
        Booking booking = new Booking(parameters)
    }

}

class Catalog{
    priavte Map<Pair<String,String>,BusItenerary> iteneraries;
    private Map<String,Route> routes;
    private Map<String,Bus> buses;
    
    searchByRoute(String source,String destination){
    
    }
    
    
    

}

We use Transactions in SQL and Message Queues for request queueing to avound concurrency

```
