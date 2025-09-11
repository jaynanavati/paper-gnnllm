===============================================
EXAMPLE INPUT AND OUTPUT FOR GRAPH GENERATION
===============================================

This document provides concrete examples of how different types of graphs 
are generated from PetClinic application code snippets. Each example shows 
the input code and the corresponding JSON output structure.

===============================================
EXAMPLE 1: CONTROL FLOW GRAPH (CFG) GENERATION
===============================================

## Task:
To generate Control Flow Graph (CFG)

## Example Input (PetClinic Code Snippet):
```java
@PostMapping("/owners/new")
public String addOwner(Owner owner) {
    if (owner.isValid()) {
        ownerRepository.save(owner);
        return "redirect:/owners";
    } else {
        return "error";
    }
}
```

## Extracted Output (JSON):
```json
{
  "nodes": ["Start", "ValidateOwner", "SaveOwner", "Redirect", "Error"],
  "edges": [
    ["Start", "ValidateOwner"],
    ["ValidateOwner", "SaveOwner", "true"],
    ["ValidateOwner", "Error", "false"],
    ["SaveOwner", "Redirect"]
  ]
}
```

## Explanation:
The CFG extraction identifies the control flow through the method, creating 
nodes for each decision point and action, with edges representing the possible 
execution paths based on the conditional logic.

===============================================
EXAMPLE 2: CALL GRAPH (CG) GENERATION  
===============================================

## Task:
To generate Call Graph (CG)

## Example Input (PetClinic Code Snippet):
```java
public String findOwner(String lastName) {
    return ownerRepository.findByLastName(lastName);
}
```

## Extracted Output (JSON):
```json
{
  "edges": [
    ["OwnerController.findOwner", "OwnerRepository.findByLastName"]
  ]
}
```

## Explanation:
The call graph extraction identifies method invocations, showing the 
relationship between the calling method and the called method across 
different classes and layers.

===============================================
EXAMPLE 3: CLASS HIERARCHY GRAPH (CHG) GENERATION
===============================================

## Task:
To generate Class Hierarchy Graph (CHG)

## Example Input (PetClinic Code Snippet):
```java
public class Owner extends Person { }

public interface OwnerRepository extends JpaRepository<Owner, Integer> { }
```

## Extracted Output (JSON):
```json
{
  "edges": [
    ["Owner", "Person", "extends"],
    ["OwnerRepository", "JpaRepository", "implements"]
  ]
}
```

## Explanation:
The class hierarchy extraction identifies inheritance and implementation 
relationships, capturing both class extension ("extends") and interface 
implementation ("implements") relationships in the codebase.

===============================================
SUMMARY
===============================================

These examples demonstrate the systematic extraction of structural information 
from source code into standardized JSON representations, enabling automated 
analysis and visualization of software architecture patterns.