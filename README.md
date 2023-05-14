# CustomEmailThroughSrevlets
CREATE TABLE contacts (
    serial_no SERIAL,
    name VARCHAR(255),
    mail_id VARCHAR(255) PRIMARY KEY,
    date_of_birth DATE,
	ph_no numeric(10,0)
);
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Akshaya','akshayavarma39@gmail.com','03-07-2002',9603442969);
select * from contacts;
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Varma','varmaakula506@gmail.com','04-07-1972',9247139775);
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Amarthya','amarthyavarmaakula@gmail.com','21-09-1999',9848422148);





//HTML FILE

<!DOCTYPE html>
<html>
<meta charset="ISO-8859-1">
<title>CustomEmail</title>

<script>


window.onload = function(){
	con();
	automaticgetInfo()
	automaticSend()
}
var request;
function con(){
	if(window.XMLHttpRequest){  
		request=new XMLHttpRequest();  
		}  
		else if(window.ActiveXObject){  
		request=new ActiveXObject("Microsoft.XMLHTTP");  
		}  
}

function automaticSend(){
	var url="automaticBirthdayWishes"; 
	try  
	{  
	request.onreadystatechange=automaticgetInfo;  
	request.open("POST",url,true); 
	request.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
	request.send();  
	}  
	catch(e)  
	{  
	alert("Unable to connect to server");  
	}  
}
function automaticgetInfo(){  
	if(request.readyState==4){  
	var val=request.responseText;  
	//document.getElementById('too').innerHTML=val;  
	  
	}  

}
function sendInfo()  
{  
var url="emailListServlet"; 
try  
{  
request.onreadystatechange=getInfo;  
request.open("POST",url,true); 
request.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
request.send();  
}  
catch(e)  
{  
alert("Unable to connect to server");  
}  
}  
 
function getInfo(){  
if(request.readyState==4){  
var val=request.responseText;  
document.getElementById('too').innerHTML=val;  
  
}  
} 
function updateEmailList() {
	var emailList = "";
	var checkboxes = document.getElementsByName("emailList");
	for (var i = 0; i < checkboxes.length; i++) {
		if (checkboxes[i].checked) {
			emailList += checkboxes[i].value + ", ";
		}
	}
	document.getElementById("email").value = emailList.slice(0, -2);
	//after click ok to hide the dropdown
	document.getElementById("too").style.display = "none";
}


</script>


