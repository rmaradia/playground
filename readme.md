project/
│
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
└── ubuntu/
    └── Dockerfile


# steps:

docker-compose up --build
ssh root@localhost -p 2222
# Password: password


Access in Browser
Prometheus: http://localhost:9090
Grafana: http://localhost:3000

Default credentials: admin / admian

#grafana 
#add datasource -> prometheus -> http://prometheus:9090
#import dashboard 1860


#Stress
sudo apt update
sudo apt install -y stress-ng iputils-ping

stress-ng --cpu 0 --cpu-load 74 --timeout 60s --metrics-brief

