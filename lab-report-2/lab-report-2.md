Vadim Victor Kim  
CSE 15L  
10/14/2022

# Lab Report 2


## **Part 1**
My `SearchEngine.java` file contents:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    private ArrayList<String> savedStrings;

    public Handler(){
        savedStrings = new ArrayList<String>();
    }

    private void add(String s){
        savedStrings.add(s);
    }

    private ArrayList<String> search(String s){
        ArrayList<String> o = new ArrayList<String>();
        for (int i = 0; i < savedStrings.size(); i++) {
            if(savedStrings.get(i).contains(s)){
                o.add(savedStrings.get(i));
            }
        }
        return o;
    }

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            if(savedStrings.size() <= 0){
                return "No strings yet!";
            }
            String allStrings = "";
            for (int i = 0; i < savedStrings.size(); i++) {
                allStrings += savedStrings.get(i) + ", ";
            }
            return String.format("All saved terms: " + allStrings.substring(0, allStrings.length() - 2));
        } else if (url.getPath().equals("/add")) {
            String[] parameters = url.getQuery().split("=");
            this.add(parameters[0]);
            return String.format("Added string " + parameters[0] + ".");
        }else if (url.getPath().equals("/search")) {
            String[] parameters = url.getQuery().split("=");
            ArrayList<String> found = this.search(parameters[0]);

            String allStrings = "";
            for (int i = 0; i < found.size(); i++) {
                allStrings += found.get(i) + ", ";
            }
            return String.format("Searched for " + parameters[0] + ". Found: " + allStrings.substring(0, allStrings.length()-2));
        } else {
            return "404 Not Found!";
        }
    }
}

class SearchServer {
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

## **What it looks like when running:**

**Server before adding anything:**
![](Screen%20Shot%202022-10-14%20at%206.37.17%20PM.png)

**Using add call with "apple" as parameter:**
![](Screen%20Shot%202022-10-14%20at%206.35.24%20PM.png)
When performing this, the `add()` call is made with the first parameter. In this case, "apple".

**Seeing the website after adding a few items:**
![](Screen%20Shot%202022-10-14%20at%206.36.12%20PM.png)

**Using search call with "app" as parameter:**
![](Screen%20Shot%202022-10-14%20at%206.34.17%20PM.png)
When performing this, the `search()` call is made with the first parameter. In this case, "app".


## **Part 2**

### Bug 1:
In `ArrayExamples.java` the `reversed(int[] arr)` method fails with input of null.

The code to recreate the failure is:
```
ArrayExaples.reversed(null);
```


This causes a symptom of a null reference error.

The simple code fix needed is to check for null value before performing any operations on it. When rewritten it could look something like this:
```
static int[] reversed(int[] arr) {
    if(arr == null) return null; //<-- new null check!
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

The bug causes this particular symptom because we never check if input is valid before working on it.

### Bug 2:
In `LinkedListExample.java` the `first()` method fails without any input if the linked list was just created.

The code to recreate the failure is:
```
LinkedList ll = new LinkedList();
ll.first(); //<-- causes a null ref
```

The symptom is a null reference error when calling first method.

The bug is due to the this.root variable not being checked for being null. A simple addition could look something like this:
```
public int first() {
    if(this.root == null) return -1;
    return this.root.value;
}
```

The connection between the symptom and the bug is that the method is trying to look at this.root's properties even though it cound be unassigned.