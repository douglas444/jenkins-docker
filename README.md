ssh-keygen -t ed25519 -C "jenkins"

docker exec -u 0 -it ${CONTAINER_ID} bash

su jenkins

ssh-keyscan -H agent >> /var/jenkins_home/.ssh/known_hosts

