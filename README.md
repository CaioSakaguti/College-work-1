// Aluno.java
Public class Aluno {
    Private int id;
    Private String nome;

    Public Aluno(int id, String nome) {
        This.id = id;
        This.nome = nome;
    }

    Public int getId() {
        Return id;
    }

    Public String getNome() {
        Return nome;
    }

    @Override
    Public String toString() {
        Return id + “;” + nome;
    }
}
// Curso.java
Public class Curso {
    Private String nome;
    Private String nivel;
    Private int ano;

    Public Curso(String nome, String nivel, int ano) {
        This.nome = nome;
        This.nivel = nivel;
        This.ano = ano;
    }

    Public String getNome() {
        Return nome;
    }

    Public String getNivel() {
        Return nivel;
    }

    Public int getAno() {
        Return ano;
    }

    Public String getArquivoNotas() {
        Return nome + “_” + nivel + “_” + ano + “.csv”;
    }

    @Override
    Public String toString() {
        Return nome + “;” + nivel + “;” + ano;
    }
}
// Nota.java
Public class Nota {
    Private int idAluno;
    Private double notaNP1;
    Private double notaNP2;
    Private double notaReposicao;
    Private double notaExame;

    Public Nota(int idAluno, double notaNP1, double notaNP2, double notaReposicao, double notaExame) {
        This.idAluno = idAluno;
        This.notaNP1 = notaNP1;
        This.notaNP2 = notaNP2;
        This.notaReposicao = notaReposicao;
        This.notaExame = notaExame;
    }

    Public int getIdAluno() {
        Return idAluno;
    }

    Public double getNotaNP1() {
        Return notaNP1;
    }

    Public double getNotaNP2() {
        Return notaNP2;
    }

    Public double getNotaReposicao() {
        Return notaReposicao;
    }

    Public double getNotaExame() {
        Return notaExame;
    }

    @Override
    Public String toString() {
        Return idAluno + “;” + notaNP1 + “;” + notaNP2 + “;” + notaReposicao + “;” + notaExame;
    }
}// Universidade.java
Import java.io.*;
Import java.util.*;

Public class Universidade {

    Public static List<Aluno> lerAlunos(String caminho) {
        List<Aluno> alunos = new ArrayList<>();
        Try (BufferedReader br = new BufferedReader(new FileReader(caminho))) {
            String linha;
            While ((linha = br.readLine()) != null) {
                String[] partes = linha.split(“;”);
                Alunos.add(new Aluno(Integer.parseInt(partes[0]), partes[1]));
            }
        } catch (IOException e) {
            System.out.println(“Erro ao ler alunos: “ + e.getMessage());
        }
        Return alunos;
    }

    Public static List<Curso> lerCursos(String caminho) {
        List<Curso> cursos = new ArrayList<>();
        Try (BufferedReader br = new BufferedReader(new FileReader(caminho))) {
            String linha;
            While ((linha = br.readLine()) != null) {
                String[] partes = linha.split(“;”);
                Cursos.add(new Curso(partes[0], partes[1], Integer.parseInt(partes[2])));
            }
        } catch (IOException e) {
            System.out.println(“Erro ao ler cursos: “ + e.getMessage());
        }
        Return cursos;
    }

    Public static List<Nota> lerNotasCurso(String caminho) {
        List<Nota> notas = new ArrayList<>();
        Try (BufferedReader br = new BufferedReader(new FileReader(caminho))) {
            String linha;
            While ((linha = br.readLine()) != null) {
                String[] partes = linha.split(“;”);
                Notas.add(new Nota(
                    Integer.parseInt(partes[0]),
                    Double.parseDouble(partes[1]),
                    Double.parseDouble(partes[2]),
                    Double.parseDouble(partes[3]),
                    Double.parseDouble(partes[4])
                ));
            }
        } catch (FileNotFoundException e) {
            System.out.println(“Nenhum dado encontrado para este curso.”);
        } catch (IOException e) {
            System.out.println(“Erro ao ler notas: “ + e.getMessage());
        }
        Return notas;
    }

    Public static void salvarAluno(Aluno aluno, String caminho) {
        Try (BufferedWriter bw = new BufferedWriter(new FileWriter(caminho, true))) {
            Bw.write(aluno.toString());
            Bw.newLine();
        } catch (IOException e) {
            System.out.println(“Erro ao salvar aluno: “ + e.getMessage());
        }
    }

    Public static void salvarCurso(Curso curso, String caminho) {
        Try (BufferedWriter bw = new BufferedWriter(new FileWriter(caminho, true))) {
            Bw.write(curso.toString());
            Bw.newLine();
        } catch (IOException e) {
            System.out.println(“Erro ao salvar curso: “ + e.getMessage());
        }
    }

    Public static void salvarNota(Nota nota, String caminho) {
        Try (BufferedWriter bw = new BufferedWriter(new FileWriter(caminho, true))) {
            Bw.write(nota.toString());
            Bw.newLine();
        } catch (IOException e) {
            System.out.println(“Erro ao salvar nota: “ + e.getMessage());
        }
    }
}
// Menu.java
Import java.util.List;
Import java.util.Scanner;

