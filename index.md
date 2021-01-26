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
