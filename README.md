# ASP.NET Framework Application with SQL Server backend

## Run the application on local machine

1. Create new database with name "MoviesDB" on local machine
2. Update the database connection string in web.config file
3. Run the database migration using "update-database" command
4. Run the application on local machine

## Run the application on Azure using App Services and Azure SQL database

1. Setup an Azure SQL Database with name "MoviesDB"
2. Update the database connection string in the web.config file
3. Run the database migration using "update-database" command
4. Setup an Azure App Service with the name "movies-app-101"
5. Setup an Application Insights (optional)
6. Deploy the applcation to Azure

## Run the app in Docker container

1.  Examine the Dockerfile

        - Highlights
                - Windows Server Core images
                - Multi-stage build process

2.  Switcht to Windows Containers - Run following command in PowerShell

        & $Env:ProgramFiles\Docker\Docker\DockerCli.exe -SwitchDaemon .

3.  Build the app using following docker command:

        docker build -t movie-rentals-app:v1 .

4.  Run the app using following docker command:

        # Interactive mode
        docker run -it --rm -p 8080:80 --env MovieDBContext="[Database Connection String]" movie-rentals-app:v1

        # Detached mode
        docker run -d -p 8080:80 --env MovieDBContext="[Database Connection String]" movie-rentals-app:v1

## Run the application on AKS

1.  Tag the docker image and push to ACR

        docker tag movie-rentals-app:v1 [ACR URL]/movie-rentals-app:v1
        az acr login --name [ACR Name]
        docker push [ACR URL]/movie-rentals-app:v1

2.  Deploy to AKS

        kubectl apply -f movie-rentals-app-dep.yaml

        kubectl apply -f movie-rentals-app-service.yaml
