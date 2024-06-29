# Desafio Dio - Redução dos Custos em Farmácias com AWS



**Projeto - Sistema de Eleição Usando o Quarkus Framework**



O Quarkus é um framework Java moderno e de alto desempenho projetado para desenvolver aplicações nativas em nuvem. Este projeto fornece uma estrutura abrangente para construir um sistema de eleição usando o Quarkus.



### **Requisitos**

- Java 11 ou superior
- Quarkus
- Banco de dados (por exemplo, PostgreSQL, MySQL)



### **Estrutura do Projeto**

O projeto será estruturado em vários módulos, incluindo:



- **Módulo de API:** Fornece uma API REST para gerenciar candidatos, votos e resultados.
- **Módulo de Banco de Dados:** Gerencia a persistência de dados usando um banco de dados relacional.
- **Módulo de Segurança:** Implementa autenticação e autorização.
- **Módulo de Interface do Usuário:** Fornece uma interface do usuário básica para interagir com o sistema.



### **Implementação**



### **Módulo de API**

java



```java
@Path("/api/candidates")
public class CandidateResource {

    @GET
    public List<Candidate> getAllCandidates() {
        return candidateService.getAllCandidates();
    }

    @POST
    public Candidate createCandidate(Candidate candidate) {
        return candidateService.createCandidate(candidate);
    }

    // ... outros métodos
}
```



### **Módulo de Banco de Dados**

java



```java
@Entity
@Table(name = "candidates")
public class Candidate {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String party;

    // ... outros campos
}
```



### **Módulo de Segurança**

java



```java
@ApplicationPath("/api")
public class RestApplication extends Application {

    @Override
    public Set<Class<?>> getClasses() {
        return new HashSet<>(Arrays.asList(
                CandidateResource.class,
                JwtTokenFilter.class
        ));
    }
}
```



java



```java
public class JwtTokenFilter implements ContainerRequestFilter {

    @Override
    public void filter(ContainerRequestContext requestContext) throws IOException {
        String authorizationHeader = requestContext.getHeaderString("Authorization");
        if (authorizationHeader != null && authorizationHeader.startsWith("Bearer ")) {
            String token = authorizationHeader.substring("Bearer ".length());
            try {
                Jwts.parser().setSigningKey(privateKey).parseClaimsJws(token);
            } catch (SignatureException e) {
                requestContext.abortWith(Response.status(Response.Status.UNAUTHORIZED).build());
            }
        }
    }
}
```



### **Módulo de Interface do Usuário**



```plaintext
<!DOCTYPE html>
<html>
<head>
    <title>Sistema de Eleição</title>
</head>
<body>
    <h1>Candidatos</h1>
    <ul>
        <li>Candidato 1</li>
        <li>Candidato 2</li>
        <li>Candidato 3</li>
    </ul>
</body>
</html>
```



### **Conclusão**

Este projeto fornece uma base abrangente para construir um sistema de eleição usando o Quarkus Framework. Ele aborda aspectos essenciais como gerenciamento de API, persistência de dados, segurança e interface do usuário. Ao implementar essas estratégias, os desenvolvedores podem criar sistemas de eleição robustos e escaláveis que atendam aos requisitos específicos de suas aplicações.

