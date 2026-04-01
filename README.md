# Lista01-Cantina
O sistema da cantina foi melhorado aplicando algumas heurísticas de Nielsen para tornar a experiência do usuário mais fácil e segura.

Primeiramente, foi aplicada a visibilidade do status do sistema, pois o programa mostra mensagens claras informando o que está acontecendo, como erros de digitação ou confirmação do pedido.

Também foi utilizado o controle e liberdade do usuário, permitindo que ele cancele a operação a qualquer momento ou confirme o pedido antes de finalizar, evitando decisões forçadas.

Outra heurística aplicada foi a prevenção de erros, já que o sistema valida as entradas do usuário, impedindo que letras sejam digitadas no lugar de números ou que valores inválidos sejam aceitos.

Por fim, foi aplicado o princípio de reconhecimento em vez de memorização, pois o sistema exibe a lista de produtos na tela, evitando que o usuário precise decorar códigos.

Dessa forma, o sistema se torna mais intuitivo, reduz erros e melhora a interação com o usuário. 

CÓDIGO:

using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Dictionary<int, string> produtos = new Dictionary<int, string>()
        {
            {1, "Coxinha"},
            {2, "Pastel"},
            {3, "Suco"},
            {4, "Refrigerante"}
        };

        int codigo = 0;
        int quantidade = 0;

        Console.WriteLine("=== Sistema da Cantina ===");

        // MOSTRAR PRODUTOS (Reconhecimento)
        Console.WriteLine("Produtos disponíveis:");
        foreach (var p in produtos)
        {
            Console.WriteLine($"{p.Key} - {p.Value}");
        }

        // LOOP PARA CÓDIGO (Prevenção de erro)
        while (true)
        {
            Console.Write("\nDigite o código do produto (ou 0 para cancelar): ");
            string input = Console.ReadLine();

            if (!int.TryParse(input, out codigo))
            {
                Console.WriteLine("⚠ Entrada inválida! Digite um número.");
                continue;
            }

            if (codigo == 0)
            {
                Console.WriteLine("Pedido cancelado.");
                return;
            }

            if (!produtos.ContainsKey(codigo))
            {
                Console.WriteLine("⚠ Produto não existe.");
                continue;
            }

            break;
        }

        // LOOP PARA QUANTIDADE
        while (true)
        {
            Console.Write("Digite a quantidade: ");
            string input = Console.ReadLine();

            if (!int.TryParse(input, out quantidade) || quantidade <= 0)
            {
                Console.WriteLine("⚠ Quantidade inválida.");
                continue;
            }

            break;
        }

        // CONFIRMAÇÃO (Controle do usuário)
        Console.WriteLine($"\nVocê pediu: {produtos[codigo]} x{quantidade}");
        Console.Write("Confirmar pedido? (S/N): ");
        string confirmacao = Console.ReadLine().ToUpper();

        if (confirmacao == "N")
        {
            Console.WriteLine("Pedido cancelado. Reinicie para novo pedido.");
            return;
        }

        // STATUS DO SISTEMA
        Console.WriteLine("\n✅ Pedido confirmado com sucesso!");
    }
}
