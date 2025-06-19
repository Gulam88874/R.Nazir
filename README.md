Application.propeeties
spring.application.name=democrud
spring.datasource.url=jdbc:mysql://localhost:3306/test_crud_db
spring.datasource.username=root
spring.datasource.password=Rashid@1234

spring.jpa.hibernate.ddl-auto=update

spring.jpa.show-sql=true
########################################################################
DemoCrudApllication
package com.democrud;

import org. org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemocrudApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemocrudApplication.class, args);
	}

}

########################################################

Employee.java

package com.democrud.entity;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name="employees")
public class Employee {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private long id;
	
	
	@Column(name="first_name" ,nullable=false, length=45)
	private String firstname;
	
	@Column(name="last_name" ,nullable=false, length=45)
	private String lastname;
	
	@Column(name="email_id", nullable=false, length=45,unique=true)
	private String emailId;
	
	@Column(name="mobile", nullable=false, unique=true)
	private String mobile;

	public long getId() {
		return id;
	}

	public void setId(long id) {
		this.id = id;
	}

	public String getFirstname() {
		return firstname;
	}

	public void setFirstname(String firstname) {
		firstname = firstname;
	}

	public String getLastname() {
		return lastname;
	}

	public void setLastname(String lastname) {
		lastname = lastname;
	}

	public String getEmailId() {
		return emailId;
	}

	public void setEmailId(String emailId) {
		emailId = emailId;
	}

	public String getMobile() {
		return mobile;
	}

	public void setMobile(String mobile) {
		this.mobile = mobile;
	}	

}

#############################################################################################
DemoCrudApplication

package com.democrud;

import java.util.List;
import java.util.Optional;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import com.democrud.entity.Employee;
import com.democrud.repository.EmployeeRepository;

@SpringBootTest
class DemocrudApplicationTests {
	@Autowired
	private EmployeeRepository employeeRepository;

	@Test
	void saveRecord() {
		Employee emp=new Employee();
		emp.setFirstname("mike");
		emp.setLastname("nazib");
		emp.setEmailId("mikenazib@gmail.com");
		emp.setMobile("6200374022");
		employeeRepository.save(emp);	
	}
	@Test
	void deleteRecord() {
		employeeRepository.deleteById(3L);

}
	@Test
	void updateRecord() {
		Employee emp=new Employee();
		emp.setId(1L);
		emp.setFirstname("mike");
		emp.setLastname("nazirr");
		emp.setEmailId("mikenazirr@gmail.com");
		emp.setMobile("6200374026");
		employeeRepository.save(emp);
		
}
	
	@Test
	void getRecordById() {
		Optional<Employee> opEmp = employeeRepository.findById(7L);
		if(opEmp.isPresent()) {
			Employee employee = opEmp.get();
			System.out.println(employee.getId());
			System.out.println(employee.getFirstname());
			System.out.println(employee.getLastname());
			System.out.println(employee.getEmailId());
			System.out.println(employee.getMobile());
		}else {
			System.out.println("no record found");
			
		}
		
		
}
	
	@Test
	void getRecords() {
		Iterable<Employee> itrEmp = employeeRepository.findAll();
		for(Employee employee :itrEmp) {
			System.out.println(employee.getId());
			System.out.println(employee.getFirstname());
			System.out.println(employee.getLastname());
			System.out.println(employee.getEmailId());
			System.out.println(employee.getMobile());
			
		}		
	
}
	@Test
	void countRecord() {
		long count = employeeRepository.count();
		System.out.println(count);
	}
	
	@Test
	void findByEmail() {
		Optional<Employee> opEmp = employeeRepository.findByEmailId("mikenazi@gmail.com");
		if(opEmp.isPresent()) {
			Employee employee = opEmp.get();
			System.out.println(employee.getId());
			System.out.println(employee.getFirstname());
			System.out.println(employee.getLastname());
			System.out.println(employee.getEmailId());
			System.out.println(employee.getMobile());
		}else {
			System.out.println("no record found");
			
		}
	}
		
