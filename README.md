# TY_AWP

2a. Create simple application to perform following operations
i. Finding factorial Value ii. Money Conversion
iii. Quadratic Equation iv. Temperature Conversion
```
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("1. Generate Fibonacci series");
        Console.WriteLine("2. Test for prime numbers");
        Console.WriteLine("3. Test for vowels");
        Console.WriteLine("4. Use of foreach loop with arrays");
        Console.WriteLine("5. Reverse a number and find sum of digits of a number");
        Console.Write("Enter your choice (1-5): ");

        int choice;
        if (int.TryParse(Console.ReadLine(), out choice))
        {
            switch (choice)
            {
                case 1:
                    GenerateFibonacciSeries();
                    break;
                case 2:
                    TestForPrimeNumbers();
                    break;
                case 3:
                    TestForVowels();
                    break;
                case 4:
                    UseForeachLoopWithArrays();
                    break;
                case 5:
                    ReverseNumberAndSumDigits();
                    break;
                default:
                    Console.WriteLine("Invalid choice. Please enter a number between 1 and 5.");
                    break;
            }
        }
        else
        {
            Console.WriteLine("Invalid input. Please enter a valid number.");
        }

        // Wait for user input before closing the console window
        Console.ReadLine();
    }

    static void GenerateFibonacciSeries()
    {
        Console.Write("Enter the number of terms in the Fibonacci series: ");
        if (int.TryParse(Console.ReadLine(), out int n))
        {
            int a = 0, b = 1;
            Console.Write("Fibonacci Series: ");
            for (int i = 0; i < n; i++)
            {
                Console.Write($"{a} ");
                int temp = a;
                a = b;
                b = temp + b;
            }
            Console.WriteLine();
        }
        else
        {
            Console.WriteLine("Invalid input. Please enter a valid number.");
        }
    }

    static void TestForPrimeNumbers()
    {
        Console.Write("Enter a number to test for prime: ");
        if (int.TryParse(Console.ReadLine(), out int num))
        {
            bool isPrime = IsPrime(num);
            Console.WriteLine($"{num} is {(isPrime ? "prime" : "not prime")}.");
        }
        else
        {
            Console.WriteLine("Invalid input. Please enter a valid number.");
        }
    }

    static void TestForVowels()
    {
        Console.Write("Enter a string to test for vowels: ");
        string input = Console.ReadLine();
        bool hasVowels = HasVowels(input);
        Console.WriteLine($"The string {(hasVowels ? "has" : "does not have")} vowels.");
    }

    static void UseForeachLoopWithArrays()
    {
        int[] numbers = { 1, 2, 3, 4, 5 };

        Console.WriteLine("Array elements using foreach loop:");
        foreach (var number in numbers)
        {
            Console.Write($"{number} ");
        }
        Console.WriteLine();
    }

    static void ReverseNumberAndSumDigits()
    {
        Console.Write("Enter a number to reverse and find the sum of its digits: ");
        if (int.TryParse(Console.ReadLine(), out int inputNumber))
        {
            int reversedNumber = ReverseNumber(inputNumber);
            int sumOfDigits = SumOfDigits(inputNumber);

            Console.WriteLine($"Reversed Number: {reversedNumber}");
            Console.WriteLine($"Sum of Digits: {sumOfDigits}");
        }
        else
        {
            Console.WriteLine("Invalid input. Please enter a valid number.");
        }
    }

    static bool IsPrime(int number)
    {
        if (number < 2)
            return false;

        for (int i = 2; i <= Math.Sqrt(number); i++)
        {
            if (number % i == 0)
                return false;
        }
        return true;
    }

    static bool HasVowels(string str)
    {
        foreach (char c in str)
        {
            if ("aeiouAEIOU".Contains(c))
            {
                return true;
            }
        }
        return false;
    }

    static int ReverseNumber(int number)
    {
        int reversedNumber = 0;
        while (number != 0)
        {
            int digit = number % 10;
            reversedNumber = reversedNumber * 10 + digit;
            number /= 10;
        }
        return reversedNumber;
    }

    static int SumOfDigits(int number)
    {
        int sum = 0;
        while (number != 0)
        {
            sum += number % 10;
            number /= 10;
        }
        return sum;
    }
}
```


2b. Create simple application to demonstrate use of following concepts
i. Function Overloading ii. Inheritance (all types)
iii. Constructor overloading iv. Interfaces
using System;
```
// Define an interface
public interface IDisplayable
{
    void Display();
}

// Base class with inheritance
public class Animal
{
    public string Name { get; set; }

    // Constructor overloading
    public Animal(string name)
    {
        Name = name;
    }

    // Function overloading
    public void MakeSound()
    {
        Console.WriteLine("Animal makes a generic sound");
    }
}

// Derived class inheriting from Animal and implementing IDisplayable interface
public class Dog : Animal, IDisplayable
{
    // Constructor overloading
    public Dog(string name) : base(name)
    {
    }

    // Function overloading
    public void MakeSound(string specificSound)
    {
        Console.WriteLine($"Dog {Name} makes a {specificSound} sound");
    }

    // Implementing interface method
    public void Display()
    {
        Console.WriteLine($"Dog {Name} is displayed");
    }
}

class Program
{
    static void Main()
    {
        // Function overloading
        Animal genericAnimal = new Animal("Generic Animal");
        genericAnimal.MakeSound();

        // Constructor overloading and inheritance
        Dog myDog = new Dog("Buddy");
        myDog.MakeSound();  // Calls the MakeSound method from the base class
        myDog.MakeSound("Woof");  // Calls the MakeSound method with parameter from the derived class

        // Interface implementation
        myDog.Display();

        Console.ReadLine();
    }
}
```
2c. Create simple application to demonstrate use of following concepts
i. Using Delegates and events ii. Exception handling

