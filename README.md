import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class BasicMinecraftGame {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Basic Minecraft Game");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(800, 600);
        
        GamePanel gamePanel = new GamePanel();
        frame.add(gamePanel);
        
        frame.setVisible(true);
    }
}

class GamePanel extends JPanel implements ActionListener {
    private boolean[][] blocks;
    private Timer timer;
    private int playerX, playerY;

    public GamePanel() {
        blocks = new boolean[10][10];
        timer = new Timer(100, this);
        timer.start();

        playerX = 5;
        playerY = 5;

        setFocusable(true);
        addKeyListener(new MovementKeyListener());
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        int blockSize = 50;
        int offsetX = 50;
        int offsetY = 50;

        for (int i = 0; i < blocks.length; i++) {
            for (int j = 0; j < blocks[i].length; j++) {
                if (blocks[i][j]) {
                    g.setColor(Color.GRAY);
                    g.fillRect(offsetX + i * blockSize, offsetY + j * blockSize, blockSize, blockSize);
                }
            }
        }

        g.setColor(Color.BLUE);
        g.fillRect(offsetX + playerX * blockSize, offsetY + playerY * blockSize, blockSize, blockSize);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        repaint();
    }

    private class MovementKeyListener extends KeyAdapter {
        @Override
        public void keyPressed(KeyEvent e) {
            int keyCode = e.getKeyCode();

            if (keyCode == KeyEvent.VK_UP) {
                playerY--;
            } else if (keyCode == KeyEvent.VK_DOWN) {
                playerY++;
            } else if (keyCode == KeyEvent.VK_LEFT) {
                playerX--;
            } else if (keyCode == KeyEvent.VK_RIGHT) {
                playerX++;
            }

            repaint();
        }
    }
}





  
