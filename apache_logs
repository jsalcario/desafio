pipeline {
    agent any
    parameters {
        string(name: 'clave', defaultValue:'', description: 'Ingresa la palabra clave:')
        string(name: 'http', defaultValue:'', description: 'Ingresa la respuesta HTTP:')
            }
        }
        stage('Ejecutar comandos') {
            steps {
                echo 'obteniendo url...'
                sh 'curl -s --output apache_logs https://raw.githubusercontent.com/elastic/examples/master/Common%20Data%20Formats/apache_logs/apache_logs'
                echo 'Buscando la palabra clave...'
                sh 'grep -E -c "${params.clave}.*${params.http}|${params.http}.*${params.clave}" apache_logs'                
            }
        }
        stage('Resultados') {
            steps {
                echo 'Resultados:'
                script {
                    def resultado = readFile('apache_logs').trim()
                    echo "La palabra clave ${params.clave} aparece ${resultado} veces en la respuesta HTTP ${params.http}"
                }
            }
        }
