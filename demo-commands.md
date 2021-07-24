Demo commands
=============

Building + running commands in containers
-----------------

1. `cd C:\repos\docker-presentation\dockerfiles\hello-world`
2. `docker build -f ./Dockerfile -t alpine-base . --target base`
3. `docker run -it alpine /bin/sh`
    - Gives us a shell in a container
4. `docker build -f ./Dockerfile -t fortune-container . --target fortune`
5. `docker run fortune-container fortune`
6. `docker build -f ./Dockerfile -t copyfiles . --target copyfiles`
7. `docker run copyfiles cat /usr/cowtext.txt`
8. `docker build -t cowsay .`
9. `docker run cowsay`
10. `cd ../sleep`
11. `docker build -t sleep .`
12. `docker run -d sleep`
    - will output container ID 
13.  `docker ps` 
14.  `docker exec -it <containerid> /bin/sh`

Exposing ports
--------------

1. `docker build -f "C:\repos\docker-presentation/src/netcorerest/Dockerfile" -t netcorerest "C:\repos\docker-presentation"`
2. Run container netcorerest (`docker run -p 5000:5000 -d netcorerest`)
3. Open browser to http://localhost:5000/WeatherForecast
