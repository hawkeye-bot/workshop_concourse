# workshop_concourse
./fly
./fly -t lite login -c http://192.168.100.4:8080
./fly -t lite set-pipeline -p hello-world -c hello.yml
./fly -t lite unpause-pipeline -p hello-world
./fly -t lite get-pipeline -p hello-world
./fly -t lite set-pipeline -p hello-world -c navi-pipeline.yml
