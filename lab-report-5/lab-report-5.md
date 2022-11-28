
Vadim Victor Kim  
CSE 15L  
11/23/2022

# Lab Report 5

## **Your grade.sh in a code block**
My grade.sh:
```
# remove student submission folder
rm -rf student-submission

# git clone the repo provided
git clone $1 student-submission

# check if file exists
if [ -f ./student-submission/ListExamples.java ]
then
    echo "Found student java file..."
else
    echo "No student java file..."
    exit 1
fi

#copy the needed files for testing
cp ./TestListExamples.java ./student-submission
cp -r ./lib ./student-submission

#go to dir
cd ./student-submission

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java

if [ $? -eq 0 ]
then
    echo "Compiled..."
else
    echo "Did not compile..."
    echo $?
    exit 1
fi
echo "--------"
echo "Running tests..."

java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > results.txt

echo "Test output:"
grep -i "test" results.txt
```

## **Screenshots of three different student submissions and their reported grade as loaded in the browser (URL like https://localhost:4000/grade?repo=https://github.com...)**

Testing `https://github.com/ucsd-cse15l-f22/list-methods-compile-error`:
![Alt text](Screen%20Shot%202022-11-27%20at%207.26.51%20PM.png)

Testing `https://github.com/ucsd-cse15l-f22/list-methods-filename`:
![Alt text](Screen%20Shot%202022-11-27%20at%207.27.29%20PM.png)

## **Then, choose one of the examples you showed in screenshot, and describe a trace of what your grade.sh does on that example.**

Testing `https://github.com/ucsd-cse15l-f22/list-methods-corrected`:
![Alt text](Screen%20Shot%202022-11-27%20at%207.25.44%20PM.png)

With this submission, it first removes the previous cloned files if they exist:
```
rm -rf student-submission
```
This does not return anything as far as I can tell while testing its output with echo.

We then clone the repo provided:
```
git clone $1 student-submission
```

This also does not seem to return anthing other than zero even if the cloning does not work.

We then run an if check to see if the file we are gonna be testing on exists:
```
if [ -f ./student-submission/ListExamples.java ]
then
    echo "Found student java file..."
else
    echo "No student java file..."
    exit 1
fi
```
The `[ -f ./student-submission/ListExamples.java ]` inside the if statement checks if file in path `./student-submission/ListExamples.java` exists. If so it outputs `"Found student java file..."` like in this case. If it did ot it would say `"No student java file..."` and then exit the script with a code of 1 indicating faliure.

We then copy the java test files needed to the folder so when we compile we can run the tests we created for grading, and set our working directory to the student-submission folder we cloned:
```
cp ./TestListExamples.java ./student-submission
cp -r ./lib ./student-submission
cd ./student-submission
```

We then compile the java files:
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
```
This either outputs a 0 if the compilation went through and a 1 if there were some errors.
In this case it outputs a 0 since there were no problems.

We then check if the output of the compilation attempt was 0:
```
if [ $? -eq 0 ]
then
    echo "Compiled..."
else
    echo "Did not compile..."
    echo $?
    exit 1
fi
echo "--------"
echo "Running tests..."
```

We first see if `$?` was set to 0 in `[ $? -eq 0 ]` and if so, we just show that it was compiled by saying `"Compiled..."`. If the code was anything other than zero, we simply say `"Did not compile..."`, followed by the error code and exit the script with a 1.

If no problems occured we write a separation line and tell the user that we are running tests.

We then run the java tests and send the output to a results.txt file:
```
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > results.txt
```

There is an exit code that is outputted from this, but we do not ever check it since we can just get to know what happened from the console output.

We then grep the output to see how many tests were passed. Since we know that number of passed tests is indicated on line that has `"test"` in it, we can just directly look for that and output it:
```
echo "Test output:"
grep -i "test" results.txt
```

and thus we get the output.