# -*- mode: ruby -*-
# vi: set ft=ruby :
	
Vagrant.configure("2") do |config|
	
  # jenkins,javaインストール
  $script_master = <<SCRIPT
    sudo yum install -y wget
    sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
    sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
    sudo yum install -y jenkins
    sudo yum install -y java-1.7.0-openjdk.x86_64
    sudo chkconfig jenkins on
    sudo service jenkins start
SCRIPT

  # javaインストール
  $script_slave = <<EOF
    sudo yum install -y java-1.7.0-openjdk.x86_64
EOF
	
  # masterサーバ作成
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.33.10"
    master.vm.provision "shell", inline: $script_master
  end
	
  # slave1サーバ作成
  config.vm.define "slave1" do |slave1|
    slave1.vm.hostname = "slave1"
    slave1.vm.network "private_network", ip: "192.168.33.11"
    slave1.vm.provision "shell", inline: $script_slave
  end
	
  # chefインストール
  config.omnibus.chef_version = :latest
	
  # boxダウンロード
  config.vm.box = "opscode-centos-6.7"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.7_chef-provisionerless.box"

end
