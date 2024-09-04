---
title: Exemple de test des APIs avec RestAssured en Java
date: 2024-08-21 16:44 +0300
categories: [Blogging, Tutorial]
tags: [github-pages,Jekyll,Markdown,TAUTO,API,RestAssured,POST,GET,JAVA]
---
# Welcome to API test wiki!

Ce projet comprend des exemples d'utilisation de REST Assured en Java , avec une classe de service dédiée pour gérer les requêtes REST. 
Voici un exemple de code avec RestAssured en utilisant une classe de service pour effectuer des requêtes GET et POST.

## Configuration Maven
Ajouter la dépendance RestAssured dans votre fichier pom.xml :
```
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>++
    <version>5.1.1</version>
    <scope>test</scope>
</dependency>
```

## Exemple de classe de service
Voici une classe de service dédiée pour gérer les requêtes REST :

```
package org.example.services;
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class RestRequestService {
    private String baseUri;

    public RestRequestService(String baseUri) {
        this.baseUri = baseUri;
        RestAssured.baseURI = baseUri;
    }

    public Response getRequest(String endpoint) {
        return RestAssured
                .given()
                .when()
                .get(endpoint)
                .then()
                .extract()
                .response();
    }

    public Response postRequest(String endpoint, String body) {
        return RestAssured
                .given()
                .header("Content-Type", "application/json")
                .body(body)
                .when()
                .post(endpoint)
                .then()
                .extract()
                .response();
    }
}

```
## Structure du projet
Placez votre fichier JSON attendu dans le répertoire src/test/resources, par exemple expectedResponse.json avec le contenu suivant :
```


```
## Exemple d'utilisation dans un test
Voici comment utiliser cette classe de service dans vos tests :
```
import io.restassured.response.Response;
import org.example.services.RestRequestService;
import org.junit.Test;

import static org.hamcrest.Matchers.equalTo;



public class RestRequestServiceTestPOST {

        private RestRequestService2 restRequestService = new RestRequestService("https://reqres.in/api");

        @Test
        public void testPostRequestWithJsonFile() {
            String jsonFilePath = "src/main/resources/input/payload-post-user-create2.json";


            Response response = restRequestService2.postRequestWithJsonFile("/users", jsonFilePath);

            response.then().statusCode(201)
                    .body("name", equalTo("name13"))
                    .body("job", equalTo("job13"));
            System.out.println("response.getBody().asString()  ==" + response.getBody().asString());
        }
    }
```
## Explications

**RestRequestService :** Cette classe contient deux méthodes pour gérer les requêtes POST en utilisant RestAssured. Elle prend en paramètre une baseUri qui est utilisée pour toutes les requêtes.

**RestRequestServiceTest :** Cette classe de test montre comment utiliser RestRequestService pour effectuer une requête POST. Elle utilise des assertions pour vérifier que les réponses contiennent les données attendues.

Vous pouvez adapter ce code à vos besoins en modifiant les endpoints et les corps de requête pour correspondre à votre API. 

## Additional Resources

[Markdown Guide](https://www.markdownguide.org/cheat-sheet),
[Documentation GitHub](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)


