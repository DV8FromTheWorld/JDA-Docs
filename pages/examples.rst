===============
Examples
===============

.. code:: java

    public class ReadyListener implements EventListener
    {
        public static void main(String[] args)
        {
            JDA jda = new JDABuilder().setBotToken(args[0])
                .addListener(new ReadyListener()).buildAsync();
        }

        @Override
        public void onEvent(Event event)
        {
            if(event instanceof ReadyEvent)
                System.out.println("API is ready!");
        }
    }

.. code:: java

    public class MessageListener extends ListenerAdapter
    {
        public static void main(String[] args)
        {
            JDA jda = new JDABuilder().setBotToken(args[0]).buildAsync();
            jda.addListener(new MessageListener());
        }

        @Override
        public void onMessageReceived(MessageReceivedEvent event)
        {
            System.out.printf("[%s][%s] %s: %s\n", event.getGuild().getName(),
                event.getTextChannel().getName(), event.getAuthor().getUsername(),
                event.getMessage().getContent());
        }
    }

More Examples
=========

We provide a small set of Examples in the `Example Directory <https://github.com/DV8FromTheWorld/JDA/tree/master/src/examples/java>`_.