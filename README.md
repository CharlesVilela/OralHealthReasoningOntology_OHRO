
# README — Oral Health Ontology

## 1. Overview

The **Oral Health Ontology** is an ontology developed to model knowledge related to oral health, with a particular focus on **oral lesions**, **risk factors**, **patients**, **medical images**, and **clinical annotations** used in AI-assisted diagnosis and computer vision tasks.

The ontology enables the representation of:

* Patients and their risk factors
* Intraoral clinical images
* Benign, potentially malignant, and malignant lesions
* Clinical diagnoses
* Region-of-interest annotations (bounding boxes)
* Dataset structures for model training and validation

---

# 2. Glossary of Terms

## Clinical Concepts

### Lesion

Represents any pathological alteration observed in oral tissue.

### Benign Lesion

A non-cancerous lesion with no significant invasive potential.

### OPMD (Oral Potentially Malignant Disorder)

A potentially malignant oral disorder, i.e., lesions with a risk of transformation into oral cancer.

### High Risk Lesion

Lesions with a high probability of malignant transformation or progression.

### Malignant Lesion

A malignant lesion characterized by uncontrolled cell growth.

### Oral Squamous Cell Carcinoma (OSCC)

Squamous cell carcinoma of the oral cavity, the most common type of oral cancer.

### Leukoplakia

A white plaque lesion of the oral mucosa considered an OPMD.

### Erythroplakia

A reddish lesion of the oral mucosa with high malignant transformation potential.

---

## Risk Factors

### Risk Factor

Any condition or habit associated with an increased risk of oral cancer.

### Smoking

Use of tobacco products.

### Alcohol Consumption

Frequent alcohol intake.

### Betel Quid Chewing

The habit of chewing betel quid, associated with oral cancer in certain populations.

### HPV

Human Papillomavirus infection.

---

## Clinical and Dataset Entities

### Patient

Represents an individual undergoing clinical evaluation.

### Medical Image

A clinical image associated with a patient.

### Annotation

An annotation made on an image (manual or automatic).

### Bounding Box

A delimited region marking a lesion within an image.

### Dataset Category

A dataset split category (e.g., training, validation, testing).

---

# 3. Class Hierarchy (Taxonomy)

Below is the main taxonomy of the ontology.

```text
Thing
│
├── Patient
├── MedicalImage
├── Annotation
├── BoundingBox
├── DatasetCategory
│
├── RiskFactor
│   ├── Smoking
│   ├── AlcoholConsumption
│   ├── BetelQuidChewing
│   └── HPV
│
└── Lesion
    ├── BenignLesion
    ├── OPMD
    │   ├── Leukoplakia
    │   └── Erythroplakia
    ├── HighRiskLesion
    └── MalignantLesion
         └── OralSquamousCellCarcinoma
```

---

# 4. Relationships (Object Properties)

**Object Properties** connect instances of classes to one another.

---

## hasRiskFactor

Relates a patient to their risk factors.

**Domain:** Patient
**Range:** RiskFactor

Example:

```text
Patient_001 hasRiskFactor Smoking
```

---

## hasMedicalImage

Relates a patient to their clinical images.

**Domain:** Patient
**Range:** MedicalImage

Example:

```text
Patient_001 hasMedicalImage Image_245
```

---

## belongsToPatient

Relates an image to its corresponding patient.

**Domain:** MedicalImage
**Range:** Patient

Example:

```text
Image_245 belongsToPatient Patient_001
```

---

## hasAnnotation

Relates an image to its annotations.

**Domain:** MedicalImage
**Range:** Annotation

Example:

```text
Image_245 hasAnnotation Annotation_01
```

---

## hasBoundingBox

Relates an annotation to its bounding box.

**Domain:** Annotation
**Range:** BoundingBox

Example:

```text
Annotation_01 hasBoundingBox BB_01
```

---

## indicatesLesion

Relates an annotation to the identified lesion.

**Domain:** Annotation
**Range:** Lesion

Example:

```text
Annotation_01 indicatesLesion Leukoplakia
```

---

## hasCategory

Relates an image to a dataset category.

**Domain:** MedicalImage
**Range:** DatasetCategory

Example:

```text
Image_245 hasCategory Training
```

---

## hasClinicalDiagnosis

Relates an image to the observed clinical diagnosis.

**Domain:** MedicalImage
**Range:** Lesion

Example:

```text
Image_245 hasClinicalDiagnosis OSCC
```

---

# 5. Attributes (Data Properties)

**Data Properties** store literal values (strings, integers, floats, etc.).

---

## Patient

| Property   | Type    | Description                 |
| ---------- | ------- | --------------------------- |
| patientID  | String  | Unique patient identifier   |
| age        | Integer | Age                         |
| gender     | String  | Sex/Gender                  |
| imageCount | Integer | Number of associated images |

---

## MedicalImage

| Property           | Type    | Description           |
| ------------------ | ------- | --------------------- |
| imageID            | String  | Image identifier      |
| imageFileName      | String  | Image filename        |
| hasAnnotationCount | Integer | Number of annotations |

---

## Annotation

| Property     | Type   | Description           |
| ------------ | ------ | --------------------- |
| annotationID | String | Annotation identifier |

---

## BoundingBox

| Property  | Type  | Description          |
| --------- | ----- | -------------------- |
| bb_x      | Float | Initial X coordinate |
| bb_y      | Float | Initial Y coordinate |
| bb_width  | Float | Bounding box width   |
| bb_height | Float | Bounding box height  |

---
