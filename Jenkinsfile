node {
    
    // Install the desired Go version
    def root = tool name: '1.12.1', type: 'go'
 
    // Export environment variables pointing to the directory where Go was installed
    withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        stage('Checkout'){
            echo 'Checking out SCM'
            git 'https://github.com/prongbang/go-testcov'
        }
        
        stage('Pre Test'){
            echo 'Pulling Dependencies'
    
            sh 'go version'
            sh 'go get -u golang.org/x/lint/golint'
            sh 'export GO111MODULE=on'
        }
        
        stage('Test'){
            echo 'Testing'
            
            sh 'pwd'
        }
    }
}