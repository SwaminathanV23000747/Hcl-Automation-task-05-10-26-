# Hcl-Automation-task-05-10-26

#  Task 1:

# Selenium code:
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

# Selenium code:
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

# selenium code:
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

# Automation Testing(06/10/26):

 # Task:
 # selenium code:
 ```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager

def auto_fill_selenium_form():
    options = webdriver.ChromeOptions()
    options.add_experimental_option("detach", True)
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
    wait = WebDriverWait(driver, 15)

    driver.get("https://vinothqaacademy.com/demo-site/")
    driver.maximize_window()

    first_name = wait.until(EC.visibility_of_element_located((By.ID, "vfb-5")))
    first_name.send_keys("Swaminathan")
    print("First Name:", first_name.get_attribute("value"))

    last_name = driver.find_element(By.ID, "vfb-7")
    last_name.send_keys("V")
    print("Last Name:", last_name.get_attribute("value"))

    gender = driver.find_element(By.XPATH, "//input[@type='radio' and @value='Male']")
    if not gender.is_selected():
        driver.execute_script("arguments[0].click();", gender)
    print("Gender selected:", gender.is_selected())

    selenium_checkbox = driver.find_element(By.XPATH, "//input[@type='checkbox' and @value='Selenium WebDriver']")
    if not selenium_checkbox.is_selected():
        driver.execute_script("arguments[0].click();", selenium_checkbox)
    print("Selenium selected:", selenium_checkbox.is_selected())

    street = driver.find_element(By.XPATH, "//input[contains(@id,'address') and not(contains(@id,'address-2'))]")
    street.send_keys("123 Main Street")
    print("Street:", street.get_attribute("value"))

    address2 = driver.find_element(By.XPATH, "//input[contains(@id,'address-2')]")
    address2.send_keys("Room 411 ")
    print("Address 2:", address2.get_attribute("value"))

    city = driver.find_element(By.XPATH, "//input[contains(@id,'city')]")
    city.send_keys("Chennai")
    print("City:", city.get_attribute("value"))

    state = driver.find_element(By.XPATH, "//input[contains(@id,'state')]")
    state.send_keys("Tamil Nadu")
    print("State:", state.get_attribute("value"))

    zip_code = driver.find_element(By.XPATH, "//input[contains(@id,'zip')]")
    zip_code.send_keys("600001")
    print("Postal Code:", zip_code.get_attribute("value"))

    email = wait.until(EC.visibility_of_element_located((By.ID, "vfb-14")))
    email.send_keys("Keerthi@example.com")
    print("Email:", email.get_attribute("value"))

    print("\nFORM FILLED SUCCESSFULLY")
    print("No submit button clicked.")
    print("Browser will remain open.")

    time.sleep(60)

if __name__ == "__main__":
    auto_fill_selenium_form()
```
# Output:
<img width="1902" height="1057" alt="image" src="https://github.com/user-attachments/assets/a324c2ca-3e66-4f86-b910-e3eb50554bde" />

# Task-2:
 # Selenium code :
