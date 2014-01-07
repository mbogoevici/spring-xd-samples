Spring XD Simple Batch Sample
=============================

This is the quintessential *Hello World* example for *Spring XD*. It consists of only one [Tasklet](http://static.springsource.org/spring-batch/apidocs/org/springframework/batch/core/step/tasklet/Tasklet.html) which prints out `Hello Spring XD!`.

## Requirements

In order for the sample to run you will need to have installed:

* Spring XD ([Instructions](https://github.com/SpringSource/spring-xd/wiki/Getting-Started))

## Building



	$ mvn clean assembly:assembly

As a result, you will see the following files and directories created under `target/springxd-batch-simple-1.0.0.BUILD-SNAPSHOT-bin/`:

```
|-- springxd-batch-simple-1.0.0.BUILD-SNAPSHOT-bin
|   |-- lib
|   |   `-- springxd-batch-simple-1.0.0.BUILD-SNAPSHOT.jar
|   `-- modules
|       `-- job
|           `-- myjob.xml
```

## Running the Sample

**IMPORTANT**: Please ensure that you have defined the `$XD_HOME` environment variable, pointing to the correct *Spring XD* home directory.

In the `batch-simple` directory run the shell script copy-files.sh.  

  
	$ ./copy-files.sh


This will move the build artifacts into the `modules/job` and `lib` directories to the right locations under *$XD_HOME*.

Now your sample is ready to be executed. Start your *Spring XD* admin server (If it was already running, you must restart it):

	xd/bin>$ ./xd-singlenode

	 _____                           __   _______
	/  ___|          (-)             \ \ / /  _  \
	\ `--. _ __  _ __ _ _ __   __ _   \ V /| | | |
	 `--. \ '_ \| '__| | '_ \ / _` |  / ^ \| | | |
	/\__/ / |_) | |  | | | | | (_| | / / \ \ |/ /
	\____/| .__/|_|  |_|_| |_|\__, | \/   \/___/
	      | |                  __/ |
	      |_|                 |___/
	1.0.0.BUILD-SNAPSHOT             eXtreme Data


	Started container : SingleNodeApplication
	Documentation: https://github.com/SpringSource/spring-xd/wiki
	...

Now start the *Spring XD Shell* in a separate window:

	shell/bin>$ ./xd-shell

	 _____                           __   _______
	/  ___|          (-)             \ \ / /  _  \
	\ `--. _ __  _ __ _ _ __   __ _   \ V /| | | |
	 `--. \ '_ \| '__| | '_ \ / _` |  / ^ \| | | |
	/\__/ / |_) | |  | | | | | (_| | / / \ \ |/ /
	\____/| .__/|_|  |_|_| |_|\__, | \/   \/___/
	      | |                  __/ |
	      |_|                 |___/
	eXtreme Data
	1.0.0.BUILD-SNAPSHOT | Admin Server Target: http://localhost:9393
	Welcome to the Spring XD shell. For assistance hit TAB or type "help".
	xd:>

You will now create a new Batch Job Stream using the *Spring XD Shell*:

	xd:>job create --name helloSpringXD --definition "myjob" --deploy false

The UI is located on the machine where xd-singlenode is running and will show you the jobs that can be deployed. The UI is located at:

* **http://localhost:9393/admin-ui**

Alternatively, you can deploy it using the command line

	xd:>job deploy helloSpringXD

And then launch the job

	xd:>job launch helloSpringXD

You should see a message:

	Hello Spring XD!
	The following 1 Job Parameter(s) is/are present:
	Parameter name: random; isIdentifying: true; type: STRING; value: 0.07119643877192872

You can also experiment with Job parameters:

	job launch helloSpringXD --params "{"myStringParameter":"foobar","-secondParam(long)":"123456"}"

	Hello Spring XD!
	The following 3 Job Parameter(s) is/are present:
	Parameter name: secondParam; isIdentifying: false; type: LONG; value: 123456
	Parameter name: myStringParameter; isIdentifying: true; type: STRING; value: foobar
	Parameter name: random; isIdentifying: true; type: STRING; value: 0.06893349621991496
	12:04:18,384  INFO http-nio-9393-exec-5 support.SimpleJobLauncher:135 - Job: [FlowJob: [name=helloSpringXD.job]] completed with the following parameters: [{secondParam=123456, myStringParameter=foobar, random=0.06893349621991496}] and the following status: [COMPLETED]

