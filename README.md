# 4D Dropdown Examples

A comprehensive collection of **4D form examples** demonstrating best practices for implementing dropdown lists in 4D projects.

This repository is part of the [Agent Skills](https://agentskills.io/home) ecosystem for 4D development.

---

## 📋 Contents

### DropdownExamples Form

An interactive 4D form that showcases **three distinct approaches** to implementing dropdown lists:

#### 1. **Object-based Dropdown** (Recommended ⭐)
The modern, recommended approach using 4D objects. The data source is a collection bound via an object with `values`, `index`, and `currentValue` properties.

```4d
Form.dropObject := New object
Form.dropObject.values := New collection("Apple"; "Banana"; "Cherry"; "Orange"; "Strawberry")
Form.dropObject.index := -1  // -1 = no selection
Form.dropObject.currentValue := "Please select an option…"
```

**To get the selection:**
```4d
If (Form.dropObject.index = -1)
    // No selection
Else
    $selected := Form.dropObject.currentValue
End if
```

#### 2. **Array-based Dropdown** (Traditional)
Uses classic 4D arrays with 1-based indexing. Element 0 holds the placeholder text.

```4d
ARRAY TEXT(asColor; 5)
asColor{1} := "Red"
asColor{2} := "Green"
asColor{3} := "Blue"
asColor{4} := "Yellow"
asColor{5} := "Purple"
asColor{0} := "Please select a color…"
asColor := 0  // No selection initially
```

**To get the selection:**
```4d
If (asColor = 0)
    // No selection
Else
    $selected := asColor{asColor}  // Idiom: asColor{asColor} = current value
End if
```

#### 3. **Choice List Dropdown** (Simple)
The simplest approach for static lists. The data source is a plain variable holding the selected value directly.

```4d
Form.dropChoice := "Please select a color…"
```

**JSON form definition:**
```json
{
  "type": "dropdown",
  "dataSource": "Form.dropChoice",
  "choiceList": ["Red", "Green", "Blue", "Yellow", "Purple"],
  "saveAs": "value"
}
```

**To get the selection:**
```4d
If (Form.dropChoice = "Please select a color…")
    // No selection
Else
    $selected := Form.dropChoice
End if
```

---

## 🎯 Key Features

- ✅ **Five items per dropdown** - Each dropdown list contains 5 sample items
- ✅ **Default placeholder text** - All dropdowns initialize with "Please select an option…"
- ✅ **Real-time feedback** - Selection results display immediately below each dropdown
- ✅ **Reset functionality** - Demonstrates how to reset all three dropdown types
- ✅ **Complete working code** - Ready-to-use form methods and object methods
- ✅ **Full documentation** - Comprehensive guide with code examples and best practices

---

## 📁 Project Structure

```
4d-skills-test-claude/
├── 4d-skills/
│   └── Project/
│       └── Sources/
│           └── Forms/
│               └── DropdownExamples/
│                   ├── form.4DForm              # Form definition in JSON
│                   ├── method.4dm               # Form On Load/On Unload
│                   ├── DROPDOWN_GUIDE.md        # Detailed guide & examples
│                   └── ObjectMethods/
│                       ├── dropObject.4dm       # Object-based dropdown handler
│                       ├── dropArray.4dm        # Array-based dropdown handler
│                       ├── dropChoice.4dm       # Choice list dropdown handler
│                       └── resetButton.4dm      # Reset button handler
├── README.md                                    # This file
├── LICENSE                                      # MIT License
└── VERSION                                      # Version info
```

---

## 🚀 Getting Started

### Prerequisites
- 4D v20 or later (for JSON form support)
- Agent Skills framework installed

### Using the Form

1. **Copy the form directory** from `4d-skills/Project/Sources/Forms/DropdownExamples/` into your 4D project
2. **Reference the form** in your application:
   ```4d
   OPEN FORM WINDOW("DropdownExamples")
   ```

### Examining the Code

1. **form.4DForm** - The form definition structure
   - 2-page form (page 0 invisible, page 1 visible)
   - 3 dropdown objects, 3 result labels, 1 reset button
   - Title and help text

2. **method.4dm** - Form lifecycle
   - `On Load`: Initializes all three dropdowns with placeholder text
   - `On Unload`: Cleans up array-based dropdown

3. **ObjectMethods/** - Individual handlers
   - `dropObject.4dm`: Handles object-based dropdown changes
   - `dropArray.4dm`: Handles array-based dropdown changes
   - `dropChoice.4dm`: Handles choice-list dropdown changes
   - `resetButton.4dm`: Resets all dropdowns to initial state

---

## 📚 Documentation References

### Official 4D Documentation
- [Dropdown List Object Overview](https://developer.4d.com/docs/FormObjects/dropdownListOverview)
- [Data Source Properties](https://developer.4d.com/docs/FormObjects/propertiesDataSource)
- [Collections in Forms](https://developer.4d.com/docs/Concepts/Collections)
- [4D Arrays](https://developer.4d.com/docs/Concepts/arrays)

### 4D Blog Articles
- [Use Collections and Lists Within Forms Objects](https://blog.4d.com/use-collections-and-lists-within-forms-objects/)
- [Modern Form Design Patterns](https://blog.4d.com/)

### Additional Resources
- See `DROPDOWN_GUIDE.md` in the DropdownExamples folder for detailed code examples
- 4D Form JSON Schema: `schemas/4dform/formsSchema.json`

---

## 💡 Best Practices

### For New Development
1. **Use object-based dropdowns** - Modern, flexible, and recommended
2. **Always provide a placeholder** - Set a default "Please select…" message
3. **Check for "no selection"** before reading values:
   - Object-based: `If (Form.drop.index = -1)`
   - Array-based: `If (array = 0)`
   - Choice-list: `If (Form.drop = "Please select…")`
4. **React to `onDataChange`** - Use this event to handle selections
5. **Avoid array-based in new code** - Still functional but deprecated

### Handling User Selections

```4d
// Object-based pattern
If (Form.dropObject.index # -1)
    $selectedFruit := Form.dropObject.currentValue
    // Process selection
End if

// Array-based pattern
If (asColor # 0)
    $selectedColor := asColor{asColor}
    // Process selection
End if

// Choice-list pattern
If (Form.dropChoice # "Please select a color…")
    $selectedColor := Form.dropChoice
    // Process selection
End if
```

---

## 🔧 Customizing the Examples

### Add More Items
**Object-based:**
```4d
Form.dropObject.values.push("Mango")
Form.dropObject.values.push("Peach")
```

**Array-based:**
```4d
APPEND TO ARRAY(asColor; "Orange")
APPEND TO ARRAY(asColor; "Pink")
```

**Choice-list:**
Update the `choiceList` property in the form JSON:
```json
"choiceList": ["Red", "Green", "Blue", "Yellow", "Purple", "Orange", "Pink"]
```

### Change the Placeholder Text
Modify the initialization in `method.4dm`:
```4d
Form.dropObject.currentValue := "Select a fruit…"
asColor{0} := "Select a color…"
Form.dropChoice := "Select a color…"
```

### Add Styling
Modify the form definition to add:
- Custom fonts and colors
- Button styles
- Styling classes
- Positioning and sizing

---

## 📄 File Descriptions

| File | Purpose |
|------|---------|
| `form.4DForm` | JSON form definition with all UI objects |
| `method.4dm` | Form lifecycle (On Load, On Unload) |
| `DROPDOWN_GUIDE.md` | Detailed guide with all code examples |
| `dropObject.4dm` | Handler for object-based dropdown |
| `dropArray.4dm` | Handler for array-based dropdown |
| `dropChoice.4dm` | Handler for choice-list dropdown |
| `resetButton.4dm` | Handler for reset button |

---

## 🎓 Learning Path

1. **Start here:** Read this README for overview
2. **Then examine:** `DROPDOWN_GUIDE.md` for detailed explanations
3. **Explore:** Open `form.4DForm` to see the JSON structure
4. **Study:** Review each `.4dm` method file to understand event handling
5. **Experiment:** Customize the form and methods for your use case
6. **Reference:** Use this as a template for your own dropdown implementations

---

## 🔗 Related Skills

This example is part of the 4D skills ecosystem:
- **4dform** - Form design and validation
- **4dlang** - 4D language and commands
- **4dlsp** - Language server protocol support
- **4dproject** - Project structure and configuration

---

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🤝 Contributing

These examples are provided as part of the Agent Skills framework. Improvements and additional examples are welcome.

---

## 📞 Support

For questions about:
- **4D Dropdown Lists** - Refer to [official 4D documentation](https://developer.4d.com/docs/FormObjects/dropdownListOverview)
- **Agent Skills Framework** - Visit [agentskills.io](https://agentskills.io/home)
- **4D Development** - Check [4D Blog](https://blog.4d.com/) and [Community](https://community.4d.com/)

---

**Last updated:** September 2026  
**Tested with:** 4D v20 LTS and later
