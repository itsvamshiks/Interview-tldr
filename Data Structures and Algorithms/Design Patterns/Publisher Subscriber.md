

##Publisher Subscriber pattern

There are three components in Pub-Sub pattern: Publisher, Subscriber and PubSub Service.

Message Publisher sends messages to the PubSub Service without any knowledge of message subscribers
Message Subscribers will only get the messages for which topics they are registered with the PubSubService. E.g. say we have three different topics (message types): a, b, c but only topic a is of interest to Subscriber 1, topics b and c are of interest to Subscriber 2 and Subscriber 3 wants messages for topics a and c. So subscriber 1 will be notified for topic a, Subscriber 2 will be notified for topics b and c, and Subscriber 3 will be notified for topics a and c by the PubSub Service.
Publishers tag each message with a topic, and send it to the PubSubService which acts like a middleman between Publishers and receivers.
Subscriber registers itself with PubSubService (middleman) and tells that it’s interested in messages related to a particular topic.
Publisher-Subscriber pattern is highly loosely coupled architecture where the publishers don’t know who the subscribers are and subscribers don’t know who the publishers of topic are.

###Publisher Interface

Publisher interface defines the abstract method publish() which sends message to PubSub Service.

```
public interface PublisherInterface{
    void publish(String message,PubSubService service);
}
```

###Publisher Implementation Class

PublisherImpl class implements Publisher interface and implements publish method, which sends the message to PubSubService.

```

public class PublisherImpl implements PublisherInterface{
    //Publishes new message to PubSubService
    public void publish(String message,PubSubService service){
        service.addMessageToQueue(message);
    }
}

```

###Message POJO Class

Message class is a simple POJO class to represent the messages. It has topic attribute (for this subscriber is interested) and an attribute for message payload.

```
    public class Message{
        private String topic;
        private String payload;
        
        public Message(){}
        
        public Message(String topic,String payload){
            this.topic = topic;
            this.payload = payload;
        }
        
        public String getTopic(){
            return this.topic;
        }
        
        public void setTopic(String topic){
            this.topic = topic;
        }
        
        public String getPayload(){
            return this.payload];
        }
        
        public void setPayload(String payload){
            this.payload = payload;
        }
    }

```

###Subscriber Abstract Class

Subscriber is an abstract class which has below: <br/><br/>
addSubscriber() – Adds/Registers subscriber for a topic with PubSub service. <br/>
unSubscribe() – Removes/Unsubscribes the subscriber for a topic with PubSub <br/>
List<Message> subscriberMessages – List of message which stores the messages received by Subscriber. <br/>
getMessagesForSubscriberOfTopic() – Method which requests for messages for subscriber of topic.

```
    public abstract class Subscriber {
        private List<Message> subscriberMessages = new ArrayList<Message>();
        
        public List<Message> getMessageList(){
            return this.subscriberMessages;
        }
        
        public void setSubscriberMessages(List<Message> subscriberMessages){
            this.subscriberMessages = subscriberMessages;
        }
        
        public abstract void addSubscriber(String topic,PubSubService service);
        
        public abstract void unSubscribe(String topic,PubSubService service);
        
        public abstract void getSubsciberTopicMessages(String topic,PubSubService service);
        
        public void printMessages(){
            for(Message message : this.subscriberMessages){
                System.out.println("Message Topic : " + message.getTopic() + " : " + message.getPayload());
            }
        }
    
    }
    
```

###Subscriber Implementation class

SubscriberImpl class extends Subscriber and implements the abstract methods mentioned above.

```
    public class SubscriberImpl extends Subscriber{
        
        public void addSubscriber(String topic,PubSubService service){
            service.addSubscriber(topic,this);
        }
        
        public void unSubscribe(String topic,PubSubService service){
            service.removeSubscriber(topic,this);
        }
        
        public void getSubsciberTopicMessages(String topic,PubSubService service){
            service.getSubsciberTopicMessages(topic,this);
        }
    
    }
```

###PubSubService implementation 

PubSubService is the main class which has below: <br/><br/>
Map<String, Set<Subscriber>> subscribersTopicMap – Stores the subscribers interested in a topic. <br/>
Queue<Message> messageQueue – Stores the messages published by publishers. <br/>
addMessageToQueue() – Adds message published by publishers to message queue. <br/>
addSubscriber () – Adds a subscriber for a topic. <br/>
removeSubscriber() – removes a subscriber for a topic. <br/>
broadcast() – Broadcast new messages added in queue to all subscribers of the topic. The messagesQueue will be empty after broadcasting is complete. <br/>
getMessagesForSubscriberOfTopic() – Sends messages about a topic for subscriber at any point. <br/>

