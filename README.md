# RECAIoT

**A Model-Driven Framework for Requirements Engineering of Context-Aware IoT Systems**

This repository contains the artefacts accompanying the paper “RECAIoT: A Model-Driven Framework for Requirements Engineering of Context-Aware IoT Systems”, including:

- The source code for the three domain-specific languages (DSLs) and the model transformation that constitute the RECAIoT toolchain.
- The requirements models developed for the University Surveillance System case study.
- The questionnaire used in the expert evaluation.

## Overview

RECAIoT treats context-awareness, dynamic goals, and dependencies among context-awareness (CA) requirements as first-class concerns at the requirements stage. The framework comprises three coordinated DSLs:

| DSL | Purpose |
| --- | --- |
| **UCM4IoT (extended)** | Specifies IoT use cases, including CA requirements, services, and operational modes. |
| **DGM (Dynamic Goal Modelling)** | Models goals whose interpretation depends on observed context evidence. |
| **CARDML4IoT** | Models and analyses temporal, data, and resource dependencies among CA requirements. |

A model transformation automatically derives a CARDML4IoT dependency model from a UCM4IoT model. Dependencies and potential conflicts are therefore obtained from the use case specification rather than entered manually.

## Repository Contents

| File | Description |
| --- | --- |
| [`UCM4IoT.zip`](UCM4IoT.zip) | Eclipse/Xtext projects for the extended UCM4IoT DSL (`.ucmiot` models). |
| [`org.dgm.parent.zip`](org.dgm.parent.zip) | Eclipse/Xtext projects for the Dynamic Goal Modelling DSL (`.dgm` models). |
| [`CARDML4IoT.zip`](CARDML4IoT.zip) | Java implementation of the UCM4IoT → CARDML4IoT model transformation, including input models and generated outputs. |
| [`surveillanceUCM.pdf`](surveillanceUCM.pdf) | UCM4IoT model of the University Surveillance System (USS). |
| [`uss-useCaseDiagram.png`](uss-useCaseDiagram.png) | Use case diagram of the USS. |
| [`SurveillanceDGM.pdf`](SurveillanceDGM.pdf) | Dynamic goal models of the USS. |
| [`Expert Evaluation Questionnaire.pdf`](Expert%20Evaluation%20Questionnaire.pdf) | Questionnaire used in the expert evaluation of the framework. |

## Requirements

| Tool | Purpose |
| --- | --- |
| **Java 21** | Required for the transformation project, which is configured for `JavaSE-21`. |
| **Eclipse IDE for Java and DSL Developers**, or **Eclipse Modeling Tools**, with **Xtext** and **EMF** installed | Required for the UCM4IoT and DGM DSL projects. |


## Using the Artefacts

### 1. UCM4IoT DSL

**Archive:** [`UCM4IoT.zip`](UCM4IoT.zip)

1. Extract the archive.
2. Import the projects into an Eclipse workspace using **File → Import → Existing Projects into Workspace**.
3. Launch a Runtime Eclipse instance using **Run → Run Configurations → Eclipse Application**.
4. In the runtime instance, create or open a file with the `.ucmiot` extension.

The editor provides syntax highlighting, content assist, and validation for use cases, CA requirements, services, and operational modes.


### 2. DGM DSL

**Archive:** [`org.dgm.parent.zip`](org.dgm.parent.zip)

Extract the archive and import the following projects into Eclipse:

- `org.dgm`
- `org.dgm.ide`
- `org.dgm.ui`
- `org.dgm.target`

The grammar is defined in:

```text
org.dgm/src/org/dgm/DynamicGoalModel.xtext
```

If the generated Xtext artefacts need to be rebuilt, run the following file as an **MWE2 Workflow**:

```text
org.dgm/src/org/dgm/GenerateDynamicGoalModel.mwe2
```

A headless build is also available. From the parent project directory, run:

```bash
mvn clean install
```

Launch a Runtime Eclipse instance and open a file with the `.dgm` extension to use the editor.

### 3. UCM4IoT → CARDML4IoT Transformation

**Archive:** [`CARDML4IoT.zip`](CARDML4IoT.zip)

The transformation is a standalone Java project with no Xtext or EMF dependency. It can be run from Eclipse or directly from the command line.

#### Run from the Command Line

```bash
unzip CARDML4IoT.zip
cd CARDML4IoT
javac -d bin src/transformation/*.java
java -cp bin transformation.StandaloneTransformationRunner
```

#### Input Models

The runner processes **every `.ucmiot` file** in the `model/` directory.

The archive includes the UCM4IoT models used in the paper, including:

- `SurveillanceUCM.ucmiot`: the University Surveillance System model.
- `SmartStoreCA.ucmiot`: the smart store model.

#### Generated Outputs

For each input model, the runner writes a CARDML4IoT dependency model and a human-readable transformation report to `output/`:

```text
output/<ModelName>_CARDML4IoT.json
output/<ModelName>_transformation_report.txt
```

The archive includes the generated dependency models reported in the paper. These outputs can be regenerated using the commands above.


## Case Study

The case study concerns a **University Surveillance System (USS)**, a context-aware IoT system in operational use.

| Artefact | Description |
| --- | --- |
| [`surveillanceUCM.pdf`](surveillanceUCM.pdf) | UCM4IoT specification of the system. |
| [`uss-useCaseDiagram.png`](uss-useCaseDiagram.png) | Use case diagram of the system. |
| [`SurveillanceDGM.pdf`](SurveillanceDGM.pdf) | Dynamic goal models developed for the system. |

## Evaluation

The [`Expert Evaluation Questionnaire.pdf`](Expert%20Evaluation%20Questionnaire.pdf) contains the instrument used in the expert evaluation reported in the paper.

The questionnaire covers:

- Evaluator background.
- Completeness of the UCM4IoT model.
- Coverage of the dynamic goal models.
- Clarity of the derived dependencies.
- Perceived usefulness and ease of use.
- Comparison with current practice.
