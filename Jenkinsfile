node {
    echo 'Hello World'

    stage('write file') {
        writeFile encoding: 'UTF-8', file: 'application.json', text: '''{
              "application": "bit-sles-tomcat",
              "description": "deployint last version of component",
              "applicationProcess": "deploy-monit",
              "environment": "ATST",
              "onlyChanged": "true",
              "properties": {
                "Prop1": "value1"
              },
              "versions": [
                {
                  "version": "5.22.0-0",
                  "component": "bit-sles-monit"
                }
              ]
            }'''
        sh 'ls -l'
    }

    stage('read file') {
        def app = readJSON file:'application.json'
        def version = app.versions[0].version
        // echo "version: ${app.versions[0].version}"
            timeout(1) {
                waitUntil {
                    version == "5.22.0-0"
                }
            println version
            }
    }
}
