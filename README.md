## Deploying In OpenShift
```bash
oc new-build -l 'role=jenkins-slave' https://github.com/masoodfaisal/owasp-zap-openshift.git
```


```groovy
    node('owasp-zap-openshift') {
        
        stage('Scan Web Application') {
            
            def retVal = sh returnStatus: true, script: 'zap-baseline.py -r baseline.html -t https://smeonboarding.apps.ambank.apac.rht-labs.com/sme-application'
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/zap/wrk', reportFiles: 'baseline.html', reportName: 'ZAP Baseline Scan', reportTitles: 'ZAP Baseline Scan'])
            echo "Return value is: ${retVal}"
            
        }
    }
```