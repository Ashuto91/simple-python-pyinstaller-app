pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') { 
            steps {
                // Run tests with caching disabled to avoid permission issues
                sh 'pytest --cache-clear --junit-xml=test-reports/results.xml sources/test_calc.py' 
            }
            post {
                always {
                    // Publish test results
                    junit 'test-reports/results.xml' 
                }
            }
        }
    }
}
