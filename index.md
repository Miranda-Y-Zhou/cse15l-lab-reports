*Hello World*
**Hello World**
# Hello World
## Hello World
[Link](http://miranda-y-zhou.github.io/cse15l-lab-reports/)
![Image](https://upload.wikimedia.org/wikipedia/commons/c/cb/The_Blue_Marble_%28remastered%29.jpg)
> Hello
* Hi
* hello
* bye
1. hi
2. hello
3. bye
---
'hello.java' file
'''
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}
'''
