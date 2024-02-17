# JMeter course

## Download Jmeter
https://jmeter.apache.org/download_jmeter.cgi

## Folder to extension JMeter
lib/ext

## Install extension manager
https://jmeter-plugins.org/
https://jmeter-plugins.org/wiki/PluginsManager/

Tab Available plugins

Add plugin: Custom Thread groups

## Performance testing process

- **Desing and build test**: Desing onlyt test that fits with uses cases from real world
- **Prepare the test environment**: Set up and environment similar to production environment
- **Run test**: 

Any query can perform well with hundreds or a coouple of thousands of rows
Problems with the DB become evident only when you have hundres of thousand or millins of records

Validate the test script and the test data to see if they work correctly

During the execution of the test, you can monitor the server logs and the test results to see if everything is okay

A high rate of errors can indicate that something is wrong with the test, the applications, the xserver or
a combination of these

- **Analyze the result**: Identify issues that need to be addressed.
Using tools to analyze the results abnd look for persistence and memory problems
- **Optimize**: Tunning application

- **Retest**

Performance testing is done after functional testing, in other words after verifying that all works

Perfromance testing should be done in an environtment equivalent to production
- Same hardware
- Same software
- Same configuration

But it can be doen in small environtments too (own machines)

- Not everyone have access to production environments
- three to ten users are enought for testing (and detect performance problems)

Tools
- Glowroot (For detecting persistence problems)
- jcmd, jstat, and jps (To dynamically get information from JVM)
- jstack (for thread dumps)
- VisualVM and Java Mission control (Form memory information)
- Eclipse MAT (To analize heap dumps)

## Summary

Performance testing: 
testing how an application or resource performs under a given load to identify bottlenecks and issues

Set up JMeter: Plugin manager to extend its functionality

JMeter is a tool to generate load
- Users
- Request

Performance testing process
- Design and build tests
- Prepare the test environment
- Run the tests
- Analyze the results
- Optimize
- Retest

Small testing environtment are okay
- They don't replace an environment equivalente to production
- Start performance testing when you have a funciontal application
- A performance problem will surface in any environment, with a Database of a good size

Expensive tools are not required

## How works JMeter

Execution Order

1. Configuration Element(s)
2. Preprocessor(s)
3. Timer(s)
4. Controlle(s)/Sampler(s)
5. Post-processor(s)
6. Assertion(s)
7. Listener(s)


Tips for desing a Script

- It's better to have one script that tests many use cases of your application
- Never use a single user for loggind in (use an amount realistic)
- Consider realistic proportions for the use cases of your application
- Add asertions to validate the script

 