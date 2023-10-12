import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.util.ArrayList;
import java.util.Random;

public class SnakeGame extends JPanel implements ActionListener {
    private final int TILE_SIZE = 20;
    private final int WIDTH = 20;
    private final int HEIGHT = 15;
    private final int TOTAL_TILES = WIDTH * HEIGHT;

    private ArrayList<Point> snake;
    private int direction;
    private Point food;
    private boolean isRunning;

    public SnakeGame() {
        snake = new ArrayList<>();
        direction = KeyEvent.VK_RIGHT;
        isRunning = true;

        setPreferredSize(new Dimension(WIDTH * TILE_SIZE, HEIGHT * TILE_SIZE));
        setBackground(Color.BLACK);
        setFocusable(true);
        addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                changeDirection(e.getKeyCode());
            }
        });

        startGame();
    }

    public void startGame() {
        snake.clear();
        snake.add(new Point(5, 5));
        spawnFood();
        isRunning = true;
        Timer timer = new Timer(100, this);
        timer.start();
    }

    public void spawnFood() {
        Random rand = new Random();
        int x, y;
        do {
            x = rand.nextInt(WIDTH);
            y = rand.nextInt(HEIGHT);
        } while (snake.contains(new Point(x, y)));
        food = new Point(x, y);
    }

    public void changeDirection(int newDirection) {
        if ((newDirection == KeyEvent.VK_LEFT && direction != KeyEvent.VK_RIGHT) ||
            (newDirection == KeyEvent.VK_RIGHT && direction != KeyEvent.VK_LEFT) ||
            (newDirection == KeyEvent.VK_UP && direction != KeyEvent.VK_DOWN) ||
            (newDirection == KeyEvent.VK_DOWN && direction != KeyEvent.VK_UP)) {
            direction = newDirection;
        }
    }

    public void actionPerformed(ActionEvent e) {
        if (isRunning) {
            move();
            checkCollision();
            repaint();
        }
    }

    public void move() {
        Point newHead = snake.get(0);
        if (direction == KeyEvent.VK_LEFT) {
            newHead = new Point(newHead.x - 1, newHead.y);
        } else if (direction == KeyEvent.VK_RIGHT) {
            newHead = new Point(newHead.x + 1, newHead.y);
        } else if (direction == KeyEvent.VK_UP) {
            newHead = new Point(newHead.x, newHead.y - 1);
        } else if (direction == KeyEvent.VK_DOWN) {
            newHead = new Point(newHead.x, newHead.y + 1);
        }

        snake.add(0, newHead);

        if (newHead.equals(food)) {
            spawnFood();
        } else {
            snake.remove(snake.size() - 1);
        }
    }

    public void checkCollision() {
        Point head = snake.get(0);
        if (head.x < 0 || head.x >= WIDTH || head.y < 0 || head.y >= HEIGHT || snake.indexOf(head) != 0) {
            isRunning = false;
        }
    }

    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        for (Point point : snake) {
            g.setColor(Color.GREEN);
            g.fillOval(point.x * TILE_SIZE, point.y * TILE_SIZE, TILE_SIZE, TILE_SIZE);
        }
        g.setColor(Color.RED);
        g.fillOval(food.x * TILE_SIZE, food.y * TILE_SIZE, TILE_SIZE, TILE_SIZE);
    }

    public static void main(String[] args) {
        JFrame frame = new JFrame("Snake Game");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.add(new SnakeGame());
        frame.pack();
        frame.setVisible(true);
    }
}
