yum install wget
yum install -y java-1.8.0-openjdk-devel.x86_64
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.2.1.rpm
sudo rpm --install elasticsearch-6.2.1.rpm
curl -XGET 'localhost:9200/?pretty'
