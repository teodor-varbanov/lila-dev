## Final project for the DevOps upskill program
# Lichess dev environment

Done so far:
lila - front end container along with a listener service
mongo - simple DB container
redis - simple container used for cache

# Notes:

Error in the original Lichess repo:
./lila/project/Dependencies.scala requires "scalachess" "15.7.4", which does not yet exist. Has to be modified by hand to 15.7.3 in the file, otherwise the sbt run fails.
Scalachess repo can be found here: https://github.com/lichess-org/lila-maven/tree/master/org/lichess/scalachess_3/15.7.3

(this will likely be fixed soon, but still, worth noting as it took me quite a few hours to find)

Additional note:
Since the app is using different containers for redis and mongodb, the base.conf file in ./lila/conf has to be modified, so it doesn't look for them @ localhost (or 127.0.0.1).
Also, because of the above, the containers have to be started with specified IP addresses, according to the listener config file below. Will be sorted by Ansble, but currently it's hardcoded. 

Listener:
Listener needs additional config file located in: lila/lila-ws/ws-config.conf

Heaps size:
Heap size has to be increased with the arg -J-Xmx4g (whole line is sbt -J-Xmx4g run or sbt -J-Xmx4g run, added in lila-entrypoint.sh)