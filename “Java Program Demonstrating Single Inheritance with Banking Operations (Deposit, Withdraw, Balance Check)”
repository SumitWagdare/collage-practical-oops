// Demonstration of Single Inheritance with Banking Example

// Superclass: BankAccount
class BankAccount {
    protected String accountHolder;
    protected double balance;

    // Constructor
    public BankAccount(String accountHolder, double initialBalance) {
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }

    // Method to check balance
    public void checkBalance() {
        System.out.println(accountHolder + "'s Current Balance: Rs. " + balance);
    }
}

// Subclass: SavingsAccount extending BankAccount
class SavingsAccount extends BankAccount {

    // Constructor
    public SavingsAccount(String accountHolder, double initialBalance) {
        super(accountHolder, initialBalance);
    }

    // Method to deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: Rs. " + amount);
        } else {
            System.out.println("Invalid deposit amount!");
        }
    }

    // Method to withdraw money
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: Rs. " + amount);
        } else if (amount > balance) {
            System.out.println("Insufficient balance!");
        } else {
            System.out.println("Invalid withdrawal amount!");
        }
    }
}

public class BankDemo {
    public static void main(String[] args) {
        // Create a SavingsAccount object
        SavingsAccount account = new SavingsAccount("Sumit Wagdare", 5000);

        // Perform banking operations
        account.checkBalance();
        account.deposit(2000);
        account.checkBalance();
        account.withdraw(1000);
        account.checkBalance();
        account.withdraw(7000);
    }
}
