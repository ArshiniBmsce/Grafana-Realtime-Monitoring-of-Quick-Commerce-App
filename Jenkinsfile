pipeline {
    agent any
    stages {
        stage('Run Metrics Simulation') {
            steps {
                sh 'docker run -d -p 8000:8000 --name metrics_service my_metrics_image'
            }
        }
        stage('Run Prometheus and Grafana') {
            steps {
                sh '''
                docker run -d --name prometheus -p 9090:9090 \
                  -v $WORKSPACE/prometheus.yml:/etc/prometheus/prometheus.yml \
                  -v $WORKSPACE/alert_rules.yml:/etc/prometheus/alert_rules.yml \
                  prom/prometheus
                docker run -d --name grafana -p 3000:3000 grafana/grafana
                '''
            }
        }
    }
}
