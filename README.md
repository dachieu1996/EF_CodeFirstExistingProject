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
