![alt text](image.png)

${__P(password)}

Logic Controllers :
    1) Handle the order of processing  Sampler/Requests in a Thread.
    2) It will decide " When & How"  to send a request  a web server.
    3) Loop Controller:
        a. Thread Group - Loop Count will applicable for all the request under that Thread group.
        b. But If u want to loop particular Request , then u need to use Loop controller.
        c. Create Loop controller, please that particular request under that loop controller


jmeter.bat -Djavax.net.ssl.keyStore=C:\Users\num\Certifications\mykeystore.jks -Djavax.net.ssl.keyStorePassword=changeit

keytool.exe -genkeypair -alias mycert -keyalg RSA -keysize 2048 -keystore  "C:\Users\num\Certifications\mykeystore.jks"
