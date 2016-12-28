# 什么是pojos
1.POJO mean Plain Old Java Object.it refers to a Java object(instance of definition) that isn't bogged down by framework extensions.
For example, to receive from JMS . you need to write a class that implements the MessageListener interface.
```java
public class ExampleListener implements MessageListener {

    public void onMessage(Message message) {
        if (message instanceof TextMessage) {
            try {
                System.out.println(((TextMessage) message).getText());
            }
            catch (JMSException ex) {
                throw new RuntimeException(ex);
            }
        }
        else {
            throw new IllegalArgumentException("Message must be of type TextMessage");
        }
    }

}
  
```
This ties your code to a particular solution (JMS in this example) and makes it hard
to later migrate to an alternative messaging solution. if you build your application with lots of listeners,choosing AMQP or something else can become hard or impossible based on biting off this much technial debt.

A POJO-driven approach means writing your message handing solution free of interfaces.

```java
@Component
public class ExampleListener {

    @JmsListener(destination = "myDestination")
    public void processOrder(String message) {
        System.out.println(message);
    }
}
```
in this example ,you cyode isn't directly tied  to any interface, the responsibility
of connecting it to a JMS queue is moved into annotations, which are easier to update. in this specific example,you could replace @JmsListener with @RabbitListener. In other situations, it's possible to hava POJO-based solutions without ANY specific annotations.

this is just one example. it is not meant to illustrate JMS vs. RabbitMQ,but instead the value of coding without Being tied to specific interfaces. By using plain old Java object,your code can be much simpler.this lends itself to better testing, flexbility, and ability to make new decisions in the future.

The Spring Framework and its various portfolio projects are always aiming for ways to reduce coupling between your code and existing libraries,this is a principle concept of dependency injection. where the way your service is utilized should be part of wiring the application and not service itself




