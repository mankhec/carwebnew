node ('ubuntu-Appserver')
{

def app
stage('Cloning Git')
{
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
}

stage('Build-and-Tag')
{
    /* This builds the actual image;
        * this is synonymous to docker build on the command line */
    app = docker.build('kevenmang/car_docker_repo')
}

stage('Post-to-dockerhub')
{
    /* Push to dockerhub */
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
        app.push('latest')
    }
}

stage('Deploy')
{
    sh 'docker-compose down'
    sh 'docker-compose up -d'
}

}