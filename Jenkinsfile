node ("test-it") {
    stage('Check Env') {
        violationDetail = GetViolationDetail("google.com")
        println violationDetail

    }
}

@NonCPS
def GetViolationDetail(url) {
    echo "GetViolationDetail: url = '${url}'"
    
    violationDetailRequest = "curl -H \"Content-type: application/json\" -X GET \"${url}\""
    echo "violationDetailRequest (detail) = '${violationDetailRequest}'"
    violationDetail = sh (returnStdout: true, script: "echo 'Script is running'")
        
    return violationDetail
}

