---------------------------------
InconsistencyInspectorResources
---------------------------------


This project contains the resources require to collect data for the InconsistencyInspector. Basically the project enables you to extract the static and dynamic call graphs for a system and export them to an XML file. Currently only projects that can be built (and have their test suite executed) by ``ant`` are supported. If you have any problems, please contact me.

** NOTE** Currently only the static targets are working.

Instructions
---------------------------------

**Simple Instructions:**

	1) Download and configure this project.
	2) Compile your system and run ``ant iStatic`` to extract the static call graph.
	3) Weave your system (``ant weave``) and run its test suite to extract the dynamic call graph.

**Complete Instructions:**

	1) Checkout this project (``hg clone XXX``)
	2) Copy ``build.inconsistency.xml`` to your project's root directory (where your ``build.xml`` is located) and add ``<import file="build.inconsistency.xml"/>`` to the bottom of your ``build.xml`` file (just above the ``</project>`` tag).
	3) Copy ``InconsistencyInspector.properties`` to the same directory as in step 2.
	4) Modify ``InconsistencyInspector.properties`` as described in the file itself; this will configure the static and dynamic analysis engines.
	5) XXX: Modify the tracer aspect.
	6) Compile your system and its tests (this depends on your ant configuration but ``ant compile`` is often right).
	7) Extract the static call graph by executing ``ant iiStatic``. The static call graph will be in the report directory you specified in the properties file.
	8) Run your test suite to make sure everything executes as it should (this step is optional).
	9) Weave your system to enable the dynamic call graph collection by executing ``ant iiWeave``.
	10) Run your test suite as you normally would (this depends on your ant configuration but ``ant test`` is often right). The dynamic call graph will be in the report directory you specified in the properties file.

Advanced Notes
---------------------------------

If you have any problem running the iStatic or iDynamic targets you may need to modify the ``build.inconsistency.xml``. This may be necessary if you have an unusual or complex build environment. 
