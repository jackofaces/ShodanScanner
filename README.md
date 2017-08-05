ShodanScanner
=============

ShodanScanner is a multithreaded shodan search results exporter. It uses some clever tricks to bypass limitations in results and returns lots of results for specific searches even with a free account.

It does not need a payed account, but if you have one the number of the results returned are even greater.

Set shodan.ini with the appropriate options.

    [TorWorkerManager]
    #default is 50
    threads=5
    #default is empty String ""
    prefix=
    #default is true;
    torRangeStart=300
    #How ofter to save the current processed number. Default is 300
    saveEvery=50
    #useTor can be true or false
    #default is true for security, only writting false will disable tor.
    #If you want to useTor, please make sure tor executable is added in your Operating system's Path
    useTor=true
    
    [Shodan]
    #query=port:81 goahead 5ccc069c403ebaf9f0171e9517f40e41
    #query=Server: squid
    query=JAWS/1.0
    shodanUsername=shodanUsername
    shodanPassword=shodanPassword
    #results are written to output/urls.txt every {sleepBetweenWritesSeconds} seconds
    sleepBetweenWritesSeconds = 32
    #where to write the results. This path is relative to output.
    outputFile = urls.txt
    
Then run Main class with shodan.ini as argument to collect. 

Main.java is a complete example.

Build
-----

1) Install dependencies 
    
    sudo apt-get update
        
    #remove maven2
    sudo apt-get remove maven2
    
    sudo apt-get install tor maven git openjdk-7-jdk openjdk-7-jre
    
2) Start tor:
    
    sudo service tor start
    
    
3) Install and run ccSnapTv

    git clone https://github.com/nikos-glikis/ShodanScanner.git
    cd ShodanScanner
    #./build.sh
    mvn clean compile assembly:single
    
Run:
-----

    #./start.sh
    java -jar target/ShodanScanner-1.0.1-jar-with-dependencies.jar shodan.ini
   
Parameters:
------
You query must be in: query= field under [Shodan] in you ini.

In the example above ShodanScanner will search for JAWS/1.0

Output:
-------
   
Output is flushed every 30 seconds in the output/urls directory. Both of those values are configurable in the shodan.ini file.

    
