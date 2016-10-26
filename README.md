# Docker
all exercises done for docker

see docker container internal ip-address

  ip route show 0.0.0.0/0 | grep -Eo 'via \S+' | awk '{ print $2 }'

172.18.0.1
