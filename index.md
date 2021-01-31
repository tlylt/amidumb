<frontmatter>
  header: header.md
  pageNav: 4
  pageNavTitle: "Dumb Stuff"
  siteNav: site-nav.md
</frontmatter>

<br>

<div class="jumbotron jumbotron-fluid bg-dark text-white">
  <div class="container">
    <h1 class="display-4 no-index">Dumb Stuff</h1>
    <p class="lead">Silly bugs that I spent MUCH time debugging and hence worth a place here in the hall of LAME</p>
  </div>
</div>

### Writing files in Java but gave a wrong file name

- Wong code

```java
Files.write(Paths.get("user.dir","data","database.txt"),
    str, StandardOpenOption.TRUNCATE_EXISTING);
```

- Correct code

```java
Files.write(Paths.get(System.getProperty("user.dir"), "data",
 "database.txt"), str, StandardOpenOption.TRUNCATE_EXISTING);
```

- What I thought

  Because the error message is about file writing, I thought that the error is
  with the creating of directory and file. So when I created the new directory
  and file using the below code, I thought that maybe it does not complete the file creation while the program is still running. Hence this might have caused the error of file not exist yet. This mistake arise also because that I only observe the new folder and file being created when the entire program exits, not right after the execution of the below code.

```java
            if (Files.notExists(folder)) {
                Files.createDirectories(folder);
            }
            if (Files.notExists(file)) {
                Files.createFile(file);
            }
```

- What actually happened

  Instead of getting the current working directory, I wrongly put in the plain string
  "user.dir" as the directory name.

- Lesson learned

  ALWAYS look at the error message properly before going into a witchhunt and trying all
  sorts of bug fix.

- Time wasted

  1.5 hours

### Pointing to the wrong IP address when adding A record in Domain DNS

- What I thought

We used a floating IP provided by DigitalOcean for the server that we are using. I therefore added the floating IP to the DNS record for the intended domain name.

- What actually happened

When we were unable to finish the deployment process, we decided to shut down the server and carry on the next day. In the meantime I suggested to remove the floating IP attached as this IP will incure cost if not attached to an instance. So the public IP of the server is the default IP address provided. However, the A record of the DNS, is still pointing to the previous floating IP. There was also an issue of DNS servers, which I should probably continue using the ones from my domain service provider, and not add the ones from DigitalOcean.

- Lesson learned

When there are issues of cannot resolve DNS, check either the A record is updated correctly and also the DNS servers are added correctly.

- Time wasted

3 hours