```
using System;

// Define a delegate
public delegate void EventHandler(string message);

// Define a class that uses the delegate and events
public class EventPublisher
{
    // Declare an event using the delegate
    public event EventHandler RaiseEvent;

    // Method to raise the event
    public void RaiseCustomEvent(string message)
    {
        // Check if there are subscribers to the event
        if (RaiseEvent != null)
        {
            // Raise the event
            RaiseEvent(message);
        }
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // Create an instance of EventPublisher
            EventPublisher publisher = new EventPublisher();

            // Subscribe to the event
            publisher.RaiseEvent += HandleEvent;

            // Trigger the event with a message
            publisher.RaiseCustomEvent("Event triggered!");

            // Simulate an exception
            throw new ApplicationException("Simulated exception.");

            // This line will not be executed if an exception occurs
            Console.WriteLine("After exception");
        }
        catch (ApplicationException ex)
        {
            // Handle the exception
            Console.WriteLine($"Exception caught: {ex.Message}");
        }
        finally
        {
            // This block is always executed, whether an exception occurred or not
            Console.WriteLine("Finally block executed.");
        }

        Console.ReadLine();
    }

    // Event handler method
    static void HandleEvent(string message)
    {
        Console.WriteLine($"Event handled: {message}");
    }
}
```

a. Create a Registration form to demonstrate use of various Validation controls
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm3.aspx.cs"
Inherits="WebApplication7.WebForm3" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="lblFirstName" runat="server" Text="First Name"></asp:Label>
<asp:TextBox ID="txtFirstName" runat="server"></asp:TextBox> &nbsp &nbsp
<asp:RequiredFieldValidator ID="rfvFirstName" runat="server"
ControlToValidate="txtFirstName" InitialValue="" ErrorMessage="First Name is required"
ForeColor="Red" Display="Dynamic"></asp:RequiredFieldValidator><br /> <br />
<asp:Label ID="lblLastName" runat="server" Text="Last Name"></asp:Label>
<asp:TextBox ID="txtLastName" runat="server"></asp:TextBox> &nbsp &nbsp
<asp:RequiredFieldValidator ID="rfvLastName" runat="server"
ControlToValidate="txtLastName" InitialValue="" ErrorMessage="Last Name is required"
ForeColor="Red" Display="Dynamic"></asp:RequiredFieldValidator> <br /> <br />
<asp:Label ID="lblEmail" runat="server" Text="Email"></asp:Label>
<asp:TextBox ID="txtEmail" runat="server"></asp:TextBox> &nbsp &nbsp
<asp:RequiredFieldValidator ID="rfvEmail" runat="server" ControlToValidate="txtEmail"
InitialValue="" ErrorMessage="Email is required" ForeColor="Red"
Display="Dynamic"></asp:RequiredFieldValidator>
<asp:RegularExpressionValidator ID="revEmail" runat="server"
ControlToValidate="txtEmail" ErrorMessage="Invalid Email Format"
ValidationExpression="\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*" ForeColor="Red"
Display="Dynamic"></asp:RegularExpressionValidator> <br /> <br />
<asp:Label ID="lblPassword" runat="server" Text="Password"></asp:Label>
<asp:TextBox ID="txtPassword" runat="server" TextMode="Password"></asp:TextBox>
&nbsp &nbsp
<asp:RequiredFieldValidator ID="rfvPassword" runat="server"
ControlToValidate="txtPassword" InitialValue="" ErrorMessage="Password is required"
ForeColor="Red" Display="Dynamic"></asp:RequiredFieldValidator> <br /> <br />
<asp:Label ID="lblConfirmPassword" runat="server" Text="Confirm
Password"></asp:Label>
<asp:TextBox ID="txtConfirmPassword" runat="server"
TextMode="Password"></asp:TextBox> &nbsp &nbsp
<asp:RequiredFieldValidator ID="rfvConfirmPassword" runat="server"
ControlToValidate="txtConfirmPassword" InitialValue="" ErrorMessage="Confirm Password is
required" ForeColor="Red" Display="Dynamic"></asp:RequiredFieldValidator>
<asp:CompareValidator ID="cvPasswordMatch" runat="server"
ControlToValidate="txtConfirmPassword" ControlToCompare="txtPassword"
ErrorMessage="Passwords do not match" ForeColor="Red"
Display="Dynamic"></asp:CompareValidator> <br /> <br />
<asp:Button ID="btnRegister" runat="server" Text="Register"
OnClick="btnRegister_Click" /> <br /> <br />
<asp:Label ID="message" runat="server" Text=""></asp:Label>
</form>
</body>
</html>
```
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace WebApplication7
{
public partial class WebForm3 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
}
protected void btnRegister_Click(object sender, EventArgs e)
{
if (Page.IsValid)
{
// Registration logic goes here
// You can save the user data to a database or perform other actions.
// The form data is valid.
}
string btnRegister = "Registration Successful";
message.Text = btnRegister;
}
}
}
```

b. Create Web Form to demonstrate use of Adrotator Control.
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm4.aspx.cs"
Inherits="WebApplication7.WebForm4" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:AdRotator ID="AdRotator1" runat="server" Height="250" Width="300"
Target="_blank" DataSourceID="XmlDataSource1"/>
<asp:XmlDataSource ID="XmlDataSource1" runat="server"
DataFile="~/XMLFile1.xml"></asp:XmlDataSource>
</div>
</form>
</body>
</html>
```
```
<?xml version="1.0" encoding="utf-8" ?>
<Advertisements>
<Ad>
<ImageUrl>image\image1.jpeg</ImageUrl>
<NavigateUrl>https://www.youtube.com/</NavigateUrl>
<AlternateText>YouTube</AlternateText>
<Impressions>50</Impressions>
<Keyboard>Free Streaming Videos</Keyboard>
</Ad>
</Advertisements>
```
c. Create Web Form to demonstrate use User Controls.
WebUserControl1.ascx
```
<%@ Control Language="C#" AutoEventWireup="true"
CodeBehind="WebUserControl1.ascx.cs" Inherits="Practical4c.WebUserControl1" %>
<asp:Label ID="Label1" runat="server" Text="User Name"></asp:Label>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox> <br />
<asp:Label ID="Label2" runat="server" Text="Password"></asp:Label>
<asp:TextBox ID="TextBox2" runat="server" TextMode="Password"></asp:TextBox><br />
<asp:Button ID="Button1" runat="server" Text="Signin" OnClick="Button1_Click"/>&nbsp
<asp:Label ID="Label3" runat="server" Text=""></asp:Label>
WebUserControl1.ascx.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical4c
{
public partial class WebUserControl1 : System.Web.UI.UserControl
{
protected void Page_Load(object sender, EventArgs e)
{
}
protected void Button1_Click(object sender, EventArgs e)
{
Label3.Text = "Valid Login";
}
}
}
```
WebForm1.aspx
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical4c.WebForm1" %>
<%@ Register Src="~/WebUserControl1.ascx" TagPrefix="uc1" TagName="WebUserControl1"
%>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<uc1:WebUserControl1 runat="server" id="WebUserControl1" />
</div>
</form>
</body>
</html>
```

