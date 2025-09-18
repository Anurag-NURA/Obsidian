	"Explicitly declare and isolate dependencies"

 Lets say we want to use [[React.js]] library for creating our frontend application 
![[Pasted image 20240915092114.png]]

and for React and react-hooks to work we need to first install the React library
![[Pasted image 20240915092225.png]]

 ==☝ A twelve factor app never relies on implicit existence of system-wide packages.== It means that we cannot assume the React.js library will already be installed when someone wants to run our application.

Here comes [[Docker]] 🐳,
Docker containers allows us to run applications on self-contained environment that is isolated from the host system. It is a more efficient and reliable way to manage dependencies. 

Here have all the dependencies required to install before the application is started. 
![[Pasted image 20240915100226.png]]

we have to make sure that in the Docker file we mention the install command is executed inside the docker image and then define the command to execute the application. This all makes sure that other developer doesn't have to go through the hassle of "But it works on my PC 😑" 