```
import getpass
import time
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import WebDriverWait
from webdriver_manager.chrome import ChromeDriverManager


def add_and_display_cart_product():
    # Prompt user for credentials securely
    phone_or_email = input("Enter your Amazon Mobile Number/Email: ")
    password = getpass.getpass("Enter your Amazon Password: ")

    # Setup Chrome Options with anti-bot evasion
    options = webdriver.ChromeOptions()
    options.add_experimental_option("detach", True)
    options.add_argument("--disable-blink-features=AutomationControlled")
    options.add_experimental_option("excludeSwitches", ["enable-automation"])
    options.add_argument(
        "user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64)"
        " AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
    )

    driver = webdriver.Chrome(
        service=Service(ChromeDriverManager().install()), options=options
    )
    wait = WebDriverWait(driver, 15)

    # Bypass webdriver property flag
    driver.execute_cdp_cmd(
        "Page.addScriptToEvaluateOnNewDocument",
        {
            "source": (
                "Object.defineProperty(navigator, 'webdriver', {get: () =>"
                " undefined})"
            )
        },
    )

    try:
        driver.maximize_window()

        # Step 1: Open Amazon Home Page (Avoids broken 404 URLs)
        print("1. Navigating to Amazon Home Page...")
        driver.get("https://www.amazon.in")
        time.sleep(2)

        # Step 2: Click the 'Hello, sign in' button
        print("2. Clicking Sign-In button...")
        signin_nav = wait.until(
            EC.element_to_be_clickable((By.ID, "nav-link-accountList"))
        )
        signin_nav.click()
        time.sleep(2)

        # Step 3: Enter Mobile Number / Email
        print("3. Entering Phone Number / Email...")
        email_field = wait.until(
            EC.element_to_be_clickable((By.ID, "ap_email"))
        )
        email_field.clear()
        email_field.send_keys(phone_or_email)

        continue_btn = wait.until(
            EC.element_to_be_clickable((By.ID, "continue"))
        )
        continue_btn.click()
        time.sleep(2)

        # Step 4: Enter Password
        print("4. Entering Password...")
        password_field = wait.until(
            EC.element_to_be_clickable((By.ID, "ap_password"))
        )
        password_field.clear()
        password_field.send_keys(password)

        sign_in_btn = wait.until(
            EC.element_to_be_clickable((By.ID, "signInSubmit"))
        )
        sign_in_btn.click()

        # Pause to handle OTP / Captcha verification if prompted by Amazon
        print("⚡ Waiting 10 seconds in case an OTP or Captcha is requested...")
        time.sleep(10)

        # Step 5: Search for a Product
        search_query = "wireless mouse"
        print(f"5. Searching for: '{search_query}'")

        search_box = wait.until(
            EC.element_to_be_clickable((By.ID, "twotabsearchtextbox"))
        )
        search_box.clear()
        search_box.send_keys(search_query)
        search_box.send_keys(Keys.ENTER)
        time.sleep(2)

        # Step 6: Select First Organic Search Product
        print("6. Selecting first product...")
        first_product_link = wait.until(
            EC.element_to_be_clickable((
                By.XPATH,
                "(//div[@data-component-type='s-search-result']//h2/a)[1]",
            ))
        )
        first_product_link.click()
        time.sleep(3)

        # Step 7: Switch to Product Tab
        driver.switch_to.window(driver.window_handles[-1])
        time.sleep(2)

        # Step 8: Click Add to Cart
        print("7. Adding product to cart...")
        add_to_cart_btn = wait.until(
            EC.presence_of_element_located((By.ID, "add-to-cart-button"))
        )
        driver.execute_script(
            "arguments[0].scrollIntoView(true);", add_to_cart_btn
        )
        time.sleep(1)
        driver.execute_script("arguments[0].click();", add_to_cart_btn)
        print("   ✓ Product added!")
        time.sleep(3)

        # Step 9: Go to Cart Page
        print("8. Navigating to Cart Page...")
        driver.get("https://www.amazon.in/gp/cart/view.html")
        time.sleep(3)

        # Wait for Cart container to load
        wait.until(
            EC.presence_of_element_located(
                (By.CLASS_NAME, "sc-list-item-content")
            )
        )

        # Extract Product Title in Cart
        product_title = driver.find_element(
            By.XPATH,
            "//span[contains(@class, 'sc-product-title') or contains(@class,"
            " 'a-truncate-cut')]",
        ).text.strip()

        # Extract Product Price in Cart
        try:
            product_price = driver.find_element(
                By.XPATH,
                "//div[contains(@class, 'sc-badge-price-to-pay')]//span[contains(@class,"
                " 'sc-price')] | //span[contains(@class, 'sc-product-price')]",
            ).text.strip()
        except Exception:
            product_price = "N/A"

        # Display Extracted Details in Console
        print("\n" + "=" * 50)
        print("🛒 ITEM DISPLAYED IN CART:")
        print(f"📌 Product Name : {product_title}")
        print(f"💰 Price        : {product_price}")
        print("=" * 50)

        # Save screenshot confirming the item display
        driver.save_screenshot("cart_item_details.png")
        print("✓ Saved screenshot as 'cart_item_details.png'")

    except Exception as e:
        print(f"\n❌ Error encountered: {e}")


if __name__ == "__main__":
    add_and_display_cart_product()
```
    
# output:

<img width="1906" height="1037" alt="image" src="https://github.com/user-attachments/assets/d8d8cfa8-c3e6-4512-87a4-a91bfebacaed" />
<img width="1907" height="967" alt="Screenshot 2026-10-07 104304" src="https://github.com/user-attachments/assets/beba5e19-c1ca-4d74-8448-cde100003fc6" />
<img width="1913" height="972" alt="Screenshot 2026-10-07 104330" src="https://github.com/user-attachments/assets/0f921039-3cb3-4904-b12f-9c0e73825ef8" />

<img width="1882" height="966" alt="image" src="https://github.com/user-attachments/assets/b02ee532-9ba2-44e6-b2f6-9aa71196fb5d" />

<img width="1902" height="1028" alt="image" src="https://github.com/user-attachments/assets/eaac16bf-8d8c-414b-84e2-384411bebc2a" />
