# PostgreSQL

## 1️⃣ What is VARCHAR ?

`VARCHAR`

* Stands for **VAR**iable **CHAR**acter
* Stores **text**
* Uses **only as much space as needed** (unlike `CHAR`)

`(255)`

* **Maximum allowed length**
* You can store **0 to 255 characters**
* Not bytes by default — **characters** (depends on DB & charset)

### VARCHAR vs CHAR (important difference)

| Type          | Behavior                                     |
|---------------|----------------------------------------------|
| `CHAR(10)`    | Always uses 10 characters (pads with spaces) |
| `VARCHAR(10)` | Uses actual length only                      |

### Example:
```postgresql
CHAR(10)    → "Hi        "
VARCHAR(10) → "Hi"
```
---