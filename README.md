# ActivitePratique1-Partie2

A noter qu'il existe deux types de développement
# developpement classique

  ``` java  
          public class Calcul()
          {
            public doubke somme(double a, double b)
            {
               return a+b;
            }
          }
     
          public class CalculTest()
          {
            @Test 
            public void testSomme(){
              double a=5;
              double b=8;
              double exp=a+b;
              Calcul c= new Calcul();
              double rest= c.somme(a,b);
              assertEqual(exp,rest);
            }
          }
       ```

## developpement  basé sur TDD

        ``` java 
        
          public class TestCalcul()
          {
            @Test 
            public void testSomme(){
              double a=5;
              double b=8;
              double exp=a+b;
              Calcul c= new Calcul(); 
              double rest= c.somme(a,b);
              assertEqual(exp,rest);
            }
          }
          
          public class Calcul()
          {
            public doubke somme(double a, double b)
            {
               return 0; // votre travaill est seulement de coder la fonction.
            }
          }
       ```

## FrameWork Spring 
### Les dépandances ```pom.xml```
Dans «External librairies» on a téléchargé 3 jars :
1. Spring core
2. Spring context
3. Spring beans
Ces jars vont être utilisés par Spring.
On utilisant Spring pour injecter les dépendances automatiquement dans le fichier ```pom.xml```: 
``` xml
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.20</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.16</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>5.3.18</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```
 
 ### XML
 ``` java
 public class PresentationSpringXML {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        Imetier imetier =(Imetier) context.getBean("metier");
        System.out.println(imetier.calcul());
        IDao iDao = (IDao) context.getBean("dao");
        System.out.println(iDao.getdate());
    }
}
```
La structure de fichier ```applicationContext.xml```
Le fichier xml de configuration de spring, dans la balise « beans » on déclare les instances qu’on a besoin avec ‘id’ est le nom de chaque instance, et ‘class’ le nom de la classe, et pour injecter la dépendance il y a la balise « property » avec un ‘name’ nom de l’objet et ‘ref’ la référence vers quelle instance :
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="dao" class="ma.enset.ext.DaoImplVWeb"></bean>
    <bean id="metier" class="ma.enset.metier.MetierImpl">
        <property name="dao" ref="dao"></property>
        <!--constructor-arg ref="dao"></constructor-arg-->
    </bean>
</beans>
```
### Annotation
``` java
public class PresSpringAnnotation {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext("ma.enset.dao","ma.enset.metier","ma.enset.ext");
        Imetier imetier = (Imetier) context.getBean("metier");
        System.out.println(imetier.calcul());
        IDao iDao = (IDao) context.getBean("dao");
        System.out.println(iDao.getdate());
    }
}
```
## Maven 
Maven : est un outil n’est pas d’un framework, qui permit l’automatisation des processus de développement d’un projet java, il utilise un paradigme connu sous le nom de POM (Project Object Model).
Principe : à chaque fois on ajoute une dépendance au fichier xml ```pom.xml```, il va  chercher dans le ```repository local``` s’il en trouve il va les utiliser, sinon il va se connecter à l’internet et il va télécharger les dépendances déclarées.
### Les commandes de Maven
- ```mvn compile``` ->  compile le code source du projet.
- ```mvn test``` ->  parcourir le projet et à chaque fois il trouve un test unitaire il va l’exécuter, puis il montre qui sont les tests réussit et qui ne sont pas.
- ```mvn package``` ->  exécute la commande ```mvn compile``` et ```mvn test``` puis archive le projet maven dans archive (.jar / .war).
- ```mvn install``` ->  exécute la commande ```mvn compile``` et ```mvn test``` puis elle installe le projet dans le repository local pour l’utiliser au cas de besoin.
- ```mvn deploy``` ->  déployer un projet vers un serveur.
- ```mvn site``` ->  générer un site de documentation.

Dans cette partie, nous avons étudier l'injection des dépendance et l'inversion de contrôle avec instation dynamique et statique, Sprig XML et annotation et finalement avec le framework Spring (XML et Annotation).