a. Create Web Form to demonstrate use of Website Navigation controls and Site Map.
WebForm1.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical_5.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:SiteMapDataSource id="nav1" runat="server" />
<asp:Menu runat="server" DataSourceId="nav1" />
</div>
</form>
</body>
</html>
```
Web.sitemap:-
```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap>
<siteMapNode title="Home" url="/aspnet/w3home.aspx">
<siteMapNode title="Services" url="/aspnet/w3services.aspx">
<siteMapNode title="Training" url="/aspnet/w3training.aspx"/>
<siteMapNode title="Support" url="/aspnet/w3support.aspx"/>
</siteMapNode>
</siteMapNode>
</siteMap>
```
b. Create a web application to demonstrate use of Master Page with applying Styles and
Themes for page beautification.
Site.Master:-
```
<%@ Master Language="C#" AutoEventWireup="true" CodeBehind="Site.master.cs"
Inherits="WebApplication8.SiteMaster" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<link href="StyleSheet1.css" rel="stylesheet" />
<asp:ContentPlaceHolder ID="head" runat="server">
</asp:ContentPlaceHolder>
<title>my layout</title>
<link href="StyleSheet1.css" rel="stylesheet" />
</head>
<body>
<header id="header">
<h1>c# corner</h1>
</header>
<nav id="nav">
<ul>
<li><a href="home.aspx">Home</a></li>
<li><a href="#">About</a></li>
<li><a href="#">Article</a></li>
<li><a href="#">Contact</a></li>
</ul>
</nav>
<aside id="side">
<h1>news</h1>
<a href="#"><p>creating html website</p></a>
<a href="#"><p>learn css</p></a>
<a href="#">learn c#</a>
</aside>
<div id="con">
<asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
</asp:ContentPlaceHolder>
</div>
<footer id="footer">
copyright @c# corner
</footer>
</body>
</html>
```
StyleSheet1.css:-
```css
#header {
color: #247BA0;
text-align: center;
font-size: 20px;
}
#nav {
background-color: #FF1654;
padding: 5px;
}
ul {
list-style-type: none;
}
li a {
color: #F1FAEE;
font-size: 30px;
column-width: 5px;
}
li {
display: inline;
padding-left: 2px;
column-width: 20px;
}
a {
text-decoration: none;
margin-left: 20px
}
li a:hover {
background-color: #F3FFBD;
color: #FF1654;
padding: 1%;
}
#side {
text-align: center;
float: right;
width: 15%;
padding-bottom: 79%;
background-color: #F1FAEE;
}
#article {
background-color: #EEF5DB;
padding: 10px;
padding-bottom: 75%;
}
#footer {
background-color: #C7EFCF;
text-align: center;
padding-bottom: 5%;
font-size: 20px;
}
#con {
border: double;
border-color: burlywood;
}
```
WebForm2.aspx:-
```
<%@ Page Title="" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"
CodeBehind="WebForm2.aspx.cs" Inherits="WebApplication8.WebForm2" %>
<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1" runat="server">
</asp:Content>
c. Create a web application to demonstrate various states of ASP.NET Pages.
WebForm3.aspx:-
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm3.aspx.cs"
Inherits="WebApplication8.WebForm3" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="View State"
/><br />
<asp:Button ID="Button2" runat="server" OnClick="Button2_Click" Text="Hidden Field"
/><br />
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br />
<asp:Button ID="Button3" runat="server" OnClick="Button3_Click" Text="Cookies" />
<asp:HiddenField ID="HiddenField1" runat="server" Value="2" /><br />
<asp:Label ID="Label1" runat="server" Text=""></asp:Label> <br />
<asp:Label ID="Label2" runat="server" Text=""></asp:Label><br />
</div>
</form>
</body>
</html>
```

WebForm3.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace WebApplication8
{
public partial class WebForm3 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
if (IsPostBack)
{
if (ViewState["count"] != null)
{
int ViewstateVal = Convert.ToInt32(ViewState["count"]) + 1; Label2.Text = "View
State :" + ViewstateVal.ToString(); ViewState["count"] = ViewstateVal.ToString();
}
else
{
ViewState["count"] = "1";
}
}
}
protected void Button1_Click(object sender, EventArgs e)
{
Label1.Text = ViewState["count"].ToString();
}
protected void Button2_Click(object sender, EventArgs e)
{
if (HiddenField1.Value != null)
{
int val = Convert.ToInt32(HiddenField1.Value) + 1; HiddenField1.Value =
val.ToString();
}
}
protected void Button3_Click(object sender, EventArgs e)
{
HttpCookie h = new HttpCookie("name"); h.Value = TextBox1.Text;
Response.Cookies.Add(h); Response.Redirect("WebForm4.aspx");
}
}
}
```
WebForm4.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm4.aspx.cs"
Inherits="WebApplication8.WebForm4" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
</form>
</body>
</html>
```
WebForm4.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace WebApplication8
{
public partial class WebForm4 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
if (Request.Cookies["name"] != null)
Response.Write("Welcome: " + Request.Cookies["name"].Value);
}
}
}
```

