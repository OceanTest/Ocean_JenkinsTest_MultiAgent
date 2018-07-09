def testnode1 = env.testnode1
def testnode2 = env.testnode2
def Nodelist = [
    [name : testnode1], 
    [name : testnode2]
]

def Tasks = [:]

node('slave1'){
    // Mark the code checkout 'stage'....
    stage('Checkout'){
        // Get some code from a GitHub repository
        git([url: 'https://github.com/OceanTest/Ocean_JenkinsTest.git', branch: 'master'])
        
    }
    // Mark the code GetParameter 'stage'....
    stage('GetParameterviaEnvironment'){
    // Run the program
        Nodelist.each{Node -> Tasks["$Node.name"] = {echo "$Node.name" }}
    }
    
    stage('GetParameterwithBuild'){
        // Script //        
        echo "${params.Greeting} World!"          
    }
    // Mark the code Run 'stage'....
}

stage('Test') {
    parallel linux1: {
        node('slave1') {
            echo "${params.Greeting} World!"
        }
    },
    windows: {
        node('ocean_windows_testnode') {
            echo "${params.Greeting} World!"
        }
    }
}
