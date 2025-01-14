---
uid: testresultxmlformat
---

# Test Result XML Format

## `<test-run>`

The required root element for any NUnit 3.0 test result file.

* **Containing Elements:** None
* **Contained Elements:** [`<command-line>`](#command-line), [`<filter>`](#filter), [`<test-suite>`](#test-suite)
* **Attributes:**
  * **id** The unique ID of this test.
  * **testcasecount** The number of test cases contained in this test run.
  * **result** The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
  * **total** The total number of test cases executed in the run. This may be less than the testcasecount due to filtering of tests.
  * **passed** The number of test cases that passed.
  * **failed** The number of test cases that failed.
  * **inconclusive** The number of test cases that were inconclusive.
  * **skipped** The number of test cases that were skipped.
  * **asserts** The number of asserts executed in the test run.
  * **engine-version** The version of the NUnit test engine in use.
  * **clr-version** The runtime version under which the engine is running, taken from Environment.Version.
  * **start-time** The UTC time that the test run started.
  * **end-time** The UTC time that the test run ended.
  * **duration** The duration of the test run in seconds, expressed as a real number.

## `<command-line>`

Holds a CDATA section containing the text of the command used to run the tests.

* **Containing Elements:** [`<test-run>`](#test-run)
* **Contained Elements:** None
* **Attributes:** None

## `<filter>`

The XML representation of the filter used to execute tests.  This element is also used as a fragment in passing the filter to a runner and by the NUnit 3.0 framework and driver.

* **Containing Elements:** [`<test-run>`](#test-run)
* **Contained Elements:** [`<or>`](#or), [`<and>`](#and), [`<not>`](#not), [`<id>`](#id), [`<test>`](#test), [`<class>`](#class), [`<method>`](#method), [`<cat>`](#cat)
* **Attributes:** None

## `<or>`

Represents a composite filter that contains other filters. At least one of the contained filters must pass in order for this filter to pass.

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** [`<or>`](#or), [`<and>`](#and), [`<not>`](#not), [`<id>`](#id), [`<test>`](#test), [`<class>`](#class), [`<method>`](#method), [`<cat>`](#cat), [`<prop>`](#prop)
* **Attributes:** None

## `<and>`

Represents a composite filter that contains other filters. All of the contained filters must pass in order for this filter to pass.

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** [`<or>`](#or), [`<and>`](#and), [`<not>`](#not), [`<id>`](#id), [`<test>`](#test), [`<class>`](#class), [`<method>`](#method), [`<cat>`](#cat), [`<prop>`](#prop)
* **Attributes:** None

## `<not>`

Represents a composite filter that contains wraps a single base filters. The base filter must fail in order for this filter to pass.

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** [`<or>`](#or), [`<and>`](#and), [`<not>`](#not), [`<id>`](#id), [`<test>`](#test), [`<class>`](#class), [`<method>`](#method), [`<cat>`](#cat), [`<prop>`](#prop)
* **Attributes:** None

## `<id>`

Represents a filter that examines the test id, which is generated by NUnit.

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:** None

## `<test>`

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:**
  * **re** Set to '1' to indicate that a regular expression comparison is to be used.

## `<class>`

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:**
  * **re** Set to '1' to indicate that a regular expression comparison is to be used.

## `<method>`

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:**
  * **re** Set to '1' to indicate that a regular expression comparison is to be used.

## `<prop>`

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:**
  * **name** The name of the property to filter on.
  * **re** Set to '1' to indicate that a regular expression comparison is to be used.

## `<cat>`

* **Containing Elements:** [`<filter>`](#filter), [`<or>`](#or), [`<and>`](#and), [`<not>`](#not)
* **Contained Elements:** None
* **Attributes:** None

## `<test-suite>`

* **Containing Elements:** [`<test-run>`](#test-run), [`<test-suite>`](#test-suite)
* **Contained Elements:** [`<environment>`](#environment), [`<settings>`](#settings), [`<properties>`](#properties), [`<reason>`](#reason), [`<failure>`](#failure), [`<output>`](#output), [`<attachments>`](#attachments), [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Attributes**
  * **type** The type of suite represented by this element. Currently supported types are Project, Assembly, TestSuite, TestFixture, GenericFixture, ParameterizedFixture, SetUpFixture, GenericMethod, ParameterizedMethod, Theory.
  * **id** The unique id of this test. Coded as "mmm-nnn" where the part before the hyphen represents the assembly and the part after it represents a test in that assembly. Currently, mmm and nnn are ints, but that is merely an accident of the implementation and should not be relied on.
  * **name** The display name of the test as generated by NUnit.
  * **fullname** The full name of the test as generated by NUnit.
  * **classname** The full name of the class (fixture) representing this test. Only present if `type` is equal to "TestFixture".
  * **testcasecount** The number of test cases contained, directly or indirectly, in this suite.
  * **runstate** An indicator of whether the suite is runnable. Value may be NotRunnable, Runnable, Explicit, Skipped or Ignored. NotRunnable means there is an error in how the test is expressed in code, for example, the signature may be wrong. Explicit, Skipped and Ignored are set by attributes on the test.
  * **result** The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
  * **label** Additional labeling information about the result. In principle, this may be any string value and is combined with the result to give a more precise reason for failure. Currently, NUnit may use the following labels in combination with the Failure result: Error, Cancelled or Invalid. It may use the following labels in combination with a Skipped result: Ignored or Explicit. Additional values may be added in future releases or supplied by extensions, so code that processes a result file should be prepared to deal with any label or none at all.
  * **site** Optional element indicating where a failure occurred. Values are Test, SetUp, TearDown, Parent or Child. Default is Test and the attribute does not normally appear in that case.
  * **start-time** The UTC time that the suite started.
  * **end-time** The UTC time that the suite ended.
  * **duration** The duration of the suite in seconds, expressed as a real number.
  * **total** The total number of test cases executed under this suite.
  * **passed** The number of test cases that passed.
  * **failed** The number of test cases that failed.
  * **inconclusive** The number of test cases that were inconclusive.
  * **skipped** The number of test cases that were skipped.
  * **asserts** The number of asserts executed by the suite, including any nested suites or test cases. Since asserts may be executed in OneTimeSetUp and in ActionAttributes, this number can be greater than the total of the asserts for the test cases.

## `<environment>`

Describes the environment in which the tests in a particular assembly are being run.

* **Containing Elements:** [`<test-suite>`](#test-suite) _(Assembly level only)_
* **Contained Elements:** None
* **Attributes:**
  * `framework-version` The version of the nunit framework in use.
  * `clr-version` The runtime version under which the tests are running, taken from Environment.Version.
  * `os-version` A text string describing the operating system running the tests, taken from Environment.OsVersion.
  * `platform` The platform id, taken from Environment.OsVersion.Platform.
  * `cwd` The current working directory path, taken from Environment.CurrentDirectory.
  * `machine-name` The machine name, taken from Environment.MachineName.
  * `user` The user id, taken from Environment.UserName.
  * `user-domain` The user domain, taken from Environment.UserDomainName.
  * `culture` The current culture, taken from CultureInfo.CurrentCulture.
  * `uiculture` The current UI culture, taken from CultureInfo.CurrentUICulture.
  * `os-architecture` The architecture, taken from GetProcessorArchitecture().

## `<settings>`

Settings used by the engine for executing an assembly. These are taken from the supplied settings in the
`TestPackage` supplemented by default settings created by the engine itself.

* **Containing Elements:** [`<test-suite>`](#test-suite) _(Assembly level only)_
* **Contained Elements:** [`<setting>`](#setting)
* **Attributes:** None

## `<setting>`

A single setting

* **Containing Elements:** [`<settings>`](#settings)
* **Contained Elements:** None
* **Attributes:**
  * **name** The name of the setting.
  * **value** The value assigned to the setting.

## `<test-case>`

* **Containing Elements:** [`<test-suite>`](#test-suite)
* **Contained Elements:** [`<properties>`](#properties), [`<reason>`](#reason), [`<failure>`](#failure), [`<output>`](#output), [`<attachments>`](#attachments)
* **Attributes**
  * `id` The unique id of this test. Coded as "mmm-nnn" where the part before the hyphen represents the assembly and the part after it represents a test in that assembly. Currently, mmm and nnn are ints, but that is merely an accident of the implementation and should not be relied on.
  * `name` The display name of the test as generated by NUnit or, in the case of some parameterized tests, specified by the user.
  * `fullname` The full name of the test as generated by NUnit.
  * `methodname` The name of the method representing the test case.
  * `classname` The full name of the class in which this test case appears.
  * `runstate` An indicator of whether the suite is runnable. Value may be NotRunnable, Runnable, Explicit, Skipped or Ignored. NotRunnable means there is an error in how the test is expressed in code, for example, the signature may be wrong. Explicit, Skipped and Ignored are set by attributes on the test.
  * `seed` The seed used to generate random arguments and other values for this test.
  * `result` The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
  * `label` Additional labeling information about the result. In principle, this may be any string value and is combined with the result to give a more precise reason for failure. Currently, NUnit may use the following labels in combination with the Failure result: Error, Cancelled or Invalid. It may use the following labels in combination with a Skipped result: Ignored or Explicit. Additional values may be added in future releases or supplied by extensions, so code that processes a result file should be prepared to deal with any label or none at all.
  * `site` Optional element indicating where a failure occurred. Values are Test, SetUp, TearDown, Parent or Child. Default is Test and the attribute does not normally appear in that case.
  * `start-time` The UTC time that the test started.
  * `end-time` The UTC time that the test ended.
  * `duration` The duration of the test in seconds, expressed as a real number.
  * `asserts` The number of asserts executed by the test.

## `<properties>`

Optional element containing any properties assigned to the test case or suite.

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** [`<property>`](#property)
* **Attributes** None

## `<property>`

A single property

* **Containing Elements:** [`<properties>`](#properties)
* **Contained Elements:** None
* **Attributes**
  * **name** The name of the property
  * **value** The value of the property

## `<reason>`

Optional element that may appear on tests or suites that were not executed. The element may also appear on tests that were short circuited using `Assert.Pass`. Contains a message giving the reason for skipping or short circuiting the test.

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** [`<message>`](#message)
* **Attributes** None

## `<failure>`

Optional element that appears on all tests or suites with a result of 'Failed'. Optionally contains the error message and/or a stack trace.

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** [`<message>`](#message), [`<stack-trace>`](#stack-trace)
* **Attributes** None

## `<assertions>`

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** [`<assertion>`](#assertion)
* **Attributes** None

## `<assertion>`

* **Containing Elements:** [`<assertions>`](#assertions)
* **Contained Elements:** [`<message>`](#message), [`<stack-trace>`](#stack-trace)
* **Attributes**
  * **result** The result of the assertion. May be Inconclusive, Passed, Warning, Failed or Error.

## `<message>`

Optional element with a CDATA section containing a message relating to the test's result.

* **Containing Elements:** [`<failure>`](#failure), [`<reason>`](#reason), [`<assertion>`](#assertion)
* **Contained Elements:** None
* **Attributes** None

## `<stack-trace>`

Optional element with a CDATA section containing a stack-trace of the location where a test failed.

* **Containing Elements:** [`<failure>`](#failure), [`<assertion>`](#assertion)
* **Contained Elements:** None
* **Attributes** None

## `<output>`

Optional element that appears on tests or suites that produce text output. The output may be intercepted from writes to the console or captured directly when the test writes to the TestContext. It is contained in a CDATA section.

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** None
* **Attributes** None

## `<attachments>`

Optional element that appears when files are attached to a test. Contains a list of `<attachment>` elements.

* **Containing Elements:** [`<test-suite>`](#test-suite), [`<test-case>`](#test-case)
* **Contained Elements:** [`<attachment>`](#attachment)
* **Attributes** None

## `<attachment>`

Groups together the file path and description of a test attachment.

* **Containing Elements:** [`<attachments>`](#attachments)
* **Contained Elements:** [`<filePath>`](#filepath), [`<description>`](#description)
* **Attributes** None

## `<filePath>`

Contains the file path for the attachment. Paths will be fully rooted.

* **Containing Elements:** [`<attachment>`](#attachment)
* **Contained Elements:** None
* **Attributes** None

## `<description>`

Optional element that contains the user's description of the attachment. It is contained in a CDATA section.

* **Containing Elements:** [`<attachment>`](#attachment)
* **Contained Elements:** None
* **Attributes** None
