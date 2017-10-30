$script = <<SCRIPT
  curl -fsSL get.docker.com -o get-docker.sh
  sudo sh get-docker.sh
  sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
  chmod +x /usr/local/bin/docker-compose
  mkdir -p keys/web keys/worker
  ssh-keygen -t rsa -f ./keys/web/tsa_host_key -N ''
  ssh-keygen -t rsa -f ./keys/web/session_signing_key -N ''
  ssh-keygen -t rsa -f ./keys/worker/worker_key -N ''
  cp ./keys/worker/worker_key.pub ./keys/web/authorized_worker_keys
  cp ./keys/web/tsa_host_key.pub ./keys/worker
  export CONCOURSE_EXTERNAL_URL=http://192.168.99.100:8080
  cp /vagrant/docker-compose.yml .
  sudo service docker restart
  echo "Starting docker machines"
  sudo docker-compose up -d
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 8080, host:8080  
  config.vm.network "private_network", ip: "192.168.99.100"
  config.vm.provision "shell", inline: $script
end
