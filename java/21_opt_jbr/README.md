## Usage

This custom pterodactyl yolk is designed to be identical to the built-in Pterodactyl [Java 21 (ghcr.io/pterodactyl/yolks:java_21)](https://github.com/pterodactyl/yolks/blob/master/java/21/Dockerfile) yolk for the **Minecraft** nest and **Paper** egg, with one exception: *the [JetBrains Runtime (JBR)](https://github.com/JetBrains/JetBrainsRuntime) is included in `/opt/jbr/bin/java`*.

This allows you to optionally [toggle between](#to-toggle-between-default-java-and-jbr) development using the JBR by changing your server's startup command. When using the JBR, you can perform java hotswapping when developing your plugins, allowing you to modify class files on the fly without restarting the server. 

### To use the yolk when creating a server
- Make sure your wings node has an Allocation for port `5005` and your wings node itself has port `5005` open
- When creating a new server with
    - Nest: Minecraft
    - Egg: Paper
- Under **Allocation Management** 
    - Add port `5005` as an **Additional Allocation(s)**, allowing you to reach the debug port when remote debugging with Intellij
- Under **Docker Configuration** enter the custom image `ghcr.io/braekpo1nt/yolks:java_21_opt_jbr`
- Under **Startup Configuration**
    - Use the default **Startup command** to use default java
    - Use something like the command below to use the JBR
    ```
    /opt/jbr/bin/java -XX:+AllowEnhancedClassRedefinition -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar {{SERVER_JARFILE}}
    ```
    - You can [change this later](#to-toggle-between-default-java-and-jbr) as desired

### To change the yolk of an existing server
- Make sure your wings node has an Allocation for port `5005` and your wings node itself has port `5005` open
- Go to your pterodactyl panel's admin view
- navigate to **Sidebar>Management>Servers** and select your server
- In the **Build Configuration** tab
    - Under **Allocation Management** use the **Assign Additional Ports** to open `5005`
- In the **Startup** tab
    - Under **Docker Image Configuration** paste in the custom image `ghcr.io/braekpo1nt/yolks:java_21_opt_jbr`
    - Under **Startup Command Modification** click **Save Modifications**
- Now exit the Admin Control and switch to user view
- Navigate to your server's **Settings** tab
    - Under **REINSTALL SERVER** click **Reinstall Server** to replace the docker image. Do this at your own risk, but I've never had it delete any of my files. 

### To toggle between default java and JBR
- Go to your pterodactyl panel's admin view
- navigate to **Sidebar>Management>Servers>Your server>Startup**
- Under **Startup Command Modification**
    - Use the **Default Service Start Command** to use default java
    - Use something like the command below to use the JBR
    ```
    /opt/jbr/bin/java -XX:+AllowEnhancedClassRedefinition -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar {{SERVER_JARFILE}}
    ```
- Restart your server for the new startup command to take effect

## Notes

You don't need [Hotswap-agent](https://github.com/HotswapProjects/HotswapAgent) to perform java hotswapping. In fact, it's a hindrance in Paper server development. 

To use Intellij Idea to remote debug and hook into the JBR, you'll need port `5005` open on your server's container (and on your wings node). You can create an allocation for your server and assign it an "Additional Allocation" and pterodactyl handles the rest. I'm assuming if you've reached this point you know how to open the port on your wings node. 
