// node ("test-it") {
//     stage('Check Env') {
//         violationDetail = GetViolationDetail("google.com")
//         println violationDetail

//     }
// }

// @NonCPS
// def GetViolationDetail(url) {
//     echo "GetViolationDetail: url = '${url}'"
    
//     violationDetailRequest = "curl -H \"Content-type: application/json\" -X GET \"${url}\""
//     echo "violationDetailRequest (detail) = '${violationDetailRequest}'"
//     violationDetail = sh (returnStdout: true, script: "echo 'Script is running'")
        
//     return violationDetail
// }

import groovy.json.JsonOutput

node ('!master') { 
    boolean recursiveSubmoduleBool=false 
    syncSourceFromGit("https://github.com/abowman32/test-scm") 
    showChangeLogs() 
}

@NonCPS 
def showChangeLogs() { 
    def changeLogSets = currentBuild.rawBuild.changeSets 
    for (int i = 0; i < changeLogSets.size(); i++) { 
        def entries = changeLogSets[i].items 
        for (int j = 0; j < entries.length; j++) { 
            def entry = entries[j] 
            echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}" 
        } 
    } 
}//showChangeLogs

def syncSourceFromGit(gitrepo,timeOut=10) { 
    checkout([$class: 'GitSCM', branches: [[name: "master"]], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'RelativeTargetDirectory', 
        [$class: 'SubmoduleOption', 
        disableSubmodules: false, parentCredentials: false, 
        reference: '', trackingSubmodules: false], 
        [timeout: timeOut], ], 
        submoduleCfg: [], 
        userRemoteConfigs: []
    ]])

} 