#!/usr/bin/groovy
@Library('github.com/hrishin/osio-pipeline@config-map')_

osio {
    config runtime: 'node'

    ci {
        def app = processTemplate()
        build app: app
    }

    cd {
/*
      def resources = processTemplate(params: [
        release_version: "1.0.${env.BUILD_NUMBER}"
      ])

      echo "-------------- build default ----------------------------"
      build resources: resources
*/

      def cm = loadResources(file: ".openshiftio/resource.configmap.yaml")
      echo "$cm"
      def role = loadResources(file: ".openshiftio/resource.roles.yaml")
      echo "$role"

/*
      echo "-------------- deploy -----------------------------------"
      deploy resources: [resources,  cm, role], env: 'stage'

      // deploy app: app, env: 'run', approval: 'manual'
      echo "---------------------------------------------------------"
*/
    }
}

