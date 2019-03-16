node {
    
    // Install the desired Go version
    def root = tool name: '1.12.1', type: 'go'
 
    // Export environment variables pointing to the directory where Go was installed
    withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        stage('Checkout'){
            echo 'Checking out SCM'
            git 'https://github.com/prongbang/golang-ci-jenkins'
        }
        
        stage('Pre Test'){
            echo 'Pulling Dependencies'
    
            sh 'go version'
            sh 'go get -u golang.org/x/lint/golint'
            sh 'export GO111MODULE=on'
        }
        
        stage('Unit Test'){
            echo 'Testing'
            
            sh 'go test -cover -v ./...'
        }

        stage('Coverage Test'){
            echo 'Testing'
            
            sh 'go test -cover ./... -coverprofile=cover.out'
            sh 'go tool cover -html=cover.out -o coverage.html'
            publishHTML (target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: './',
                reportFiles: 'coverage.html',
                reportName: "Test Coverage Report"
            ])
        }
    }
}