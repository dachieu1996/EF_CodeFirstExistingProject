# CodeFirstExistingProject

## Install EntityFramework: 
<pre>
Install-Package EntityFramework
</pre>

## Run migration and update database
<pre>
enable-migrations
</pre>
<pre>
add-migration InitialModel
</pre>
<pre>
add-migration InitialModel -IgnoreChanges -Force
</pre>
<pre>
update-database
</pre>

## Add new Model Class
<pre>
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }
}
</pre>

### Add new line in Class adopts DbContext
<pre>
public virtual DbSet<Category> Categories { get; set; }
</pre>

### Run Command
<pre>
add-migration AddCategoriesTable
</pre>
> Note: You can use SQL function to execute raw sql query on AddCategoriesTable class

> Example: Sql("INSERT INTO Categories VALUES ('Web Development')");
<pre>
update-database
</pre>
