CREATE DATABASE IF NOT EXISTS pecas_db;
USE pecas_db;

CREATE TABLE IF NOT EXISTS clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS solicitacoes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    codigo_peca VARCHAR(20) NOT NULL,
    peca VARCHAR(100) NOT NULL,
    veiculo VARCHAR(100) NOT NULL,
    cliente_id INT NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class Conexao {
    public static Connection getConnection() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/pecas_db";
        String user = "root";
        String password = "";
        return DriverManager.getConnection(url, user, password);
    }
}


import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;

public class TelaPrincipal extends JFrame {

    private JTable tabelaClientes, tabelaPecas;
    private JButton btnCadastrar, btnAtualizar, btnExcluir, btnBuscar;

    public TelaPrincipal() {
        setTitle("Gerenciamento de Peças e Solicitações");
        setSize(900, 600);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        JTabbedPane abas = new JTabbedPane();

        // Painel da Tabela 1
        JPanel painel1 = new JPanel(new BorderLayout());
        tabelaClientes = new JTable(new DefaultTableModel(
            new Object[][]{},
            new String[]{"Código da Peça", "Veículo", "Nome do Cliente", "CPF"}
        ));
        painel1.add(new JScrollPane(tabelaClientes), BorderLayout.CENTER);
        abas.addTab("Solicitações por Cliente", painel1);

        // Painel da Tabela 2
        JPanel painel2 = new JPanel(new BorderLayout());
        tabelaPecas = new JTable(new DefaultTableModel(
            new Object[][]{},
            new String[]{"Código da Peça", "Nome da Peça", "Veículo", "Nome do Cliente", "CPF"}
        ));
        painel2.add(new JScrollPane(tabelaPecas), BorderLayout.CENTER);
        abas.addTab("Detalhes da Peça", painel2);

        // Painel dos botões
        JPanel painelBotoes = new JPanel(new FlowLayout());
        btnCadastrar = new JButton("Cadastrar");
        btnAtualizar = new JButton("Atualizar");
        btnExcluir = new JButton("Excluir");
        btnBuscar = new JButton("Buscar Cliente");

        painelBotoes.add(btnCadastrar);
        painelBotoes.add(btnAtualizar);
        painelBotoes.add(btnExcluir);
        painelBotoes.add(btnBuscar);

        // Adicionando tudo ao frame
        add(abas, BorderLayout.CENTER);
        add(painelBotoes, BorderLayout.SOUTH);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new TelaPrincipal().setVisible(true);
        });
    }
}


    public class Cliente {
    private int id;
    private String nome;
    private String cpf;

    public Cliente(int id, String nome, String cpf) {
        this.id = id;
        this.nome = nome;
        this.cpf = cpf;
    }

    public Cliente(String nome, String cpf) {
        this.nome = nome;
        this.cpf = cpf;
    }

    public int getId() { return id; }
    public String getNome() { return nome; }
    public String getCpf() { return cpf; }

    public void setId(int id) { this.id = id; }
    public void setNome(String nome) { this.nome = nome; }
    public void setCpf(String cpf) { this.cpf = cpf; }
}
    public class Solicitacao {
    private int id;
    private String codigoPeca;
    private String peca;
    private String veiculo;
    private Cliente cliente;

    public Solicitacao(int id, String codigoPeca, String peca, String veiculo, Cliente cliente) {
        this.id = id;
        this.codigoPeca = codigoPeca;
        this.peca = peca;
        this.veiculo = veiculo;
        this.cliente = cliente;
    }

    public String getCodigoPeca() { return codigoPeca; }
    public String getPeca() { return peca; }
    public String getVeiculo() { return veiculo; }
    public Cliente getCliente() { return cliente; }

    public void setCodigoPeca(String codigoPeca) { this.codigoPeca = codigoPeca; }
    public void setPeca(String peca) { this.peca = peca; }
    public void setVeiculo(String veiculo) { this.veiculo = veiculo; }
    public void setCliente(Cliente cliente) { this.cliente = cliente; }
}
    
