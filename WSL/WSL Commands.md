//Mongodb command for WSL ---->

sudo systemctl status <name of the service>
In our case it is mongodb server
So, "sudo systemctl status mongod"
If it shows, "Active: inactive(dead)" that means mongodb is not running


To start the service 
"sudo systemctl start mongod"

Than again run the command "sudo systemctl status mongod" to check the current status
after starting the mongod service.

Than to see the database on the CLI use "mongosh" command.
It will automatically connect to the hosted service on local machine and display the data.




//If symlink for multishells error occurs
just a work around ---> sudo systemctl restart user@1000


//for check running processes (including background processes) ----> bashtop (try "sudo" to run as admin)


//for running a html server in neovim ----> http://localhost:8000/


//Redis -----> docker ps (take id of runing redis-stack image)
	       docker exec -it 'redis-id' bash


//For killing processes(fzf installed required with autocompletion) ------> kill -9 ** (then press tab)