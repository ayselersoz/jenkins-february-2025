template = '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: docker
  name: docker
spec:
  volumes:
  - name: docker
    hostPath:
      path: /var/run/docker.sock
  containers:
  - command:
    - sleep
    - "3600"
    image: docker
    name: docker
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker
'''

podTemplate(cloud: 'kubernetes', label: 'docker', yaml: template) {
node ("docker") {
    container ("docker") {
    stage ("Checkout SCM") {
        git branch: 'main', url: 'https://github.com/ayselersoz/jenkins-february-2025.git'
    }

    stage ("Docker Login") {
        sh "docker login -u ayselersoz -p kaizen123"
    }

    stage ("Docker Build") {
        sh "docker build -t ayselersoz/myapache:1.0.0 ."
    }

    stage ("Docker Push") {
        sh "docker push ayselersoz/myapache:1.0.0"
    }
    }
}
}