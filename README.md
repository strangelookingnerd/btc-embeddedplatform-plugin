# Description

The Jenkins Automation Plugin for BTC EmbeddedPlatform provides easy to
use steps for Jenkins Pipeline enabling you to execute test workflow
steps from Jenkins. The BTC EmbeddedPlatform HTML reports become
available automatically on the Jenkins job page and a JUnit XML report
is generated that feeds into Jenkins test trends and status overview
dashboards.

The following workflow steps are available for Jenkins Pipeline:

-   Profile Load / Create / Update
-   Import of Test Cases and Stimuli Vectors
-   Import / Export of Tolerances and Input Restrictions
-   Execution of Functional Tests
-   Automatic Vector Generation & Analysis
-   Back-to-Back Test Execution
-   Regression Test Execution
-   Formal Verification
-   Formal Test
-   Configuration of Additional Coverage Goals
-   Export of different reports
-   BTC Migration Suite

For these workflow steps many additional settings can be configured
(optional) in order to adapt the automated test runs to your individual
project needs. In addition, two utility methods help you to connect to
instances of BTC EmbeddedPlatform and to close them if again required.
In addition, the Migration Suite use case can be addressed (see section
Migration Suite below).

# Release Notes

Version | Release Notes | EP Version | Update BTC-part | Update Jenkins-part
--------|---------------|------------|-----------------|--------------------
2.5.3 | - Added workaround that allows EmbeddedCoder architecture udpate in Jenkins scenarios that currently don't work out of the box. CodeModel and Mapping XML must be provided in the btc.profileLoad step. | 2.5 | X | 
2.5.2 | - Fixed: updating the default compiler in a model-based profile needed some additional efforts and could lead to problems before now. | 2.5 | X | 
2.4.19 | - Fixed: updating the default compiler in a model-based profile needed some additional efforts and could lead to problems before now. | 2.4.1 | X | 
2.4.17 | - Available execution configs can now be queried for a profile allowing a generic way to handle steps on different kinds of existing profiles. | 2.4.1 | X | X
2.4.15 | - Fixed: model paths were only updated if updateRequired option was true. However, there are use cases where the model paths need to be updated even though updateRequired is false. | 2.4.1 | X | X
2.4.14 | - Fixed: model paths were only updated if updateRequired option was true. However, there are use cases where the model paths need to be updated even though updateRequired is false. | 2.4.1 | X | 
2.4.13 | - Fixed: robustnessTestFailure property of vectorGeneration step was not properly handled | 2.4.1 | X | 
2.4.12 | - Added option to control Matlab Instance Policy<br>- Fixed path conversion issues for Jenkins related archiving tasks | 2.4.1 | X | X
2.4.11 | - Added explicit step to create Test Execution Reports: btc.testExecutionReport<br>- The step btc.rbtExecution no longer creates Test Execution Reports by default but this can still be achieved by setting its new property "createReport" to true.<br>- Added robustness for duplicate separators when using absolute paths | 2.4.1 | | X
2.4.10 | - Adaptions for EP 2.4.1 | 2.4.1 |  |
2.4.1 | - Fixed a bug that caused Test Execution and Regression Test steps to return the wrong return code. | 2.4 | X | 
2.4.0 | - Support for EmbeddedTester BASE (see parameter "licensingPackage" in the "startup" step for more details). | 2.4 | X | X
2.3.0 | - Added filters for scopes, folders and testcase names. For each of the three a whitelist and blacklist can be defined as a comma separated string. | 2.4 | X | X
2.2.0 | - Added a step to generate and export a model coverage report (RBT & B2B). Requires the Simulink V&V / Simulink Coverage license.<br>- Test cases (so far only test cases, no SVs, ERs, etc.) that come from a different architecture can now be imported. An automatic scope-mapping is done using the scope name (first match). Smart mapping is only performed if the direct import (which is based on the full scope path) is not possible. | 2.4 | X | X
2.1.0 | - Adaptions for EP 2.4 | 2.4 | X | X 
2.0.11 | - Added the possibility to select requirement sources as the report source for test execution reports. | 2.3 |  | 
2.0.10 | - Fixed issue: Architecture Update doesn't work if model path changes (relative and absolute) | 2.3 |  | 
2.0.9 | - Added CalibrationHandling as a parameter for the TargetLin profile creation<br>- Added Export of Tolerances and Input Restrictions to support programmatic modification & re-import | 2.3 |  | 
2.0.8 | - Fixed a bug that prevented combined PLL strings of default and contributed coverage goals (e.g. Statements and Domain Coverage Goals together in one PLL String).<br>- Fixed the CSV vector import for test cases and stimuli vectors<br>- Fixed an issue with backslashes in absolute paths which point to a location inside the workspace<br>- For Domain Coverage and Range Violation goals users can now set a scopePath of "*" to consider all scopes. Not settings a scope path will still default to the toplevel scope.<br>- Added the parameter "useCase" for the Code Analysis Report Step (RBT / B2B)<br>- Removed obsolete parameter "inputRestrictions" from the Vector Generation step. Input Restrictions can be defined through their own step.<br>- Users can now select the use case for the codeAnalysisReport step (RBT / B2B)<br>- The codeAnalysisReport now exports a csv file ("BTCCoverageOverview_B2B.csv" / "BTCCoverageOverview_RBT.csv") to the report directory which contains overall coverage percentage (Statement, Decision and MCDC). This CSV file can be used by other Jenkins plugins to display the coverage. | 2.3 |  | 
2.0.7 | - Fixed missing parameters (reuseExistingCode, pilConfig, pilTimeout)<br>- Added parameters for environmentXmlPath (TL Profile Creation), testMode (grey box / black box) and startupScriptPath | 2.3 |  | 
2.0.3 | - Adapted to EP 2.3<br>- A Failed Profile Creation / Profile load will now always throw an exception to break the build<br>- In case of failures during profile creation profile messages will be exported and made available in Jenkins (if possible)<br>- Fixed a bug that prevented the use of some settings for the wrapUp step.<br>- Fixed a bug that caused a specified PLL to be ignored.<br>- Jenkins: HPI plugin ("btc-embeddedplatform-plugin") is now available in the official Jenkins plugin repository | 2.3 |  | 
2.0.1 | - The Vector Generation step now supports dummy toplevels. If the toplevel subsystem is a dummy scope (no C-function available) then the vector generation will be done on the direct children of the toplevel.<br>- Domain Coverage and Range Violation goals can now be added to the profile and considered during vector generation (requires additional plugins)<br>- Fixed a bug that caused execution records to not be available for debugging in the migration suite use case.<br>- archiveArtifacts and stash commands used by the btc-embeddedplatform plugin are now only called if needed and were changed to be more specific<br>- Fixed an issue that could cause existing profiles to be loaded in the migration suite scenario. From now on the migrationSuite will always create a new profile.<br>- Profile Creation can now be invoked explicitly.<br>- The Code Analysis Report can now be created explicitly. It was formerly created by the Vector Generation step. That's still possible but not enabled by default (controlled by property "createReport" in the btc.vectorGeneration step). | 2.2p2 |  | 

