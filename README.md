import java.util.Scanner;

class Node {
    double coefficient;
    int power;
    Node next;
    
    public Node(double coefficient, int power) {
        this.coefficient = coefficient;
        this.power = power;
        this.next = null;
    }
}

public class Polynomial {
    private Node head;
    private int degree;
    private int numTerms;

    public Polynomial() {
        this.head = null;
        this.degree = 0;
        this.numTerms = 0;
    }

    public void addTerm(double coefficient, int power) {
        if (coefficient != 0) {
            Node newNode = new Node(coefficient, power);
            if (head == null || power > head.power) {
                newNode.next = head;
                head = newNode;
            } else {
                Node current = head;
                while (current.next != null && power < current.next.power) {
                    current = current.next;
                }
                newNode.next = current.next;
                current.next = newNode;
            }
            if (power > degree) {
                degree = power;
            }
            numTerms++;
        }
    }

    public double evaluate(double xValue) {
        double result = 0.0;
        Node current = head;
        while (current != null) {
            result += current.coefficient * Math.pow(xValue, current.power);
            current = current.next;
        }
        return result;
    }

    public int getDegree() {
        return degree;
    }

    public int getNumTerms() {
        return numTerms;
    }

    public static void main(String[] args) {
        Polynomial poly = new Polynomial();
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter number of terms: ");
        int numTerms = scanner.nextInt();

        for (int i = 0; i < numTerms; i++) {
            System.out.print("Enter coefficient for term " + (i+1) + ": ");
            double coefficient = scanner.nextDouble();
            System.out.print("Enter power for term " + (i+1) + ": ");
            int power = scanner.nextInt();
            poly.addTerm(coefficient, power);
        }

        System.out.print("Enter the value of x: ");
        double xValue = scanner.nextDouble();

        double result = poly.evaluate(xValue);
        System.out.println("Result for x = " + xValue + ": " + result);

        int degree = poly.getDegree();
        int numPolyTerms = poly.getNumTerms();
        System.out.println("Degree: " + degree);
        System.out.println("Number of Terms: " + numPolyTerms);
    }
}
