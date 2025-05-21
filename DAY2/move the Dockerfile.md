# by mistake given touch Dokerfile
instead of Dockerfile, in Ubauntu machine, how to change this or rename this
  ![alt text](image.png)
No worries, If you've accidentally created a file named `Dokerfile` instead of `Dockerfile` on your Ubuntu machine, you can simply rename it using the `mv` (move) command in the terminal.

### ✅ Command to rename the file:

```bash
mv Dokerfile Dockerfile
```

### Step-by-step:

1. Open your terminal.
2. Navigate to the directory where the `Dokerfile` is located:

   ```bash
   cd /path/to/your/project
   ```
3. Run the rename command:

   ```bash
   mv Dokerfile Dockerfile
   ```

### To verify:

```bash
ls
```

You should now see `Dockerfile` listed instead of `Dokerfile`.

Let me know if you want to automate checking or fixing this in a script!
= -----------------------------------------------------------------------
# by mistaken done this inside target/
now plase help me to place this dockerfile inside maven-web-app-kk-funda diectory

You're close, The issue is that you're trying to move the `Dockerfile` into a **directory named the same as your current working directory**, but you're **not in the parent directory**, so it's being treated as a **file name**, not a directory.

### ✅ Here's how to fix it:

You need to move **up one level** to the parent directory, then move the file properly.

### Run these commands:

```bash
cd ..
mv target/Dockerfile .
```

Or, if you're already inside `target/`, you can do:

```bash
mv Dockerfile ../
```

This will move `Dockerfile` from `target/` to your main project directory `maven-web-app-project-kk-funda`.

### To confirm:

```bash
ls ../
```

You should now see the `Dockerfile` there.

Let me know if you also want to add typical contents to your Dockerfile!
