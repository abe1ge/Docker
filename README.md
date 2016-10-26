# Docker
all exercises done for docker

see docker container internal ip-address

  ip route show 0.0.0.0/0 | grep -Eo 'via \S+' | awk '{ print $2 }'

172.18.0.1

docker inspect DC_Zabbix | grep IPAddress | awk 'NR==3 { print $2 }' | cut -d '"' -f 2

