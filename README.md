Steps
-------

AWS Account
------------
Create a personal AWS account

Jenkins
-------- 
install Jenkins
```
# sudo apt-get install jenkins
```

Nodes/Serverless
--------
Install nodejs/nmp/serverless
```
# apt-get install nodejs npm
# sudo npm install serverless -g
````

Jenkins Job
------------
Create jenkins job with pipeline groovy script:
```
node {
    ansiColor('xterm') {
        stage("checkout") {
            git url: 'git@github.com:k-pammi/hellowordnodejs.git', branch: "master"
        }
        stage("install express") {
            sh "npm install express --save"
        }
        stage('serverless-http') {
            sh "npm install serverless-http --save"
        }
        stage("deploy") {
            sh "sls deploy"
        }
    }
}
```
make sure jenkins user, jenkins, has aws api keys for deployment to work.
Create .aws/credentials in /var/lib/jenkins

