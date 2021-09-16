
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.define "PostgreSQL"
config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "4096"
   end

config.vm.provision "shell", inline: <<-SHELL
apt-get update
sudo apt-get install gcc libreadline-dev zlib1g-dev make -y
wget https://ftp.postgresql.org/pub/source/v8.4.0/postgresql-8.4.0.tar.gz
tar xzf postgresql-8.4.0.tar.gz
cd /home/vagrant/postgresql-8.4.0
./configure CFLAGS="-Wno-aggressive-loop-optimizations"
make
sudo make install
cd /home/vagrant/
sudo rm -r postgresql-8.4.0*
sudo mkdir /usr/local/pgsql/data
sudo useradd -m -s /bin/bash postgres
sudo chown -R postgres:postgres /usr/local/pgsql
sudo runuser -l postgres -c '/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data'
sudo runuser -l postgres -c '/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data >logfile 2>&1 &'
echo "export PATH=$PATH:/usr/local/pgsql/bin/" >> /home/postgres/.bashrc
   SHELL
end