a. Create a web application bind data in a multiline textbox by querying in another textbox.
WebForm1.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical_6.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:TextBox ID="queryTextBox" runat="server" Width="300"></asp:TextBox><br />
<asp:Button ID="queryButton" runat="server" Text="Query"
OnClick="queryButton_Click"/><br />
<asp:SqlDataSource ID="sds1" runat="server"></asp:SqlDataSource>
<asp:TextBox ID="resultTextBox" runat="server" TextMode="MultiLine" Rows="10"
Width="300"></asp:TextBox>
</div>
</form>
</body>
</html>
```

WebForm1.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Data.SqlClient;
using System.Web.UI.WebControls;
using System.Xml.Linq;
namespace Practical_6
{
public partial class WebForm1 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
{
resultTextBox.Text = "Enter a query and click the 'Query' button.";
}
}
protected void queryButton_Click(object sender, EventArgs e)
{
string connectionString = @"Data Source=DESKTOP-OKNH711\SQLEXPRESS; Initial
Catalog=TYIT; Integrated Security=True; Encrypt=False";
string query = queryTextBox.Text;
using (SqlConnection connection = new SqlConnection(connectionString))
{
connection.Open();
SqlCommand command = new SqlCommand(query, connection);
try
{
SqlDataReader reader = command.ExecuteReader();
resultTextBox.Text = "Query Results:\n";
while (reader.Read())
{
for (int i = 0; i < reader.FieldCount; i++)
{
resultTextBox.Text += reader[i] + "\t";
}
resultTextBox.Text += "\n";
}
reader.Close();
}
catch (Exception ex)
{
resultTextBox.Text = "Error: " + ex.Message;
}
}
}
}
}
```
b. Create a web application to display records by using database.
WebForm2.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm2.aspx.cs"
Inherits="Practical_6.WebForm2" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox> &nbsp &nbsp
<asp:Button ID="Button1" runat="server" Text="Button" OnClick="Button1_Click" />
&nbsp &nbsp <br />
<asp:Label ID="Label1" runat="server" Text=""></asp:Label><br />
<asp:SqlDataSource ID="SqlDataSource1" runat="server" SelectCommand="SELECT
[Id], [Name] FROM [Student]"></asp:SqlDataSource>
</div>
</form>
</body>
</html>
```
WebForm2.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_6
{
public partial class WebForm2 : System.Web.UI.Page
{
SqlConnection cn = new SqlConnection(@"Data
Source=DESKTOP-OKNH711\SQLEXPRESS; Initial Catalog=TYIT; Integrated Security=True;
Encrypt=False");
SqlCommand co = new SqlCommand(); SqlDataReader ds;
protected void Page_Load(object sender, EventArgs e)
{
cn.Open();
co.Connection = cn;
}
protected void Button1_Click(object sender, EventArgs e)
{
co.CommandText = "select Name from Student where Id ='" + TextBox1.Text + "';";
Label1.Text = co.ExecuteScalar().ToString();
}
}
}
```
c. Demonstrate the use of Datalist link control.
WebForm3.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm3.aspx.cs"
Inherits="Practical_6.WebForm3" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<p>The DataList shows data of DataTable</p>
</div>
<asp:DataList ID="DataList1" runat="server">
<ItemTemplate>
<table cellpadding="2" cellspacing="0" border="1" style="width: 300px; height: 100px;
border: dashed 2px #04AFEF; background-color: #FFFFFF">
<tr>
<td>
<b>ID: </b><span class="city"><%# Eval("ID") %></span><br />
<b>Name: </b><span class="postal"><%# Eval("Name") %></span><br />
<b>Email: </b><span class="country"><%# Eval("Address")%></span><br />
</td>
</tr>
</table>
</ItemTemplate>
</asp:DataList>
</form>
</body>
</html>
```
WebForm3.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_6
{
public partial class WebForm3 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
DataTable table = new DataTable();
table.Columns.Add("ID");
table.Columns.Add("Name");
table.Columns.Add("Address");
table.Rows.Add("101", "Vivek Vishwakarma", "Santacruz");
table.Rows.Add("102", "Omkar Kamat", "Vile Parle");
table.Rows.Add("103", "Jatin Verma", "Malad");
DataList1.DataSource = table;
DataList1.DataBind();
}
}
}
```
a. Create a web application to display Databinding using dropdownlist control.
WebForm1.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical_7.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Button" /><br
/>
<asp:Label ID="Label1" runat="server" Text=""></asp:Label>
<asp:DropDownList ID="DropDownList1" runat="server"
OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged"></asp:DropDownList><br
/>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" SelectCommand="SELECT *
FROM [Student]"></asp:SqlDataSource>
</div>
</form>
</body>
</html>
```
WebForm1.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_7
{
public partial class WebForm1 : System.Web.UI.Page
{
SqlConnection cn = new SqlConnection(@"Data
Source=DESKTOP-OKNH711\SQLEXPRESS;Initial Catalog=TYIT;Integrated Security=True");
SqlCommand co = new SqlCommand(); SqlDataReader ds;
protected void Page_Load(object sender, EventArgs e)
{
cn.Open(); co.Connection = cn;
}
protected void Button1_Click(object sender, EventArgs e)
{
co.CommandText = "select * from Student;";
ds = co.ExecuteReader();
DropDownList1.DataSource = ds;
DropDownList1.DataTextField = "Name";
DropDownList1.DataBind();
}
protected void DropDownList1_SelectedIndexChanged(object sender, EventArgs e)
{
TextBox1.Text = DropDownList1.Text;
}
}
}
```
b. Create a web application for to display the phone no of an author using database.
WebForm2.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm2.aspx.cs"
Inherits="Practical_7.WebForm2" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox> &nbsp &nbsp
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Button" />
&nbsp &nbsp <br />
<asp:Label ID="Label1" runat="server" Text=""></asp:Label>
</div>
</form>
</body>
</html>
```
WebForm2.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_7
{
public partial class WebForm2 : System.Web.UI.Page
{
SqlConnection cn = new SqlConnection(@"Data
Source=DESKTOP-OKNH711\SQLEXPRESS;Initial Catalog=TYIT;Integrated Security=True");
SqlCommand co = new SqlCommand(); SqlDataReader ds;
protected void Page_Load(object sender, EventArgs e)
{
cn.Open(); co.Connection = cn;
}
protected void Button1_Click(object sender, EventArgs e)
{
co.CommandText = "select Contacts from Student where Name='" + TextBox1.Text + "';";
Label1.Text = co.ExecuteScalar().ToString();
}
}
}
```
c. Create a web application for inserting and deleting record from a database. (Using
Execute-Non Query).
WebForm3.aspx:-
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="WebApplication14.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="Id"></asp:Label>&nbsp &nbsp
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br />
<asp:Label ID="Label2" runat="server" Text="Name"></asp:Label>&nbsp &nbsp
<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox><br />
<asp:Label ID="Label3" runat="server" Text="Subject"></asp:Label>&nbsp
&nbsp
<asp:TextBox ID="TextBox3" runat="server"></asp:TextBox><br />
<asp:Label ID="Label4" runat="server" Text="Contacts"></asp:Label>&nbsp
&nbsp
<asp:TextBox ID="TextBox4" runat="server"></asp:TextBox><br />
<asp:Button ID="InsertButton" runat="server" Text="Insert"
OnClick="InsertButton_Click" /> &nbsp &nbsp &nbsp &nbsp
<asp:Button ID="Button1" runat="server" Text="Delete"
OnClick="DeleteButton_Click"/>
</div>
</form>
</body>
</html>
```
WebForm3.aspx.cs:-
```
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace WebApplication14
{
public partial class WebForm1 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
}
protected void InsertButton_Click(object sender, EventArgs e)
{
string connectionString =
ConfigurationManager.ConnectionStrings["TYIT"].ConnectionString;
using (SqlConnection connection = new SqlConnection(connectionString))
{
connection.Open();
string insertQuery = "INSERT INTO Student (Id, Name,Subject, Contacts)
VALUES (@Value1, @Value2,@Value3, @Value4)";
using (SqlCommand cmd = new SqlCommand(insertQuery, connection))
{
cmd.Parameters.AddWithValue("@Value1", TextBox1.Text);
cmd.Parameters.AddWithValue("@Value2", TextBox2.Text);
cmd.Parameters.AddWithValue("@Value3", TextBox3.Text);
cmd.Parameters.AddWithValue("@Value4", TextBox4.Text);
cmd.ExecuteNonQuery();
}
}
}
protected void DeleteButton_Click(object sender, EventArgs e)
{
string connectionString =
ConfigurationManager.ConnectionStrings["TYIT"].ConnectionString;
using (SqlConnection connection = new SqlConnection(connectionString))
{
connection.Open();
string deleteQuery = "DELETE FROM Student WHERE ID = @Value1";
using (SqlCommand cmd = new SqlCommand(deleteQuery, connection))
{
cmd.Parameters.AddWithValue("@Value1", TextBox1.Text);
cmd.Parameters.AddWithValue("@Value2", TextBox2.Text);
cmd.Parameters.AddWithValue("@Value3", TextBox3.Text);
cmd.Parameters.AddWithValue("@Value4", TextBox4.Text);
cmd.ExecuteNonQuery();
}
}
}
}
}
```
8A. Create a web application to demonstrate various uses and properties of
SqlDataSource.
WebForm1.aspx:
```
<div>
<asp:Label ID="Label1" runat="server" Text="ID"></asp:Label>&nbsp
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br /><br />
<asp:Label ID="Label2" runat="server" Text="Name"></asp:Label>
<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox><br /><br />
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Insert" /><br />
<asp:Label ID="Label3" runat="server"></asp:Label><br />
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
ConflictDetection="CompareAllValues" ConnectionString="<%$ConnectionStrings:TYIT %>"
DeleteCommand="DELETE FROM [Student2] WHERE [Id] = @Id AND (([Name] = @Name)
OR ([Name] IS NULL AND @Name IS NULL)) AND (([Subject] = @Subject) OR ([Subject]
IS NULL AND @Subject IS NULL))" InsertCommand="INSERT INTO [Student2] ([Id],
[Name], [Subject]) VALUES (@Id, @Name, @Subject)"
OldValuesParameterFormatString="{0}" SelectCommand="SELECT * FROM [Student2]"
UpdateCommand="UPDATE [Student2] SET [Name] = @Name, [Subject] = @Subject WHERE
[Id] = @Id AND (([Name] = @Name) OR ([Name] IS NULL AND @Name IS NULL)) AND
(([Subject] = @Subject) OR ([Subject] IS NULL AND @Subject IS NULL))">
<DeleteParameters>
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</DeleteParameters>
<InsertParameters>
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</InsertParameters>
<UpdateParameters>
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</UpdateParameters>
</asp:SqlDataSource>
</div>
```
WebForm1.aspx.cs:
```
protected void Button1_Click(object sender, EventArgs e)
{
SqlDataSource1.InsertParameters["id"].DefaultValue = TextBox1.Text;
SqlDataSource1.InsertParameters["name"].DefaultValue = TextBox2.Text;
SqlDataSource1.InsertParameters["subject"].DefaultValue = "";
SqlDataSource1.Insert();
Label3.Text = "DONE";
TextBox1.Text = "";
TextBox2.Text = "";
}
```
Web.config:
```
<connectionStrings>
<add name="TYIT" connectionString="Data
Source=DESKTOP-OKNH711\SQLEXPRESS;Initial Catalog=TYIT;Integrated
Security=True"></add>
</connectionStrings>
8B. Create a web application to demonstrate data binding using DetailsView
and FormView Control.
```
WebForm2.aspx:
```
<div>
<asp:FormView ID="FormView1" runat="server" AllowPaging="True"
DataKeyNames="Id" DataSourceID="SqlDataSource1" Height="208px" Width="305px">
<EditItemTemplate>
Id:
<asp:Label ID="IdLabel1" runat="server" Text='<%# Eval("Id") %>' /><br />
Name:
<asp:TextBox ID="NameTextBox" runat="server" Text='<%# Bind("Name")%>' /><br />
Subject:
<asp:TextBox ID="SubjectTextBox" runat="server" Text='<%#Bind("Subject") %>' /><br />
<asp:LinkButton ID="UpdateButton" runat="server" CausesValidation="True"
CommandName="Update" Text="Update" />&nbsp
<asp:LinkButton ID="UpdateCancelButton" runat="server" CausesValidation="False"
CommandName="Cancel" Text="Cancel" />
</EditItemTemplate>
<InsertItemTemplate>
Id:
<asp:TextBox ID="IdTextBox" runat="server" Text='<%# Bind("Id") %>' /><br />
Name:
<asp:TextBox ID="NameTextBox" runat="server" Text='<%# Bind("Name")%>' /><br />
Subject:
<asp:TextBox ID="SubjectTextBox" runat="server" Text='<%#Bind("Subject") %>' /><br />
<asp:LinkButton ID="InsertButton" runat="server" CausesValidation="True"
CommandName="Insert" Text="Insert" />&nbsp
<asp:LinkButton ID="InsertCancelButton" runat="server" CausesValidation="False"
CommandName="Cancel" Text="Cancel" />
</InsertItemTemplate>
<ItemTemplate>
Id:
<asp:Label ID="IdLabel" runat="server" Text='<%# Eval("Id") %>' /><br />
Name:
<asp:Label ID="NameLabel" runat="server" Text='<%# Bind("Name") %>'/><br />
Subject:
<asp:Label ID="SubjectLabel" runat="server" Text='<%# Bind("Subject")%>' /><br />
<asp:LinkButton ID="EditButton" runat="server" CausesValidation="False"
CommandName="Edit" Text="Edit" />&nbsp
<asp:LinkButton ID="DeleteButton" runat="server" CausesValidation="False"
CommandName="Delete" Text="Delete" />&nbsp
<asp:LinkButton ID="NewButton" runat="server" CausesValidation="False"
CommandName="New" Text="New" />
</ItemTemplate>
</asp:FormView>
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
ConflictDetection="CompareAllValues" ConnectionString="<%$ConnectionStrings:TYIT%>"
ProviderName="<%$ ConnectionStrings:TYIT.ProviderName %>" DeleteCommand="DELETE
FROM [Student2] WHERE [Id] = @Id AND (([Name] = @Name) OR ([Name] IS NULL AND
@Name IS NULL)) AND (([Subject] = @Subject) OR ([Subject] IS NULL AND @Subject IS
NULL))" InsertCommand="INSERT INTO [Student2] ([Id], [Name], [Subject]) VALUES (@Id,
@Name, @Subject)" OldValuesParameterFormatString="{0}" SelectCommand="SELECT *
FROM [Student2]" UpdateCommand="UPDATE [Student2] SET [Name] = @Name, [Subject] =
@Subject WHERE [Id] = @Id AND (([Name] = @Name) OR ([Name] IS NULL AND @Name
IS NULL)) AND (([Subject] = @Subject) OR ([Subject] IS NULL AND @Subject IS
NULL))">
<DeleteParameters>
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</DeleteParameters>
<InsertParameters>
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</InsertParameters>
<UpdateParameters>
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
<asp:Parameter Name="Id" Type="Int32" />
<asp:Parameter Name="Name" Type="String" />
<asp:Parameter Name="Subject" Type="String" />
</UpdateParameters>
</asp:SqlDataSource>
</div>
```
8C. Create a web application to display Using Disconnected Data Access and
Databinding using GridView.
WebForm3.aspx:
```
div>
Subject
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click"
Text="Button"/><br />
<asp:GridView ID="GridView1" runat="server">
</asp:GridView>
</div>
WeForm3.aspx.cs:
protected void Button1_Click(object sender, EventArgs e)
{
string constr = WebConfigurationManager.ConnectionStrings["TYIT"].ConnectionString;
using (SqlConnection con = new SqlConnection(constr))
{
con.Open();
string sql = "SELECT * FROM Student WHERE Subject = @Subject";
using (SqlDataAdapter d = new SqlDataAdapter(sql, con))
{
d.SelectCommand.Parameters.AddWithValue("@Subject", TextBox1.Text);
DataSet ds = new DataSet();
d.Fill(ds);
GridView1.DataSource = ds.Tables[0];
GridView1.DataBind();
}
}
}
```
Web.config:
```
<connectionStrings>
<add name="TYIT" connectionString="Data
Source=DESKTOP-OKNH711\SQLEXPRESS;Initial Catalog=TYIT;Integrated
Security=True"></add>
</connectionStrings>

