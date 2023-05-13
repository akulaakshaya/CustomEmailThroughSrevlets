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
<head>
	<title>Email </title>
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
		label, input[type="email"], textarea {
			display: block;
			margin-bottom: 10px;
			width: 100%;
			box-sizing: border-box;
			border: none;
			border-radius: 5px;
			padding: 10px;
			font-size: 16px;
			line-height: 1.4;
		}
		input[type="submit"] {
			background-color: #4CAF50;
			color: #fff;
			border: none;
			border-radius: 5px;
			padding: 10px 20px;
			font-size: 16px;
			cursor: pointer;
			float: right;
		}
		input[type="submit"]:hover {
			background-color: #3e8e41;
		}
	</style>
</head>
<body>
	<div class="container">
		<h2>Send Email</h2>
		<form action="sendEmailServlet" method="post">
			<label for="name">Name</label>
			<input type="text" id="name" name="name" required>
			
			<label for="email">Email</label>
			
			<select id="email" name="email[]" multiple required>
	<option value="example1@example.com">Example 1</option>
	<option value="example2@example.com">Example 2</option>
	<option value="example3@example.com">Example 3</option>
	<option value="example4@example.com">Example 4</option>
</select>			
			<label for="subject">Subject</label>
			<input type="text" id="subject" name="subject" required>
			
			<label for="message">Message</label>
			<textarea id="message" name="message" rows="5" required></textarea>
			
			<input type="submit" value="Send">
		</form>
	</div>
</body>
</html>






//SERVLET FILE




import java.io.IOException;
import java.util.Properties;

import java.io.PrintWriter;

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
 * Servlet implementation class sendEmailServlet
 */
@WebServlet("/sendEmailServlet")
public class sendEmailServlet extends HttpServlet {
	
	private static final long serialVersionUID = 1L;
	 final String user="akshayaakula047@gmail.com"; 
	 final String password="akD@d2544";
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public sendEmailServlet() {
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
		
		
		
		// Get form data from the request
        String name = request.getParameter("name");
        String email = request.getParameter("email");
        String subject = request.getParameter("subject");
        String message = request.getParameter("message");

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
            out.println("<h3>Error sending email: " + e.getMessage() + "</h3>");
            out.println("</body></html>");
        }
		
		doGet(request, response);
	}

}
