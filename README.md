#How to use AccessRemoteMySQLDB?

1. Copy file 'handleSQL.php' to the remote server where your database is located (remember to note down the url of the 'handleSQL.php'. url ex: example.com/somedirectory/handleSQL.php)
2. Add AccessRemoteMySQLDB.jar to your project
3. import required classes and that's all
:)

for any query write me at rohit.sybero@rediffmail.com

example program:


file name: Example.java


import armdb.*;

public class Example {
    
    public static void main(String[] args) {
	
	      String fileURL="http://example.com/some_directory/handleSQL.php";	//url of 'habdleSQL.php', remember that the 'habdleSQL.php' must be in the same server in which interested database is located
        String host="mysql.some_hosting.com";					//server host name
        String user="some_user";						//username
        String pass="some_password";						//password
        String DBName="some_dbname";						//database name
        
	ConnectHost con=new ConnectHost(fileURL, host, user, pass, DBName);	//make connection



	//make a query and print the set of retrieved data

	SQLQuery query=new SQLQuery(con);     					
	try{
            QueryResult qr=query.statement("select * from table_name");		//execution of query statement
            while(qr.nextFlag()){						//setting flag to next row till next row exists
                System.out.println(qr.getValue("column_1")+", ");		//printing column_1 data of the row where flag is set
                System.out.print(qr.getValue("column_2")+", ");			//printing column_2 data of the row where flag is set
                System.out.print(qr.getValue("column_3")+", ");			//printing column_3 data of the row where flag is set
                System.out.print(qr.getValue("column_4"));			//printing column_4 data of the row where flag is set
            }
        }catch(SQLQueryException e){						//catch exception if occurred
            System.out.println(e.getMessage());					//print exception message 
        }



	//execute an update statement and print the number of rows affected	
	
	SQLUpdate update=new SQLUpdate(con);					
        try{
            int rows=update.statement("insert into table_name values ('value_1','value_2','value_3','value_4')");	//execution of update statement
            System.out.println(rows+" no. of rows affected");								//printing no. of affected rows
        }catch(SQLUpdateException e){											//catch exception if occurred
            System.out.println(e.getMessage());										//print exception message
        }
    }
}
