First Download run "Postgres" image for docker
Then create a container by executing the below command with a PORT number:
```bash
docker run --name postgres-db -e POSTGRES_PASSWORD=anurag -p 5432:5432 -d postgres
```

To execute/run the Postgres CLI, use this command:
```bash
docker exec -it postgres-db psql -U postgres
```

But if you want to use 'PGadmin'. We can use it through the docker extension. Go to extension tab and download the extension 
![[Pasted image 20250807101312.png]]

or, you can download PGadmin on your machine and use it locally instead of the extension. Both will work fine with the forward configuration.

After that open the extension and use the password you provided when you created the container through the postgres image.

Now refer the image provided below and in the Host name/address use **host.docker.internal**
![[Pasted image 20250807101540.png]]

