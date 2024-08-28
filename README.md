/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Main.java to edit this template
 */
package javaapplication14;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator extends JFrame implements ActionListener {
    // أزرار الأرقام والعمليات
    private final JButton[] numberButtons = new JButton[10];
    private final JButton addButton;
    private final JButton subButton;
    private final JButton mulButton;
    private final JButton divButton;
    private final JButton decButton;
    private final JButton equButton;
    private final JButton delButton;
    private final JButton clrButton;
    private final JTextField textField;
    
    // متغيرات للعمليات الحسابية
    private double tempFirst , tempSecond  , result ;
    private char math_operator;
    
    // البناء
    public Calculator() {
        setLayout(new FlowLayout());
        setTitle("Calculator");
        
        textField = new JTextField(16);
        textField.setEditable(false);
        
        // إضافة الأزرار
        addButton = createButton("+");
        subButton = createButton("-");
        mulButton = createButton("x");
        divButton = createButton("/");
        decButton = createButton(".");
        equButton = createButton("=");
        delButton = createButton("Delete");
        clrButton = createButton("Clear");
        
        // إضافة الأزرار إلى النافذة
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 4, 10, 10));
        
        // هذا الحلقة تضيف أزرار الأرقام
        for (int i = 0; i < 10; i++) {
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            panel.add(numberButtons[i]);
        }
        
        // إضافة أزرار العمليات
        panel.add(addButton);
        panel.add(subButton);
        panel.add(mulButton);
        panel.add(divButton);
        panel.add(decButton);
        panel.add(equButton);
        panel.add(delButton);
        panel.add(clrButton);
        
        // إضافة النص واللوحة إلى الإطار
        add(textField);
        add(panel);
        
        setSize(500, 550);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }
    
    // معالجة الأحداث
    @Override
    public void actionPerformed(ActionEvent e) {
        Object source = e.getSource();
        
        for (int i = 0; i < 10; i++) {
            if (source == numberButtons[i]) {
                textField.setText(textField.getText().concat(String.valueOf(i)));
            }
        }
        
        if (source == decButton && !textField.getText().contains(".")) {
            textField.setText(textField.getText().concat("."));
        }
        
        if (source == addButton || source == subButton || source == mulButton || source == divButton) {
            tempFirst = Double.parseDouble(textField.getText());
            math_operator = ((JButton)source).getText().charAt(0);
            textField.setText("");
        }
        
        if (source == equButton) {
            tempSecond = Double.parseDouble(textField.getText());
            switch(math_operator) {
                case '+':
                     System.out.println("+");
                    result = tempFirst + tempSecond;
                    break;
                case '-':
                     System.out.println("-");
                    result = tempFirst - tempSecond;
                    break;
                case 'x':
                     System.out.println("x");
                    result = tempFirst * tempSecond;
                    break;
                case '/':
                     System.out.println("/");
                    result = tempFirst / tempSecond;
                    break;
            }
            textField.setText(String.valueOf(result));
            tempFirst = result;
        }
        
        if (source == delButton && textField.getText().length() > 0) {
            textField.setText(textField.getText().substring(0, textField.getText().length() - 1));
        }
        
        if (source == clrButton) {
            textField.setText("");
            tempFirst = 0.0;
            tempSecond = 0.0;
            result = 0.0;
        }
    }
    
    // طريقة لإنشاء الأزرار
    private JButton createButton(String text) {
        JButton button = new JButton(text);
        button.addActionListener(this);
        return button;
    }
    
    // الدالة الرئيسية
    public static void main(String[] args) {
        new Calculator();
    }
}














