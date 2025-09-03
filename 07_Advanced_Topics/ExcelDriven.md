## Apache poi - data driven testing from excel

**maven dependencies**

add the following dependencies to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi</artifactId>
    <version>5.2.3</version>
</dependency>
```

---

**strategy to access excel data**

**1. create object for xssfworkbook class**

```java
FileInputStream file = new FileInputStream("testdata.xlsx");
XSSFWorkbook workbook = new XSSFWorkbook(file);
```

**2. get access to sheet**

```java
XSSFSheet sheet = workbook.getSheet("Sheet1");
```

**3. get access to all rows of the sheet**

```java
int rowCount = sheet.getLastRowNum();
```

**4. access a specific row from all rows**

```java
XSSFRow row = sheet.getRow(0); // first row
```

**5. get access to all cells of a row**

```java
int cellCount = row.getLastCellNum();
for (int i = 0; i < cellCount; i++) {
    String value = row.getCell(i).getStringCellValue();
    System.out.println(value);
}
```

**6. access the data from excel into arrays**

```java
String[][] data = new String[rowCount][cellCount];

for (int i = 1; i <= rowCount; i++) {
    XSSFRow currentRow = sheet.getRow(i);
    for (int j = 0; j < cellCount; j++) {
        data[i - 1][j] = currentRow.getCell(j).getStringCellValue();
    }
}
```

---

**best practices**

* close workbook and input stream to avoid memory leaks:

```java
workbook.close();
file.close();
```

* use try-catch or try-with-resources for exception handling
* keep data files in a separate `/resources` folder
* name sheets and headers clearly for maintainability

---
 
