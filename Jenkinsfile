node('mac') {

    stage('Checkout') {

        // Checkout files.
        checkout([
            $class: 'GitSCM',
            branches: [[name: 'master']],
            doGenerateSubmoduleConfigurations: false,
            extensions: [], submoduleCfg: [],
            userRemoteConfigs: [[
                name: 'github',
                url: 'https://github.com/rajibmitra/time-table.git'
            ]]
        ])

        // Build and Test
        sh 'export HTTP_PROXY=http://10.22.72.223:8080'
        sh 'export HTTPS_PROXY=http://10.22.72.223:8080'
        sh 'export NO_PROXY=127.0.0.1,localhost,.pwcinternal.com,cms,clients,engagements,searchparty,employee,redis'
        
        stage('build'){
        
        sh 'xcodebuild -scheme "TimeTable" -configuration "Debug" build test -destination "platform=iOS Simulator,name=iPhone 6,OS=11.1" -enableCodeCoverage YES | /usr/local/bin/xcpretty -r junit'
        }
        
        stage('test'){
        // Publish test restults.
        step([$class: 'JUnitResultArchiver', allowEmptyResults: true, testResults: 'build/reports/junit.xml'])
    }
    }

     
    
}