Public class Menu {
    Private static final String ARQ_ALUNOS = “alunos.csv”;
    Private static final String ARQ_CURSOS = “cursos.csv”;

    Public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Int opcao;

        Do {
            System.out.println(“\n===== Sistema Universidade Amazônia =====”);
            System.out.println(“1. Cadastrar aluno”);
            System.out.println(“2. Cadastrar curso”);
            System.out.println(“3. Cadastrar nota de aluno em curso”);
            System.out.println(“4. Listar alunos”);
            System.out.println(“5. Listar cursos”);
            System.out.println(“6. Ver notas de um curso”);
            System.out.println(“0. Sair”);
            System.out.print(“Escolha uma opção: “);
            Opcao = sc.nextInt();
            Sc.nextLine(); // limpar buffer

            Switch (opcao) {
                Case 1 -> cadastrarAluno(sc);
                Case 2 -> cadastrarCurso(sc);
                Case 3 -> cadastrarNota(sc);
                Case 4 -> listarAlunos();
                Case 5 -> listarCursos();
                Case 6 -> verNotasDeCurso(sc);
                Case 0 -> System.out.println(“Encerrando o sistema.”);
                Default -> System.out.println(“Opção inválida!”);
            }
        } while (opcao != 0);

        Sc.close();
    }

    Private static void cadastrarAluno(Scanner sc) {
        System.out.print(“ID do aluno: “);
        Int id = sc.nextInt();
        Sc.nextLine();
        System.out.print(“Nome do aluno: “);
        String nome = sc.nextLine();

        Universidade.salvarAluno(new Aluno(id, nome), ARQ_ALUNOS);
        System.out.println(“Aluno cadastrado com sucesso!”);
    }

    Private static void cadastrarCurso(Scanner sc) {
        System.out.print(“Nome do curso: “);
        String nome = sc.nextLine();
        System.out.print(“Nível (Ex: Bacharelado): “);
        String nivel = sc.nextLine();
        System.out.print(“Ano: “);
        Int ano = sc.nextInt();
        Sc.nextLine();

        Universidade.salvarCurso(new Curso(nome, nivel, ano), ARQ_CURSOS);
        System.out.println(“Curso cadastrado com sucesso!”);
    }

    Private static void cadastrarNota(Scanner sc) {
        System.out.print(“Nome do curso: “);
        String nome = sc.nextLine();
        System.out.print(“Nível: “);
        String nivel = sc.nextLine();
        System.out.print(“Ano: “);
        Int ano = sc.nextInt();
        Sc.nextLine();

        String caminhoNotas = nome + “_” + nivel + “_” + ano + “.csv”;

        System.out.print(“ID do aluno: “);
        Int id = sc.nextInt();
        System.out.print(“Nota NP1: “);
        Double np1 = sc.nextDouble();
        System.out.print(“Nota NP2: “);
        Double np2 = sc.nextDouble();
        System.out.print(“Nota Reposição: “);
        Double rep = sc.nextDouble();
        System.out.print(“Nota Exame: “);
        Double exame = sc.nextDouble();

        Universidade.salvarNota(new Nota(id, np1, np2, rep, exame), caminhoNotas);
        System.out.println(“Nota cadastrada com sucesso!”);
    }

    Private static void listarAlunos() {
        List<Aluno> alunos = Universidade.lerAlunos(ARQ_ALUNOS);
        System.out.println(“\n--- Alunos ---“);
        For (Aluno a : alunos) {
            System.out.println(“ID: “ + a.getId() + “, Nome: “ + a.getNome());
        }
    }

    Private static void listarCursos() {
        List<Curso> cursos = Universidade.lerCursos(ARQ_CURSOS);
        System.out.println(“\n--- Cursos ---“);
        For (Curso c : cursos) {
            System.out.println(c.getNome() + “ – “ + c.getNivel() + “ – “ + c.getAno());
        }
    }

    Private static void verNotasDeCurso(Scanner sc) {
        System.out.print(“Nome do curso: “);
        String nome = sc.nextLine();
        System.out.print(“Nível: “);
        String nivel = sc.nextLine();
        System.out.print(“Ano: “);
        Int ano = sc.nextInt();
        Sc.nextLine();

        String caminho = nome + “_” + nivel + “_” + ano + “.csv”;
        List<Nota> notas = Universidade.lerNotasCurso(caminho);

        System.out.println(“\n--- Notas ---“);
        For (Nota n : notas) {
            System.out.println(“ID: “ + n.getIdAluno() + “ | NP1: “ + n.getNotaNP1() + “ | NP2: “ + n.getNotaNP2() +
                    “ | Reposição: “ + n.getNotaReposicao() + “ | Exame: “ + n.getNotaExame());
        }
    }
}
