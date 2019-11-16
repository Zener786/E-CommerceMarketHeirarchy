
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import static java.util.Spliterators.iterator;

/**
 *
 * @author ZAINAB
 */class Employee
{
    String name;
    String id;
     public String getID() {
      return id;
   }
   
   public void setID(String id) {
      this.id = id;
   }
   
   public String getName() {
      return name;
   }
   
   public void setName(String name) {
      this.name = name;
   }
}

class EmployeeView
{
    public void printDetails( List<Employee> e1)
    {
     
//      for(int i=0;i<e1.size();i++){
//      System.out.println(e1.get(i));
      Iterator itr= e1.iterator(); 
{
         
     while(itr.hasNext())
    {  
      Employee e=(Employee)itr.next();
        System.out.println(e.getID()+"\t"+e.getName());
       
    }
    
    
    /*while(itr.hasNext())
          {
              System.out.println(e1);
          }
      
      } 
    }*/
   
}

    }
}
class Controller 
{
   
    ArrayList<Employee> e;
    EmployeeView v;
    
      Controller(ArrayList<Employee> m, EmployeeView view) {
          
        this.e=m;
        this.v=view;
    }

    Controller(ArrayList<Employee>m) {
       this.e=m;
    }
    
    public void setName(List<Employee> name)
    {
        this.e= new ArrayList<Employee>(name);  
    }
    
     

   public List<Employee> getName(){
      return e;  
   }

   public void setID(List<Employee> id){
      	this.e= new ArrayList<Employee>(id); 	
   }

   public List<Employee> getID(){
      return e;	
   }

   public void updateView(){				
      v.printDetails(e);
   }	
   
   public ArrayList<Employee> getAllEmployees()
   {
       return e;
   }
}


interface Developer
{
    public void showEmployeeDetails() ;
    
}

class Dev1 implements Developer
{ 
    private String name; 
    private long empId; 
    private String position; 
    
  
    public Dev1(long empId, String name, String position) 
    { 
        this.empId = empId; 
        this.name = name; 
        this.position = position; 
    } 

       public void showEmployeeDetails()  
    { 
        System.out.println(empId+" " +name+ " " + position ); 
    } 
} 


class Dev2 implements Developer 
{ 
    private String name; 
    private long empId; 
    private String position; 
    
    public Dev2(long empId, String name, String position) 
    { 
        this.empId = empId; 
        this.name = name; 
        this.position = position; 
    } 


    
    
      public void showEmployeeDetails()  
    { 
        System.out.println(empId+" " +name+ " " + position ); 
    } 
    
}

class BusinessLookUp  
{ 
    public Developer getBusinessService(String serviceType) 
    { 
        if(serviceType.equalsIgnoreCase("Dev1")) 
        { 
            return new Dev1(1,"Rashmi","CEO");
        } 
        else
        { 
            return new Dev2(1,"",""); 
        } 
   } 
}

class BusinessDelegate 
{ 
    private BusinessLookUp lookupService = new BusinessLookUp(); 
    private Developer businessService; 
    private String serviceType; 
  
    public void setServiceType(String serviceType) 
    { 
    this.serviceType = serviceType; 
    } 
  
    public void doTask() 
    { 
        businessService = lookupService.getBusinessService(serviceType); 
        businessService.showEmployeeDetails();
    } 
} 

class Client  
{ 
    BusinessDelegate businessService; 
  
    public Client(BusinessDelegate businessService) 
    { 
        this.businessService  = businessService; 
    } 
  
    public void doTask() 
    {         
        businessService.doTask(); 
    } 
} 
  


interface Insert
{
    public void insertingDev(String name,String id);
    public void insertingDir1(String name,String id);
    public void insertingDir2(String name,String id);
}
  
class Composite implements Developer
{ 
    private List<Developer> employeeList = new ArrayList<Developer>(); 
       
    
        
    @Override
    public void showEmployeeDetails()  
    { 
        for(Developer emp:employeeList) 
        { 
            emp.showEmployeeDetails(); 
        } 
    } 
       
    public void addEmployee(Developer emp) 
    { 
        employeeList.add((Developer) emp); 
    } 
       
    public void removeEmployee(Developer emp) 
    { 
        employeeList.remove(emp); 
    } 
    
