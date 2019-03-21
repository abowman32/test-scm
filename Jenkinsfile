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
    println changeLogSets.size()
    for (int i = 0; i < changeLogSets.size(); i++) { 
        def entries = changeLogSets[i].items 
        println entries.toString()
        for (int j = 0; j < entries.length; j++) { 
            def entry = entries[j] 
            println "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}" 
        } 
    } 
}//showChangeLogs

def syncSourceFromGit(gitrepo) { 
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/abowman32/test-scm']]])

} 