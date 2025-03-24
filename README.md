// Classe base
class Funcionario {
    protected String nome;
    protected double salarioBase;

    public Funcionario(String nome, double salarioBase) {
        this.nome = nome;
        this.salarioBase = salarioBase;
    }

    public void exibirDados() {
        System.out.println("Nome: " + nome);
        System.out.println("Salário: " + calcularSalario());
    }

    public double calcularSalario() {
        return salarioBase;
    }
}

// Classe derivada Gerente
class Gerente extends Funcionario {
    private double bonus;

    public Gerente(String nome, double salarioBase, double bonus) {
        super(nome, salarioBase);
        this.bonus = bonus;
    }

    @Override
    public double calcularSalario() {
        return salarioBase + bonus;
    }
}

// Classe derivada Desenvolvedor
class Desenvolvedor extends Funcionario {
    private int horasExtras;
    private double valorHoraExtra;

    public Desenvolvedor(String nome, double salarioBase, int horasExtras, double valorHoraExtra) {
        super(nome, salarioBase);
        this.horasExtras = horasExtras;
        this.valorHoraExtra = valorHoraExtra;
    }

    @Override
    public double calcularSalario() {
        return salarioBase + (horasExtras * valorHoraExtra);
    }
}

// Classe principal para teste
public class Empresa {
    public static void main(String[] args) {
        Funcionario f1 = new Gerente("Ana", 5000, 1500);
        Funcionario f2 = new Desenvolvedor("Carlos", 4000, 10, 50);

        f1.exibirDados();
        System.out.println("---------------------");
        f2.exibirDados();
    }
}
