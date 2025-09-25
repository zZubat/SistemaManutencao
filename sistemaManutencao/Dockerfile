# Etapa 1: Build da aplicação com Amazon Corretto
# <--- MUDANÇA AQUI: Usando uma imagem base que não tem limite de download
FROM public.ecr.aws/amazoncorretto/amazoncorretto:21 AS build

# Define diretório de trabalho dentro do container
WORKDIR /app

# Copia todos os arquivos do projeto para o container
COPY . .

# Garante que o mvnw tenha permissão de execução
RUN chmod +x mvnw

# Build do projeto sem rodar testes
RUN ./mvnw clean package -DskipTests

# Etapa 2: Imagem final para rodar a aplicação
# <--- MUDANÇA AQUI: Usando a mesma imagem base, garantindo consistência e corrigindo o erro "not found"
FROM public.ecr.aws/amazoncorretto/amazoncorretto:21

WORKDIR /app

# Copia o JAR gerado na etapa de build
COPY --from=build /app/target/*.jar app.jar

# Expõe a porta padrão do Spring Boot
EXPOSE 8080

# Comando para rodar a aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]