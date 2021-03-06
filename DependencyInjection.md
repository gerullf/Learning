# Inyección de Dependencias
## Definición
Inyección de dependencias (en inglés **Dependecy Injection**) es un **patrón de diseño** en el cual se suministra a una clase los objetos (dependencias) en lugar de ser la propia clase la que los cree. 
El patrón busca establecer un nivel de abstracción por medio de una interfaz pública y remover la dependencia sobre otros componentes supliendo una arquitectura de 'plugin'; aunque el pasar una conexión a una base de datos como un argumento de un método puede ser categorizado como una inyección de dependencia, esta no corresponde a la definición del patrón de diseño.

## Beneficios
Algunos de los beneficios de utilizar la inyección de depencencias son:

**Reduce el acoplamiento**

Dedido a que la clase ya no es responsable de crear la instancia de la dependencia, si la clase de la que depende cambia ya no es necesario actualizar la(s) clase(s) dependiente(s), esto ayuda a facilitar las pruebas, el mentenimiento y la extensión de funcionalidades de ambas clases.

**Simplifica las pruebas**

Se puede simular por medio de mocks el comportamiento de la clase dependiente en distintos escenarios.

## Detrimentos
**Mayor complejidad**

La inyección de dependencias, especialmente la inyección a través de un constructor, implica una mayor complejidad que hace que pronto sea complicado construir objetos en la aplicación y se tenga que recurrir al uso de contenedores de inversión de control.
Adicionalmente, se complica el *debuggeo* ya que hay que rastrear las excepciones generadas hasta la clase que inyecta la dependencia, esto es especialmente notorio en los desarrollos con muchas clases.

## Implementando Inyección de Dependencias
Existen al menos 3 tipos de inyección de dependencias:
1. Inyección por constructor, la dependencia es provista por el contructor de una clase
2. Inyección por *setter*, el cliente expone un método *setter* que el inyector utiliza para inyectar la dependencia
3. Inyección por interfaz, la dependencia provee un método inyector que inyectará la dependencia a cualquier cliente que se le pase. Los clientes deben implementar una interfaz que exponga un método *setter* que acepte la dependencia

### Inyección de Dependencia por Constructor
La clase que recibirá la dependencia la especifica por medio de su constructor, para esto la clase necesita declarar un constructor que incluya todo lo que necesita ser inyectado:
```
class Dependient
{
    private Dependency dependency;
    public Dependient(Dependency _dependency)
    {
        this.dependency = _dependency;
    }
}
```

### Inyección de Dependencia por *Setter*
Para obtener la dependencia, la clase define un método para tal propósito:
```
class Dependient
{
    private Dependency dependency;
    public void setDependency(Dependency _dependency)
    {
        this.dependency = _dependency;
    }
}
```

### Inyección de Dependencia por Interfaz
La tercera técnica involucra el uso de interfaces, con este método se define una interface de se utilizará para llevar a cabo la inyección:
```
public interface iInjectDependency
{
    void InjectDependency(Dependency _dependency)
}
```
Esta interfaz debe ser implementada por cualquier clase que requiera utilizar la dependencia:
```
class Dependient : iInjectDependency
{
    private Dependency dependency;
    public void InjectDependency(Dependency _dependency)
    {
        this.dependency = _dependency;
    }
}
```

## Fuentes
[1] https://en.wikipedia.org/wiki/Dependency_injection

[2] https://blogs.endjin.com/2014/04/understanding-dependency-injection/

[3] http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/dependency_injection.html

[4] http://blog.koalite.com/2016/02/las-ventajas-de-no-usar-inyeccion-de-dependencias/

[5] http://www.dotnettricks.com/learn/dependencyinjection/implementation-of-dependency-injection-pattern-in-csharp

[6] https://martinfowler.com/articles/injection.html
