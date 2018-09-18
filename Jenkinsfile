#!/usr/bin/groovy
@Library('github.com/hrishin/osio-pipeline@config-map')_

osio {
    config runtime: 'node'

    ci {
        def app = processTemplate()
        build app: app
    }

    cd {
      def cm = loadResources(file: ".openshiftio/resource.configmap.yaml")

      echo "$cm"

      def resources = processTemplate(params: [
        release_version: "1.0.${env.BUILD_NUMBER}"
      ])

      echo "-------------- build default ----------------------------"
      build resources: resources
      echo "-------------- build separate ----------------------------"
      build resources: [
        [ BuildConfig: resources.BuildConfig],
        [ImageStream: resources.ImageStream],
      ]


      echo "-------------- deploy -----------------------------------"
      deploy resources: resources + cm, env: 'stage'

      // deploy app: app, env: 'run', approval: 'manual'
      echo "---------------------------------------------------------"
    }
}

