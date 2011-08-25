README.rst

---------------------------------
InconsistencyInspectorResources
---------------------------------


This project contains the resources require to collect data for the InconsistencyInspector. Basically the project enables you to extract the static and dynamic call graphs for a system and export them to an XML file. Currently only projects that can be built (and have their test suite executed) by ``ant`` are supported. If you have any problems, please contact me.

**NOTE** The static targets are easy to use and configure; the dynamic targets are much more finicky (expect to succeed, but be frustrated in the process).

Instructions
---------------------------------

**Simple Instructions:**

	1) Download and configure this project.
	2) Compile your system and run ``ant iStatic`` to extract the static call graph.
	3) Weave your system (``ant weave``) and run its test suite to extract the dynamic call graph.

**Complete Instructions:**

	1) Checkout this project (``hg clone ssh://hg@bitbucket.org/rtholmes/inconsistencyinspectorresources``)
	2) Copy ``build.inconsistency.xml`` to your project's root directory (where your ``build.xml`` is located) and add ``<import file="build.inconsistency.xml"/>`` to the bottom of your ``build.xml`` file (just above the ``</project>`` tag).
	3) Copy ``InconsistencyInspector.properties`` to the same directory as in step 2.
	4) Modify ``InconsistencyInspector.properties`` as described in the file itself; this will configure the static and dynamic analysis engines.
	5) Compile your system and its tests (this depends on your ant configuration but ``ant compile`` is often right).
	6) Extract the static call graph by executing ``ant iiStatic``. The static call graph will be in the report directory you specified in the properties file.
	7) Run your test suite to make sure everything executes as it should (this step is optional).
	8) Make a custom copy of ``Tracer.aj`` (e.g., ``Tracer_MyProject.aj``). Using search and replace, substitute the base package name (e.g., ``org.foo.project``) for ``org.joda.time`` in the tracer aspect. Update ``aspect.lst`` to list your tracer filename instead of ``Tracer.aj``.
	9) Weave your system to enable the dynamic call graph collection by executing ``ant iiWeave``. Optional: update your ant heap size (export ``ANT_OPTS="-Xms512m -Xmx512m"`` in bash).
	10) Update the ``iiDynamic`` target in ``build.inconsistency.xml`` to look like the target that runs the tests in your own system. Important: you should run the test code from the directory that the iiWeave target outputs the code from. XXX: more detail needed here. (Classpath setup?)
	11) Run your test suite as you normally would (this depends on your ant configuration but ``ant test`` is often right). The dynamic call graph will be in the report directory you specified in the properties file.

Advanced Notes
---------------------------------

** Logging **

Two parameters are provided for disabling logging in the inconsistencyinspectorresources projects:

	1) ``-Dlsmr.logLevel="OFF"`` Will disable the majority of log messages (in anything that uses log4j).
	2) ``-Dii.logLevel="OFF"`` Will disable log messages in the ``inconsistecy.core`` project (GWT does not let this project use log4j directly).

NOTE: these parameters work on the command line or in Eclipse but will not work through ant (e.g., ant does not forward the values to any JVMs it launches).

If you have any problem running the iStatic or iDynamic targets you may need to modify the ``build.inconsistency.xml``. This may be necessary if you have an unusual or complex build environment. 
