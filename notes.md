# Host
git clone https://github.com/awslabs/amazon-kinesis-client-python.git
cd amazon-kinesis-client-python/
mkdir vm
cd vm
vagrant init ubuntu/trusty64
# Include in Vagrantfile:
#   config.vm.synced_folder "..", "/home/vagrant/existence",
#       owner: "vagrant", group: "vagrant"
vagrant up
vagrant ssh

# VM
sudo apt-get update
sudo apt-get install openjdk-7-jre
sudo apt-get install python-setuptools
python setup.py download_jars
sudo python setup.py install
mkdir ~/.aws
cd ~/.aws
cat > credentials
cd -
chmod 700 ~/.aws
python samples/sample_kinesis_wordputter.py --stream winton -w steve -w harrison -w melinda -w chris -p 5
# Edit sample.properties:
# executableName = /home/vagrant/existence/samples/sample_kclpy_app.py
# streamName = winton
chmod +x /home/vagrant/existence/samples/sample_kclpy_app.py
`python samples/amazon_kclpy_helper.py --print_command \
    --java /usr/bin/java --properties samples/sample.properties`