# Dockerfile para a aplicação Backend Java/Maven

# Estágio de Build usando Maven
FROM maven:3.9.7-eclipse-temurin-17 AS builder

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia o arquivo de configuração do Maven (pom.xml) da pasta 'api' do contexto de build
# para o diretório de trabalho /app na imagem.
COPY api/pom.xml .

# Copia o diretório .mvn (wrapper do Maven) da pasta 'api' do contexto de build
# para o diretório .mvn dentro de /app na imagem.
# Certifique-se de que existe um espaço entre 'api/.mvn/' (origem) e '.mvn/' (destino).
COPY api/.mvn/ .mvn/

# Copia o código-fonte (diretório src) da pasta 'api' do contexto de build
# para o diretório src dentro de /app na imagem.
# Certifique-se de que existe um espaço entre 'api/src/' (origem) e 'src/' (destino).
COPY api/src/ src/

# Executa o build do Maven.
# O comando 'clean package' limpa builds anteriores e empacota a aplicação.
# '-DskipTests' pula a execução dos testes para acelerar o build (remova se precisar rodar testes no build).
RUN mvn clean package -DskipTests

# Estágio Final usando uma imagem OpenJDK leve
FROM openjdk:17-jdk-slim

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia o artefato .jar construído do estágio 'builder' (de /app/target/*.jar)
# para o diretório de trabalho /app na imagem final, nomeando-o como app.jar.
COPY --from=builder /app/target/*.jar app.jar

# Define o comando que será executado quando o container iniciar.
# Executa a aplicação Java empacotada no app.jar.
ENTRYPOINT ["java","-jar","app.jar"]
