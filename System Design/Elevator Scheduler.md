
## Elevator Scheduler

### Questions 

 - How many elevators : 1
 - Is there any capacity Limits? If yes - better to go by count
 - What is minFloor and maxFloor?

### Use Cases
 - Request from outside to go to a floor above
 - Request from outside to go to a floor below
 - Request to a floor stop from inside
 - Open Door
 - Close Door

### Entities Involved

 - Elevator
 - Request
 - Buttons
 - Controller (interaction layer to the chips)

```

Directions: 

public enum Direction{
    UP,
    DOWN,
    IDLE
}

public class Request{
    private int floor;
    private Type type;
    private Direction direction;
    
    public Request(int floor){
        this.floor = floor;
    }
    
    public Request(){
    
    }
    
    public void setFloor(int floor){
        this.floor = floor;
    }
    
    public void assignType(Type type){
        this.type = type;
    }
    
    public void assignDirection(Direction direction){
        this.direction = direction;
    }
}

public class InternalRequest extends Request{
    public InternalRequest(int floor){
        super(floor);
        super.assignType(Type.INTERNAL);
    }
}

public class ExternalRequest extends Request{
    public ExternalRequest(int floor,Direction direction){
        super.assignType(Type.EXTERNAL);
        super.assignDirection(direction);
    }
}

public class Button{
    int floor;
    public Button(int floor){
        this.floor;
    }
}

public class Elevator{

    public Direction direction;
    public int currentFloor;
    public boolean[] upStops;
    public boolean[] downStops;
    public int upStopCount;
    public int downStopCount;
    public Button[] buttons;
    public Controller controller;
    public Direction direction;
    
    public Elevator(){
        this.direction = Direction.IDLE:
        this.currentFloor = 1;
        this.buttons = new Button[n];
        this.upStops = new boolean[n];
        this.downStops = new boolean[n];
        this.upStopCount = 0;
        this.downStopCount = 0;
        this.Controller = new Controller();
    }
    
    public void processUpRequest(){
        if(this.direction == Direction.IDLE)
            return;
        for(int i = this.currentFloor+1;i < upStops.length;i++){
            if(upStops[i]){
            
                this.controller.goUp(i);
                openGate(Direction.UP);
                closeGate();
            }
        }
    
    }
    
    public void processDownRequest(){
        if(this.direction == Direction.IDLE)
            return;
            
        for(int i = this.currentFloor -1;i >=0;i--){
            if(downStops[i]){
                this.controller.goDown(i);
                openGate(Direction.DOWN);
                
                    
                closeGate();
            }
        }
    
    }
    
    public void processInternalButton(Button button){
        addRequest(new IntenalRequest(button.floor));
    }
    
    public void processExternalButton(Button button,Direction direction){
        addRequest(new ExternalRequest(button.floor,direction));
    }
    
    public void addRequest(Request request){
        if(this.direction == Direction.UP){
        
            if(request.floor > this.currentFloor){
                this.upStops[request.floor] = true;
                this.upStopCount++;
                processUpRequest();
            }else{
                this.downStops[request.floor] = true;
                this.downStopCount++;
                processDownRequest();
            }
        }else if(this.direction == Direction.DOWN){
            if(request.floor < this.currentFloor){
                this.downStops[request.floor] = true;
                this.downStopCount++;
                processDownRequest();
            }else{
                this.upStops[request.floor] = true;
                this.upStopCount++;
                processUpRequest();
            }
        }else{
            if(request.floor > this.currentFloor){
                upStops[request.floor] = true;
                upStopCount++;
                this.direction = Direction.UP;
                processUpRequest();
            }else{
                downStops[request.floor] = true;
                downStopCount++;
                this.direction = Direction.DOWN;
                processDownRequest();
                           
            }
        }
        
        public void closeGate(){
            this.controller.closeGate();
        }
        
        public void openGate(Direction direction){
            this.controller.openGate();
            this.currentFloor = i;
            if(direction == Direction.UP){
                upStops[i] == false;
                upStopCount--;
                
            }else if(direction == Direction.DOWN){
                downStops[i] == false;
                downStopCount--;
            }
            
            this.controller.sleep(10);
        }
        
        public void clickButton(Button button){
            processInternalButton(button button);
        }
    
    
    }
    
    
    
    
}


```
