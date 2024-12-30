1. `find_by_<columnname>(<columnvalue>)`
2. `find(:first, :conditions => { <columnname> => <columnvalue> }`
3. `where(<columnname> => <columnvalue>).first`

And it looks like all of them end up generating exactly the same SQL. Also, I believe the same is true for finding multiple records:

1. `find_all_by_<columnname>(<columnvalue>)`
2. `find(:all, :conditions => { <columnname> => <columnvalue> }`
3. `where(<columnname> => <columnvalue>)`