		@Test
		void findByMobile() {
			Optional<Employee> opEmp = employeeRepository.findByMobile("6200374026");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
				
			}
	}
		
		@Test
		void existsBYEmail() {
			boolean result = employeeRepository.existsByEmailId("mikenazi@gmail.com");
			if(result) {
				System.out.println("Record exists");
			}else {
				System.out.println("no record found");
				
			}
}
		@Test
		void existsByMobile() {
			boolean result = employeeRepository.existsByMobile("6200374026");
			if(result) {
				System.out.println("Record exists");
			}else {
				System.out.println("no record found");
				
			}
}
		
		@Test
		void countByEmail() {
			long result = employeeRepository.countByEmailId("mikenazi@gmail.com");
			System.out.println(result);
				
		
		}
	
		@Test
		void searchByEmialAndMobile() {
			Optional<Employee> opEmp =employeeRepository.findByEmailIdAndMobile("mikenazi@gmail.com","6200374028");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
				
			}
		}
		

		@Test
		void searchByEmailIdOrMobile() {
			List<Employee> emp =employeeRepository.findByEmailIdOrMobile("mikenazirr", "6200374026");
			for(Employee e:emp) {
				System.out.println(e.getFirstname());
				System.out.println(e.getLastname());
				System.out.println(e.getMobile());
				System.out.println(e.getEmailId());
			}
		}
		
		@Test
		void searchByEmail() {
			Optional<Employee> opEmp =employeeRepository.searchByEmail("mikenazirr@gmail.com");
			
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
			 
}
		}
		
		@Test
		void searchByMobile() {
			Optional<Employee> opEmp =employeeRepository.searchByMobile("6200374028");
			
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
}
		}
		@Test
		void getByEmailAndMobile() {
			Optional<Employee> opEmp =employeeRepository.findByEmailIdAndMobile("mikenazirr","6200374028");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
				
			}
		}
		@Test
		void getByEmailOrMobile() {
			List<Employee> emp =employeeRepository.findByEmailIdOrMobile("mikenazirr", "6200374026");
			for(Employee e:emp) {
				System.out.println(e.getFirstname());
				System.out.println(e.getLastname());
				System.out.println(e.getMobile());
				System.out.println(e.getEmailId());
			}
		}
		@Test
		void searchByEmailIdSql() {
			Optional<Employee> opEmp =employeeRepository.findByEmailIdUsingSQl("mikenazib@gmail.com");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
			}
		}
		@Test
		void searchByMobileSql() {
			Optional<Employee> opEmp =employeeRepository.findByMobileUsingSQl("6200374026");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
			}
		}
		@Test
		void getByEmailAndMobileSql() {
			Optional<Employee> opEmp =employeeRepository.findByEmailandMobileUsingSQl("mikenazirr","6200374028");
			if(opEmp.isPresent()) {
				Employee employee = opEmp.get();
				System.out.println(employee.getId());
				System.out.println(employee.getFirstname());
				System.out.println(employee.getLastname());
				System.out.println(employee.getEmailId());
				System.out.println(employee.getMobile());
			}else {
				System.out.println("no record found");
				
			}
		
		
			}
			
}
#############################################################################################
EmployeeRepository

package com.democrud.repository;

import java.util.List;
import java.util.Optional;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.data.repository.query.Param;

import com.democrud.entity.Employee;

public interface EmployeeRepository extends CrudRepository<Employee, Long> {


	Optional<Employee> findByEmailId(String email);
	
	Optional<Employee>findByMobile(String mobile);
	
	boolean existsByEmailId(String email);
	
	boolean existsByMobile(String mobile);
	
	long countByEmailId(String email);
	
	Optional<Employee> findByEmailIdAndMobile(String email, String mobile);
	
	   List<Employee> findByEmailIdOrMobile(String email,String mobile);
	
	@Query("select e from Employee e where e.emailId=:x")
    Optional<Employee> searchByEmail(@Param("x")String email);
	
	@Query("select e from Employee e where e.mobile=:m")
	     Optional<Employee>searchByMobile(@Param("m")String mobile);
	
	@Query("select e from Employee e where e.emailId=:x and e.mobile=:m")
	Optional<Employee> searchByEmailIdAndMobile(@Param("x")String emailId,@Param("m")String mobile);

	
	@Query("select e from Employee e where e.emailId=:x or e.mobile=:m")
	List<Employee> searchByEmailIdOrMobile(@Param("x")String emailId,@Param("m")String mobile);
	
	@Query(value = "SELECT * FROM employees WHERE email_id = ?1", nativeQuery = true)
	Optional<Employee> findByEmailIdUsingSQl(String email);
	
	
	@Query(value="SELECT * FROM employees WHERE mobile= ?1",nativeQuery=true)
	Optional<Employee> findByMobileUsingSQl(String mobile);

     
	@Query(value="SELECT * FROM employee WHERE email_id=?1 and Mobile=?2",nativeQuery=true)
	Optional<Employee> findByEmailandMobileUsingSQl(String Email,String Mobile);
	
	
}


		
	



