# Diving into Vapor, Part 3: Routes and Queries in Vapor 3

In that [last tutorial](https://theswiftwebdeveloper.com/diving-into-vapor-part-2-persisting-data-in-vapor-3-c927638301e8), we learned how to connect a database to our app and save models to it. In this tutorial, we will learn how to query that database to get, update, or delete that data.

---

Before we start adding routes though, we are going to make a change to the `User` model. As it currently is built, the unique property of the model is the `id` property, which is a UUID. Wouldn't it make sense to have the `username` property be unique? It's actually pretty simple to do that.

The `PostgreSQLUUIDModel` sets the `Database` and `ID` types and `idKey` property of the model that conforms to it. To make the `ID` type a string, we need to conform to `Model` and implement the requirements manually:

https://gist.github.com/calebkleveter/4bb5ed95ec995d0f091d0bdb8dc5fad1

Then remove the `id` property from the `User` model and make the `username` property optional:

https://gist.github.com/calebkleveter/35bc4275ef699ef3d8a5a3f6fd2bba97

We need to update the database structure for this change.  Add the following snippet to the global `configure` method:

https://gist.github.com/calebkleveter/ab75958a9acc187eb42a1a3805838cc5

Then go to the project in the terminal and run `vapor build && vapor run revert --all`.

---

# Routing

