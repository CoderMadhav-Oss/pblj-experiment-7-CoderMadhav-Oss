[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_-JrKZbN)
public class Student {
    private int studentID;
    private String name;
    private String department;
    private int marks;

    public Student(int studentID, String name, String department, int marks) {
        this.studentID = studentID;
        this.name = name;
        this.department = department;
        this.marks = marks;
    }

    // Getters and Setters
    public int getStudentID() { return studentID; }
    public void setStudentID(int studentID) { this.studentID = studentID; }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public String getDepartment() { return department; }
    public void setDepartment(String department) { this.department = department; }

    public int getMarks() { return marks; }
    public void setMarks(int marks) { this.marks = marks; }

    @Override
    public String toString() {
        return "StudentID: " + studentID + ", Name: " + name +
               ", Department: " + department + ", Marks: " + marks;
    }
}
import java.util.*;

public class Main {
    public static void main(String[] args) {
        try {
            StudentController controller = new StudentController();
            Scanner scanner = new Scanner(System.in);
            while (true) {
                System.out.println("\n1. Add Student\n2. View Student\n3. View All\n4. Update\n5. Delete\n6. Exit");
                System.out.print("Choose an option: ");
                int choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        System.out.print("ID: ");
                        int id = scanner.nextInt();
                        scanner.nextLine(); // consume newline
                        System.out.print("Name: ");
                        String name = scanner.nextLine();
                        System.out.print("Department: ");
                        String dept = scanner.nextLine();
                        System.out.print("Marks: ");
                        int marks = scanner.nextInt();
                        controller.addStudent(new Student(id, name, dept, marks));
                        break;

                    case 2:
                        System.out.print("Enter Student ID: ");
                        int sid = scanner.nextInt();
                        Student student = controller.getStudent(sid);
                        System.out.println(student != null ? student : "Student not found");
                        break;

                    case 3:
                        List<Student> list = controller.getAllStudents();
                        for (Student s : list) System.out.println(s);
                        break;

                    case 4:
                        System.out.print("Enter ID to update: ");
                        int uid = scanner.nextInt();
                        scanner.nextLine();
                        System.out.print("New Name: ");
                        String newName = scanner.nextLine();
                        System.out.print("New Dept: ");
                        String newDept = scanner.nextLine();
                        System.out.print("New Marks: ");
                        int newMarks = scanner.nextInt();
                        controller.updateStudent(new Student(uid, newName, newDept, newMarks));
                        break;

                    case 5:
                        System.out.print("Enter ID to delete: ");
                        int did = scanner.nextInt();
                        controller.deleteStudent(did);
                        break;

                    case 6:
                        controller.close();
                        System.out.println("Goodbye!");
                        return;

                    default:
                        System.out.println("Invalid option");
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
