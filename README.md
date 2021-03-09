## Contrast Security Protect - Quick Trial

Contrast Protect is a runtime attack detection and protection tool. You can compare it to a WAF, although WAF is sitting external to the application and Protect is embedded inside the app and has a very high degree of accuracy compared to a WAF. No hardware or software deployment is needed. You drop the agent in your app and start getting protection.


## Let’s try out Protect with Webgoat (a vulnerable Java application)
Requriments: A Mac or Linux machine with Java installed. Basic understanding of Java , [Java Agent](https://www.developer.com/java/data/what-is-java-agent.html) , [WebGoat](https://github.com/WebGoat/WebGoat), Terminal, Curl

1. Get the following attributes from User Settings in Contrast Portal. If you are not a customer you can use [Community Edition](https://www.contrastsecurity.com/contrast-community-edition) 
    - Organization ID, Authorization Header, API Key and Contrast URL
2. [Download WebGoat Server jar](https://github.com/WebGoat/WebGoat/releases/download/v8.1.0/webgoat-server-8.1.0.jar). This is a vulnerable application, so be careful about where you run it. In terminal, run steps 3 and 4 from the same folder where you placed WebGoat jar. 
3. Download contrast agent jar
    - `curl --max-time 20 https://CONTRAST_URL/api/ng/ORG_ID/agents/default/JAVA -H API-Key:API_Key -H Authorization:Authorization_Header= -o contrast.jar`
4. Start Webgoat and instrument it with Contrast agent
    - `java -javaagent:contrast.jar -Dcontrast.standalone.appname=Put_An_AppName  -Dcontrast.server=Put_A_ServerName -Dconstrast.protect.enabled=true -jar webgoat-server-8.1.0.jar`
5. Exercise WebGoat by logging into http://localhost:8080/WebGoat/, trying some attacks manually, using a DAST tool or by using my quick and dirty curl enclosed below
6. Log into Contrast portal UI. You should see your server under the Servers and attack traffic under the Attacks. Pat yourself on the back and continue exploring.

