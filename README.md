import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.Random;

public class CaptchaDemo extends JDialog implements ActionListener {

    JTextField nameField, emailField, ageField, captchaField;
    JLabel captchaLabel;
    String captchaCode;

    public CaptchaDemo(Frame parent) {
        super(parent, "🌈 User Info Form with CAPTCHA", true);
        setSize(500, 450);
        setLocationRelativeTo(parent);
        setUndecorated(true);  // Remove default border
        setLayout(new BorderLayout());

        JPanel mainPanel = new JPanel();
        mainPanel.setLayout(null);
        mainPanel.setBackground(new Color(255, 248, 225));  // Soft yellow-orange
        mainPanel.setBorder(BorderFactory.createLineBorder(new Color(70, 130, 180), 4)); // Steel blue border
        add(mainPanel);

        Font labelFont = new Font("Segoe UI", Font.BOLD, 16);
        Font fieldFont = new Font("Segoe UI", Font.PLAIN, 15);
        Font captchaFont = new Font("Consolas", Font.BOLD, 22);

        JLabel header = new JLabel("✨ Enter Your Details ✨", JLabel.CENTER);
        header.setFont(new Font("Segoe UI", Font.BOLD, 20));
        header.setBounds(0, 10, 500, 30);
        header.setForeground(new Color(0, 102, 102));
        mainPanel.add(header);

        JLabel nameLabel = new JLabel("Name:");
        nameLabel.setFont(labelFont);
        nameLabel.setBounds(50, 60, 100, 25);
        mainPanel.add(nameLabel);

        nameField = new JTextField();
        nameField.setFont(fieldFont);
        nameField.setBounds(160, 60, 270, 28);
        mainPanel.add(nameField);

        JLabel emailLabel = new JLabel("Email:");
        emailLabel.setFont(labelFont);
        emailLabel.setBounds(50, 100, 100, 25);
        mainPanel.add(emailLabel);

        emailField = new JTextField();
        emailField.setFont(fieldFont);
        emailField.setBounds(160, 100, 270, 28);
        mainPanel.add(emailField);

        JLabel ageLabel = new JLabel("Age:");
        ageLabel.setFont(labelFont);
        ageLabel.setBounds(50, 140, 100, 25);
        mainPanel.add(ageLabel);

        ageField = new JTextField();
        ageField.setFont(fieldFont);
        ageField.setBounds(160, 140, 270, 28);
        mainPanel.add(ageField);

        captchaLabel = new JLabel();
        captchaLabel.setOpaque(true);
        captchaLabel.setHorizontalAlignment(SwingConstants.CENTER);
        captchaLabel.setFont(captchaFont);
        captchaLabel.setBackground(new Color(180, 220, 255));
        captchaLabel.setBounds(160, 180, 180, 40);
        captchaLabel.setBorder(BorderFactory.createLineBorder(Color.DARK_GRAY, 1));
        mainPanel.add(captchaLabel);

        JLabel captchaPrompt = new JLabel("Enter CAPTCHA:");
        captchaPrompt.setFont(labelFont);
        captchaPrompt.setBounds(50, 240, 140, 25);
        mainPanel.add(captchaPrompt);

        captchaField = new JTextField();
        captchaField.setFont(fieldFont);
        captchaField.setBounds(190, 240, 240, 28);
        mainPanel.add(captchaField);

        JButton submitBtn = new JButton("🚀 Submit");
        submitBtn.setFont(new Font("Segoe UI", Font.BOLD, 15));
        submitBtn.setBounds(180, 300, 130, 40);
        submitBtn.setBackground(new Color(72, 201, 176));
        submitBtn.setForeground(Color.white);
        submitBtn.setFocusPainted(false);
        submitBtn.setBorder(BorderFactory.createLineBorder(Color.DARK_GRAY, 1));
        submitBtn.addActionListener(this);
        mainPanel.add(submitBtn);

        JButton closeBtn = new JButton("❌");
        closeBtn.setBounds(460, 10, 30, 25);
        closeBtn.setFocusable(false);
        closeBtn.setBackground(new Color(255, 99, 71));
        closeBtn.setForeground(Color.white);
        closeBtn.setBorder(BorderFactory.createEmptyBorder());
        closeBtn.addActionListener(e -> dispose());
        mainPanel.add(closeBtn);

        generateCaptcha();
    }

    private void generateCaptcha() {
        String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        StringBuilder sb = new StringBuilder();
        Random rand = new Random();
        for (int i = 0; i < 6; i++) {
            sb.append(chars.charAt(rand.nextInt(chars.length())));
        }
        captchaCode = sb.toString();
        captchaLabel.setText(captchaCode);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String userCaptcha = captchaField.getText().trim();

        if (userCaptcha.equalsIgnoreCase(captchaCode)) {
            String name = nameField.getText();
            String email = emailField.getText();
            String age = ageField.getText();

            // Simulate saving
            System.out.println("Data Saved:");
            System.out.println("Name: " + name);
            System.out.println("Email: " + email);
            System.out.println("Age: " + age);

            JOptionPane.showMessageDialog(this,
                    "✅ Successfully Submitted!",
                    "Success",
                    JOptionPane.INFORMATION_MESSAGE);

            dispose(); // Close dialog
        } else {
            JOptionPane.showMessageDialog(this,
                    "❌ CAPTCHA Incorrect. Please try again.",
                    "Error",
                    JOptionPane.ERROR_MESSAGE);
            generateCaptcha();
            captchaField.setText("");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            CaptchaDemo form = new CaptchaDemo(null);
            form.setVisible(true);
        });
    }
}