# Prerequisites

This plugin only works in combination with BTC EmbeddedPlatform which
needs to be installed and licensed separately.

![](https://wiki.jenkins.io/download/attachments/173703174/Jenkins-EP.png?version=1&modificationDate=1558695678000&api=v2)

# Jenkins Pipeline

## Overview

Integrating test runs with BTC EmbeddedPlatform in your Jenkins
workflows combines the automation and traceability concepts and results
in great benefits:

1.  The automated workflows scale for multiple components / projects
    with low configuration effort
2.  You are easily able to trace changes made to your system under test
    from the Source Code Management to the integrated product and
    recognize test failures early in the process
3.  The pipeline visualization intuitively shows how much time each
    phase of the testing process takes  
    ![](https://wiki.jenkins.io/download/attachments/173703174/StageView_Tracability.png?version=1&modificationDate=1558695687000&api=v2)
4.  The Jenkins Automation Plugin produces an XML report in the JUnit
    format that can be analyzed by Jenkins to provide test status trends
    over multiple executions and projects  
    ![](https://wiki.jenkins.io/download/attachments/173703174/JUnit-Test-Result-Trend.png?version=1&modificationDate=1558695680000&api=v2)
5.  Comprehensive HTML Reports from BTC EmbeddedPlatform are available
    directly from the Jenkins job page  
      

    Jenkins' Content Security Policy can prevent the reports from being
    displayed properly. See [Configuring Content Security
    Policy](https://wiki.jenkins.io/display/JENKINS/Configuring+Content+Security+Policy)
    for further details.

6.  Relevant artifacts like the test profile are accessible for easy
    debugging and analysis

    ![](https://wiki.jenkins.io/download/thumbnails/173703174/save-profile.png?version=1&modificationDate=1558695685000&api=v2)

## Licensing for Jenkins Integration

In addition to the basic license requirements that depend on the chosen
workflow steps which require EmbeddedTester or EmbeddedValidator the
Jenkins Automation use case requires the "Test Automation Server"
floating network license (ET\_AUTOMATION\_SERVER).

Since v2.4.0 it's possible to run ET\_BASE use cases (Architecture
Import, Test Case Import, Test Execution, Reporting) with an
EmbeddedTester BASE installation and the license
ET\_AUTOMATION\_SERVER\_BASE.

## Configuration

In a Jenkins Pipeline the configuration of a job can be defined as
simple groovy code which can be versioned alongside the main source
files of the component. A full documentation of the Jenkins Pipeline can
be found **[here](https://jenkins.io/doc/book/pipeline/)**. The
following example shows of how BTC EmbeddedPlatform can be automated
from Jenkins via the BTC DSL for Pipeline Plugin. The Plugin needs to be
installed in Jenkins and dedicated BTC methods to create a test
automation workflow.

**Pipeline Example**  Expand source

``` syntaxhighlighter-pre
node {
    // checkout changes from SCM
    checkout scm
 
    // start EmbeddedPlatform and connect to it
    btc.startup {}
 
    // load / create / update a profile
    btc.profileCreateTL {
        profilePath = "profile.epp"
        tlModelPath = "powerwindow_tl_v01.slx"
        tlScriptPath = "start.m"
        matlabVersion = "2017b"
    }
 
    // generate stimuli vectors
    btc.vectorGeneration {
        pll = "STM, D, MCDC"
        createReport = true
    }
 
    // execute back-to-back test MIL vs. SIL
    btc.backToBack {
        reference = "TL MIL"
        comparison = "SIL"
    }
 
    // close EmbeddedPlatform and store reports
    btc.wrapUp {}
}
```

# Workflow Steps

### Step “startup”

DSL Command: btc.startup {...}

**Description**

Method to connect to BTC EmbeddedPlatform with a specified port. If BTC
EmbeddedPlatform is not available it is started and the method waits
until it is available. The following optional settings are available:

Property | Description | Example Value(s)
---------|-------------|-----------------
port | Port used to connect to EmbeddedPlatform.<br>(default: 29267) | 1234, 29268, 8073
timeout | Timeout in seconds before the attempt to connect to EmbeddedPlatform is cancelled. This timeout should consider the worst case CPU & IO performance which influences the tool startup.<br>(default: 120) | 40, 60, 120
licensingPackage | Name of the licensing package to use, e.g. to use a EmbeddedTester BASE.<br>(default: ET_COMPLETE) | ET_BASE

**Possible Return values**

| **Return Value** | **Description**                                                                              |
| 200              | Started a new instance of BTC EmbeddedPlatform and successfully connected to it.             |
| 201              | Successfully connected to an already running instance of BTC EmbeddedPlatform.               |
| 400              | Timeout while connecting to BTC EmbeddedPlatform (either manually specified or 120 seconds). |
| 500              | Unexpected Error                                                                             |

Jenkins will always connect to the active version of EmbeddedPlatform
since many tasks will only work with the version that is integrated into
Matlab. Please ensure that the correct EP version is active by
choosing Activate BTC EmbeddedPlatform in your start menu for the
desired version and also ensure that the Jenkins Automation Plugin is
installed for this version of EmbeddedPlatform.

### Step “profileLoad”

DSL Command: btc.profileLoad {...}

**Description**

Opens the profile if the specified profile exists, otherwise creates a
new profile. A profile update is only performed if this is required.
Profile Creation requires either a TargetLink model or C-Code in
combination with a CodeModel.xml architecture description.

The “profileLoad” step or any of the "profileCreate" steps are a
mandatory starting point for all automation workflows.

[TABLE]

**Possible Return values**

|                  |                                                                                                                   |
|------------------|-------------------------------------------------------------------------------------------------------------------|
| **Return Value** | **Description**                                                                                                   |
| 200              | Successfully loaded an existing profile.                                                                          |
| 201              | Successfully loaded an existing profile and performed an architecture update (see updateRequired property above). |
| 202              | Successfully created a new profile.                                                                               |
| 400              | Error during profile creation. Throws an exception because further testing is not possible.                       |
| 500              | Unexpected Error. Throws an exception because further testing is not possible.                                    |

### Step “profileCreateTL”

DSL Command: btc.profileCreateTL {...}

**Description**

Creates a new profile for a TargetLink model.

The listed properties only show the TargetLink specific properties. Each
of the properties listed in the "profileLoad" step also apply here.

[TABLE]

### Step “profileCreateSL”

DSL Command: btc.profileCreateSL {...}

**Description**

Creates a new profile for a Simulink model.

The listed properties only show the Simulink specific properties. Each
of the properties listed in the "profileLoad" step also apply here.

[TABLE]

### Step “profileCreateC”

DSL Command: btc.profileCreateC {...}

**Description**

Creates a new profile for supported ansi C-Code.

The listed properties only show the C-Code specific properties. Each of
the properties listed in the "profileLoad" step also apply here.

[TABLE]

### Step “vectorImport”

DSL Command: btc.vectorImport {...}

**Description**

Imports test cases or stimuli vectors from the specified location. The
following settings are available:

[TABLE]

**Possible Return values**

|                  |                                               |
|------------------|-----------------------------------------------|
| **Return Value** | **Description**                               |
| 200              | Successfully imported all vectors.            |
| 300              | No valid vectors were found in the importDir. |
| 400              | Error during vector import.                   |
| 500              | Unexpected Error                              |

### Step “toleranceImport”

DSL Command: btc.toleranceImport {...}

**Description**

Imports tolerance settings from the specified file. The following
options are available:

**Possible Return values**

[TABLE]

**Possible Return values**

|                  |                                               |
|------------------|-----------------------------------------------|
| **Return Value** | **Description**                               |
| 200              | Successfully imported the tolerance settings. |
| 400              | No path specified.                            |
| 401              | The file at specified path does not exist.    |
| 402              | The specified useCase is invalid.             |
| 500              | Unexpected Error                              |

### Step “toleranceExport”

DSL Command: btc.toleranceExport {...}

**Description**

Exports tolerance settings to the specified file. The following options
are available:

**Possible Return values**

[TABLE]

**Possible Return values**

|                  |                                               |
|------------------|-----------------------------------------------|
| **Return Value** | **Description**                               |
| 200              | Successfully exported the tolerance settings. |
| 400              | No path specified.                            |
| 402              | The specified useCase is invalid.             |
| 500              | Unexpected Error                              |

### Step “inputRestrictionsImport”

DSL Command: btc.inputRestrictionsImport {...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Imports Input Restrictions from the specified file. The following
options are available:

**Possible Return values**

[TABLE]

**Possible Return values**

|                  |                                               |
|------------------|-----------------------------------------------|
| **Return Value** | **Description**                               |
| 200              | Successfully imported the tolerance settings. |
| 400              | No path specified.                            |
| 401              | The file at specified path does not exist.    |
| 500              | Unexpected Error                              |

### Step “executionRecordExport”

DSL Command: btc.executionRecordExport {...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Exports Execution Records to the specified directory. The following
options are available:

**Possible Return values**

[TABLE]

You can define whitelists and blacklists for scopes, folders and test
cases. Everything will be merged resulting in a filtered set of test
cases. Blacklists always have precedence over whitelists (i.e. if
something is whitelisted and blacklisted it will be excluded).

  

**Possible Return values**

|                  |                                              |
|------------------|----------------------------------------------|
| **Return Value** | **Description**                              |
| 200              | Successfully exported the execution records. |
| 500              | Unexpected Error                             |

### Step “inputRestrictionsExport”

DSL Command: btc.inputRestrictionsExport {...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Exports Input Restrictions to the specified file. The following options
are available:

**Possible Return values**

[TABLE]

**Possible Return values**

|                  |                                               |
|------------------|-----------------------------------------------|
| **Return Value** | **Description**                               |
| 200              | Successfully exported the tolerance settings. |
| 400              | No path specified.                            |
| 500              | Unexpected Error                              |

### Step “rbtExecution”

DSL Command: btc.rbtExecution {...}

**Required License**

EmbeddedTester (ET\_BASE)

**Description**

Executes all functional test cases in the profile. A Test Execution
Report will be exported to the “exportDir” specified in the
“profileLoad” step. The following optional settings are available:

[TABLE]

Filtering via White- & Blacklists

You can define whitelists and blacklists for scopes, folders and test
cases. Everything will be merged resulting in a filtered set of test
cases. Blacklists always have precedence over whitelists (i.e. if
something is whitelisted and blacklisted it will be excluded).

  

**Possible Return values**

|                  |                                                               |
|------------------|---------------------------------------------------------------|
| **Return Value** | **Description**                                               |
| 200              | All test cases passed (status: PASSED)                        |
| 201              | Nothing to Execute (no functional test cases in the profile). |
| 300              | There were failed test cases (status: FAILED)                 |
| 400              | There were errors during test case execution (status: ERROR)  |
| 500              | Unexpected Error                                              |

### Step “testExecutionReport”

DSL Command: btc.testExecutionReport{...}

**Required License**

EmbeddedTester (ET\_BASE)

**Description**

Creates the Test Execution Report and exports it to the "exportDir"
specified in the "profileLoad" / "profileCreate" step. If no reportName
is specified the reports will be placed into a subdirectory in order to
avoid multiple reports overwriting each other.

[TABLE]

  

**Possible Return values**

|                  |                  |
|------------------|------------------|
| **Return Value** | **Description**  |
| 200              | Success          |
| 500              | Unexpected Error |

### Step “xmlReport”

DSL Command: btc.xmlReport{...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Creates the XML Report and exports it to the "exportDir" specified in
the "profileLoad" / "profileCreate" step. Requires BTC Plugin for
XMLReports. The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                  |
|------------------|------------------|
| **Return Value** | **Description**  |
| 200              | Success          |
| 500              | Unexpected Error |

### Step “codeAnalysisReport”

DSL Command: btc.codeAnalysisReport{...}

**Required License**

EmbeddedTester (ET\_COMPLETE) for B2B use case.

**Description**

Creates the Code Analysis Report and exports it to the "exportDir"
specified in the "profileLoad" / "profileCreate" step. The following
optional settings are available:

[TABLE]

**Possible Return values**

|                  |                  |
|------------------|------------------|
| **Return Value** | **Description**  |
| 200              | Success          |
| 500              | Unexpected Error |

In addition, this step creates a CSV file
"BTCCoverageOverview\_*USECASE*.csv" (with USECASE being B2B or RBT)
which can be used by other Jenkins Plugins like the [Plot
Plugin](https://plugins.jenkins.io/plot) to report coverage.

**Example content of the CSV File:**

``` syntaxhighlighter-pre
Statement Coverage, Decision Coverage, MC/DC Coverage
100.0, 90.0, 91.98
```

  

**Example of plots created by the [Plot
Plugin](https://plugins.jenkins.io/plot):**

![](https://wiki.jenkins.io/download/attachments/173703174/plots.png?version=1&modificationDate=1558695682000&api=v2)

``` syntaxhighlighter-pre
plot csvFileName: 'plot-b2b-codecoverage.csv', csvSeries: [[displayTableFlag: false, exclusionValues: '', file: "reports/BTCCoverageOverview_B2B.csv", inclusionFlag: 'OFF', url: '']], group: 'BTC Code Coverage Overview', style: 'line', title: 'B2B Code Coverage (Structural)', yaxis: 'Coverage Percentage'
```

### Step “modelCoverageReport”

DSL Command: btc.modelCoverageReport{...}

**Required License**

EmbeddedTester (ET\_COMPLETE) for B2B use case

Simulink Coverage (formerly V&V)

**Description**

Creates the Model Coverage Report and exports it to the "exportDir"
specified in the "profileLoad" / "profileCreate" step. The following
optional settings are available:

[TABLE]

**Possible Return values**

|                  |                  |
|------------------|------------------|
| **Return Value** | **Description**  |
| 200              | Success          |
| 500              | Unexpected Error |

  

### Step “formalTest”

DSL Command: btc.formalTest{...}

**Required License**

EmbeddedTester (ET\_BASE) + Formal Test Add-On

**Description**

Executes a Formal Test based on all formal requirements in the profile.
A Formal Test Report will be exported to the “exportDir” specified in
the “profileLoad” step (and will be linked in the overview report). The
following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                                              |
|------------------|--------------------------------------------------------------|
| **Return Value** | **Description**                                              |
| 200              | All test cases passed (status: PASSED / FULLFILLED)          |
| 201              | Nothing to Execute (no formal requirements in the profile).  |
| 300              | There were violations (status: FAILED / VIOLATED)            |
| 400              | There were errors during test case execution (status: ERROR) |
| 500              | Unexpected Error                                             |

  

### Step “rangeViolationGoals”

DSL Command: btc.rangeViolationGoals{...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Required Plugin**

Plugin RangeViolationGoals

**Description**

Adds Range Violation Goals to the profile which contribute to the Code
Analysis Report and can be considered during vector generation (pll:
"RVG"). The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                            |
|------------------|--------------------------------------------|
| **Return Value** | **Description**                            |
| 200              | Success                                    |
| 400              | Range Violation Goals plugin not installed |
| 500              | Unexpected Error                           |

### Step “domainCoverageGoals”

DSL Command: btc.domainCoverageGoals{...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Required Plugin**

Plugin DomainCoverageGoals

**Description**

Adds Domain Coverage Goals to the profile which contribute to the Code
Analysis Report and can be considered during vector generation (pll:
"DCG"). The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                            |
|------------------|--------------------------------------------|
| **Return Value** | **Description**                            |
| 200              | Success                                    |
| 400              | Domain Coverage Goals plugin not installed |
| 500              | Unexpected Error                           |

### Step “vectorGeneration”

DSL Command: btc.vectorGeneration{...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Executes the engines for analysis and stimuli vector generation for
structural coverage. The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------|
| **Return Value** | **Description**                                                                                                              |
| 200              | Successfully generated vectors and reached all selected coverage goals (see PLL property). No robustness goals were covered. |
| 300              | Ran into timeouts before completely analyzing all selected goals (see PLL property). No robustness goals were covered.       |
| 41x              | Covered Robustness Goal: Downcast                                                                                            |
| 4x1              | Covered Robustness Goal: Division by Zero                                                                                    |
| 500              | Unexpected Error                                                                                                             |

### Step “backToBack”

DSL Command: btc.backToBack {...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Executes a Back-to-Back Test between the specified reference and
comparison configuration (e.g. TL MIL vs. SIL). This step requires
stimuli vectors or functional test cases in the profile. A Back-to-Back
Test Report will be exported to the “exportDir” specified in the
“profileLoad” step.

In automated scenarios the effort for manual reviews of frequently
executed Back-to-Back tests can become quite high. The BTC plugin
"ApplyFailedAccepted" deals with this challenge by applying your
manually accepted deviations to all future Back-to-Back Tests as long as
the deviating values are equal. For more information, please contact
<support@btc-es.de>.

  

The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                                                                          |
|------------------|------------------------------------------------------------------------------------------|
| **Return Value** | **Description**                                                                          |
| 200              | Back-to-Back Test passed (status: PASSED)                                                |
| 201              | Back-to-Back Test has accepted failures (status: FAILED ACCEPTED)                        |
| 300              | There were deviations between the reference and comparison architecture (status: FAILED) |
| 400              | There were errors during the execution (status: ERROR)                                   |
| 500              | Unexpected Error                                                                         |

### Step “regressionTest”

DSL Command: btc.regressionTest {...}

**Required License**

EmbeddedTester (ET\_COMPLETE)

**Description**

Executes a Regression Test between the current SUT and old Execution
Records that have been saved. If no saved Execution Records are
available, the vectors will only be executed on the current SUT and the
Execution Records will be stored for a later Regression Test. This
requires stimuli vectors or functional test cases in the profile.  A
Regression Test Report will be exported to the “exportDir” specified in
the “profileLoad” step. The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                                                            |
|------------------|----------------------------------------------------------------------------|
| **Return Value** | **Description**                                                            |
| 200              | Regression Test passed (status: PASSED)                                    |
| 201              | Nothing to compare. Simulation results stored for later Regression Tests.  |
| 300              | There were deviations between the old and the new version (status: FAILED) |
| 400              | There were errors during the execution (status: ERROR)                     |
| 500              | Unexpected Error                                                           |

### Step “formalVerification”

DSL Command: btc.formalVerification {...}

**Required License**

EmbeddedValidator (EV)

**Description**

Executes all existing proofs in the profile and generates a Formal
Verification Report. The following optional settings are available:

[TABLE]

**Possible Return values**

|                  |                                                |
|------------------|------------------------------------------------|
| **Return Value** | **Description**                                |
| 200              | All proofs are fulfilled (status: FULFILLED)   |
| 300              | There was a violation (status: VIOLATED)       |
| 301              | Unknown (status: UNKNOWN)                      |
| 400              | BTC EmbeddedValidator package is not installed |
| 500              | Unexpected Error                               |

### Step “wrapUp”

DSL Command: btc.wrapUp {...}

**Description**

Publishes HTML reports and the JUnit XML report to Jenkins and closes
BTC EmbeddedPlatform. The following optional settings are available:

[TABLE]

  

# BTC Migration Suite

The BTC Migration Suite allows you to perform a fully automatic
regression test between different Matlab or TargetLink versions. This
makes it easy to document that the change of a tool version in a
particular project does not influence the behavior of software
components on model and code level.

**Required License**

EmbeddedTester (ET\_COMPLETE)

### Step “migrationSource”

DSL Command: btc.migrationSource {...}

**Description**

Creates a profile on the source configuration (e.g. old Matlab /
TargetLink version), generates vectors for full coverage and exports the
simulation results.

### Step “migrationTarget”

DSL Command: btc.migrationTarget {...}

**Description**

Creates a profile on the target configuration (e.g. newMatlab /
TargetLink version), imports the simulation results from the source
config and runs a regression test.

  

For both steps (migrationSource and migrationTarget) the following
parameters are mandatory:

[TABLE]

In Addition, you can add all other the parameters from the
steps btc.profileLoad and btc.vectorGeneration if required.

### Migration Suite Example: Jenkinsfile

The following example shows a Jenkinsfile for a complete migration of a
TargetLink model. The labels that are specified for the node describe
the resource requirements for each configuration and allow Jenkins to
provide a suitable agent. Any data produced by the migrationSource step
which is needed by the migrationTarget step will be automatically
handled by Jenkins. This way, the agent for the target config (which is
obviously a different one machine due to the different Windows versions)
will have access to the simulation results from the source config
required for the regression test.

**Migration Suite Example**

**Migration Suite Example**  Expand source

``` syntaxhighlighter-pre
node ('Win7 && TL41 && ML2015b') {

    checkout scm
 
    stage ("Migration Source") {
        btc.migrationSource {
            matlabVersion = "2015b"
            tlModelPath = "source/model.mdl"
            tlScriptPath = "start.m"
        }
    }
}
 
node ('Win10 && TL43 && ML2017b') {

    checkout scm
 
    stage ("Migration Target") {
        btc.migrationTarget {
            matlabVersion = "2017b"
            tlModelPath = "target/model.mdl"
            tlScriptPath = "start.m"
        }
    }
}
```

# Adding the BTC Plugin to Jenkins

In order to use the convenient pipeline syntax described above you need
to add the BTC Plugin to Jenkins. This is very easy and can be done with
the following steps:

On your Jenkins web UI go to Jenkins \> Manage Jenkins \> Manage Plugins

Click on the Available tab and search for btc-embeddedplatform

Select the plugin btc-embeddedplatform and install it

1.  Once the plugin is installed new versions which are available will
    appear in the Updates section
2.  Updating a plugin usually requires you to restart your Jenkins
    master

The BTC Pipeline plugin is now available in Jenkins and you can benefit
from the convenient BTC pipeline methods described in the sections
above. Enjoy!

If your Jenkins master can't access the internet you can manually
download the plugin
[here](https://updates.jenkins-ci.org/latest/btc-embeddedplatform.hpi)
and upload it to the server via the advanced section of the "Manage
Plugins" page.

  

  
