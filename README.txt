# Spring Boot Docker App
Simple Spring Boot REST app for Docker deployment:
- Exposes GET / endpoint
- Build with Maven: mvn package
- Build Docker: docker build -t springboot-docker .
- Run: docker run -p 8080:8080 springboot-docker
// test commit for Jenkins auto build
// trigger test
