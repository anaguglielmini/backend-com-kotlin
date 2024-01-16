# Aprendendo Kotlin e Sua Documentação Oficial

## Introdução ao Kotlin

- Linguagem recente mas madura;
- Interoperável com Java e outras linguagens;
- Virou linguagem oficial para desenvolvimento mobile pela Google;
- Não está mais atrelada apenas com o desenvolvimento de aplicativos mobile;
- Oferece muitas opções para reutilizar código entre várias plataformas;
- Está ampliando seus "horizontes";
- O Kotlin está incluso no **IntelliJ IDEA** e **Android Studio** mas pode ser utilizado através do [Kotlin Playground](https://play.kotlinlang.org/).

**Documentação**

- [Documentação Oficial - kotlinlang.org](https://kotlinlang.org/)
- [Introdução ao Kotlin](https://kotlinlang.org/docs/getting-started.html)

## Introdução Prática à Linguagem de Programação Kotlin

[Learn Kotlin by Example](https://play.kotlinlang.org/byExample/overview)

**Hello World**

```
// Definindo o pacote (muito comum para organização do código)
// site ao contrário e depois o nome desse pacote
package me.dio.helloworld 

// Ponto de entrada de um código Kotlin, definido pela função [main]
fun main() {
    // Imprime na saída padrão um texto, pulando linha por causa do ln
    // se fosse apenas print ele não pularia a linha
    println("Hello, World!")
    print("Exemplo de que")
    print("Não pulou a linha")
}
```

**Funções**
- **Valores de Parâmetro Padrão e Argumentos Nomeados:**

```
// função que recebe como parâmetro um texto, alfanumérico, para realizar as operações dentro dela
// um pouco redundante esse função pois é possível chamar um println de forma mais simples
// mas serve como exemplo de como criar um parâmetro
fun printMessage(message: String): Unit {                               
    println(message)
}

// função que imprime uma mensagem com um prefixo
// Info é um prefixo padrão para caso não seja especificado 
fun printMessageWithPrefix(message: String, prefix: String = "Info") {  
    // interpolação de strings
    // método mais simples de concatenar 
    println("[$prefix] $message")
}

// função de soma
// existe um retorno explicíto, como int (inteiro)
fun sum(x: Int, y: Int): Int {                                          
    return x + y
}

// inline function: está sendo definida em apenas uma linha
// função de multiplicação
// retorno declarado implicitamente
fun multiply(x: Int, y: Int) = x * y                                    

// função principal que irá executar as funções anteriores passando os valores para que elas funcionem 
fun main() {
    printMessage("Hello")  

    // sem definir o prefixo
    printMessageWithPrefix("World")

    // com prefixo definido na ordem que foi criado na função
    // message e depois prefix
    printMessageWithPrefix("World", "Hello") 

    // com prefixo definido em outra ordem pois conseguimos definir quem é quem
    printMessageWithPrefix(prefix = "Hello", message = "World") 

    // chamando as outras duas funções de conta          
    println(sum(1, 2))                                                  
    println(multiply(2, 4))                                            
}
```

- **Parâmetros vararg**
Varargs permitem que você passe qualquer número de argumentos, desde que respeitem o tipo especificado (string, int, etc) separando-os com vírgulas.
```
// função principal
// note que as funções podem ser criadas dentro dela 
// sendo assim possível criar um tipo de hierarquia de funções
fun main() {

    // função que pega todas as mensagens e printa elas 
    // chama messages de m para simplificar
    fun printAll(vararg messages: String) {                            
        for (m in messages) println(m)
    }
    // inserindo strings 
    printAll("Hello", "Hallo", "Salut", "Hola", "你好", "Olá")                 
    
    // mesma coisa mas definindo um prefixo 
    fun printAllWithPrefix(vararg messages: String, prefix: String) {  
        for (m in messages) println(prefix + m)
    }
    printAllWithPrefix(
            "Hello", "Hallo", "Salut", "Hola", "你好",
            prefix = "Greeting: "                                          
    )

    // função que chama outra que também é um vararg
    fun log(vararg entries: String) {
        // necessário o * para identificar esses dados como vararg e não como array
        // nos outros casos estava como array
        printAll(*entries)                                             
    }
    log("Hello", "Hallo", "Salut", "Hola", "你好")

}
```

**Variáveis var e val**
- var é uma variável, mutáve;
- val é um valor imutável.
```
fun main() {

    // aqui também não há a necessidade de especificar como string
    var a: String = "initial"  
    println(a)
    a = "final"
    // tipo sendo explicito como inteiro 
    val b: Int = 1             
    println(b)

    // inferencia de código, ele sabe que é um inteiro
    val c = 3                  
    println(c)

    println(a)
}
```

**Null Safety - Nulidade**
Segurança Nula: necessidade de deixar explicito se a variável pode receber valores nulos ou não.

```
fun main() {

    // declarando uma variável que não pode ser nula
    // ao declarar ela como string, o kotlin entende que será uma string válida
    var neverNull: String = "This can't be null"            
    
    // vamos tentar atribuir um valor nulo a ela
    // mas demonstrará um erro 
    neverNull = null                                        
    
    // nesse caso é possível aceitar nulo por causa o "?"
    var nullable: String? = "You can keep a null here"      
    nullable = null                                         
    
    // mesmo sem ter o tipo especificado como string
    // o código entende que com o valor sendo atribuido (inferência)
    // essa variável não pode ser nula
    var inferredNonNull = "The compiler assumes non-null"   
    inferredNonNull = null                                  
    
    // função que está esperando como parâmetro um valor não nulo 
    fun strLength(notNull: String): Int {                   
        return notNull.length
    }
    
    strLength(neverNull)                                    
    strLength(nullable)                                     

}
```

**Classes**

```
// declarando classe chamada Customer
class Customer                                  

// declarando classe Contato com construtor personalizado
// o meio de criar um objeto Contact é atribuindo um id imutável (val)
// e um e-mail mutável (var)
class Contact(val id: Int, var email: String)   

fun main() {

    // criando instância da classe customer, mas ela não tem operação/atributo
    val customer = Customer()                   
    
    // atribuindo valores 
    val contact = Contact(1, "mary@gmail.com")  

    println(contact.id)  
    println(contact.email)                       
    contact.email = "jane@gmail.com"            
    println(contact.email)                       
}
```

**Generics**
Flexibilidade na tipagem das informações. Muito comum em coleções como listas.

- **Classes Genéricas**

```
// classe que recebe como parâmetro qualquer valor
// "E" é um parâmetro genérico 
class MutableStack<E>(vararg items: E) {              

  private val elements = items.toMutableList()

// funções de ação dentro da pilha
  fun push(element: E) = elements.add(element)        

  fun peek(): E = elements.last()                    

  fun pop(): E = elements.removeAt(elements.size - 1)

  fun isEmpty() = elements.isEmpty()

  fun size() = elements.size

// converte a pilha para texto
  override fun toString() = "MutableStack(${elements.joinToString()})"
}


fun main() {
    // adicionando valores na pilha
  val stack = MutableStack(0.62, 3.14, 2.7)
  // adiciona mais um por fora
  stack.push(9.87)
  // imprime a pilha
  println(stack)

// pegando o último elemento da pilha, o que está em cima
  println("peek(): ${stack.peek()}")
  println(stack)

// pegando e removendo o último item da pilha até não ter mais
  for (i in 1..stack.size()) {
    println("pop(): ${stack.pop()}")
    println(stack)
  }
}
```

- **Funções Genéricas**

```
class MutableStack<E>(vararg items: E) {              

  private val elements = items.toMutableList()

  fun push(element: E) = elements.add(element)        

  fun peek(): E = elements.last()                     

  fun pop(): E = elements.removeAt(elements.size - 1)

  fun isEmpty() = elements.isEmpty()

  fun size() = elements.size

  override fun toString() = "MutableStack(${elements.joinToString()})"
}

// função que cria uma nova pilha mutável quando for chamada
fun <E> mutableStackOf(vararg elements: E) = MutableStack(*elements)

fun main() {
  val stack = mutableStackOf(0.62, 3.14, 2.7)
  println(stack)
}
```