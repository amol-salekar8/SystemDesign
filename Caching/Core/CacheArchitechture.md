

# Cache aside 
![](image/Cache_aside.png)
**Q.How it works?**
1) Application checks the cache.
2) If the data is there, return it.
3) If not, fetch from the database, store 4) it in the cache, and return it.

# Write-Through Caching

**Q. What it is ?**
1) With write-through caching, the application writes only to the cache.
2) The cache then synchronously writes to the database before returning to the application.
3) The write operation does not complete until both the cache and database are updated.
   <span style="color:red">This text is red</span>
# Write-Behind (Write-Back) Caching

# Read through