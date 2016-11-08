---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Logging and tracing
{: #logging_tracing}

Last Updated: 15 September 2016
{: .last-updated}

## Log files
{: #log_files}

The standard Liberty logs, such as messages.log or the ffdc directory, are available in IBM Bluemix in the logs directory of each application instance. These logs can be accessed from the IBM Bluemix console or by using the cf logs and cf files commands.
For example, to see the messages.log file, run the command:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

The log level and other trace options can be set through the Liberty configuration file. For more information, see [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Tracing can also be adjusted on a running application instance by using the IBM Bluemix console.

## Using the trace and dump capabilities
{: #using_trace_and_dump}

In the IBM Bluemix user interface, there are trace and dump capabilities.
* Use Trace to view and update the Liberty logging traceSpecification on running application instances.
* Use Dump to create thread and heap dumps on running application instances.

To do this action, select a Liberty application in the user interface. In the category Runtime in the navigation, you can open the instance details. Select an instance or multiple instances. In the Actions menu, you can choose TRACE or DUMP.

## Download dump files
{: #download_dumps}

	* Prerequisite:
 	1. [Install CF CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
 	2. [Install Diego-Enabler plugin](https://github.com/cloudfoundry-incubator/Diego-Enabler) on CF CLI for Diego

	* In DEA, you can download dump files through following steps:
    
		Step 1: get app_guid
		```
		$ cf app <yourappname> --guid
		```

		Step 2: download dump file to local

		```
		$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dumpname> --output <dumpname>
		```

	* In Diego, you can access dump files through following steps

    
		Step 1: get app_guid
		```
		$ cf app <yourappname> --guid
		```

		Step 2: get app_ssh_endpoint(host:port) and app_ssh_host_key_fingerprint

		```
		$ cf curl /v2/info
		```

		Step 3: get ssh-code for scp command

		```
		$ cf ssh-code
		```

		Step 4: scp remote dump file to local
		
		```
		$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file> <local_file_name>
		```

		when ask password, please input <ssh-code>

	Refer to [Accessing Apps with SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) for more details


# rellinks
{: #rellinks}
## general
{: #general}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

