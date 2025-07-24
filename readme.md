
```
project/
│
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
└── ubuntu/
    └── Dockerfile
```

# steps:
```
download docker engine on macbook
run docker engine
```

open terminal -> `docker ps`

download github playground directory: 

`git clone git@github.com:rmaradia/playground.git`

```
docker-compose up --build
ssh root@localhost -p 2222
# Password: password
```


Access in Browser
Prometheus: `http://localhost:9090`
Grafana: `http://localhost:3000`

Default credentials: `admin / admin`

#grafana 
#add datasource -> prometheus -> `http://prometheus:9090`
#import dashboard 1860


#Stress
```
sudo apt update
sudo apt install -y stress-ng iputils-ping

stress-ng --cpu 0 --cpu-load 74 --timeout 60s --metrics-brief
```

