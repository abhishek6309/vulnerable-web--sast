# Vulnerable-web-app---SAST

# 2) Performing Static Application Security Testing Using SonarQube on Vulnerable web application:

1 Download  source code from https://github.com/OWASP/Vulnerable-Web-Application.git

2 Open SonarQube Click on create project and add an project name like " Vulnerable web application Source code review "

3 Go to With the configuration best suited for you in this we will go manually with GitHub Actions

4 we have to Create GitHub Secrets in our repository containing Vulnerable web application source code

5 Create a " sonar-project.properties " file in your repository and paste the content mentioned in below :
sonar.projectKey=Vulnerable-web-application-Source-code-review

6 Create or update your .github/workflows/build.ymland paste the content :

" name: Build on:
 push:
   branches:
     - master # or the name of your main branch
jobs
 build:
   name: Build
   runs-on: ubuntu-latest
   steps:
     - uses: actions/checkout@v2
       with:
         fetch-depth: 0
     - uses: sonarsource/sonarqube-scan-action@master
       env:
         SONAR_TOKEN: $Template:Secrets.SONAR TOKEN
         SONAR_HOST_URL: $Template:Secrets.SONAR HOST URL
     # If you wish to fail your job when the Quality Gate is red, uncomment the
     # following lines. This would typically be used to fail a deployment.
     # - uses: sonarsource/sonarqube-quality-gate-action@master
     #   timeout-minutes: 5
     #   env:
     #     SONAR_TOKEN: $Template:Secrets.SONAR TOKEN

7 Commit and push your code to start the analysis. Each new push you make on your main branch will trigger a new analysis in SonarQube

# Observations:

SonarQube will give you detailed analysis report within 5 minutes which will help you to improve your code quality

The results of analysis will be as following:

-78 Bugs
-5 Vulnerabilities
-108 Code Smells
-7.5% Duplications

You can then see the details of bugs , vulnerabilities, code smells , etc. found by clicking on then

it will also shows suggestion about how you can improve your code and mitigate the bugs

ex:

$username = "root";
25

	$password = "";
26

	$db = "1ccb8097d0e9ce9f154608be60224c7c";
27

28

	// Create connection
29

	$conn = new mysqli($servername, $username, $password,$db);
Add password protection to this database.

	// Check connection
32

	if ($conn->connect_error) {
33

	    die("Connection failed: " . $conn->connect_error);
34

	} 
35

	//echo "Connected successfully";
36

	if(isset($_POST["submit"])){
37

		$number = $_POST['number'];
38

		$query = "SELECT bookname,authorname FROM books WHERE number = $number"; //Int
