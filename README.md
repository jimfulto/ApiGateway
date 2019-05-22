# ApiGateway Service

## Useful APIs

   [Employee Service](https://github.com/KeyurTankaria9/EmployeeServiceBackend): Service that provides details of an Employee.
   [Calling Employee Service with /all endpoint](https://apigatewayservice.cfapps.io/employees/all)
    

# build.gradle

    ext {
          set('springCloudVersion', 'Greenwich.SR1')
        }

    dependencies {
        implementation 'org.springframework.cloud:spring-cloud-starter-netflix-zuul'
    }

    dependencyManagement {
        imports {
             mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
        }
    }

# In Api Gateway service /Application.properties - add in new microservices here:

   When a service calls API gatway service with /employee/** endpoint, then it will get redirect or route to https://employeebackendservice.cfapps.io/employees/all url endpoint.
   
    zuul.routes.employee.path=/employee/**
    zuul.routes.employee.url=https://employeebackendservice.cfapps.io/employees/all


# In actual Employee web service, on top of the controller add below to accept any host to access the operation.
  
  In Main application of Actual web service Employee in controller on top add,
  
    @CrossOrigin(origins = "*", maxAge = 3600)
    @RestController
    @RequestMapping("/employee")
    public class EmployeeController {
    }
