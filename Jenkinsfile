pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
            securityContext:
                fsGroup: 1000
            containers:
            - name: node
              image: node:18-alpine
              command:
              - sleep
              args:
              - 99d
            - name: kubectl
              image: gcr.io/cloud-builders/kubectl
              command:
              - sleep
              args:
              - 99d
              volumeMounts:
              - name: docker-run
                mountPath: /var/run
            volumes:
            - name: docker-run
              hostPath:
                path: /var/run
                type: Directory
''' 
    }
   }
stages{
    stage('test'){
        steps{
            container('node'){
                script{
                    sh script: 'node --version'
                    sh script: 'pwd'
                }

            }
        }
    }
}
}