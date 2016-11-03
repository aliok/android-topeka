#!groovy

node{

}

node {
    // Mark the code checkout 'stage'....
    stage 'Stage Checkout'

    // Checkout code from repository and update any submodules
    checkout scm
    // sh 'git submodule update --init'

    stage 'Stage Build'

    //branch name from Jenkins environment variables
    echo "My branch is: ${env.BRANCH_NAME}"

//    def flavor = flavor(env.BRANCH_NAME)
//    echo "Building flavor ${flavor}"

    //build your gradle flavor, passes the current build number as a parameter to gradle
//    sh "./gradlew clean assemble${flavor}Debug -PBUILD_NUMBER=${env.BUILD_NUMBER}"
//    sh "./gradlew clean assembleDebug -PBUILD_NUMBER=${env.BUILD_NUMBER}"
    echo "Gonna build now"
    sh "./gradlew clean assembleDebug"

    stage 'Stage Archive'
    echo "Gonna archive now"
    //tell Jenkins to archive the apks
    step([$class: 'ArtifactArchiver', artifacts: 'App/build/outputs/apk/*.apk', fingerprint: true])

    //stage 'Stage Upload To Fabric'
    //sh "./gradlew crashlyticsUploadDistribution${flavor}Debug  -PBUILD_NUMBER=${env.BUILD_NUMBER}"
}

//// Pulls the android flavor out of the branch name the branch is prepended with /QA_
//@NonCPS
//def flavor(branchName) {
//    def matcher = (env.BRANCH_NAME =~ /QA_([a-z_]+)/)
//    assert matcher.matches()
//    matcher[0][1]
//}