<head>
	<title>Email Front-End Page</title>
	<style>
		body {
			font-family: Arial, sans-serif;
			background-color: #f4f4f4;
		}
		.container {
			margin: 0 auto;
			width: 50%;
			background-color: #fff;
			padding: 20px;
			box-shadow: 0 2px 5px rgba(0,0,0,0.3);
		}
		label, textarea {
			display: block;
			margin-bottom: 10px;
			width: 100%;
			box-sizing: border-box;
			font-size: 16px;
			line-height: 1.4;
		}
		input[type="submit"] {
			background-color: #4CAF50;
			color: #fff;
			border: none;
			border-radius: 10px;
			padding: 10px 10px;
			font-size: 16px;
			cursor: pointer;
			float: right;
			margin-right:10px;
			margin-top:10px;
		}
		input[type="submit"]:hover {
			background-color: #3e8e41;
		}
		
		#dropdownmargin{
		margin:20px;}
		.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {

  display: none;
  position: absolute;
  z-index: 1;
  background-color: #f9f9f9;

    width:350px;
  min-width: 250px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  margin-top: 5px;
  border-radius: 5px;
  overflow: auto;
  max-height: 200px;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown-content label {
  display: block;
  margin-bottom: 5px;
}

.dropdown-content input[type="checkbox"] {
  margin-right: 5px;
  display: inline-block;
}

.dropdown-content label:hover {
  background-color: #f1f1f1;
}

.dropdown-content input[type="checkbox"]:checked + label {
  background-color: #f1f1f1;
}
		
	</style>

</head>
<body>
	<div class="container">
		<h2>Send Email</h2>
		
		<form action="multipleEmailSend" method="post">
			<label for="name">Name</label>
			<input type="text" id="name" name="name" required>
			
			<label for="email">Email</label>
			<div class="dropdown">
				<input type="text" id="email" name="email" readonly required  onclick="sendInfo()">	
				<p id="too"></p>
			<!--
		 	<div class="dropdown-content"  >
					<label><input type="checkbox" name="emailList" value="akshayavarma39@gmail.com">akshayavarma39@gmail.com</label>
					<label><input type="checkbox" name="emailList" value="akshayavarma39@gmail.com">akshayavarma39@gmail.com</label>
					<label><input type="checkbox" name="emailList" value="akshayavarma39@gmail.com">akshayavarma39@gmail.com</label>
				
					<button type="submit" value="OK" onclick="updateEmailList()" >OK</button>
				</div>  -->	
			
				
			
			 	
			
			</div>
			<div class="d-flex flex-row justify-content-center">
				<div>
					<label for="subject">Subject</label>
					<input type="text" id="subject" name="subject" required>
				</div>
				
			</div>	
			
			<label for="message">Message</label>
			<textarea id="message" name="message" rows="5" required></textarea>
			
			<div>
					<label for="scheduledTime">Scheduled Time</label>
						<div class="input-group date" id="datetimepicker">
							<input type="text" id="scheduledTime" name="scheduledTime" class="form-control" required>
							<span class="input-group-addon">
							<span class="glyphicon glyphicon-calendar"></span>
							</span>
						</div>
				</div>
			
				
			<input type="submit"  class="mr-3" value="ScheduledSend">
			
			<!--  <input type="submit" value="Send"> -->
		</form>
	</div>
	
	
	
	
	
	
	
	<!-- Bootstrap CSS --> 
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">

<!-- Bootstrap DateTimePicker CSS -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datetimepicker/4.17.47/css/bootstrap-datetimepicker.min.css" />

<!-- jQuery -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- Moment.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.18.1/moment.min.js"></script>  

<!-- Bootstrap JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script> 


<!-- Bootstrap DateTimePicker JavaScript -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datetimepicker/4.17.47/js/bootstrap-datetimepicker.min.js"></script>
	
	<script>$(function () {
	    $('#datetimepicker').datetimepicker({
	        format: 'YYYY-MM-DD HH:mm:ss'
	    });
	});
</script>
	
	
	
	
	
	
	
	
</body>
</html>

	
	
	
	
	//multipleEmailSendServlet
	

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Calendar;
import java.util.Date;
import java.util.Properties;
import java.util.TimerTask;
import java.text.ParseException;
import java.util.Timer;


import java.text.SimpleDateFormat;
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class multipleEmailSend
 */
@WebServlet("/multipleEmailSend")
public class multipleEmailSend extends HttpServlet {
	private static final long serialVersionUID = 1L;
	 final String user="akshayaakula047@gmail.com"; 
	 final String password="passwordak";
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public multipleEmailSend() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		
		String scheduledTimeStr = request.getParameter("scheduledTime");
		SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Date scheduledTime=null;
		try {
			scheduledTime = dateFormat.parse(scheduledTimeStr);
		} catch (ParseException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		Calendar calendar = Calendar.getInstance();
		Date currentTime = calendar.getTime();
		
		
		// Get form data from the request
        String name = request.getParameter("name");
        String email = request.getParameter("email");
        String subject = request.getParameter("subject");
        String message = request.getParameter("message");
       // String[] checkboxOptions = request.getParameterValues("emailList");
    
        // Set up email properties
        Properties properties = new Properties();
        properties.put("mail.smtp.auth", "true");
        properties.put("mail.smtp.starttls.enable", "true");
        properties.put("mail.smtp.host", "smtp.gmail.com");
        properties.put("mail.smtp.port", "587");

        // Set up email session
       

        Session session = Session.getInstance(properties, new javax.mail.Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication(user,password);
            }
        });
      
        try {
            // Create a new message
            Message emailMessage = new MimeMessage(session);

            // Set the sender and recipient addresses
            emailMessage.setFrom(new InternetAddress(user));
            emailMessage.setRecipients(Message.RecipientType.TO, InternetAddress.parse(email));

            // Set the email subject and body
            emailMessage.setSubject(subject);
            emailMessage.setText("Name: " + name + "\n\nMessage: " + message);
            
            if (scheduledTime.compareTo(currentTime) <= 0) {
                Transport.send(emailMessage);
            } else {
                // Schedule email for later
                Timer timer = new Timer();
                timer.schedule(new TimerTask() {
                    public void run() {
                        try {
                            Transport.send(emailMessage);
                        } catch (MessagingException e) {
                            e.printStackTrace();
                        }
                    }
                }, scheduledTime);
            }
           
           
            // Return a success message to the user
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html><body>");
            out.println("<h3>Email sent successfully!</h3>");
            out.println("</body></html>");

        } catch (MessagingException e) {
            // Return an error message to the user
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html><body>");
            //out.println(""+checkboxOptions);
            out.println("hello");
            out.println("<h3>Error sending email: " + e.getMessage() + "</h3>");
            out.println("</body></html>");
        }
		
		
		doGet(request, response);
	}

}
							 
							 
							 
							 
							 
							 
							 

							 
							 
							 
							 
							 //EmailListRetrievingServlet
							 
							 
							 

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class emailListServlet
 */
