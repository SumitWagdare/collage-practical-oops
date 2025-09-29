import java.awt.*;
import java.awt.event.*;

public class CohenSutherlandClipping extends Frame {

    // Define the boundaries of the clipping window
    private static final int X_MIN = 100;
    private static final int Y_MIN = 100;
    private static final int X_MAX = 300;
    private static final int Y_MAX = 300;

    // Region codes for Cohen-Sutherland
    private static final int INSIDE = 0; // 0000
    private static final int LEFT = 1;   // 0001
    private static final int RIGHT = 2;  // 0010
    private static final int BOTTOM = 4; // 0100
    private static final int TOP = 8;    // 1000

    public CohenSutherlandClipping() {
        setTitle("Cohen-Sutherland Line Clipping");
        setSize(500, 500);
        setVisible(true);

        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    // --- Helper function to compute the region code for a point (x, y) ---
    private int computeCode(double x, double y) {
        int code = INSIDE;

        if (x < X_MIN) {
            code |= LEFT;
        } else if (x > X_MAX) {
            code |= RIGHT;
        }

        if (y < Y_MIN) {
            code |= BOTTOM;
        } else if (y > Y_MAX) {
            code |= TOP;
        }

        return code;
    }

    // --- The Cohen-Sutherland Line Clipping Algorithm ---
    private void cohenSutherlandClip(Graphics g, double x1, double y1, double x2, double y2) {
        int code1 = computeCode(x1, y1);
        int code2 = computeCode(x2, y2);
        boolean accept = false;

        while (true) {
            // Case 1: Trivial Accept (Both endpoints are inside the window)
            if ((code1 == 0) && (code2 == 0)) {
                accept = true;
                break;
            }
            // Case 2: Trivial Reject (Both endpoints are outside and on the same side)
            else if ((code1 & code2) != 0) {
                break;
            }
            // Case 3: Clipping required
            else {
                int codeOut;
                double x = 0, y = 0;

                // Pick the outside point to clip
                codeOut = (code1 != 0) ? code1 : code2;

                // Find intersection point using slope (m = (y2-y1)/(x2-x1))
                if ((codeOut & TOP) != 0) { // Point is above the clip window
                    x = x1 + (x2 - x1) * (Y_MAX - y1) / (y2 - y1);
                    y = Y_MAX;
                } else if ((codeOut & BOTTOM) != 0) { // Point is below the clip window
                    x = x1 + (x2 - x1) * (Y_MIN - y1) / (y2 - y1);
                    y = Y_MIN;
                } else if ((codeOut & RIGHT) != 0) { // Point is to the right of the clip window
                    y = y1 + (y2 - y1) * (X_MAX - x1) / (x2 - x1);
                    x = X_MAX;
                } else if ((codeOut & LEFT) != 0) { // Point is to the left of the clip window
                    y = y1 + (y2 - y1) * (X_MIN - x1) / (x2 - x1);
                    x = X_MIN;
                }

                // Now replace the outside point with the intersection point
                if (codeOut == code1) {
                    x1 = x;
                    y1 = y;
                    code1 = computeCode(x1, y1); // Recompute code for the new point
                } else {
                    x2 = x;
                    y2 = y;
                    code2 = computeCode(x2, y2); // Recompute code for the new point
                }
            }
        }

        // Draw the clipped line segment
        if (accept) {
            // Draw the clipped line in green
            g.setColor(Color.GREEN);
            g.drawLine((int) Math.round(x1), (int) Math.round(y1), (int) Math.round(x2), (int) Math.round(y2));
        }
    }

    // --- Paint method to draw the window and test lines ---
    public void paint(Graphics g) {
        // 1. Draw the Clipping Window (in RED)
        g.setColor(Color.RED);
        g.drawRect(X_MIN, Y_MIN, X_MAX - X_MIN, Y_MAX - Y_MIN);
        g.drawString("Clipping Window (Red)", X_MIN + 5, Y_MIN - 5);

        // 2. Define and Draw Test Line Segments (Original lines in GRAY)
        g.setColor(Color.LIGHT_GRAY);

        // Line 1: Trivial Accept (Fully inside)
        double l1_x1 = 150, l1_y1 = 150, l1_x2 = 250, l1_y2 = 250;
        g.drawLine((int) l1_x1, (int) l1_y1, (int) l1_x2, (int) l1_y2);

        // Line 2: Trivial Reject (Fully outside, top)
        double l2_x1 = 10, l2_y1 = 400, l2_x2 = 450, l2_y2 = 450;
        g.drawLine((int) l2_x1, (int) l2_y1, (int) l2_x2, (int) l2_y2);

        // Line 3: Needs Clipping (Intersects the window)
        double l3_x1 = 50, l3_y1 = 50, l3_x2 = 350, l3_y2 = 350;
        g.drawLine((int) l3_x1, (int) l3_y1, (int) l3_x2, (int) l3_y2);

        // Line 4: Needs Clipping (Vertical line)
        double l4_x1 = 300, l4_y1 = 50, l4_x2 = 300, l4_y2 = 350;
        g.drawLine((int) l4_x1, (int) l4_y1, (int) l4_x2, (int) l4_y2);

        // 3. Clip and Draw the Clipped Lines (in GREEN)
        g.drawString("Clipped Line (Green)", 305, 305);
        cohenSutherlandClip(g, l1_x1, l1_y1, l1_x2, l1_y2);
        cohenSutherlandClip(g, l2_x1, l2_y1, l2_x2, l2_y2);
        cohenSutherlandClip(g, l3_x1, l3_y1, l3_x2, l3_y2);
        cohenSutherlandClip(g, l4_x1, l4_y1, l4_x2, l4_y2);
    }

    // --- Main method ---
    public static void main(String[] args) {
        new CohenSutherlandClipping();
    }
}
