## Docker Run

docker run --restart unless-stopped --name naiveproxy -p 1080:1080 -v /home/naive/config.json:/usr/local/bin/naive/config.json -d omengye/naiveproxy:v103.0.5060.53-3