@WebServlet("/emailListServlet")
public class emailListServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
	
	 final String user="akshayaakula047@gmail.com"; 
	 final String password="passwordak";
    /**
     * @see HttpServlet#HttpServlet()
     */
    public emailListServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		String s1="<div class=\"dropdown-content\" > <div id=\"dropdownmargin\">";
		PrintWriter pw = response.getWriter();
		Connection c = null;
		Statement s = null;
		ResultSet rs = null;
		try {
			Class.forName("org.postgresql.Driver");
			c = DriverManager.getConnection(
					"jdbc:postgresql://LocalHost:5432/postgres?user=postgres&password=Akshaya@2001");
			s = c.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);
			rs = s.executeQuery("select * from contacts");
			rs.absolute(0);
			while (rs.next()) {
			    s1 += "<label><input type=\"checkbox\" name=\"emailList\" value=\"" + rs.getString(3) + "\">";
			    s1 += rs.getString(3) + "</label>";
			}
			s1 += "<button type=\"submit\" value=\"OK\" onclick=\"updateEmailList()\" >OK</button></div></div>";

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		};
		
		pw.print(s1);
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		//String s1 = "<div class=\"dropdown-content\"  > ";
		
		doGet(request, response);
	}

}


							 
							 
							 
							 
							 
							 
							 
							 
							 
							 //AutomaticBirthdayWishesServlet
							 
							 
							 
							 
							 
							 
							 
							 

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;

import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class automaticBirthdayWishes
 */
@WebServlet("/automaticBirthdayWishes")
public class automaticBirthdayWishes extends HttpServlet {
	private static final long serialVersionUID = 1L;
	 final String user="akshayaakula047@gmail.com"; 
	 final String password="passwordak";   
    /**
     * @see HttpServlet#HttpServlet()
     */
    public automaticBirthdayWishes() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		//response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		String s1="";
		PrintWriter pw = response.getWriter();
		Connection c = null;
		Statement s = null;
		ResultSet rs = null;
		try {
			
			Class.forName("org.postgresql.Driver");
			c = DriverManager.getConnection(
					"jdbc:postgresql://LocalHost:5432/postgres?user=postgres&password=Akshaya@2001");
			s = c.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);
			rs = s.executeQuery("select * from contacts where extract(day from current_date)=extract(day from date_of_birth) and\r\n"
					+ " extract(month from current_date)=extract(month from date_of_birth)");
			rs.absolute(0);
	
			while (rs.next()) {
			   s1+=rs.getString(3)+",";
			}
			

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		};
		//pw.print(s1);
		// Get form data from the request
        String name = "Akshaya";
        String email = s1;
        String subject = "Happy Birthday Dear";
        String message = "Happy Birthday to you ! Live Long";
		
		 // Set up email properties
        Properties properties = new Properties();
        properties.put("mail.smtp.auth", "true");
        properties.put("mail.smtp.starttls.enable", "true");
        properties.put("mail.smtp.host", "smtp.gmail.com");
        properties.put("mail.smtp.port", "587");

        // Set up email session
       

        Session session = Session.getInstance(properties, new javax.mail.Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication(user,password);
            }
        });

        try {
            // Create a new message
            Message emailMessage = new MimeMessage(session);

            // Set the sender and recipient addresses
            emailMessage.setFrom(new InternetAddress(user));
            emailMessage.setRecipients(Message.RecipientType.TO, InternetAddress.parse(email));

            // Set the email subject and body
            emailMessage.setSubject(subject);
            emailMessage.setText("Name: " + name + "\n\nMessage: " + message);

            // Send the email
            Transport.send(emailMessage);

//            // Return a success message to the user
//            response.setContentType("text/html");
//            PrintWriter out = response.getWriter();
//            out.println("<html><body>");
//            out.println("<h3>Email sent successfully!</h3>");
//            out.println("</body></html>");

        } catch (MessagingException e) {
            // Return an error message to the user
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html><body>");
            //out.println(""+checkboxOptions);
            out.println("hello");
            out.println("<h3>Error sending email: " + e.getMessage() + "</h3>");
            out.println("</body></html>");
        }
		
		
		
		
		doGet(request, response);
	}

}

							 
							 
							 
							 
