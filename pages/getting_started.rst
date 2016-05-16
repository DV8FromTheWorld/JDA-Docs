===============
Getting Started
===============

Requirements
=============

**Needed:**

- `A discord bot account <https://discordapp.com/developers/applications/me>`_

- `Java Development Kit 8 <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>`_

**Recommended:**

- An IDE: `Eclipse <http://www.eclipse.org/>`_ or `IntelliJ <https://www.jetbrains.com/idea/>`_ are the most common out there


Setup
=============

Eclipse
^^^^^^^^^^^^
To start developing with Eclipse, follow one of the guides below:

-  `Normal Setup`_
-  `Gradle Setup`_
-  `Maven Setup`_

----------------

Normal Setup
""""""""""""""""""

#. Download the latest (Binary) version of JDA (with Dependencies):
    -  `Recommended <https://github.com/DV8FromTheWorld/JDA/releases/>`_

    -  `Latest/Dev <http://ci.dv8tion.net/job/JDA/>`_

#. Create a new Java Project
#. Fill out the bot name, and set it to Java 8 (if available).
    
    .. image:: ../images/setup/eclipse/normal_1.png
    
#. Right click the project, go to **Properties**
#. Click on **Java Build Path**, then click on **Libraries**, then on **Add External JARs…**

    .. image:: ../images/setup/eclipse/normal_2.png

#. Add your downloaded **JDA-withDependencies-x.x.x\_xxx.jar** and expand It's properties

    `If you don't want Javadoc and source annotations, skip to 11.`
   
    .. image:: ../images/setup/eclipse/normal_3.png

#. Click on **Source Attachment**, then on **Edit…**, then mark **External Locations** and click on **External File**

    .. image:: ../images/setup/eclipse/normal_4.png

#. Here, add your **JDA-x.x.x\_xxx-sources.jar** and click on **OK**
#. Next, click on **Javadoc Location**, then on **Edit…**, then mark **Javadoc in archive** and click on **Browse**

    .. image:: ../images/setup/eclipse/normal_5.png

#. Here, add your **JDA-x.x.x\_xxx-javadoc.jar** and click on **OK**

You Are Done!

------------------

Gradle Setup
""""""""""""""""""

#. If you have *Eclipse IDE for Java Developers* installed, skip to **2.**, otherwise you need to install the *Buildship Gradle Integration plugin* first:
    -  Open up Eclipse and go to the Marketplace (located under the *Help* tab)
   
    -  Search for *\“gradle\”* and install **Buildship Gradle Integration** (`Plugin-Page <http://marketplace.eclipse.org/content/buildship-gradle-integration>`_)
   
    -  After the plugin is installed, relaunch Eclipse
   
    -  Right click within *Package/Project Explorer* and select **New > Other\…**
   
    -  In the *Gradle* folder, select **Gradle Project**
   
    -  Type a name for your Project and click on *Finish*. Your setup should look like this at this point:
   
    -  Delete the classes within ``src/main/java`` and ``src/test/java``
   
    -  Open up and edit the file ``build.gradle``
   
    -  Replace its content with the following code:
   

    .. code-block:: java
        
        apply plugin: 'java'
        
        dependencies {
            compile 'net.dv8tion:JDA:X.X.X\_XXX'
        }
        
        repositories {
            jcenter()
        }
        
        task fatJar(type: Jar) {
            manifest {
                attributes 'Main-Class': 'your.main.class.goes.Here'
            }
            
            from { 
                configurations.compile.collect {
                    dependency ->
                    if (dependency.directory) {
                        return dependency
                    } else {
                        return zipTree(dependency)
                    }
                }
            }
            with jar
        }



    - Adjust the version of JDA you want to use (see dependencies-section of file) and fill in your Main-Class as soon as you have one (the one containing your `public static void main(String[] args)` method)
- Save the file and do the following: *Right click your project > Gradle > Refresh All*
- Once all of the dependencies have been downloaded, create your desired packages/classes in ``src/main/java`` and start coding!

------------------

Maven Setup
""""""""""""""""""

**Prerequisites**: Maven-Plugin and local Maven installation

#. Create a new Maven project. (File -> New -> Other -> Maven -> Maven Project)
#. Now let's start configuring it, first off, open up your pom.xml and add the following lines right after `</description>`
    .. code-block:: xml
	
        <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <maven.compiler.source>1.8</maven.compiler.source>
            <maven.compiler.target>1.8</maven.compiler.target>
          </properties>
  
  - This will make your project support UTF-8 characters (So you can have it on Japanese servers for example) and also force Java 8, which is needed.

#. Now let's add JDA's repository so we can fetch the jar (Place this after `</properties>`)
    .. code-block:: xml
    
        <repositories>
            <repository>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
                <id>bintray-dv8fromtheworld-maven</id>
                <name>bintray</name>
                <url>http://dl.bintray.com/dv8fromtheworld/maven</url>
            </repository>
        </repositories>


#. Now, add the dependency, make sure you change `X.X.X_XXX` to the latest version number (Check out at http://ci.dv8tion.net/job/JDA/)
    .. code-block:: xml
	
        <dependencies>
            <dependency>
                <groupId>net.dv8tion</groupId>
                <artifactId>JDA</artifactId>
                <version>X.X.X_XXX</version>
                <type>jar</type>
                <scope>compile</scope>
            </dependency>
        </dependencies>

#. Now you need to set up the (build) maven-shade and maven-compile plugins, add the following lines right after `\</dependencies\>`
    .. code-block:: xml
	
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.5.1</version>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-shade-plugin</artifactId>
                    <version>2.4.3</version>
                    <executions>
                        <execution>
                            <phase>package</phase>
                            <goals>
                                <goal>shade</goal>
                            </goals>
                            <configuration>
                                <artifactSet>
                                    <excludes>
                                        <exclude>example</exclude> <!-- You may add jars to exclude from shading -->
                                    </excludes>
                                </artifactSet>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>

#. You are done!


IntelliJ
^^^^^^^^^^^^

#. `Download gradle.zip <https://dl.dropboxusercontent.com/u/33175902/ideaJDA/gradle.zip>`_ and extract it
#. Rename contained folder to your desired project name
#. Navigate to the folder
#. in the ``build.gradle`` file, edit the line in the dependencies section to contain desired JDA version (e.g. 1.3.0_188), set your Main-Class in the fatJar section (if you already have one) and save the changes
#. Open a terminal in this folder
#. Type *"gradlew idea"*

    .. image:: ../images/setup/intellij/1.png

#. Open the newly created Idea project
#. Locate following Message at the top right corner and press *"Import Gradle Project"*:

    .. image:: ../images/setup/intellij/2.png

#. In the popup-window, select *\"Use auto-import\"* and press OK

    .. image:: ../images/setup/intellij/3.png

#. Navigate to the Project Properties (Icon in top-right corner: |Project Properties icon|, add the JDK(SDK) if necceccary (1.8), and set the Language-Level to 8

    .. image:: ../images/setup/intellij/4.png

#. Apply
#. You are done!

.. |Project Properties icon| image:: ../images/intellij/5.png
   :align: middle
   :width: 12