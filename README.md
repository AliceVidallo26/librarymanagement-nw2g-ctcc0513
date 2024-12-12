# librarymanagement-nw2g-ctcc0513
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class LibraryManagementGUI extends JFrame {
    private Library library;
    private JTextArea displayArea;
    private JTextField titleField, authorField, searchField;
    private boolean isLoggedIn = false;
    private JPanel mainPanel;

    public LibraryManagementGUI() {
        library = new Library();
        library.addBook(new Book("To Kill a Mockingbird", "Harper Lee"));
        library.addBook(new Book("1984", "George Orwell"));
        library.addBook(new Book("Pride and Prejudice", "Jane Austen"));
        library.addBook(new Book("The Great Gatsby", "F. Scott Fitzgerald"));
        library.addBook(new Book("The Catcher in the Rye", "J.D. Salinger"));
        library.addBook(new Book("The Hunger Games", "Suzanne Collins"));
        library.addBook(new Book("The Fault in Our Stars", "John Green"));
        library.addBook(new Book("Divergent", "Veronica Roth"));
        library.addBook(new Book("The Maze Runner", "James Dashner"));
        library.addBook(new Book("The Giver", "Lois Lowry"));
        library.addBook(new Book("The Perks of Being a Wallflower", "Stephen Chbosky"));
        library.addBook(new Book("The Book Thief", "Markus Zusak"));
        library.addBook(new Book("The Nightingale", "Kristin Hannah"));
        library.addBook(new Book("The Hate U Give", "Angie Thomas"));
        library.addBook(new Book("The Sun is Also a Star", "Nicola Yoon"));
        library.addBook(new Book("The Poet X", "Elizabeth Acevedo"));
        library.addBook(new Book("The Poppy War", "R.F. Kuang"));
        library.addBook(new Book("The Song of Achilles", "Madeline Miller"));
        library.addBook(new Book("The Power", "Naomi Alderman"));
        library.addBook(new Book("The Fifth Season", "N.K. Jemisin"));
        library.addBook(new Book("The First Fifteen Lives of Harry August", "Claire North"));
        library.addBook(new Book("The City & The City", "China Miéville"));
        library.addBook(new Book("The Gone-Away World", "Nick Harkaway"));
        library.addBook(new Book("The House of Shattered Wings", "Aliette de Bodard"));

        setTitle("Library Management System");
        setSize(500, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null); // Center window

        // Login panel
        JPanel loginPanel = new JPanel();
        loginPanel.setLayout(new GridLayout(3, 2));
        JTextField usernameField = new JTextField();
        JPasswordField passwordField = new JPasswordField();
        JButton loginButton = new JButton("Login");

        loginPanel.add(new JLabel("Username:"));
        loginPanel.add(usernameField);
        loginPanel.add(new JLabel("Password:"));
        loginPanel.add(passwordField);
        loginPanel.add(loginButton);

        // Add action listener for login button
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                if (username.equals("Alice") && password.equals("password")) {
                    isLoggedIn = true;
                    loginPanel.setVisible(false);
                    createMainPanel();
                } else {
                    JOptionPane.showMessageDialog(null, "Invalid credentials, please try again.", "Error", JOptionPane.ERROR_MESSAGE);
                }
            }
        });

        add(loginPanel);
    }

    // Create the main panel after login
    private void createMainPanel() {
        // Main panel for the UI
        mainPanel = new JPanel();
        mainPanel.setLayout(new BorderLayout());

        // Display area to show books
        displayArea = new JTextArea(10, 40);
        displayArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(displayArea);
        mainPanel.add(scrollPane, BorderLayout.CENTER);

        // Panel for input fields and buttons
        JPanel inputPanel = new JPanel();
        inputPanel.setLayout(new GridLayout(7, 2));

        JLabel titleLabel = new JLabel("Book Title:");
        titleField = new JTextField(30);

        JLabel authorLabel = new JLabel("Book Author:");
        authorField = new JTextField(30);

        JLabel searchLabel = new JLabel("Search Book:");
        searchField = new JTextField(30);

        inputPanel.add(titleLabel);
        inputPanel.add(titleField);
        inputPanel.add(authorLabel);
        inputPanel.add(authorField);
        inputPanel.add(searchLabel);
        inputPanel.add(searchField);

        JButton addButton = new JButton("Add Book");
        JButton displayButton = new JButton("Display Books");
        JButton checkOutButton = new JButton ("Check Out");
        JButton returnButton = new JButton("Return Book");
        JButton searchButton = new JButton("Search");
        JButton logOutButton = new JButton("Log Out");

        inputPanel.add(addButton);
        inputPanel.add(displayButton);
        inputPanel.add(checkOutButton);
        inputPanel.add(returnButton);
        inputPanel.add(searchButton);
        inputPanel.add(logOutButton);

        mainPanel.add(inputPanel, BorderLayout.NORTH);

        // Add action listeners to buttons
        addButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                addBook();
            }
        });

        displayButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                displayBooks();
            }
        });

        checkOutButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                checkOutBook();
            }
        });

        returnButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                returnBook();
            }
        });

        searchButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                searchBooks();
            }
        });

        logOutButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                logOut();
            }
        });

        // Add the main panel to the frame
        add(mainPanel);
    }

    // Log out the user
    private void logOut() {
        isLoggedIn = false;
        mainPanel.setVisible(false);
        createLoginPanel();
    }

    // Create the login panel again
    private void createLoginPanel() {
        JPanel loginPanel = new JPanel();
        loginPanel.setLayout(new GridLayout(3, 2));
        JTextField usernameField = new JTextField();
        JPasswordField passwordField = new JPasswordField();
        JButton loginButton = new JButton("Login");

        loginPanel.add(new JLabel("Username:"));
        loginPanel.add(usernameField);
        loginPanel.add(new JLabel("Password:"));
        loginPanel.add(passwordField);
        loginPanel.add(loginButton);

        // Add action listener for login button
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                if (username.equals("Alice") && password.equals("password")) {
                    isLoggedIn = true;
                    loginPanel.setVisible(false);
                    createMainPanel();
                } else {
                    JOptionPane.showMessageDialog(null, "Invalid credentials, please try again.", "Error", JOptionPane.ERROR_MESSAGE);
                }
            }
        });

        add(loginPanel);
        revalidate();
        repaint();
    }

    // Add a book to the library
    private void addBook() {
        String title = titleField.getText();
        String author = authorField.getText();
        if (title.isEmpty() || author.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please enter both title and author.", "Error", JOptionPane.ERROR_MESSAGE);
        } else {
            Book book = new Book(title, author);
            library.addBook(book);
            JOptionPane.showMessageDialog(this, "Book added successfully!", "Success", JOptionPane.INFORMATION_MESSAGE);
            titleField.setText("");
            authorField.setText("");
        }
    }

    // Display all books in the library
    private void displayBooks() {
        StringBuilder sb = new StringBuilder();
        for (Book book : library.getBooks()) {
            sb.append(book).append("\n");
        }
        displayArea.setText(sb.toString());
    }

    // Check out a book
    private void checkOutBook() {
        String title = titleField.getText();
        if (title.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please enter the book title to check out.", "Error", JOptionPane.ERROR_MESSAGE);
        } else {
            boolean success = library.checkOutBook(title);
            if (success) {
                JOptionPane.showMessageDialog(this, "You have checked out the book: " + title, "Success", JOptionPane.INFORMATION_MESSAGE);
            } else {
                JOptionPane.showMessageDialog(this, "Book not available or not found.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    // Return a book
    private void returnBook() {
        String title = titleField.getText();
        if (title.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please enter the book title to return.", "Error", JOptionPane.ERROR_MESSAGE);
        } else {
            boolean success = library.returnBook(title);
            if (success) {
 JOptionPane.showMessageDialog(this, "You have returned the book: " + title, "Success", JOptionPane.INFORMATION_MESSAGE);
            } else {
                JOptionPane.showMessageDialog(this, "Book not found or not checked out.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    // Search for books
    private void searchBooks() {
        String query = searchField.getText();
        if (query.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please enter a title to search.", "Error", JOptionPane.ERROR_MESSAGE);
        } else {
            ArrayList<Book> results = library.searchBooks(query);
            StringBuilder sb = new StringBuilder();
            for (Book book : results) {
                sb.append(book).append("\n");
            }
            if (results.isEmpty()) {
                displayArea.setText("No books found matching: " + query);
            } else {
                displayArea.setText(sb.toString());
            }
        }
    }

    public static void main(String[] args) {
        // Run the GUI in the Event Dispatch Thread
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                LibraryManagementGUI frame = new LibraryManagementGUI();
                frame.setVisible(true);
            }
        });
    }
}


//lIBRARY
import java.util.ArrayList;

public class Library {
    private ArrayList<Book> books;

    public Library() {
        this.books = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public ArrayList<Book> getBooks() {
        return books;
    }

    public boolean checkOutBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title) && book.isAvailable()) {
                book.setAvailable(false);
                return true;
            }
        }
        return false;
    }

    public boolean returnBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title) && !book.isAvailable()) {
                book.setAvailable(true);
                return true;
            }
        }
        return false;
    }

    public ArrayList<Book> searchBooks(String query) {
        ArrayList<Book> results = new ArrayList<>();
        for (Book book : books) {
            if (book.getTitle().toLowerCase().contains(query.toLowerCase())) {
                results.add(book);
            }
        }
        return results;
    }
}


//Book

import java.util.ArrayList;

public class Library {
    private ArrayList<Book> books;

    public Library() {
        this.books = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public ArrayList<Book> getBooks() {
        return books;
    }

    public boolean checkOutBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title) && book.isAvailable()) {
                book.setAvailable(false);
                return true;
            }
        }
        return false;
    }

    public boolean returnBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title) && !book.isAvailable()) {
                book.setAvailable(true);
                return true;
            }
        }
        return false;
    }

    public ArrayList<Book> searchBooks(String query) {
        ArrayList<Book> results = new ArrayList<>();
        for (Book book : books) {
            if (book.getTitle().toLowerCase().contains(query.toLowerCase())) {
                results.add(book);
            }
        }
        return results;
    }
}

