# Let's create an example of a One-to-Many and Many-to-One relationship using Spring Boot with JPA (Java Persistence API) and Hibernate. In this example, we'll model a simple relationship between a "Department" entity and an "Employee" entity. One department can have many employees, and each employee can belong to only one department.

Here are the steps to create the example:

Step 1: Set up the Spring Boot project
Create a new Spring Boot project using your favorite IDE or use Spring Initializr. Include the following dependencies: "Spring Data JPA," "MySQL Driver" (or any other database driver of your choice), and "Spring Web" (for REST API).

Step 2: Create the Department and Employee Entities
Create two classes representing the Department and Employee entities with a One-to-Many and Many-to-One relationship, respectively.

1. Department.java:

```java
import javax.persistence.*;
import java.util.List;

@Entity
@Table(name = "departments")
public class Department {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL)
    private List<Employee> employees;

    // Constructors, getters, and setters (omitted for brevity).
}
```

2. Employee.java:

```java
import javax.persistence.*;

@Entity
@Table(name = "employees")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Constructors, getters, and setters (omitted for brevity).
}
```

Step 3: Set up the database configuration
Configure your database connection properties in the `application.properties` file. Replace the values with your actual database credentials.

```
spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
spring.datasource.username=your_database_username
spring.datasource.password=your_database_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

Step 4: Create a Repository for each Entity
Create two repositories for the Department and Employee entities by extending the JpaRepository interface.

1. DepartmentRepository.java:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface DepartmentRepository extends JpaRepository<Department, Long> {
}
```

2. EmployeeRepository.java:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}
```

Step 5: Implement a REST Controller
Create a REST controller to handle HTTP requests for creating departments and employees and fetching department details along with their employees.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class DepartmentEmployeeController {
    private final DepartmentRepository departmentRepository;
    private final EmployeeRepository employeeRepository;

    @Autowired
    public DepartmentEmployeeController(DepartmentRepository departmentRepository,
                                        EmployeeRepository employeeRepository) {
        this.departmentRepository = departmentRepository;
        this.employeeRepository = employeeRepository;
    }

    @PostMapping("/departments")
    public Department createDepartment(@RequestBody Department department) {
        return departmentRepository.save(department);
    }

    @PostMapping("/employees")
    public Employee createEmployee(@RequestBody Employee employee) {
        return employeeRepository.save(employee);
    }

    @GetMapping("/departments/{id}")
    public Department getDepartment(@PathVariable Long id) {
        return departmentRepository.findById(id).orElse(null);
    }
}
```

Step 6: Test the One-to-Many and Many-to-One Relationship
You can now run the Spring Boot application and use tools like Postman to test the REST API endpoints. For example:

- Create a new department:
  - POST: http://localhost:8080/api/departments
  - Request body: {"name": "HR Department"}

- Create a new employee and associate with the HR department:
  - POST: http://localhost:8080/api/employees
  - Request body: {"name": "John Doe", "department": {"id": 1}}

- Fetch department details along with their employees:
  - GET: http://localhost:8080/api/departments/1

Please note that this example uses the MySQL database, but you can use any other database supported by Hibernate by updating the `application.properties` file accordingly.