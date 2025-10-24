Maurício Mendes ( brisollamauricio2020@gmail.com )

Desenvolver um jogo de inverter palavras, utilizando Java em modo texto ou gráfico (você escolhe). O jogador digita uma frase e o programa a inverte, exibindo a frase invertida na tela.

Exibir um menu para que o jogador escolha entre inverter uma nova frase, ver as frases já inseridas, desfazer a última inversão, inverter as letras de cada palavra ou sair do programa.
O programa deve utilizar uma pilha (Stack ou Deque) para armazenar as palavras da frase original.
A frase deve ser composta por palavras separadas por espaços.
O programa deve inverter a ordem das palavras da frase, mantendo a ordem das letras em cada palavra.
A frase original e a versão invertida devem ser exibidas na tela.
Todas as frases originais devem ser armazenadas em uma lista (List) e exibidas em ordem alfabética, quando solicitado.
O programa deve permitir inverter as letras de cada palavra individualmente, mantendo a ordem das palavras.
O programa deve manter um histórico das frases invertidas em uma pilha, permitindo desfazer a última inversão realizada.
Opcionalmente, a pilha de frases pode ter tamanho máximo limitado (ex: 5 frases). Se ultrapassado, a frase mais antiga deve ser descartada.

import java.util.Scanner;
import java.util.List;
import java.util.ArrayList;
import java.util.Deque;
import java.util.ArrayDeque;
import java.util.Collections;
import java.util.Stack;

/**
 * Jogo de Inversão de Palavras
 * Permite ao jogador inverter frases, visualizar histórico e desfazer ações.
 * Utiliza estruturas de dados como List, Stack e Deque.
 *
 * @author Mauricio
 * @version 1.0
 */
public class PalavraInversaGame {
    private final List<String> frasesOriginais;
    private final Deque<String> historicoInversoes;

    /**
     * Método principal que inicia o jogo.
     * @param args argumentos da linha de comando
     */
    public static void main(String[] args) {
        PalavraInversaGame jogo = new PalavraInversaGame();
        jogo.iniciar();
    }

    /**
     * Construtor que inicializa as estruturas de dados.
     */
    public PalavraInversaGame() {
        frasesOriginais = new ArrayList<>();
        historicoInversoes = new ArrayDeque<>();
    }

    /**
     * Exibe o menu principal e gerencia as opções do jogador.
     */
    public void iniciar() {
        Scanner scanner = new Scanner(System.in);
        int opcao;

        do {
            System.out.println("\n--- MENU ---");
            System.out.println("1. Inverter nova frase");
            System.out.println("2. Ver frases inseridas");
            System.out.println("3. Desfazer última inversão");
            System.out.println("4. Inverter letras de cada palavra");
            System.out.println("5. Sair");
            System.out.print("Escolha uma opção: ");
            opcao = scanner.nextInt();
            scanner.nextLine(); // limpar buffer

            switch (opcao) {
                case 1 -> inverterFrase(scanner);
                case 2 -> mostrarFrasesOrdenadas();
                case 3 -> desfazerInversao();
                case 4 -> inverterLetras(scanner);
                case 5 -> System.out.println("Encerrando o jogo...");
                default -> System.out.println("Opção inválida.");
            }
        } while (opcao != 5);
    }

    /**
     * Inverte a ordem das palavras da frase digitada.
     * @param scanner Scanner para entrada do usuário
     */
    public void inverterFrase(Scanner scanner) {
        System.out.print("Digite a frase: ");
        String frase = scanner.nextLine();
        frasesOriginais.add(frase);

        Stack<String> pilhaPalavras = new Stack<>();
        for (String palavra : frase.split(" ")) {
            pilhaPalavras.push(palavra);
        }

        StringBuilder fraseInvertida = new StringBuilder();
        while (!pilhaPalavras.isEmpty()) {
            fraseInvertida.append(pilhaPalavras.pop()).append(" ");
        }

        String resultado = fraseInvertida.toString().trim();
        System.out.println("Frase original: " + frase);
        System.out.println("Frase invertida: " + resultado);

        if (historicoInversoes.size() == 5) {
            historicoInversoes.removeFirst();
        }
        historicoInversoes.addLast(resultado);
    }

    /**
     * Exibe todas as frases originais em ordem alfabética.
     */
    public void mostrarFrasesOrdenadas() {
        List<String> ordenadas = new ArrayList<>(frasesOriginais);
        Collections.sort(ordenadas);
        System.out.println("\nFrases inseridas:");
        for (String frase : ordenadas) {
            System.out.println("- " + frase);
        }
    }

    /**
     * Desfaz a última inversão realizada, removendo do histórico.
     */
    public void desfazerInversao() {
        if (!historicoInversoes.isEmpty()) {
            String removida = historicoInversoes.removeLast();
            System.out.println("Última inversão desfeita: " + removida);
        } else {
            System.out.println("Nenhuma inversão para desfazer.");
        }
    }

    /**
     * Inverte as letras de cada palavra, mantendo a ordem das palavras.
     * @param scanner Scanner para entrada do usuário
     */
    public void inverterLetras(Scanner scanner) {
        System.out.print("Digite a frase: ");
        String frase = scanner.nextLine();
        frasesOriginais.add(frase);

        StringBuilder resultado = new StringBuilder();
        for (String palavra : frase.split(" ")) {
            resultado.append(new StringBuilder(palavra).reverse()).append(" ");
        }

        System.out.println("Frase original: " + frase);
        System.out.println("Letras invertidas: " + resultado.toString().trim());
    }
}


<img width="576" height="533" alt="image" src="https://github.com/user-attachments/assets/194fd04d-a562-4d2f-8cbb-1aaf52b70299" />
