### 1. Interagir avec une page

```
<input type="text" name="passwd" id="passwd-id" />
```


```
element = driver.find_element(By.ID, "passwd-id")
element = driver.find_element(By.NAME, "passwd")
element = driver.find_element(By.TAG_NAME, "input")
element = driver.find_element(By.XPATH, "//input[@id='passwd-id']")

element = driver.find_element(By.XPATH, "//input[@id='passwd-id' and @name='passwd-name']")

element = driver.find_element(By.XPATH, "//input[contains(@id, 'passwd')]")
element = driver.find_element(By.XPATH, "//input[starts-with(@id, 'passwd')]")

element = driver.find_element(By.XPATH, "//label[text()='Password']")
element = driver.find_element(By.XPATH, "//label[contains(text(), 'Pass')]")

element = driver.find_element(By.XPATH, "//input[@type='password' and @id='passwd-id']")
element = driver.find_element(By.XPATH, "//input[@type='password' and contains(@id, 'passwd')]")

element = driver.find_element(By.CSS_SELECTOR, "input#passwd-id")
content = driver.find_element(By.CSS_SELECTOR, 'p.content')//tag.class

continue_link = driver.find_element(By.LINK_TEXT, 'Continue')
continue_link = driver.find_element(By.PARTIAL_LINK_TEXT, 'Conti')

content = driver.find_element(By.CLASS_NAME, 'content')
```

### 2. Renseigner un formulaire
```
element.send_keys("some text")

element = driver.find_element(By.XPATH, "//select[@name='name']")
all_options = element.find_elements(By.TAG_NAME, "option")
for option in all_options:
    print("Value is: %s" % option.get_attribute("value"))
    option.click()

# Assume the button has the ID "submit" :)
driver.find_element(By.ID, "submit").click()

element.submit()
```


### 3. Drag and drop

```
element = driver.find_element(By.NAME, "source")
target = driver.find_element(By.NAME, "target")

from selenium.webdriver import ActionChains
action_chains = ActionChains(driver)
action_chains.drag_and_drop(element, target).perform()
```

### 6. Navigation: history and location

```
driver.get("http://www.example.com")

driver.back()
driver.forward()
```