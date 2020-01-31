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
```csharp
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

### Add new line in Class adopts DbContext
```csharp
public virtual DbSet<Category> Categories { get; set; }
```

### Run Command
<pre>
add-migration AddCategoriesTable
</pre>
> Note: You can use SQL function to execute raw sql query on AddCategoriesTable class

> Example: Sql("INSERT INTO Categories VALUES ('Web Development')");
<pre>
update-database
</pre>

## Delete Table

<pre>
add-migration DeleteCategoriesTable
</pre>

### Modify migration
* Clone the table you want to delete to new table to preserve data
```csharp
public partial class DeleteCategoriesTable : DbMigration
{
    public override void Up()
    {
        CreateTable(
                "dbo._Categories",
                c => new
                {
                    Id = c.Int(nullable: false, identity: true),
                    Name = c.String(),
                })
            .PrimaryKey(t => t.Id);
        Sql("INSERT INTO _Categories(Name) SELECT Name FROM Categories");

        DropTable("dbo.Categories");
    }
        
    public override void Down()
    {
        CreateTable(
            "dbo.Categories",
            c => new
                {
                    Id = c.Int(nullable: false, identity: true),
                    Name = c.String(),
                })
            .PrimaryKey(t => t.Id);
        Sql("INSERT INTO Categories(Name) SELECT Name FROM _Categories");
        DropTable("dbo._Categories");
    }
}
```

## Revert to previous migration
<pre>
update-database -TargetMigration:AddCategoryColumnToCoursesTable
</pre>
