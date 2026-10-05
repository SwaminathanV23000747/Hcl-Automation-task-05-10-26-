# Hcl-Automation-task-05-10-26

#  Task 1:

# Selenaium code:
```
import time
import undetected_chromedriver as uc
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

def search_actor_suriya_stealth():
    print("Launching Stealth Chrome browser...")

    # Initialize undetected chrome driver
    options = uc.ChromeOptions()
    # Adding language and window options to look natural
    options.add_argument("--start-maximized")
    options.add_argument("--lang=en-US")

    # Launches Chrome without standard Selenium automation flags
    driver = uc.Chrome(options=options)

    try:
        url = "https://images.google.com"
        print(f"Navigating to: {url}")
        driver.get(url)

        # Pause slightly to simulate natural human delay
        time.sleep(2)

        # Locate search bar
        search_box = driver.find_element(By.NAME, "q")
        query = "actor Suriya"
        print(f"Searching for: '{query}'...")

        # Type query naturally
        search_box.clear()
        search_box.send_keys(query)
        search_box.send_keys(Keys.RETURN)

        # Wait for images to load
        time.sleep(4)

        # Take screenshot
        screenshot_filename = "suriya_stealth_result.png"
        driver.save_screenshot(screenshot_filename)
        print(f"✓ Screenshot saved as '{screenshot_filename}'")

    except Exception as e:
        print(f"❌ Error during automation: {e}")

    finally:
        print("Closing browser...")
        driver.quit()


if __name__ == "__main__":
    search_actor_suriya_stealth()
```
# output:
<img width="1883" height="1015" alt="Screenshot 2026-10-05 111713" src="https://github.com/user-attachments/assets/23933f98-f828-4289-aae6-b1c18f83c680" />

# Task 2:

# Selenaium code:
```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager

def saucedemo_login_and_view_product():
    print("Launching Chrome Browser...")

    # Keep browser open after script execution
    options = webdriver.ChromeOptions()
    options.add_experimental_option("detach", True)

    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
    wait = WebDriverWait(driver, 10)

    try:
        driver.maximize_window()

        # Step 1: Open SauceDemo Website
        url = "https://www.saucedemo.com/"
        print(f"1. Navigating to: {url}")
        driver.get(url)

        # Step 2: Auto-enter credentials
        username_field = wait.until(EC.visibility_of_element_located((By.ID, "user-name")))
        password_field = driver.find_element(By.NAME, "password")
        login_btn = driver.find_element(By.ID, "login-button")

        username_field.clear()
        username_field.send_keys("standard_user")
        print("   ✓ Entered Username: standard_user")

        password_field.clear()
        password_field.send_keys("secret_sauce")
        print("   ✓ Entered Password: secret_sauce")

        # Inspect element states
        print("   Username Placeholder:", username_field.get_attribute("placeholder"))
        print("   Is Login Button Enabled?:", login_btn.is_enabled())

        # Step 3: Perform Login
        login_btn.click()
        print("\n2. Clicked Login Button.")

        # Step 4: Verify Product Inventory Page Loaded
        page_title = wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "title"))).text
        print(f"   ✓ Successfully logged in! Page Header: '{page_title}'")

        # Step 5: List and View all Products on the Catalog Page
        products = driver.find_elements(By.CLASS_NAME, "inventory_item")
        print(f"\n3. Found {len(products)} products on catalog page:")
        print("=" * 50)

        for idx, item in enumerate(products, 1):
            name = item.find_element(By.CLASS_NAME, "inventory_item_name").text
            price = item.find_element(By.CLASS_NAME, "inventory_item_price").text
            print(f"   {idx}. {name} — {price}")

        # Step 6: Click on a specific product to view its detail page
        first_product_name = products[0].find_element(By.CLASS_NAME, "inventory_item_name")
        target_product = first_product_name.text
        print(f"\n4. Opening detail page for: '{target_product}'...")
        first_product_name.click()

        # Step 7: Verify Detailed Product View
        detail_title = wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_details_name"))).text
        detail_price = driver.find_element(By.CLASS_NAME, "inventory_details_price").text
        detail_desc = driver.find_element(By.CLASS_NAME, "inventory_details_desc").text

        print("\n" + "=" * 50)
        print("✓ PRODUCT DETAIL PAGE OPENED SUCCESSFULLY")
        print(f"  Title: {detail_title}")
        print(f"  Price: {detail_price}")
        print(f"  Description: {detail_desc}")
        print("=" * 50)

        # Save screenshot of product view
        driver.save_screenshot("viewed_product_detail.png")
        print("\n✓ Screenshot saved as 'viewed_product_detail.png'")

    except Exception as e:
        print(f"❌ Automation Error: {e}")

if __name__ == "__main__":
    saucedemo_login_and_view_product()
```
# output:
<img width="1907" height="1010" alt="Screenshot 2026-10-05 114918" src="https://github.com/user-attachments/assets/426e2331-56a2-4018-a9c1-c422f6bf0cea" />