```
    public class PubSubService {
        //Keeps set of subscriber topic wise, using set to prevent duplicates 
        private Map<String,Set<Subscriber>> subscribersTopicMap = new HashMap<String,Set<Subscriber>>();
        
        //Holds messages published by publishers
        private Queue<Message> messageQueue = new LinkedList<Message>();
        
        //Adds message sent by publisher to queue
        public void addMessageToQueue(Message message){
            this.messageQueue.add(message)
        }
        
        //Add a new Subscriber for a topic
        public void addSubscriber(Subscriber subscriber,String topic){
            if(!subscribersTopicMap.containsKey(topic)){
                subscribersTopicMap.put(topic,new HashSet<Subscriber>());
            }
            
            Set<Subscriber> subscribers = subscribersTopicMap.get(topic);
            subscribers.add(subscriber);
            subscribersTopicMap.put(subscribers);
        }
        
        public void removeSubscriber(String topic,Subscriber subscriber){
            if(subscribersTopicMap.containsKey(topic)){
                Set<Subscriber> subscribers = subscribersTopicMap.get(topic);
                subscribers.remove(subscriber);
                subscribersTopicMap.put(subscribers);
            }
        
        }
        
        public void broadcast(){
            if(this.messageQueue.isEmpty()){
                System.out.println('No messages from publishers to display);
            }else{
                while(!this.messageQueue.isEmpty()){
                    Message message = this.messageQueue.remove();
                    
                    Set<Subscriber> subscribersOfTopic = subscribersTopicMap.get(message.getTopic());
                    
                    for(Subscriber subscriber : subscribersOfTopic){
                        List<Message> subscriberMessages = subscriber.getSubscriberMessages();
                        subscriberMessages.add(message);
                        subscriber.setSubscriberMessages(subscriberMessages);
                    }
                }
            }
        }
        
        public void getMessagesForSubscriberOfTopic(String topic,Subscriber subscriber){
            if(this.messageQueue.isEmpty()){
                System.out.println("No messages from publishers to display");
            }else{
                while(!this.messageQueue.isEmpty()){
                    Message message = this.messageQueue.remove();
                    
                    if(message.getTopic().equalsIgnoreCase(topic)){
                        Set<Subscriber> subscribersOfTopic = subscribersTopicMap.get(topic);
                        
                        for(Subscriber subscriber : subscribersOfTopic){
                            List<Message> subscriberMessages = subscriber.getSubscriberMessages();
                            subscriberMessages.add(message);
                            subscriber.setSubscriberMessages(subscriberMessages);
                        }
                    
                    }
                
                }
            }
        }
        
        
    }
```

###Driver Class 

The Driver Class is where we run the whole thing. 

```
public class DriverClass {
	public static void main(String[] args) {
		
		//Instantiate publishers, subscribers and PubSubService 
		Publisher javaPublisher = new PublisherImpl();
		Publisher pythonPublisher = new PublisherImpl();
		
		Subscriber javaSubscriber = new SubscriberImpl();
		Subscriber allLanguagesSubscriber = new SubscriberImpl();
		Subscriber pythonSubscriber = new SubscriberImpl();
		
		PubSubService pubSubService = new PubSubService();
		
		//Declare Messages and Publish Messages to PubSubService
		Message javaMsg1 = new Message("Java", "Core Java Concepts");
		Message javaMsg2 = new Message("Java", "Spring MVC : Dependency Injection and AOP");
		Message javaMsg3 = new Message("Java", "JPA & Hibernate");
		
		javaPublisher.publish(javaMsg1, pubSubService);
		javaPublisher.publish(javaMsg2, pubSubService);
		javaPublisher.publish(javaMsg3, pubSubService);
		
		Message pythonMsg1 = new Message("Python", "Easy and Powerful programming language");
		Message pythonMsg2 = new Message("Python", "Advanced Python message");
		
		pythonPublisher.publish(pythonMsg1, pubSubService);
		pythonPublisher.publish(pythonMsg2, pubSubService);
		
		//Declare Subscribers 
		javaSubscriber.addSubscriber("Java",pubSubService);		//Java subscriber only subscribes to Java topics
		pythonSubscriber.addSubscriber("Python",pubSubService);   //Python subscriber only subscribes to Python topics
		allLanguagesSubscriber.addSubscriber("Java", pubSubService);	//all subscriber, subscribes to both Java and Python
		allLanguagesSubscriber.addSubscriber("Python", pubSubService);
		
		//Trying unSubscribing a subscriber
		//pythonSubscriber.unSubscribe("Python", pubSubService);
		
		//Broadcast message to all subscribers. After broadcast, messageQueue will be empty in PubSubService
		pubSubService.broadcast();
		
		//Print messages of each subscriber to see which messages they got
		System.out.println("Messages of Java Subscriber are: ");
		javaSubscriber.printMessages();
		
		System.out.println("\nMessages of Python Subscriber are: ");
		pythonSubscriber.printMessages();
		
		System.out.println("\nMessages of All Languages Subscriber are: ");
		allLanguagesSubscriber.printMessages();
		
		//After broadcast the messagesQueue will be empty, so publishing new messages to server
		System.out.println("\nPublishing 2 more Java Messages...");
		Message javaMsg4 = new Message("Java", "JSP and Servlets");
		Message javaMsg5 = new Message("Java", "Struts framework");
		
		javaPublisher.publish(javaMsg4, pubSubService);
		javaPublisher.publish(javaMsg5, pubSubService);
		
		javaSubscriber.getMessagesForSubscriberOfTopic("Java", pubSubService);
		System.out.println("\nMessages of Java Subscriber now are: ");
		javaSubscriber.printMessages();		
	}
}

```


