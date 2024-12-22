# BankBalanceAPP
Simple GUI application that handles deposits and withdrawals and displays remaining balance before exiting.





Here is the source code:

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class BankBalanceApp {
    private JFrame frame;
    private JPanel panel;
    private JTextField balanceField;
    private JTextField depositField;
    private JTextField withdrawField;
    private JTextArea displayArea;
    private double balance;

    public BankBalanceApp() {
        balance = 0.0; // Initialize balance
        createGUI();
    }

    private void createGUI() {
        frame = new JFrame("Bank Balance Application");
        panel = new JPanel();
        panel.setLayout(new GridLayout(0, 2)); // Use GridLayout for better organization

        // Create components
        balanceField = new JTextField(10);
        depositField = new JTextField(10);
        withdrawField = new JTextField(10);
        displayArea = new JTextArea(10, 30);
        displayArea.setEditable(false); // Make display area non-editable
        JButton addButton = new JButton("Deposit");
        JButton withdrawButton = new JButton("Withdraw");
        JButton showBalanceButton = new JButton("Show Balance");

        // Add components to the panel
        panel.add(new JLabel("Initial Balance:"));
        panel.add(balanceField);
        panel.add(new JLabel("Deposit Amount:"));
        panel.add(depositField);
        panel.add(addButton);
        panel.add(withdrawButton);
        panel.add(new JLabel("Withdraw Amount:"));
        panel.add(withdrawField);
        panel.add(showBalanceButton);
        panel.add(new JScrollPane(displayArea)); // Add scroll pane for display area

        // Add action listeners
        addButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                deposit();
            }
        });

        withdrawButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                withdraw();
            }
        });

        showBalanceButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                showBalance();
            }
        });

        // Finalize frame
        frame.add(panel);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.pack();
        frame.setVisible(true);
    }

    // Methods for deposit, withdraw, and show balance
    private void deposit() {
        try {
            double depositAmount = Double.parseDouble(depositField.getText());
            balance += depositAmount;
            displayArea.append("Deposited: " + depositAmount + "\n");
            depositField.setText(""); // Clear input field
        } catch (NumberFormatException e) {
            displayArea.append("Invalid deposit amount!\n");
        }
    }

    private void withdraw() {
        try {
            double withdrawAmount = Double.parseDouble(withdrawField.getText());
            if (withdrawAmount <= balance) {
                balance -= withdrawAmount;
                displayArea.append("Withdrawn: " + withdrawAmount + "\n");
            } else {
                displayArea.append("Insufficient funds for withdrawal!\n");
            }
            withdrawField.setText(""); // Clear input field
        } catch (NumberFormatException e) {
            displayArea.append("Invalid withdrawal amount!\n");
        }
    }

    private void showBalance() {
        displayArea.append("Current Balance: " + balance + "\n");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new BankBalanceApp());
    }
}
