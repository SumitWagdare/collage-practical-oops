import java.awt.*;
import java.awt.event.*;

public class CircleDrawingAWT extends Frame implements ActionListener {
    int algo = 1, style = 1; // Defaults: Midpoint, Solid

    public CircleDrawingAWT() {
        setTitle("Circle Drawing AWT");
        setSize(500, 500);
        setLayout(new FlowLayout());

        String[] algos = { "Midpoint", "Bresenham", "DDA" };
        String[] styles = { "Solid", "Dotted", "Dashed" };

        Choice algoChoice = new Choice(), styleChoice = new Choice();
        for (String a : algos) algoChoice.add(a);
        for (String s : styles) styleChoice.add(s);

        Button drawBtn = new Button("Draw Circle");
        algoChoice.addItemListener(e -> algo = algoChoice.getSelectedIndex() + 1);
        styleChoice.addItemListener(e -> style = styleChoice.getSelectedIndex() + 1);
        drawBtn.addActionListener(this);

        add(new Label("Algorithm:")); add(algoChoice);
        add(new Label("Style:")); add(styleChoice);
        add(drawBtn);

        setVisible(true);
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) { System.exit(0); }
        });
    }

    public void actionPerformed(ActionEvent e) {
        repaint();
    }

    public void paint(Graphics g) {
        int xc = 250, yc = 250, r = 100;
        switch (algo) {
            case 1: drawMidpoint(g, xc, yc, r); break;
            case 2: drawBresenham(g, xc, yc, r); break;
            case 3: drawDDA(g, xc, yc, r); break;
        }
    }

    void plot(Graphics g, int x, int y, int count) {
        if (style == 2 && count % 4 != 0) return; // Dotted
        if (style == 3 && (count / 5) % 2 == 1) return; // Dashed
        g.drawLine(x, y, x, y);
    }

    void drawSymmetricPoints(Graphics g, int xc, int yc, int x, int y, int count) {
        plot(g, xc + x, yc + y, count);
        plot(g, xc - x, yc + y, count);
        plot(g, xc + x, yc - y, count);
        plot(g, xc - x, yc - y, count);
        plot(g, xc + y, yc + x, count);
        plot(g, xc - y, yc + x, count);
        plot(g, xc + y, yc - x, count);
        plot(g, xc - y, yc - x, count);
    }

    void drawMidpoint(Graphics g, int xc, int yc, int r) {
        int x = 0, y = r, p = 1 - r, count = 0;
        drawSymmetricPoints(g, xc, yc, x, y, count++);
        while (x < y) {
            x++;
            p += (p < 0) ? 2 * x + 1 : 2 * (x - y--) + 1;
            drawSymmetricPoints(g, xc, yc, x, y, count++);
        }
    }

    void drawBresenham(Graphics g, int xc, int yc, int r) {
        int x = 0, y = r, d = 3 - 2 * r, count = 0;
        while (x <= y) {
            drawSymmetricPoints(g, xc, yc, x, y, count++);
            if (d < 0) d += 4 * x++ + 6;
            else d += 4 * (x++ - y--) + 10;
        }
    }

    void drawDDA(Graphics g, int xc, int yc, int r) {
        double angle = 0, count = 0;
        while (angle <= 360) {
            int x = (int)(r * Math.cos(Math.toRadians(angle)));
            int y = (int)(r * Math.sin(Math.toRadians(angle)));
            plot(g, xc + x, yc + y, (int)count++);
            angle += 0.5;
        }
    }

    public static void main(String[] args) {
        new CircleDrawingAWT();
    }
}
