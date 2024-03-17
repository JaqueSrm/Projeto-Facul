# Projeto-Facul
//Controle de estoque em C#

using System;
using System.Collections.Generic;

class Program
{
    class Eletronico
    {
        public string Opcao { get; set; }
        public double Preco { get; set; }
        public string Produto { get; set; }
        public int Estoque { get; set; }

        public Eletronico(string opcao, double preco, string produto, int estoque)
        {
            Opcao = opcao;
            Preco = preco;
            Produto = produto;
            Estoque = estoque;
        }

        public override string ToString()
        {
            return $"Eletrônico: {Produto} (Opção: {Opcao}, Preço: {Preco:C}, Estoque: {Estoque})";
        }
    }

    class EstoqueEletronicos
    {
        private List<Eletronico> eletronicos = new List<Eletronico>();

        public void AdicionarEletronico(Eletronico eletronico)
        {
            eletronicos.Add(eletronico);
            Console.WriteLine("Eletrônico adicionado!");
            Console.WriteLine(eletronico);
        }

        public void ListarEletronicos()
        {
            if (eletronicos.Count == 0)
            {
                Console.WriteLine("Nenhum eletrônico cadastrado.");
            }
            else
            {
                Console.WriteLine("Lista de Eletrônicos e Estoque:");
                foreach (var eletronico in eletronicos)
                {
                    Console.WriteLine(eletronico);
                }
            }
        }

        public void RemoverEletronico(string nomeEletronico)
        {
            var eletronico = eletronicos.Find(e => e.Produto == nomeEletronico);

            if (eletronico != null)
            {
                eletronicos.Remove(eletronico);
                Console.WriteLine("Eletrônico removido!");
            }
            else
            {
                Console.WriteLine("Eletrônico não encontrado.");
            }
        }

        public void AtualizarEstoque(bool entrada)
        {
            Console.WriteLine("Informe o nome do eletrônico:");
            string nomeEletronico = Console.ReadLine();

            var eletronico = eletronicos.Find(e => e.Produto == nomeEletronico);

            if (eletronico != null)
            {
                Console.WriteLine($"Quantidade {(entrada ? "adicionada" : "retirada")} ao estoque:");
                int quantidadeAlterada = int.Parse(Console.ReadLine());

                if (!entrada && quantidadeAlterada > eletronico.Estoque)
                {
                    Console.WriteLine("Esta ação não é recomendada!");
                }
                else
                {
                    eletronico.Estoque += (entrada ? quantidadeAlterada : -quantidadeAlterada);
                    Console.WriteLine($"A quantidade atualizada de unidades é {eletronico.Estoque}");
                    Console.WriteLine(eletronico);
                }
            }
            else
            {
                Console.WriteLine("Eletrônico não encontrado.");
            }
        }
    }

    static void Main(string[] args)
    {
        EstoqueEletronicos estoqueEletronicos = new EstoqueEletronicos();

        int escolha;

        do
        {
            Console.WriteLine("CONTROLE DE ESTOQUE-PRODUTOS ELETRÔNICOS");
            Console.WriteLine("[1] Novo Produto");
            Console.WriteLine("[2] Listar Produtos");
            Console.WriteLine("[3] Removedor de Produto");
            Console.WriteLine("[4] Entrada Estoque");
            Console.WriteLine("[5] Saída Estoque");
            Console.WriteLine("[0] Sair");
            Console.Write("Escolha uma opção: ");

            escolha = int.Parse(Console.ReadLine());

            switch (escolha)
            {
                case 1:
                    Console.WriteLine("Adicionar produto:");
                    string opcao = Console.ReadLine();

                    Console.WriteLine("Preço do produto:");
                    double preco = double.Parse(Console.ReadLine());

                    Console.WriteLine("Nome do produto:");
                    string produto = Console.ReadLine();

                    Console.WriteLine("Saldo atualizado do estoque:");
                    int estoque = int.Parse(Console.ReadLine());

                    Eletronico novoEletronico = new Eletronico(opcao, preco, produto, estoque);
                    estoqueEletronicos.AdicionarEletronico(novoEletronico);
                    break;
                case 2:
                    estoqueEletronicos.ListarEletronicos();
                    break;
                case 3:
                    Console.WriteLine("Informe o nome do eletrônico a ser removido:");
                    string nomeEletronicoRemover = Console.ReadLine();
                    estoqueEletronicos.RemoverEletronico(nomeEletronicoRemover);
                    break;
                case 4:
                    estoqueEletronicos.AtualizarEstoque(entrada: true);
                    break;
                case 5:
                    estoqueEletronicos.AtualizarEstoque(entrada: false);
                    break;
                case 0:
                    Console.WriteLine("Programa encerrado");
                    break;
                default:
                    Console.WriteLine("Opção inválida.");
                    break;
            }
        } while (escolha != 0);
    }
}
