# Lab Report 2 
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 10/22/2023

Back to [index](https://miranda-y-zhou.github.io/cse15l-lab-reports/)

---

## Servers and SSH Keys (Week 3)

The objective of this lab is to create a Java web server, `StringServer`, to accumulate and display messages.
This lab also delve into SSH key authentication, showcasing a password-less login to `ieng6`, followed by reflections on the learnings from weeks 2 and 3.


* [Web Server: `StringServer`](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report2.html#string-server)
* [SSH Key](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report2.html#ssh-key-authentication)
* [Learning Reflection](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report2.html#learning-reflection)

---

### String Server

The `StringServer` is a Java web server designed to maintain a running string of messages. Users can add messages via incoming requests, and each message gets prefixed with a sequential number. When accessed without a specific query in the URL, the server displays the accumulated list of messages to the user.

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.

    // num is the current number of messages in the server
    int num = 0;
    String allMessages = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Current messages:" + '\n' + allMessages;
        } 
        else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    num += 1;
                    allMessages = allMessages + String.format("\n %d. %s", num, parameters[1]);
                    return String.format("The message '%s' is successfully added!", parameters[1]);
                }
                else {
                return "ERROR: '/add-message' requires a valid query that begins with '?s=<string>'" + 
                        "\n Example: '/add-message?s=Hello'" + 
                        "\n The page would show: '1. Hello'";
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

The server page should look like this in a web browser:

![image of server home page](Images/Screen Shot 1.png)

&nbsp;

#### Example 1: 

The user adds the string message: `Daisy`

![image of adding Daisy](Images/Screen Shot 2.png)

Resulting string of messages:

![image of server home page](Images/Screen Shot 3.png)

The state of the server is stored in two variables: `num` (number of messages) and `allMessages` (accumulated messages).

> In this example, `num` is currently `0`, and `allMessages` is an empty string since there are no messages stored in the server yet.

By using `/add-message?s=Daisy`, the method `handleRequest` in the `Handler` Class is called. This method serves to manage the incoming URL requests, thus the relevant argument to this method is the `url`.

> In this example, `url` is `/add-message?s=Daisy`.

After checking correctness of the path of the `url` using the `getPath()` method of 'URI' Class (improted), the `url` is then extracted only the query part using the `getQuery()` method of 'URI' Class (improted). 

> In this example, query is `?s=Daisy`.

The query is splited at the `=` character, resulting in a string array `parameters`. This allows for validation of the query parameter `s` and extraction of the message following the `=`.

Since the request in this example, `/add-message?s=Daisy`, comes with the valid path `/add-message` and the right query parameter `s`, the `num` is incremented, the message along with its list number sequence is concatenated to `allMessages`, and a success message is returned. 

> In this example, the resulting `num` is now `1` and the resulting `allMessages` is now `\n 1. Daisy`.

&nbsp;

#### Example 2: 

The user adds the string message: `Roses are red` 

![image of adding Roses are red](Images/Screen Shot 4.png)

It is noted that spaces in the query appears as `%20`.

Resulting string of messages:

![image of server home page](Images/Screen Shot 5.png)

The state of the server is stored in two variables: `num` (number of messages) and `allMessages` (accumulated messages).

> In this example, `num` is `1`, and `allMessages` is `\n 1. Daisy` continuing from the previous example.

By using `/add-message?s=Roses are red`, the method `handleRequest` in the `Handler` Class is called. This method serves to manage the incoming URL requests, thus the relevant argument to this method is the `url`.

> In this example, `url` is `/add-message?s=Roses%20are%20red`.

After checking correctness of the path of the `url` using the `getPath()` method of 'URI' Class (improted), the `url` is then extracted only the query part using the `getQuery()` method of 'URI' Class (improted). 

> In this example, query is `?s=Roses%20are%20red`.

The query is splited at the `=` character, resulting in a string array `parameters`. This allows for validation of the query parameter `s` and extraction of the message following the `=`.

Since the request in this example, `/add-message?s=Roses%20are%20red`, comes with the valid path `/add-message` and the right query parameter `s`, the `num` is incremented, the message along with its list number sequence is concatenated to `allMessages`, and a success message is returned. 

> In this example, the resulting `num` is now `2` and the resulting `allMessages` is now `\n 1. Daisy\n 2. Roses are red`.

&nbsp;

#### Example 3: 

When the user tries to add a string message, but without following the correct query syntax:

![image of error](Images/Screen Shot 6.png)

Resulting string of messages:

![image of server home page](Images/Screen Shot 5.png)

An error message guides the user on the correct usage, and no variables are changed.

This is because the server `StringServer` has been programmed to expect a specific query structure for adding messages. If the incoming request doesn't adhere to this expected format, the server is designed to recognize the discrepancy and respond with an error message to inform the user of the incorrect input. This ensures that users adhere to the expected input pattern and that the server remains resilient against unintended or malicious inputs.

&nbsp;

---

### SSH Key Authentication

SSH key authentication is a secure method for remote server access, utilizing a pair of cryptographic keys: a private key kept by the user and a public key stored on the server. Instead of using passwords, the server confirms the identity of the user by challenging them to prove ownership of the private key. This method enhances security and facilitates password-less logins.

#### 1. Locating the private key on local computer:

![image of private key location](Images/Screen Shot private key on local.png)

As shown in the image above, the path to the private key for logging into `ieng6` is `/Users/zhoujijun/.ssh/id_rsa` on the user's local computer.

&nbsp;

#### 2. Locating the public key on `ieng6`:

![image of public key location](Images/Screen Shot public key on ieng6.png)

As shown in the image above, the path to the public key for logging into `ieng6` is `/home/linux/ieng6/cs15lfa23/cs15lfa23do/.ssh/authorized_keys` on the remote computer `ieng6`.

&nbsp;

#### 3. Logging into `ieng6` without password:

![image of login using key](Images/Screen Shot login with key.png)

As shown in the image above, the user can now access the remote computer `ieng6` both swiftly and securely.

&nbsp;

---

### Learning Reflection

During weeks 2 and 3 of our labs, I discovered the elegance of crafting simple Java-based web servers—a feat I hadn't realized could be achieved with just a handful of Java files. I was also introduced to remote computer access via `ssh`, and the invaluable role of SSH keys in facilitating password-free user authentication. Utilizing SSH keys not only streamlines the login process but also enhances security through cryptographic measures. 

&nbsp;

