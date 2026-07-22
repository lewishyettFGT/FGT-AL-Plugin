---
applyTo: "**/*.al"
description: "TES naming conventions for AL objects, fields, variables, and procedures"
---

# TES Naming Conventions

Consistent use of the "TES" prefix ensures clear identification of custom objects and avoids conflicts with other extensions.

## Rule 1: New Object Naming

### Intent
All new AL objects must be prefixed with "TES " to clearly identify them as custom objects belonging to this extension.

### Examples

```al
// Good examples
table 50100 "TES Notification Buffer"
page 50101 "TES Notification Prompt"
codeunit 50102 "TES Variance"
report 50103 "TES Custom Notification"
enum 50104 "TES Notification Type"
```

```al
// Bad examples (missing TES prefix)
table 50100 "Notification Buffer"
page 50101 "Notification Prompt"
codeunit 50102 "Variance"
```

## Rule 2: Extension Object Naming

### Intent
Extension objects must include "TES" in their name to identify them as belonging to this extension.

### Examples

```al
// Good examples
tableextension 50100 "TES CDC Document" extends "CDC Document"
pageextension 50101 "TES CDC Setup" extends "CDC Setup"
reportextension 50102 "TES Approval Summary" extends "Approval Summary"
```

```al
// Bad examples (missing TES in name)
tableextension 50100 "CDC Document Ext" extends "CDC Document"
pageextension 50101 "CDC Setup Extension" extends "CDC Setup"
```

## Rule 3: Fields on Table Extensions

### Intent
Fields added to table extensions must be prefixed with "TES" to avoid naming conflicts with other extensions and to clearly identify custom fields. Fields on custom tables (prefixed with "TES ") do not need the "TES" prefix.

### Examples

```al
// Good example - Table extension fields must have TES prefix
tableextension 50100 "TES Purchase Line" extends "Purchase Line"
{
    fields
    {
        field(50100; "TES Variance Amount"; Decimal) { }
        field(50101; "TES Approved"; Boolean) { }
    }
}

// Good example - Custom table fields do NOT need TES prefix
table 50100 "TES Notification Buffer"
{
    fields
    {
        field(1; "Entry No."; Integer) { }
        field(2; "Document No."; Code[20]) { }
        field(3; "Notification Type"; Enum "TES Notification Type") { }
    }
}
```

```al
// Bad example - Table extension field missing TES prefix
tableextension 50100 "TES Purchase Line" extends "Purchase Line"
{
    fields
    {
        field(50100; "Variance Amount"; Decimal) { }
    }
}
```

## Rule 4: Global Variables and Procedures on Extension Objects

### Intent
Global variables and procedures on extension objects must be prefixed with "TES" to avoid naming conflicts with other extensions and the base application. Local variables and local procedures do not require the prefix.

### Examples

```al
// Good example - Extension object with TES-prefixed globals and procedures
pageextension 50100 "TES CDC Setup" extends "CDC Setup"
{
    var
        TESNotificationEnabled: Boolean;
        TESVarianceThreshold: Decimal;

    procedure TESCalculateVariance(DocumentNo: Code[20]): Decimal
    begin
        // Implementation
    end;

    local procedure HandleInternalLogic()
    var
        LocalCounter: Integer;
    begin
        // Local variables and procedures do not need TES prefix
    end;
}
```

```al
// Bad example - Missing TES prefix on global variable and procedure
pageextension 50100 "TES CDC Setup" extends "CDC Setup"
{
    var
        NotificationEnabled: Boolean;

    procedure CalculateVariance(DocumentNo: Code[20]): Decimal
    begin
        // Implementation
    end;
}
```
