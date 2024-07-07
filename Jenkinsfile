pipeline {
    agent {
        label 'ansible_node'
    }

    stages {
        stage("Git Checkout") {
            steps {
                // Checkout your source code repository
                git branch: 'main',
                    url: 'https://github.com/gaman5575/Jenkins-ansible-project.git'
            }
        }

        stage('Verify Ansible packages') {
            steps {
                // Checking Ansible pacakages
                sh 'whereis ansible-playbook'
                sh 'whereis ansible-lint'
            }
        }

        stage('Scaning Playbook') {
            steps {
              // checking playbook syntax and lint
            sh 'ansible-playbook playbook.yaml --syntax-check'
            sh 'ansible-lint playbook.yaml'
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                //Running Ansible playbook
                sh 'ansible-playbook playbook.yaml -i inventory'
            }
        }
    }
    post {
        always {
            // Archive the Ansible Playbook execution logs
            archiveArtifacts '*.log'
        }

        success {
            // Notify Success
            echo 'Ansible Playbook Executed Successfully!'
        }

        failure {
            // Notify Failure Message
            echo 'Ansible Execution Failed!!!!'
        }
    }
}