# What is Jenkins

CI/CD tool들 중 하나

[About CI/CD](/42_CS_STUDY/WEEK2.md#cicd)

# How to Install Jenkins LTS with Ubuntu

```sh
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

직접 설치가 싫다면 Docker를 이용하여 jenkins를 사용할 수도 있다.

ex)
```
docker pull jenkins/jenkins:lts
docker run --name jenkins-docker -d -p 8080:8080 -p 50000:50000 -v /home/jenkins:/var/jenkins_home -u root jenkins/jenkins:lts
```

# Start Jenkins

- Jenkins Service가 동작 중인 port로 접근한다.
    ex) localhost:8080 or 127.0.0.1:8080

- 초기 암호는 /var/lib/jenkins/secrets/initialAdminPassword에서 확인 가능(환경마다 path가 다른 것 같다.)