# task 3:

# selenaium code:
```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager

def flipkart_login_with_otp():
    print("Launching Chrome Browser...")

    # Keep browser open after execution
    options = webdriver.ChromeOptions()
    options.add_experimental_option("detach", True)
    options.add_argument("--disable-blink-features=AutomationControlled")
    options.add_experimental_option("excludeSwitches", ["enable-automation"])

    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
    wait = WebDriverWait(driver, 15)

    try:
        driver.maximize_window()

        # Step 1: Open Flipkart Login Page
        url = "https://www.flipkart.com/account/login"
        print(f"1. Navigating to: {url}")
        driver.get(url)

        # Step 2: Enter Mobile Number
        phone_number = "YOUR_MOBILE_NUMBER_HERE"  # Replace with your 10-digit mobile number
        
        # Locate the mobile number input box
        mobile_field = wait.until(
            EC.visibility_of_element_located((By.XPATH, "//input[@class='r4v19z' or @class='_2IX_2- _2UU23e' or @type='text']"))
        )
        mobile_field.clear()
        mobile_field.send_keys(phone_number)
        print(f"   ✓ Entered Mobile Number: {phone_number}")

        # Step 3: Click Request OTP Button
        request_otp_btn = wait.until(
            EC.element_to_be_clickable((By.XPATH, "//button[contains(text(),'Request OTP') or contains(text(),'CONTINUE')]"))
        )
        request_otp_btn.click()
        print("   ✓ Clicked 'Request OTP'.")

        # Step 4: Handle OTP Input
        print("\n" + "="*50)
        print("📲 OTP HAS BEEN SENT TO YOUR MOBILE PHONE.")
        print("Please type the OTP directly into the browser window or press Enter here once you submit it.")
        print("="*50 + "\n")

        # Pause script execution for up to 30 seconds to allow manual OTP entry
        # Wait until Flipkart redirects away from login or shows the user profile/search bar
        wait.until(
            EC.presence_of_element_located((By.XPATH, "//input[@placeholder='Search for Products, Brands and More']"))
        )

        # Step 5: Verify Login & Dashboard Access
        print("✓ Login Successful! Entered Flipkart Dashboard/Homepage.")
        
        # Take a screenshot of the logged-in dashboard
        driver.save_screenshot("flipkart_dashboard.png")
        print("   ✓ Dashboard screenshot saved as 'flipkart_dashboard.png'")

    except Exception as e:
        print(f"\n❌ Error or Timeout during execution: {e}")

if __name__ == "__main__":
    flipkart_login_with_otp()
```
# output:
<img width="1917" height="1071" alt="Screenshot 2026-10-05 135010" src="https://github.com/user-attachments/assets/12511fc0-5102-4f89-a87c-5f94de0a5f36" />
<img width="1916" height="1075" alt="Screenshot 2026-10-05 135038" src="https://github.com/user-attachments/assets/7444dc52-3c7f-4685-b5b0-999b64c1044a" />

<img width="1917" height="1078" alt="Screenshot 2026-10-05 135052" src="https://github.com/user-attachments/assets/1a47cfb3-2372-4dec-befc-b4cffa433f81" />



    
