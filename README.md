# SimpleCalculator
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;


public class SimpleCalculator extends JFrame implements ActionListener {

    private final JTextField num1Field, num2Field, resultField;
    private final JButton addButton, subButton, mulButton, divButton;

    public SimpleCalculator() {
        setTitle("Simple Cal");
        setSize(350, 250);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new GridLayout(5, 2, 10, 10));

        // Number 1 input
        add(new JLabel("Number 1:"));
        num1Field = new JTextField();
        add(num1Field);

        // Number 2 input
        add(new JLabel("Number 2:"));
        num2Field = new JTextField();
        add(num2Field);

        // Result display
        add(new JLabel("Result:"));
        resultField = new JTextField();
        resultField.setEditable(false);
        add(resultField);

        // Buttons
        addButton = new JButton("Add");
        subButton = new JButton("Subtract");
        mulButton = new JButton("Multiply");
        divButton = new JButton("Divide");

        // Add listeners
        addButton.addActionListener(this);
        subButton.addActionListener(this);
        mulButton.addActionListener(this);
        divButton.addActionListener(this);

        // Add buttons to layout
        add(addButton);
        add(subButton);
        add(mulButton);
        add(divButton);

        // Show window
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        try {
            double num1 = Double.parseDouble(num1Field.getText().trim());
            double num2 = Double.parseDouble(num2Field.getText().trim());
            double result = 0;

            if (e.getSource() == addButton) {
                result = num1 + num2;
            } else if (e.getSource() == subButton) {
                result = num1 - num2;
            } else if (e.getSource() == mulButton) {
                result = num1 * num2;
            } else if (e.getSource() == divButton) {
                if (num2 == 0) {
                    JOptionPane.showMessageDialog(this, "Cannot divide by zero!");
                    return;
                }
                result = num1 / num2;
            }

            resultField.setText(String.valueOf(result));

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Please enter valid numbers.");
        }
    }

    public static void main(String[] args) {
        // Use SwingUtilities for thread safety
        SwingUtilities.invokeLater(SimpleCalculator::new);
    }
}

