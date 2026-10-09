## WebTable

## Program:

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select

driver = webdriver.Chrome()
driver.get("https://assertqa.com/practice/webtables")
driver.maximize_window()


headings = driver.find_elements(By.XPATH, "//table/thead/tr/th")

print("TC01 - Column Headings")
for heading in headings:
    print(heading.text)


rows = driver.find_elements(By.XPATH, "//table/tbody/tr")

print("\nTC02 - First Data Row")
if rows:
    print(rows[0].text)


print("\nTC03 - Last Data Row")
if rows:
    print(rows[-1].text)


search = driver.find_element(
    By.XPATH, "//input[contains(@placeholder,'Search')]"
)
search.send_keys("Smith")

print("\nTC04 - Search by Last Name")
results = driver.find_elements(By.XPATH, "//table/tbody/tr")

for row in results:
    print(row.text)

search.clear()


emails = driver.find_elements(
    By.XPATH, "//table/tbody/tr/td[3]"
)

print("\nTC05 - Email Addresses")
for email in emails:
    print(email.text)


print("\nTC06 - Highest Due Amount")

headers = driver.find_elements(By.XPATH, "//table/thead/tr/th")
due_column = -1

for i, header in enumerate(headers):
    if header.text.strip().lower() == "due":
        due_column = i + 1
        break

if due_column != -1:
    rows = driver.find_elements(By.XPATH, "//table/tbody/tr")
    highest_due = -1
    employee = ""

    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "td")
        amount = float(
            cells[due_column - 1].text.replace("$", "").replace(",", "")
        )

        if amount > highest_due:
            highest_due = amount
            employee = row.text

    print("Employee:", employee)
    print("Highest Due:", highest_due)
else:
    print("FAIL - Due column not found")


print("\nTC07 - Website Link Verification")

links = driver.find_elements(
    By.XPATH, "//table//a[@href]"
)

if links:
    print("PASS - Website link exists")
    for link in links:
        print(link.get_attribute("href"))
else:
    print("FAIL - Website link not found")


rows = driver.find_elements(By.XPATH, "//table/tbody/tr")

print("\nTC08 - Data Row Count")
print("Number of displayed data rows:", len(rows))

driver.quit()
```



## Output:

<img width="1220" height="907" alt="image" src="https://github.com/user-attachments/assets/7c3c1654-07c6-4d42-a42b-e64b3179e204" />

<img width="1192" height="566" alt="Screenshot 2026-10-09 134512" src="https://github.com/user-attachments/assets/588f32fa-024b-4838-b99d-28c26724bc78" />