```
A. Create a web application to demonstrate use of GridView control
template and GridView hyperlink.
WebForm3.aspx:
```
<div>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False"
OnRowDataBound="GridView1_RowDataBound">
<Columns>
<asp:BoundField DataField="ID" HeaderText="ID" SortExpression="ID" />
<asp:BoundField DataField="Name" HeaderText="Name"
SortExpression="Name" />
<asp:TemplateField HeaderText="Details">
<ItemTemplate>
<asp:HyperLink ID="HyperLink1" runat="server" NavigateUrl='<%#
Eval("ID", "Details.aspx?id={0}") %>' Text="View Details"></asp:HyperLink>
</ItemTemplate>
</asp:TemplateField>
</Columns>
</asp:GridView>
</div>
```
WebForm3.aspx.cs:
```
public partial class WebForm2 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
{
BindGridView();
}
}
private void BindGridView()
{
// Replace this with your actual data source
DataTable dt = GetDataSource();
GridView1.DataSource = dt;
GridView1.DataBind();
}
private DataTable GetDataSource()
{
// Replace this with your actual data retrieval logic
DataTable dt = new DataTable();
dt.Columns.Add("ID", typeof(int));
dt.Columns.Add("Name", typeof(string));
// Sample data
dt.Rows.Add(1, "Vivek");
dt.Rows.Add(2, "Omkar");
return dt;
}
protected void GridView1_RowDataBound(object sender, GridViewRowEventArgs e)
{
// Add any additional row-bound logic here
}
}
Details.aspx.cs:
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
{
if (Request.QueryString["id"] != null)
{
// Retrieve the ID from the query string
string id = Request.QueryString["id"];
// Check the value of the ID and display the corresponding message
if (id == "1")
{
Response.Write("Vivek");
}
else if (id == "2")
{
Response.Write("Omkar");
}
else
{
// Handle the case where the ID is not 1 or 2
Response.Write("Unknown ID");
}
}
else
{
// Handle the case where the ID is not provided in the query string
Response.Write("ID not specified");
}
}
}
```
B. Create a web application to demonstrate use of GridView button column
and GridView events.
WebForm1.aspx:
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical_9.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="false"
OnRowCommand="GridView1_RowCommand" DataKeyNames="ID">
<Columns>
<asp:BoundField DataField="ID" HeaderText="ID" SortExpression="ID" />
<asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name"
/>
<asp:ButtonField ButtonType="Button" Text="Click Me"
CommandName="ButtonClick" />
</Columns>
</asp:GridView>
</div>
</form>
</body>
</html>
```
WebForm1.aspx.cs:
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_9
{
public partial class WebForm1 : System.Web.UI.Page
{
public class Item
{
public int ID { get; set; }
public string Name { get; set; }
}
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
{
// Dummy data for demonstration purposes
List<Item> items = new List<Item>
{
new Item { ID = 1, Name = "Vivek" },
new Item { ID = 2, Name = "Omkar" },
new Item { ID = 3, Name = "Jatin" }
};
GridView1.DataSource = items;
GridView1.DataBind();
}
}
protected void GridView1_RowCommand(object sender, GridViewCommandEventArgs e)
{
if (e.CommandName == "ButtonClick")
{
// Get the index of the row where the button was clicked
int rowIndex = Convert.ToInt32(e.CommandArgument);
// Access data from the clicked row
int id = Convert.ToInt32(GridView1.DataKeys[rowIndex].Value);
string name = GridView1.Rows[rowIndex].Cells[1].Text; // Assuming Name is in the
second cell
// Perform any action based on the button click
// For example, display a message
Response.Write($"Button clicked for Item ID: {id}, Name: {name}");
}
}
}
}
```
C. Create a web application to demonstrate GridView paging and Creating
own table format using GridView.
```
WebForm2.aspx:
<div>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False"
AllowPaging="True"
PageSize="5" OnPageIndexChanging="GridView1_PageIndexChanging">
<Columns>
<asp:BoundField DataField="ProductId" HeaderText="Product ID"
SortExpression="ProductId" />
<asp:BoundField DataField="ProductName" HeaderText="Product Name"
SortExpression="ProductName" />
<asp:BoundField DataField="Category" HeaderText="Category"
SortExpression="Category" />
</Columns>
</asp:GridView>
</div>
```
WebForm2.aspx.cs:
```
public partial class WebForm2 : System.Web.UI.Page
{
public class Product
{
public int ProductId { get; set; }
public string ProductName { get; set; }
public string Category { get; set; }
}
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack)
{
BindGridView();
}
}
private void BindGridView()
{
List<Product> products = new List<Product>
{
new Product { ProductId = 1, ProductName = "Laptop", Category = "Electronics" },
new Product { ProductId = 2, ProductName = "Smartphone", Category = "Electronics" },
new Product { ProductId = 3, ProductName = "Tablet", Category = "Electronics" },
new Product { ProductId = 4, ProductName = "Coffee Maker", Category = "Appliances"
},
new Product { ProductId = 5, ProductName = "Toaster", Category = "Appliances" },
new Product { ProductId = 6, ProductName = "Blender", Category = "Appliances" },
new Product { ProductId = 7, ProductName = "Bookshelf", Category = "Furniture" },
new Product { ProductId = 8, ProductName = "Sofa", Category = "Furniture" },
new Product { ProductId = 9, ProductName = "Dining Table", Category = "Furniture" },
new Product { ProductId = 10, ProductName = "Running Shoes", Category = "Clothing"
}
};
GridView1.DataSource = products;
GridView1.DataBind();
}
protected void GridView1_PageIndexChanging(object sender,
System.Web.UI.WebControls.GridViewPageEventArgs e)
{
GridView1.PageIndex = e.NewPageIndex;
BindGridView();
}
}
```


a. Create a web application to demonstrate reading and writing operation
with XML.
WebForm1.aspx:
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs"
Inherits="Practical_10.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:TextBox ID="xmlInput" runat="server" TextMode="MultiLine" Rows="5"
Columns="10"></asp:TextBox><br />
<asp:Button ID="btnWriteXml" runat="server" Text="Write XML"
OnClick="btnWriteXml_Click" />
<asp:Button ID="btnReadXml" runat="server" Text="Read XML"
OnClick="btnReadXml_Click" /><br />
<asp:Label ID="lblResult" runat="server" Text=""></asp:Label>
</div>
</form>
</body>
</html>
```
WebForm1.aspx.cs:
```
using System;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Xml;
namespace Practical_10
{
public partial class WebForm1 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
}
protected void btnWriteXml_Click(object sender, EventArgs e)
{
try
{
string xmlContent = xmlInput.Text;
// Specify the path where you want to save the XML file
string filePath = Server.MapPath("~/App_Data/XMLFile1.xml");
// Write XML to the file
File.WriteAllText(filePath, xmlContent);
lblResult.Text = "XML written successfully.";
}
catch (Exception ex)
{
lblResult.Text = $"Error writing XML: {ex.Message}";
}
}
protected void btnReadXml_Click(object sender, EventArgs e)
{
try
{
// Specify the path of the XML file to read
string filePath = Server.MapPath("~/App_Data/XMLFile1.xml");
// Read XML from the file
string xmlContent = File.ReadAllText(filePath);
lblResult.Text = $"Read XML:\n{xmlContent}";
}
catch (Exception ex)
{
lblResult.Text = $"Error reading XML: {ex.Message}";
}
}
}
}
```
Write XML
Read XML
b. Create a web application to demonstrate form security and windows
security with proper authentication and authorization properties.
Login_form.aspx:
```
<div>
<asp:Panel ID="p1" runat="server" GroupingText="Login Form " BackColor="Pink">
<asp:Label ID="lb1" runat="server" Text="Username:" />&nbsp
<asp:TextBox ID="txt1" runat="server" /><br /><br />
<asp:Label ID="lb2" runat="server" Text="Password:" />&nbsp
<asp:TextBox ID="txt2" runat="server" TextMode="Password" /><br /><br />
<asp:Button ID="btn1" runat="server" Font-Bold="true" Font-Size="Large"
ForeColor="DarkSlateBlue" OnClick="btn1_Click" Text="Login" />&nbsp &nbsp
<asp:Button ID="btn2" runat="server" Font-Bold="true" Font-Size="Large"
ForeColor="DarkSlateBlue" OnClick="btn2_Click" Text="Cancel" />
</asp:Panel>
</div>
Login_form.aspx.cs:
public partial class Login_form : System.Web.UI.Page
{
SqlConnection cn;
SqlCommand cmd;
protected void Page_Load(object sender, EventArgs e)
{
/*if (User.Identity.IsAuthenticated)
{
// If authenticated, redirect to WebForm1.aspx
Response.Redirect("~/WebForm1.aspx");
}*/
}
public bool checkuser()
{
string s1 = WebConfigurationManager.ConnectionStrings["db1"].ConnectionString;
cn = new SqlConnection(s1);
cn.Open();
cmd = new SqlCommand("select * from ulogin where uname=@uname and
upass=@upass", cn);
cmd.Parameters.AddWithValue("@uname", txt1.Text);
cmd.Parameters.AddWithValue("@upass", txt2.Text);
object obj = cmd.ExecuteScalar();
if (obj != null)
return true;
else
return false;
}
protected void btn1_Click(object sender, EventArgs e)
{
if (checkuser())
{
FormsAuthentication.RedirectFromLoginPage(txt1.Text, false);
Response.Redirect("~/WebForm1.aspx");
}
else
Response.Write("Login is Fail");
}
protected void btn2_Click(object sender, EventArgs e)
{
txt1.Text = "";
txt2.Text = "";
}
}
```
WebForm1.aspx:
```
<div>
<asp:Label ID="Label1" runat="server" Text="Roll Number"></asp:Label>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br /><br />
<asp:Label ID="Label2" runat="server" Text="Name"></asp:Label>
<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox><br /><br />
<asp:Label ID="Label3" runat="server" Text="Class: "></asp:Label>
<asp:RadioButton ID="RadioButton1" runat="server" GroupName="class" Text="FY" />
<asp:RadioButton ID="RadioButton2" runat="server" GroupName="class" Text="SY" />
<asp:RadioButton ID="RadioButton3" runat="server" GroupName="class" Text="TY" /><br
/><br />
<asp:Label ID="Label4" runat="server" Text="Course"></asp:Label>
<asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="True"
OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged1" style="height: 25px">
<asp:ListItem>BSC(IT)</asp:ListItem>
<asp:ListItem>BSC(CS)</asp:ListItem>
</asp:DropDownList><br /><br />
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Submit" /><br
/><br />
<asp:Label ID="Label5" runat="server" Text=""></asp:Label>
</div>
```
WebForm1.aspx.cs:
```
protected void Button1_Click(object sender, EventArgs e)
{
string s;
if (RadioButton1.Checked == true)
{
s = RadioButton1.Text;
}
if (RadioButton2.Checked == true)
{
s = RadioButton2.Text;
}
else
{
s = RadioButton3.Text;
}
Label5.Text += "You have enrolled in " + s;
}
protected void DropDownList1_SelectedIndexChanged1(object sender, EventArgs e)
{
Label5.Text = "You have been enrolled in " + DropDownList1.SelectedItem;
}
```
Web.config:
```
<connectionStrings>
<add name="db1" connectionString="Data
Source=DESKTOP-OKNH711\SQLEXPRESS;Initial Catalog=db1;Integrated Security=True"/>
</connectionStrings>
<authentication mode="Forms">
<forms loginUrl="Login_form.aspx" name="login" timeout="60"/>
</authentication>
<authorization>
<allow users="*" />
</authorization>
```
After Login