    public void insertingDev(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
//            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
//            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

            
            String sq = "INSERT INTO DEVELOPER"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
                
//              System.out.println(name);
//              System.out.println(id);
//            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 
    
    
    
    public void insertingDir1(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
//            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
//            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

             
            String sq = "INSERT INTO DIRECTOR1"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
//                
//              System.out.println(name);
//              System.out.println(id);
            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 
    
    public void insertingDir2(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
//            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
//            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

            
            String sq = "INSERT INTO DIRECTOR2"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
                
//              System.out.println(name);
//              System.out.println(id);
//            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 
    
}
 
class InsertInto implements Insert
{
    @Override
    public void insertingDev(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

             System.out.println("Method ");
            String sq = "INSERT INTO DEVELOPER"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
                
              System.out.println(name);
              System.out.println(id);
            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 
    
    
    @Override
    public void insertingDir1(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

             System.out.println("Method ");
            String sq = "INSERT INTO DIRECTOR1"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
                
              System.out.println(name);
              System.out.println(id);
            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 
    
    public void insertingDir2(String name,String id)
    {
        
            
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

             System.out.println("Method ");
            String sq = "INSERT INTO DIRECTOR2"+"(name,id)"+"VALUES(?,?)";
            PreparedStatement pr = conn.prepareStatement(sq);
            
                pr.setString(1,name);
                pr.setString(2,id);
                
                
              System.out.println(name);
              System.out.println(id);
            
             pr.executeUpdate();
        }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
           


            }
           //executeBatch();
        } 

}

 
        
class E1
{
     static ArrayList<Employee> RetrieveFromDatabase()
    {
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
                ArrayList <Employee> ListOfEmployees = new ArrayList<>();
                Employee e=null;
        try {
//        Step 1: Register the driver class
            Class.forName("org.apache.derby.jdbc.ClientDriver");
            System.out.println("Driver registered");

//        STEP 2: Establish Connection
            conn = DriverManager.getConnection("jdbc:derby://localhost:1527/pqr", "pqr", "pqr");
            System.out.println("Connection established");

//        Step 3: Create Statement
            stmt = conn.createStatement();

            String query1 = "select * from DEVELOPER";
//    //    String query2 = "delete from Student where roll = 4";

//        Step 4:Execute the query
            rs = stmt.executeQuery(query1);//for  select query
//    //    int rowsAffected = stmt.executeUpdate(query2);//for insert/update/delete

//        Step 5: Process the ResultSet
          
                
                while (rs.next()) {
                    e=new Employee();
                    e.setName(rs.getString("name"));
                    e.setID(rs.getString("id"));
                     ListOfEmployees.add(e); 
                  
                    }
                 
              
            }
        
         catch (ClassNotFoundException ex) {
            System.out.println(ex);
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
         finally
        {   //        Step 6: Close all resources
            try {
                if(rs!=null)
                    rs.close();
                if(stmt!=null)
                    stmt.close();
                if(conn!=null)
                    conn.close();
            } catch (SQLException ex) {
                System.out.println("Exception occured while releasing resources");
            }
       
        }
          return ListOfEmployees;
    } 
        
     
     
     
     
     

    }
      
    
     
        

   

public class Dp  {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args)throws SQLException, ClassNotFoundException {
           {
        Developer CEO = new Dev1(1, "Rashmi Agrawal", "CEO"); 
        
        Composite DirectorTeam=new Composite();
        Developer director1= new Dev1(102, "Vinay Sharma", "director"); 
        Developer director2= new Dev1(103, "Manaswi Purohit", "director");
        DirectorTeam.addEmployee(director1);
        DirectorTeam.addEmployee(director2);
        
        
        Composite c=new Composite();
        c.insertingDir1("Zainab", "4");
        c.insertingDir1("Anshul", "5");
        c.insertingDev("Zainab", "4");
        c.insertingDev("Anshul", "5");
        
        c.insertingDir2("Riya", "6");
        c.insertingDir2("Vedant", "7");
        c.insertingDev("Riya", "6");
        c.insertingDev("Vedant", "7");
         
        
        
        Composite Director1Employee=new Composite();
        Developer dev3=new Dev1(104,"Zainab","Employee1.1");
        Developer dev4=new Dev1(105,"Anshul","Employee1.2");
        Director1Employee.addEmployee(dev4);
        Director1Employee.addEmployee(dev3);
        
        
        
        Composite Director2Employee=new Composite();
        Developer dev5=new Dev1(106,"Riya","Employee2.1");
        Developer dev6=new Dev1(107,"Vedant","Employee2.2");
        Director1Employee.addEmployee(dev5);
        Director1Employee.addEmployee(dev6);
        
        
        Composite CEOTeam=new Composite();
        CEOTeam.addEmployee(DirectorTeam);
        CEOTeam.addEmployee(Director1Employee);
        CEOTeam.addEmployee(Director2Employee);
       
        
        
        
        
        
       
        
        
      
       
        
//       Director1Employee.insertingDir1("zainab", "4");
//       Director1Employee.insertingDir1("Anshul", "5");
//       
//       
//        
////        i.insertingDir2("Riya","6");
////        i.insertingDir2("Vedant","7");
//        
//        Director2Employee.insertingDir2("Riya","6");
//        Director2Employee.insertingDir2("Vedant","7");
//        
//        CEOTeam.addEmployee(Director1Employee);
//        CEOTeam.addEmployee(Director2Employee);
////        c.addEmployee(Director1Employee);
////        c.addEmployee(Director2Employee);
         
         System.out.println("CEO team has");
         CEOTeam.showEmployeeDetails();
         E1 e=new E1();
        
        
        ArrayList<Employee> m=e.RetrieveFromDatabase();
        EmployeeView view = new EmployeeView();
        
           
       

      Controller controller = new Controller(m, view);

      controller.updateView();

      //update model data
     

      controller.updateView();
     
      
       Controller studentBusinessObject = new Controller(m);

      //print all students
      for (Employee x : studentBusinessObject.getAllEmployees()) {
         System.out.println("Employee: [ ID: " + x.getID()+"\tName:"+x.getName());
      }
      

        BusinessDelegate businessDelegate = new BusinessDelegate(); 
        businessDelegate.setServiceType("Dev1"); 
  
        Client client = new Client(businessDelegate); 
        client.doTask(); 
  
      //  businessDelegate.setServiceType("Dev1"); 
        client.doTask(); 
      
      
      
   }
        
}
 // TODO code application logic here
    }
    

