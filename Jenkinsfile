node {
    stage('Git checkout') {
        git branch: "${params.BRANCH}", url: 'https://github.com/Projet-Automation-Infra-SI-Ynov/Node_exporter'
    }
    // ----------------- Grafana -----------------
    stage('Add Grafana address IP') {
        sh "sed -i 's/IP_GRAFANA/${params.GRAFANA_IP}/g' ./Grafana/grafana.ini"
    }
    stage('Execute playbook for Grafana server') {
        sh "ansible-playbook -i ./Grafana/grafana.ini ./Grafana/grafana.yml"
    }
    // ----------------- Registry -----------------
    stage('Add Docker Registry address IP') {
        sh "sed -i 's/IP_REGISTRY/${params.REGISTRY_IP}/g' ./Registry/registry.ini"
    }
    stage('Execute playbook for Registry server') {
        sh "ansible-playbook -i ./Registry/registry.ini ./Registry/registry.yml"
    }
    // ----------------- K3S -----------------
    stage('Add K3S Master address IP') {
        sh "sed -i 's/IP_MASTER/${params.MASTER_IP}/g' ./K3s-master/k3s-master.ini"
    }
    stage('Execute playbook for k3s master server') {
        sh "ansible-playbook -i ./K3s-master/k3s-master.ini ./K3s-master/k3s-master.yml"
    }
    stage('Add K3S Worker address IP') {
        sh "sed -i 's/IP_WORKER/${params.WORKER_IP}/g' ./K3s-worker/k3s-worker.ini"
    }
    stage('Execute playbook for k3s worker server') {
        sh "ansible-playbook -i ./K3s-worker/k3s-worker.ini ./K3s-worker/k3s-worker.yml"
    }
}