node {
    stage('Checkout') {
        bat "xcopy /E /exclude:D:\\Workspaces\\vscode_workspace\\gift-shop-monolith\\frontend\\ignore.txt D:\\Workspaces\\vscode_workspace\\gift-shop-monolith\\frontend /Y"
    }
    stage ('Install dependency') {
        bat 'npm install'
    } 
    stage ('Testing Stage') {
        bat 'npx ng test --no-watch --code-coverage'
    }
    stage('Sonar Scanner Coverage') {
        bat "npm run sonar"
    }
    stage('Make Prod Build') {
        bat 'npx ng build --prod --base-href=/frontend/ && cd dist/frontend && jar -cvf frontend.war *'
    }
    stage ('Deploy on this Server') {
        deploy adapters: [tomcat10(credentialsId: 'admin', path: '', url: 'http://localhost:8081')], contextPath: null, war: '**/*.war'
    }
}
