# Exceções em Java
## O que são Exceções?

Em Java, uma exceção é um evento que ocorre durante a execução de um programa e interrompe o fluxo normal de instruções. Elas são usadas para lidar com erros ou situações excepcionais, como divisão por zero, acesso a um índice inválido em um array, ou tentativa de abrir um arquivo que não existe.

As exceções são representadas por classes no Java, e todas herdam da classe base Throwable. As duas principais subclasses são:

 -   Exception: Para situações que podem ser tratadas (ex: IOException, NullPointerException).

-  Error: Para problemas graves que geralmente não podem ser recuperados (ex: OutOfMemoryError).

### Tipos de Exceções

  #### Exceções Verificadas (Checked Exceptions):

        São exceções que o compilador obriga você a tratar ou declarar.

        Exemplos: IOException, SQLException.

        Herdam de Exception, mas não de RuntimeException.

 ####   Exceções Não Verificadas (Unchecked Exceptions):

        São exceções que não precisam ser explicitamente tratadas.

        Exemplos: NullPointerException, ArithmeticException, ArrayIndexOutOfBoundsException.

        Herdam de RuntimeException.

#### Erros (Errors):

        Representam problemas graves que geralmente não podem ser recuperados.

        Exemplos: OutOfMemoryError, StackOverflowError.

        Herdam de Error.

***
## Estrutura Básica de Tratamento de Exceções

Em Java, o tratamento de exceções é feito usando os blocos try, catch, finally e a palavra-chave throw.
Bloco try-catch

    try {
    // Código que pode gerar uma exceção
    int resultado = 10 / 0; // Isso lançará uma ArithmeticException
    } catch (ArithmeticException e) {
    // Tratamento da exceção
    System.out.println("Erro: Divisão por zero!");
    }

### Bloco finally

O bloco finally é executado independentemente de uma exceção ter sido lançada ou não. É útil para liberar recursos, como fechar arquivos ou conexões de banco de dados.


    try {
    // Código que pode gerar uma exceção
    } catch (Exception e) {
    System.out.println("Exceção capturada: " + e.getMessage());
     } finally {
    System.out.println("Bloco finally executado.");
     }

Palavra-chave throw

Usada para lançar explicitamente uma exceção.


    if (idade < 18) {
        throw new IllegalArgumentException("Idade mínima não atingida!");
    }

     // Palavra-chave throws

Usada para declarar que um método pode lançar uma exceção.

    public void abrirArquivo(String caminho) throws IOException {
    // Código que pode lançar uma IOException
    }

## Exemplo Completo

### exemplo que combina todos os conceitos:

    import java.io.FileInputStream;
    import java.io.FileNotFoundException;
    import java.io.IOException;

    public class ExemploExcecoes {

      public static void main(String[] args) {
          try {
              lerArquivo("arquivo.txt");
          } catch (FileNotFoundException e) {
              System.out.println("Erro: Arquivo não encontrado!");
          } catch (IOException e) {
              System.out.println("Erro de leitura: " + e.getMessage());
          } finally {
            System.out.println("Processamento concluído.");
          }
      }

      public static void lerArquivo(String caminho) throws FileNotFoundException, IOException {
          FileInputStream arquivo = new FileInputStream(caminho);
          // Simulação de leitura do arquivo
          arquivo.close();
      }
    }

## Boas Práticas

   - Capture exceções específicas em vez de usar catch (Exception e) para evitar mascarar problemas.

   -  Libere recursos no bloco finally ou use a estrutura try-with-resources (disponível a partir do Java 7).

  - Documente exceções usando a palavra-chave throws em métodos que podem lançar exceções.

  -  Evite capturar e ignorar exceções sem tratamento adequado.

- Try-with-Resources

A partir do Java 7, você pode usar a estrutura try-with-resources para garantir que recursos como arquivos, conexões de banco de dados, etc., sejam fechados automaticamente.
java
Copy

    try (FileInputStream arquivo = new FileInputStream("arquivo.txt")) {
          // Código para ler o arquivo
    } 
    catch (IOException e) {
    System.out.println("Erro de leitura: " + e.getMessage());
    }
*** 
# Conclusão

O tratamento de exceções é uma parte essencial do desenvolvimento em Java. Ele permite que seu programa lide com erros de forma elegante e continue funcionando mesmo em situações inesperadas. Use este guia como referência para implementar boas práticas de tratamento de exceções em seus projetos.
Referências

-  Documentação Oficial do Java
- Livro: "Effective Java" por Joshua Bloch.
