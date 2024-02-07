#!groovy
@Library('roboshop-jenkins-shared-library')_

def configMap = [
    application: "nodejs",
    component: "catalogue"
]

if(! env.BRANCH_NAME.equalsIgnoreCase('master')){
    pipelineDecision.decidePipeline(configMap)
}else{
    echo "This is PRODUCTION, deal with CR process"
}