----------
C. Create a web application to demonstrate use of various Ajax controls.
WebForm3.aspx:
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm2.aspx.cs"
Inherits="Practical_10.WebForm2" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager runat="server"></asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<asp:Button ID="Button1" runat="server" Text="Click Me"
OnClick="Button1_Click" />
</ContentTemplate>
</asp:UpdatePanel>
<ajaxToolkit:CalendarExtender ID="CalendarExtender1" runat="server"
TargetControlID="txtDate" Format="dd/MM/yyyy">
</ajaxToolkit:CalendarExtender>
<asp:TextBox ID="txtDate" runat="server"></asp:TextBox>
<asp:Button ID="btnSubmit" runat="server" Text="Submit"
OnClick="btnSubmit_Click" />
<asp:Label ID="lblMessage" runat="server" Text=""></asp:Label>
</div>
</form>
</body>
</html>
```
WebForm3.aspx.cs:
```
using AjaxControlToolkit;
using System;
using System.Collections.Generic;
using System.Globalization;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
namespace Practical_10
{
public partial class WebForm2 : System.Web.UI.Page
{
protected void Page_Load(object sender, EventArgs e)
{
}
protected void Button1_Click(object sender, EventArgs e)
{
TextBox1.Text = "Button Clicked at " + DateTime.Now.ToString("hh:mm:ss");
}
protected void btnSubmit_Click(object sender, EventArgs e)
{
// Handle the button click event
DateTime selectedDate;
if (DateTime.TryParseExact(txtDate.Text, "dd/MM/yyyy", CultureInfo.InvariantCulture,
DateTimeStyles.None, out selectedDate))
{
// Display a message based on the selected date
if (selectedDate.DayOfWeek == DayOfWeek.Saturday || selectedDate.DayOfWeek ==
DayOfWeek.Sunday)
{
lblMessage.Text = "It's a weekend!";
}
else
{
lblMessage.Text = "It's a weekday!";
}
}
else
{
lblMessage.Text = "Invalid date!";
}
}
}
}
```


Class1.cs:
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
namespace WebApplication12
{
public class Class1
{
public int add(int a, int b)
{
int c = a + b;
return c;
}
}
}
ConsoleApp7(Program.cs):
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace ConsoleApp7
{
internal class Program
{
static void Main(string[] args)
{
WebApplication12.Class1 c = new WebApplication12.Class1();
int t = c.add(19, 2);
Console.WriteLine("addition={0}", t);
Console.ReadKey();
}
}
}
```
