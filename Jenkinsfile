 node("master") {

     stage("Deploy"){
        checkout scm
        sh '''
            SERVICES=$(docker service ls --filter name=viz --quiet | wc -l)
            if [[ "$SERVICES" -eq 0 ]]; then
                docker service create \
                    --name=viz \
                    --publish=5000:8080/tcp \
                    --constraint=node.role==manager \
                    --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
                    dockersamples/visualizer
            else
                docker service update --image dockersamples/visualizer viz
            fi
        '''
    
     }
 }