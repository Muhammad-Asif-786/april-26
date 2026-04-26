node {
    def appDir = '/var/www/april-26'

    stage('Clean Workspace') {
        echo 'Clean jenkins workspace...'
        deleteDir()
    }
    stage('Clone Repository') {
        echo 'Cloning the repository from git...'
        git (
            branch: 'main',
            url: 'https://github.com/Muhammad-Asif-786/april-26.git'
        )
    }
    stage('Deploy to Ec2') {
        echo 'Deploying to EC2 instance...'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 5173/tcp || true
            npm run dev
        """
    }
}