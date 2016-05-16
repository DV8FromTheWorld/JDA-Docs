===============
Event System
===============

Registering your Listener
=============

To register your listener, we currently have 2 Systems. Annotated
Listeners *(AnnotatedEventManager)* and Listeners implementing the
Interface *EventListener (InterfacedEventManager)*. By default, the
Interfaced one is used.

To switch between them, you can either use
``JDABuilder#useAnnotatedEventManager(boolean)``, or
``JDA#setEventManager(IEventManager)``.

After that, you just need to call ``JDABuilder#addListener(Object)`` or
``JDA#addEventListener(Object)`` with your Listener object.

Using the Interfaced System (default)
=============

When using the interfaced system (default), your Listener(s) have to
implement the Interface *EventListener*, which only has a single
function to implement: ``public void handle(Event event)``.

For convenience, we also included the class *ListenerAdapter*, which
comes with a wide set of predefined functions targeted at specific
event-types.

**Example (EventListener)**

.. code:: java

    public class Test implements EventListener
    {
        @Override
        public void handle(Event event)
        {
            if(event instanceof MessageReceivedEvent)
                System.out.println(event.getMessage().getContent());
        }
    }

**Example (ListenerAdapter)**

.. code:: java

    public class Test extends ListenerAdapter
    {
        @Override
        public void onMessageReceived(MessageReceivedEvent event)
        {
            System.out.println(event.getMessage().getContent());
        }
    }

*(don't forget actually registering this listener)*

Using the Annotated System
=============

When using the annotated system, all listener methods have to have the
``@SubscribeEvent`` annotation present, and only accept a single
parameter, which has to be a instance of *Event*.

**Example**

.. code:: java

    public class Test
    {
        @SubscribeEvent
        public void ohHeyAMessage(MessageReceivedEvent event)
        {
            System.out.println(event.getMessage().getContent());
        }
    }

*(don't forget actually registering this listener)*


List of events
=============
TODO
