===============
Audio
===============

Connect to a VoiceChannel
===============
To join a Voice Channel you have to get AudioManager. You can get it from the guild instance.
To connect to a channel you want to open an audio connection.

.. code:: java

  public void connectTo(VoiceChannel channel)
  {
    AudioManager manager = channel.getGuild().getAudioManager();
    manager.openAudioConnection(channel);
  }

Sending Audio
==============

Sending audio requires an AudioSendingHandler implementation. We provide two implementations in JDA itself.
  
**FilePlayer**

Use this implementation to play audio files from your local storage.

.. code:: java
  
  public FilePlayer getMyFilePlayer()
  {
    return new FilePlayer(new File("my audio file.mp3");
  } 

**URLPlayer**

Use this implementation to play audio from external audio files. Like a file that is uploaded to a service. (e.g. Discord attachments)
The URLPlayer requires a JDA instance.

.. code:: java
  
  public URLPlayer getMyURLPlayer(JDA api)
  {
    return new URLPlayer(api, new URL("https://mydomain.com/myfile.mp3"));
  }

**Start sending audio**

When you have your player you need to register it as a guild's sending handler and call ``play()``:

.. code:: java

  public void startPlaying(Guild guild)
  {
    guild.setSendingHandler(getMyURLPlayer(guild.getJDA()));
  }

Receiving Audio
===============

TODO
