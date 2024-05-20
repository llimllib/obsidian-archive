---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
To run a selenium instance locally:

1. install chromedriver: `brew install --cask chromedriver`
2. `gem install 'webdrivers'
3. test script:

```
require 'selenium-webdriver'

driver = Selenium::WebDriver.for :chrome

driver.get 'https://google.com'

driver.title # => 'Google'

driver.manage.timeouts.implicit_wait = 500

search_box = driver.find_element(name: 'q')
search_button = driver.find_element(name: 'btnK')

search_box.send_keys 'Selenium'
search_button.click

driver.find_element(name: 'q').attribute('value') # => "Selenium"

driver.quit
```

4. Mac complained that the app (chromedriver) could not be opened because it was from an unknown devloper, but it had "open in finder" as an option
	1. click "open in finder"
	2. right-click on chromedriver, click open
	3. on the dialog box that pops up, you can hit "open" to allow mac to open it
5. 💥 now it runs