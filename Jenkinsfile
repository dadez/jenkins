//use JsonSlurperClassic because it produces HashMap that could be serialized by pipeline
import groovy.json.JsonSlurperClassic

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
        def version = ${app.versions[0].version}
        println version
        echo "version: ${app.versions[0].version}"
    }

    stage('read file as text') {
        script {
            def json = readFile(file:'application.json')
            def data = new JsonSlurperClassic().parseText(json)
            echo "version: ${data.versions[0].version}"
        }
    }
}
