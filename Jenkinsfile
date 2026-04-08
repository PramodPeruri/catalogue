@Library('jenkins-shared-library') 

def configMap = [
    project: "roboshop"
    component: "catalogue"
]


echo "Going to Execute"
// if branch is not equal to main, then run CI pipeline
if ( ! env.BRANCH_NAME.equalsIgnoreCase('main') ){
    nodeJSEKSPipeline(configMap)
}
else {
    echo "Please follow the CR process"

}