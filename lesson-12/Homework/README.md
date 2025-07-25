# Power BI Lesson 12 - Text, Informational, and Logical Functions

## Prerequisites
- Connect to SQL Server in Power BI Desktop.
- Import the `DimCustomer` table from the `AdventureWorksDW2019` database.

---

## 🟢 Basic Level (1–10)

1. **Concatenate First and Last Name**
```DAX
FullName = DimCustomer[FirstName] & " " & DimCustomer[LastName]
```

2. **Convert Email Address to Uppercase**
```DAX
Email_Upper = UPPER(DimCustomer[EmailAddress])
```

3. **Extract First 3 Characters from First Name**
```DAX
First3Chars = LEFT(DimCustomer[FirstName], 3)
```

4. **Count Characters in Last Name**
```DAX
LastNameLength = LEN(DimCustomer[LastName])
```

5. **Convert First Name to Lowercase**
```DAX
FirstName_Lower = LOWER(DimCustomer[FirstName])
```

6. **Trim Spaces in EnglishEducation**
```DAX
Education_Trim = TRIM(DimCustomer[EnglishEducation])
```

7. **Repeat '*' Character Equal to Length of First Name**
```DAX
Stars = REPT("*", LEN(DimCustomer[FirstName]))
```

8. **Get Last 4 Characters of Phone Number**
```DAX
Phone_Last4 = RIGHT(DimCustomer[Phone], 4)
```

9. **Format YearlyIncome to Currency with 2 Decimals**
```DAX
Income_Currency = FORMAT(DimCustomer[YearlyIncome], "$#,##0.00")
```

10. **Check If FirstName and LastName Are Exactly the Same**
```DAX
Is_Same = IF(DimCustomer[FirstName] = DimCustomer[LastName], TRUE(), FALSE())
```

---

## 🟡 Intermediate Level (11–20)

11. **Find If 'Manager' Appears in Occupation (Case Sensitive)**
```DAX
Is_Manager = IF(FIND("Manager", DimCustomer[EnglishOccupation],, 0) > 0, TRUE(), FALSE())
```

12. **Search for 'graduate' in EnglishEducation (Case Insensitive)**
```DAX
Is_Graduate = IF(SEARCH("graduate", DimCustomer[EnglishEducation],, 0) > 0, TRUE(), FALSE())
```

13. **Extract Characters 3–7 from First Name**
```DAX
Mid_FirstName = MID(DimCustomer[FirstName], 3, 5)
```

14. **Replace Area Code in Phone Number with 'XXX'**
```DAX
Phone_Replaced = "XXX" & MID(DimCustomer[Phone], 4, LEN(DimCustomer[Phone])-3)
```

15. **Format BirthDate as 'DD-MM-YYYY'**
```DAX
FormattedBirthDate = FORMAT(DimCustomer[BirthDate], "DD-MM-YYYY")
```

16. **Create Initial + Last Name Format (e.g. J.Smith)**
```DAX
Initial_Last = LEFT(DimCustomer[FirstName],1) & "." & DimCustomer[LastName]
```

17. **Capitalize First Letter of FirstName, Lowercase the Rest**
```DAX
Proper_FirstName = UPPER(LEFT(FirstName,1)) & LOWER(MID(FirstName,2,LEN(FirstName)))
```

18. **Substitute Dashes with Spaces in Phone**
```DAX
Phone_Spaces = SUBSTITUTE(DimCustomer[Phone], "-", " ")
```

19. **Convert BirthDate Year to Numeric Using VALUE**
```DAX
BirthYear = VALUE(YEAR(DimCustomer[BirthDate]))
```

20. **Show YearlyIncome Rounded to 1 Decimal Without Commas**
```DAX
Income_Rounded = FORMAT(DimCustomer[YearlyIncome], "0.0")
```

---

## 🔴 Advanced Level (21–30)

21. **Customer Code: First 2 Letters of LastName + Last 2 of CustomerKey**
```DAX
Customer_Code = LEFT(LastName, 2) & RIGHT(CONVERT(CustomerKey, STRING), 2)
```

22. **Validate Email Ends with '.com' and Contains '@'**
```DAX
Is_Valid_Email = IF(RIGHT(EmailAddress, 4) = ".com" && FIND("@", EmailAddress,, 0) > 0, TRUE(), FALSE())
```

23. **Extract Domain Name from EmailAddress**
```DAX
Domain = RIGHT(EmailAddress, LEN(EmailAddress) - FIND("@", EmailAddress))
```

24. **Mask Phone Number Except Last 4 Digits**
```DAX
Phone_Masked = REPT("*", LEN(Phone) - 4) & RIGHT(Phone, 4)
```

25. **Proper Casing of Last Name (simulate manually)**
```DAX
Proper_LastName = UPPER(LEFT(LastName,1)) & LOWER(MID(LastName,2,LEN(LastName)))
```

26. **Replace Multiple Spaces in EnglishOccupation with Single Space**
```Power Query M
Text.Combine(List.Select(Text.Split(Text.Trim([EnglishOccupation]), " "), each _ <> ""), " ")
```

27. **Generate Custom ID: Initials + Birth Year (e.g., JD_1985)**
```DAX
Custom_ID = LEFT(FirstName,1) & LEFT(LastName,1) & "_" & YEAR(BirthDate)
```

28. **Remove Hyphens and Convert Phone to Number**
```Power Query M
Number.FromText(Text.Remove([Phone], {"-"," "}))
```

29. **Customer Segmentation**
```DAX
Customer_Segment =
SWITCH(TRUE(),
    DimCustomer[EnglishEducation] = "Graduate Degree" && DimCustomer[YearlyIncome] > 90000, "Elite",
    DimCustomer[EnglishEducation] = "Bachelors" && DimCustomer[YearlyIncome] >= 60000 && DimCustomer[YearlyIncome] <= 90000, "Professional",
    DimCustomer[EnglishEducation] = "High School", "Basic",
    "Other"
)
```

30. **Measure: Gender-Based Total Count with Selection Logic**
```DAX
CustomerCountByGender =
VAR SelectedGenders = VALUES(DimCustomer[Gender])
RETURN
    IF(COUNTROWS(SelectedGenders) = 1,
        CALCULATE(COUNTROWS(DimCustomer)),
        IF(COUNTROWS(SelectedGenders) > 1, "Multiple Values Selected", COUNTROWS(DimCustomer))
    )
```

---

✅ All transformations are done either using DAX Calculated Columns/Measures or Power Query as noted.