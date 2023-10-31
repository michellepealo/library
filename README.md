# CodeVA Curriculum Library

This repository is the CodeVA Curriculum Library, containing metadata about all of CodeVA's curricular artifacts accessible via [https://curriculum.codevirginia.org](https://curriculum.codevirginia.org). This page contains information about the structure of the repository and information about contributing to the library.

## Library Structure

## Contributing to the Library

If the auditor script finds errors in the library, it will throw an error:

```
Error: Found problems in the library. See errors.log for details
```

The auditor will create a file (`errors.log`) with information about the problems that must be corrected in order to upload the new library version to the Curriculum Library website.

### Markdown Details

The library supports several "directives", special Markdown elements that allow contributors to add additional detail or important styled features to Element pages.

#### `::nsf`

The `::nsf` directive allows contributors to insert the NSF disclaimer boilerplate language into the body of the Element along with the NSF logo as required by the terms of NSF grants. The `::nsf` directive has one required attribute, `number`, which should be set to the grant number associated with the Element. For example:

```
## Overview

The *Twine Trail Guide* is a website with resources, tutorials, and projects for novice programmers to use as they develop coding skills in Twine.

::nsf{number=123456}
```

If the directive does not define a number, the auditor script will throw an error:

```
Error: File {filename} uses the ::nsf directive, but does not define a number!
```

### Field Details

Below, you'll find special-case information for each of the Element frontmatter fields.

### `title`

| Name | Type | Description | Required? | Inheritable? | Example |
| ---- | ---- | ----------- | --------- | ----------- | ------- |
| `title` | string | The name of the resource to be displayed prominently in its `ElementView` and `ElementCard` | ✅ | ❌ | `title: Data Science Project-Based Learning` |

**Notation:** If the title needs to include a `:`, enclose the title in single or double-quotes to avoid a parsing error: `title: "CS for CTE: Endorsement, Expertise, Empowerment"`

If an Element fails to define a valid title, the auditor script will throw an error:

```
Error: File {filename} fails to define a valid title!
```

### `authors`

| Name | Type | Description | Required? | Inheritable? | Example |
| ---- | ---- | ----------- | --------- | ----------- | ------- |
| `authors` | comma-separated list | A list of the authors of the Element | ✅ | ✅ (default: CodeVA Curriculum) | `authors: Valerie Fawley, Jess Newsome` |

If an Element fails to define a valid `authors` value, the auditor script will throw an error:

```
Error: File {filename} fails to define a valid authors list!
```

### `standards`

| Name | Type | Description | Required? | Inheritable? | Example |
| ---- | ---- | ----------- | --------- | ------------ | ------- |
| `standards` | comma-separated list | A list of the standards associated with the element | optional | ✅ | `standards: K.CS.AP.1, K.MT, K.CS.IC` |

**Notation:** Use "standard IDs" to reference standards. The ID structure is `[grade].[subject].[strand].[number]`, with each component separated by a `.`. All four of these ID components are required unless you want to reference a range of standards (see below). You can find the list of allowed grade, subject, and strand abbreviations here: https://github.com/CodeVA-Curriculum/index/blob/main/src/routes/api/standards/id_key.yaml. If a specified standard does not exist in the [library standards data](https://github.com/CodeVA-Curriculum/index/tree/main/src/routes/api/standards) (often because it uses an incorrect ID component), the auditor script will throw an error:

```
Error: {filename} references a standard ({standard ID}) that does not exist!
```

**Standard Ranges:** Use dash notation to denote a range of grades. Omit strand or number ID to include all standards in subject or strand. For example, `K-2.CS` selects all CS standards K-2, or `8.CS.AP` selects all grade 8 CS Algorithms & Programming standards