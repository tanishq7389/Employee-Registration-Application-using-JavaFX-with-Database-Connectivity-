import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class EmployeeManagementApp extends Application {
    private ObservableList<Employee> employeeList = FXCollections.observableArrayList();

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Employee Management App");

        // Creating input fields
        TextField idField = new TextField();
        idField.setPromptText("Employee ID");
        TextField nameField = new TextField();
        nameField.setPromptText("Name");
        TextField ageField = new TextField();
        ageField.setPromptText("Age");
        TextField emailField = new TextField();
        emailField.setPromptText("Email");
        TextField departmentField = new TextField();
        departmentField.setPromptText("Department");

        // Creating buttons
        Button addButton = new Button("Add Employee");
        Button viewButton = new Button("View Employees");
        Button updateButton = new Button("Update Employee");

        // Adding event handlers
        addButton.setOnAction(event -> {
            String id = idField.getText();
            String name = nameField.getText();
            int age = Integer.parseInt(ageField.getText());
            String email = emailField.getText();
            String department = departmentField.getText();

            Employee employee = new Employee(id, name, age, email, department);
            employeeList.add(employee);

            clearFields(idField, nameField, ageField, emailField, departmentField);
        });

        viewButton.setOnAction(event -> {
            displayEmployeeList();
        });

        updateButton.setOnAction(event -> {
            String id = idField.getText();
            Employee employeeToUpdate = findEmployeeById(id);
            if (employeeToUpdate != null) {
                employeeToUpdate.setName(nameField.getText());
                employeeToUpdate.setAge(Integer.parseInt(ageField.getText()));
                employeeToUpdate.setEmail(emailField.getText());
                employeeToUpdate.setDepartment(departmentField.getText());
                System.out.println("Employee with ID " + id + " updated successfully!");
            } else {
                System.out.println("Employee with ID " + id + " not found!");
            }
        });

        // Creating a grid pane for layout
        GridPane gridPane = new GridPane();
        gridPane.setHgap(10);
        gridPane.setVgap(10);

        // Adding components to the grid pane
        gridPane.addRow(0, new Label("Employee ID:"), idField);
        gridPane.addRow(1, new Label("Name:"), nameField);
        gridPane.addRow(2, new Label("Age:"), ageField);
        gridPane.addRow(3, new Label("Email:"), emailField);
        gridPane.addRow(4, new Label("Department:"), departmentField);
        gridPane.addRow(5, addButton);
        gridPane.addRow(6, viewButton);
        gridPane.addRow(7, updateButton);

        // Creating the scene
        Scene scene = new Scene(gridPane, 400, 300);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void clearFields(TextField... fields) {
        for (TextField field : fields) {
            field.clear();
        }
    }

    private void displayEmployeeList() {
        System.out.println("Registered Employees:");
        for (Employee employee : employeeList) {
            System.out.println(employee);
        }
    }

    private Employee findEmployeeById(String id) {
        for (Employee employee : employeeList) {
            if (employee.getId().equals(id)) {
                return employee;
            }
        }
        return null;
    }

    // Employee class
    static class Employee {
        private String id;
        private String name;
        private int age;
        private String email;
        private String department;

        public Employee(String id, String name, int age, String email, String department) {
            this.id = id;
            this.name = name;
            this.age = age;
            this.email = email;
            this.department = department;
        }

        // Getters and setters
        public String getId() {
            return id;
        }

        public void setId(String id) {
            this.id = id;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public int getAge() {
            return age;
        }

        public void setAge(int age) {
            this.age = age;
        }

        public String getEmail() {
            return email;
        }

        public void setEmail(String email) {
            this.email = email;
        }

        public String getDepartment() {
            return department;
        }

        public void setDepartment(String department) {
            this.department = department;
        }

        @Override
        public String toString() {
            return "Employee{" +
                    "id='" + id + '\'' +
                    ", name='" + name + '\'' +
                    ", age=" + age +
                    ", email='" + email + '\'' +
                    ", department='" + department + '\'' +
                    '}';
        }
    }
}
