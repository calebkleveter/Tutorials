# Diving into Vapor, Part 2: Persisting Data in Vapor 3

In the [previous tutorial](https://theswiftwebdeveloper.com/diving-into-vapor-part-1-up-and-running-with-vapor-3-edab3c79aab9), we looked at how to setup a Vapor project. It's a good place to start, but not very fun. Let's get out application off the ground by adding data persistence!

In this tutorial, we will be covering how to connect to a relational database (both PostgreSQL and MySQL) and then storing data in it.

The first part will cover connecting to a MySQL database, the second covers connecting to a PostgreSQL database, and the third covers how to create and store models (you do the, almost, same thing for each DB).

# [MySQL](https://docs.vapor.codes/3.0/mysql/getting-started/)
---

Open your terminal and run `brew install mysql && brew services start mysql`. This will install MySQL and boot it up. MySQL will subsequently boot whenever you login, so you won't have to do that again. 

We also need to create that database for our app to connect to. Run `mysql -u root -p` and press enter twice (you shouldn't need to enter a password). Run this command in the MySQL prompt:

https://gist.github.com/calebkleveter/c510f93c3f78213d1a6bb85dced707a9

You can change the name of the database if you want, but make sure you do that in the reset of this tutorial also. I prefer to just use the name of my application for the database name. 

You can exit the MySQL prompt by running `QUIT`

We need to install the package for MySQL in our application, so replace the reference to `FluentSQLite` with this package instance in your manifest's `dependencies` array:

https://gist.github.com/calebkleveter/0adec972862d9bb1404d57d265392b5c

Make sure you replace `FluentSQLite` with `FluentMySQL` in the `dependencies` array of you `App` target. Then run `vapor update -y` or `swift package update`.

Now we need to add Fluent and the MySQL database to our app's configuration. Go to `Configuration/configure.swift` and replace the `Fluent` import with `FluentMySQL`. At the top of your `configure` function, add this:

https://gist.github.com/calebkleveter/014e1d0229bd32a61f4cc42154e6ef60

This provider handles operations such as creating tables in our database when we boot the application.

Below where you initialize `DatabaseConfig`, add the MySQL database configuration:

https://gist.github.com/calebkleveter/3b4f8b7a12e10f41d71ba3613cbd5652

Your `configure.swift` file should look like this now:

https://gist.github.com/calebkleveter/dcc6cb4dc2d70024770e1bc58fa0c305

You now have MySQL configured with your Vapor application!


# [PostgreSQL](https://docs.vapor.codes/3.0/postgresql/getting-started/)

Open your terminal and run `brew install postgres && brew services start postgres`. This will install and boot Postgres. Postgres will subsequently boot whenever you login, so you shouldn't have to start it again.

We also need to create the database our app will connect to. You can do this by running `createdb <NAME>` in your terminal. I will name it `chatter` to match the name of the application.

To interact with the database, we need to install `FluentPostgreSQL` to our app. Replace the `FluentSQLite` dependency with this declaration in your manifest's `dependencies` array:

https://gist.github.com/calebkleveter/c2ef099ac7a1a5457995d180a05b271a

Make sure you also replaced `FluentSQLite` in the `App` target's dependencies with `FluentPostgreSQL`. You also need to update your packages by running `vapor update -y` or `swift package update`.

Now we need to add `Fluent` and the PostgreSQL database to our app's configuration. Go to `Configuration/configure.swift` and replace the `Fluent` import with `FluentPostgreSQL`. At the top of your configure function, add this:

https://gist.github.com/calebkleveter/4720018fc188c11d1bc6a0fba40f318a

This provider handles operations such as creating tables in our database when we boot the application.

Below where you initialize `DatabaseConfig`, we need to create a `PostgreSQLDatabaseConfig` it to the databases:

https://gist.github.com/calebkleveter/2b6a335f07ef0c89fa3805fb542796a1

Your `configure.swift` file should look like this now:

https://gist.github.com/calebkleveter/a2e985e3f28507eb102b115ad65b39e7

You now have PostgreSQL configured with your Vapor application!